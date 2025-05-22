---
title: "Custom JRE로 경령화된 Dockering II"
excerpt: "Jdeps와 Jlink를 사용하여 경량화된 Custom JRE와 Layered Jars를 사용하는 Dockerizng을 통해 CI/CD 성능 최적화"
last_modified_at: 2024-11-22T21:00:00
header:
  image: /assets/images/java/lightweight-jdk-docker.png
categories:
  - Java
tags:
  - Programming
  - Docker
  - Java
  - Spring
  - Jdeps
  - Jlink
  - Layered Jars

toc: true
toc_ads: true
toc_sticky: true
---
# 개요
- 이전 포스트인 [Custom JRE로 경령화된 Dockering I](../lightweight-jdk-docker-I){:target="_blank"}에서 이야기한 내용과 절차는 동일하지만, 공식적으로 제공하는 Layered Jars[^Creating_Docker_images]를 사용하는 방법을 설명한다.
- 이 포스트에서는 기존 방식과 차별화된 방식에 대한 설명을 진행하므로, 기본 절차를 이해하고 싶다면 이전 포스트를 읽은 다음에 보는 것을 추천한다.

# Layered Jars
- Layered Jars는 기존의 Fat jars의 형태인 모든 의존성과 리소스 파일들을 단일 jar 파일로 패키징 하는 방법을 아래와 같이 필요한 레이어로 패키징을 활용하는 기능이다.
```sh
./app
├─ /dependencies           ## for any dependency whose version does not contain SNAPSHOT.
├─ /spring-boot-loader     ## for the jar loader classes.
├─ /snapshot-dependencies  ## for any dependency whose version contains SNAPSHOT.
└─ /application            ## for application classes and resources.
```

## Setting
- Layered 기능을 사용하기 위해서는 아래와 같이 빌드 툴 별 설정이 필요하지만, Spring Boot 2.3.0 부터 빌드 툴의 설정 없이 사용이 가능하다.

### Maven(pom.xml)
```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <version>{maven-project-version}</version>
        <configuration>
        <layers>
          <enabled>true</enabled>
        </layers>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### Gradle(build.gradle)
```
bootJar {
  layered()
}
```

## Structure
- 기본적으로 사용하는 구조는 "/BOOT-INF/layers.idx"에 아래와 같이 정의된다.

```sh
- "dependencies":
  - "BOOT-INF/lib/"
- "spring-boot-loader":
  - "org/"
- "snapshot-dependencies":
- "application":
  - "BOOT-INF/classes/"
  - "BOOT-INF/classpath.idx"
  - "BOOT-INF/layers.idx"
  - "META-INF/"
```

## Customizing
- 필요에 따라 각 빌드 툴 별 설정 방식으로 layer를 정의하여 사용할 수 있다.

### Maven(layer.xml)
```xml
<layers xmlns="http://www.springframework.org/schema/boot/layers"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://www.springframework.org/schema/boot/layers
              https://www.springframework.org/schema/boot/layers/layers-{spring-boot-xsd-version}.xsd">
  <application>
    <into layer="spring-boot-loader">
      <include>org/springframework/boot/loader/**</include>
    </into>
    <into layer="application" />
  </application>
  <dependencies>
    <into layer="snapshot-dependencies">
      <include>*:*:*SNAPSHOT</include>
    </into>
    <into layer="company-dependencies">
      <include>com.acme:*</include>
    </into>
    <into layer="dependencies"/>
  </dependencies>
  <layerOrder>
    <layer>spring-boot-loader</layer>
    <layer>application</layer>
    <layer>company-dependencies</layer>
    <layer>snapshot-dependencies</layer>
    <layer>dependencies</layer>
  </layerOrder>
</layers>
```

### Gradle(build.gradle)
```
bootJar {
  layered {
    application {
      intoLayer("spring-boot-loader") {
        include "org/springframework/boot/loader/**"
      }
      intoLayer("application")
    }
    dependencies {
      intoLayer("snapshot-dependencies") {
        include "*:*:*SNAPSHOT"
      }
      intoLayer("company-dependencies") {
        include "com:gracefulsoul:*"
      }
      intoLayer("dependencies")
    }
    layerOrder = ["spring-boot-loader", "application", "company-dependencies", "snapshot-dependencies", "dependencies"]
  }
}
```

# Dockerfile
- 기존 방식과 Layered Jars와 차이를 분석한다.

## Stage 1
```sh
# Stage 1. Create custom JRE
FROM amazoncorretto:21-alpine AS jrebuilder

# Add the application jar to the container
COPY ./build/libs/hello-docker-*-SNAPSHOT.jar app.jar

# Install binutils
RUN apk add --no-cache binutils

# Extract jar file and generate custom JRE using dependency
RUN java -Djarmode=tools -jar app.jar extract --layers --launcher \
  && DEPENDENCY=$(jdeps --ignore-missing-deps --print-module-deps --recursive --multi-release 21 --class-path="/app/dependencies/BOOT-INF/lib/*" /app.jar) \
  && ${JAVA_HOME}/bin/jlink \
    --verbose \
    --add-modules ${DEPENDENCY} \
    --strip-debug \
    --no-man-pages \
    --no-header-files \
    --compress=2 \
    --output customjre
```
- 이전에는 jar 명령어를 이용하여 압축 해제한 폴더를 사용했다면, 이번에는 java 명령어 내 "jarmode" 중 "tools"를 사용하여 압축을 해제한다.

  | Option | Description |
  |:--------|:--------|
  | --launcher | 스프링 부트 런처 추출. |
  | --layers | 레이어를 활용한 추출. |

## Stage 2
```sh
# Stage 2. Make container for application
FROM alpine:3.20
ENV JAVA_HOME=/jre
ENV PATH="${JAVA_HOME}/bin:${PATH}"
ARG DEPENDENCY=/app

# Add Maintainer Info
LABEL maintainer="GracefulSoul on <gracefulsoul@github.com>"

# Copy custom JRE
COPY --from=jrebuilder /customjre ${JAVA_HOME}

# Copy extract files in jar
COPY --from=jrebuilder ${DEPENDENCY}/dependencies/ ${DEPENDENCY}/
COPY --from=jrebuilder ${DEPENDENCY}/snapshot-dependencies/ ${DEPENDENCY}/
COPY --from=jrebuilder ${DEPENDENCY}/spring-boot-loader/ ${DEPENDENCY}/
COPY --from=jrebuilder ${DEPENDENCY}/application/ ${DEPENDENCY}/

# Move work directory
WORKDIR ${DEPENDENCY}

# Run application
ENTRYPOINT [ "java", "org.springframework.boot.loader.launch.JarLauncher" ]
```
- 기존 BOOT-INF, META-INF에서 필요한 폴더를 나누어 썼듯이 Layer로 분리된 각 폴더에서 필요한 폴더를 사용한다.
- 애플리케이션 실행은 기존과 다르게 Main Class를 실행하는 것이 아닌, Layered Jars를 같이 추출된 Launcher를 사용하여 Main Class를 실행한다.

# 정리
- 코드를 보면 이전 화와 크게 다를 바 없는 내용이지만, 복잡한 구성의 애플리케이션에서는 단순 빌드된 Fat Jars를 원하는 형태로 배치하기 위해 소모되는 자원과 시간은 개발자에게 불필요하다.
- Spring Boot는 초기 사상과 같이 개발자는 비즈니스 로직에 더 집중할 수 있는 다양한 환경을 구성해주며, 이러한 기능들은 실무에 다양하게 활용할 수 있다.

# 여담
- Layered Jars는 Spring Boot 3.3부터 공식적으로 지원하는 [Class Data Sharing(CDS)](https://docs.oracle.com/en/java/javase/17/vm/class-data-sharing.html){:target="_blank"} [^Spring-Boot-3.3-Release-Notes]를 사용하기 위해 공유할 자원을 분리하여 애플리케이션을 실행 할 때에도 사용된다.
- jarmode의 경우도, 해당 버전부터 layertools가 deprecated 되었으로 아래 내용을 참고하였으면한다.
  - 3.3 이상 : java -Djarmode=tools -jar app.jar extract --layers --launcher
  - 3.3 미만 : java -Djarmode=layertools -jar app.jar

# 이전
[Custom JRE로 경령화된 Dockering I](../lightweight-jdk-docker-I){:target="_blank"}

# Reference
[^Creating_Docker_images]: [Creating-Efficient-Docker-Images-with-Spring-Boot-2.3_Spring-Blog](https://spring.io/blog/2020/08/14/creating-efficient-docker-images-with-spring-boot-2-3){:target="_blank"}
[^Spring-Boot-3.3-Release-Notes]: [Spring-Boot-3.3-Release-Notes_Spring-GitHub](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.3-Release-Notes#cds-support){:target="_blank"}
※ Sample Code는 [여기](https://github.com/GracefulSoul/lightweight-jdk-docker){:target="_blank"}에서 확인 가능합니다.