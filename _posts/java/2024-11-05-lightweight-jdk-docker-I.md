---
title: "Custom JRE로 경령화된 Dockering I"
excerpt: "Jdeps와 Jlink를 이용하여 경량화된 Custom JRE를 사용하는 Dockerizng으로 CI/CD 성능 최적화"
last_modified_at: 2024-11-05T20:00:00
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

toc: true
toc_ads: true
toc_sticky: true
---
# 개요
- Java 애플리케이션은 JVM(Java Virtual Machine)이 함께 컨테이너에 배포되어야 하기 때문에 비교적 타 언어로 배포되는 컨테이너보다 용량이 매우 크므로, 이 부분을 해소하기 위한 경량화된 Dockerizng[^Dockerizng]을 Amazon Crretto JDK[^Amazon_Crretto_JDK]를 이용하여 설명하고자한다.
- 여기서는 Custom JRE를 생성하는 Docker의 Multi-Stage builds[^Multi-Stage-builds]를 활용하여 실제 빌드하는 JAVA 애플리케이션을 경량화한다.

# Stage 1
- Stage 1에서는 애플리케이션 의존 관계를 분석하여 경량화된 Custom JRE를 만드는 부분에 중점을 둔다.
- 부가적으로 빌드된 jar 파일을 필요한 파일들만 사용하기 위하여 압축 해제한다.

```sh
# Stage 1. Create custom JRE
FROM amazoncorretto:21-alpine AS jrebuilder

# Add the application jar to the container
COPY ./build/libs/hello-docker-*-SNAPSHOT.jar /app.jar

# Install binutils
RUN apk add --no-cache binutils

# Extract jar file and generate custom JRE using dependency
RUN mkdir -p /app && (cd /app; jar -xf /app.jar) \
	&& DEPENDENCY=$(jdeps --ignore-missing-deps --print-module-deps --recursive --multi-release 21 --class-path="/app/BOOT-INF/lib/*" /app.jar) \
	&& ${JAVA_HOME}/bin/jlink \
		--verbose \
		--add-modules ${DEPENDENCY} \
		--strip-debug \
		--no-man-pages \
		--no-header-files \
		--compress=2 \
		--output \
		customjre
```

## Image
- Custom JRE는 JDK에서 필요한 의존성만 추출해야 하므로 기본 이미지는 JDK 이미지로 사용하고, jrebuilder로 명명한다.

## Copy application
- Gradle을 이용하여 빌드된 jar파일은 /build/libs/ 경로 아래 생성되며, 해당 jar 파일을 사용하기 위해 컨테이너 내부로 복사한다.

## Install Binutils[^Binutils]
- 컨테이너 내부에서 jlink 명령어를 사용하기 위해서 objcopy가 필요한데, 이는 binutils를 설치하여 사용할 수 있다.
- 만일 해당 부분을 설치하지 않는다면 아래의 오류를 마주할 수 있다.
```sh
Error: java.io.IOException: Cannot run program "objcopy": error=2, No such file or directory
```

## Generate custom JRE
- 이제 가장 중요한 Custom JRE를 만드는 부분이다.
- "/app" 폴더를 만든 후 해당 경로에 애플리케이션 jar 파일을 압축 해제해준다.
- 빌드된 jar 파일 구성은 아래와 같다.
```sh
./hello-docker
├─ /BOOT-INF
│  ├─ /classes ## Folder where the class file where the
│  │           ## JAVA file is compiled is stored.
│  └─ /lib     ## Folder where the dependency injected jar
│              ## library is stored.
├─ /META-INF   ## Folder where the meta data and setting data.
└─ /org
```

### Jdeps[^Jdeps]
- Jdeps는 JAVA Class의 의존성 분석을 위한 도구로, 모듈화가 적용된 JAVA 9 버전 이상부터 사용이 가능하다.

| Option | Description |
|:--------|:--------|
| --ignore-missing-deps | 외존성이 존재하지 않는 모듈은 제외. |
| --print-module-deps | Jlink에서 요구하는 포멧에 맞는 쉼표로 구분된 모듈 의존성 목록을 출력. |
| --recursive | 모든 런타임 종속성을 재귀적으로 탐색. |
| --multi-release ${VERSION} | 의존성을 분석할 JAVA 버전을 ${VERSION}에 명시. 단, 모듈화가 적용된 9 버전 이상만 적용. |
| --class-path="${PATH}" | 의존성을 분석할 class 파일들을 찾을 위치를 ${PATH}에 지정. |

### Jlink[^Jlink]
- Jlink는 Jdeps를 이용하여 분석된 의존성을 활용하여 최적화된 Custom JRE를 구성할 수 있는 도구이다.

| Option | Description |
|:--------|:--------|
| --verbose | 진행 중 상세 내역을 출력. |
| --add-modules ${DEPENDENCY} | jdeps를 이용하여 분석한 쉼표로 구분된 모듈 의존성 목록 |
| --strip-debug | 디버그 정보를 제거. |
| --no-man-pages | man page(특정 명령이나 자원들의 메뉴얼을 출력하는 영역) 미사용. |
| --no-header-files | header files(로직이 저장된 파일) 미사용. |
| --compress=2 | 리소스 압축 여부. 0 : 미사용, 1 : 상수 문자열 공유, 2 : 압축을 의미하며, 보편적으로 2를 사용. |
| --output=${PATH} | 리소스를 저장할 위치를 ${PATH}에 지정. |

# Stage 2
- Stage 2에서는 Stage 1에서 분석된 의존성을 통해 완성된 Custom JRE와 압축 해제한 jar에서 필요한 파일로 이미지를 구성하여 경량화된 JAVA 애플리케이션 컨테이너를 구성한다.

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
COPY --from=jrebuilder ${DEPENDENCY}/BOOT-INF/lib ${DEPENDENCY}/lib
COPY --from=jrebuilder ${DEPENDENCY}/META-INF ${DEPENDENCY}/META-INF
COPY --from=jrebuilder ${DEPENDENCY}/BOOT-INF/classes ${DEPENDENCY}

# Move work directory
WORKDIR ${DEPENDENCY}

# Run application
ENTRYPOINT [ "java", "-cp", "${DEPENDENCY}:${DEPENDENCY}/lib/*", "gracefulsoul.HelloDockerApplication" ]
```

## Image
- Stage 1에서 Custom JRE를 만들었으므로, 경량화된 Alpine Linux[^Alpine_Linux] 이미지를 아래의 환경 설정을 이용하여 사용한다.
- JAVA_HOME 환경 변수를 추가하기 위하여 JAVA_HOME은 "/jre"로 준 후 PATH에 "JAVA_HOME/bin"을 추가한다.
- "/app" 폴더를 전역 변수로 사용하기 위한 DEPENDENCY를 정의한다.

## Copy custom JRE
- Stage 1에서 생성한 Custom JRE가 저장된 "/customjre" 폴더를 "/jre"로 복사한다.

## Copy extract files in jar
- jar 파일에서 JAVA 애플리케이션 구동을 위해 필요한 아래의 폴더들을 복사한다.
- 의존성 주입된 Library가 저장된 "/app/BOOT-INF/lib" 폴더를 "/app/lib" 폴더로 복사한다.
- 메타 데이터와 설정 정보를 저장된 "/app/META-INF" 폴더를 "/app/META-INF" 폴더로 복사한다.
- 컴파일된 class 파일이 저장된 "/app/BOOT-INF/classes" 폴더를 "/app" 폴더로 복사한다.

## Move work directory
- JAVA 애플리케이션 실행 위치인 "/app" 위치를 컨테이너 기본 위치로 설정한다.

## Run application
- ENTRYPOINT인 컨테이너가 실행될 때 기본으로 동작하는 명령어는 아래의 조합으로 완성한다.
- "java" 명령어는 JAVA 애플리케이션 실행을 위한 명령어이다.
- "-cp /app:/app/lib/*"은 classpath를 지정하는 명령어로, 컴파일된 class 파일 루트 위치인 "/app"과 의존성으로 추가된 Library들을 포함하는 "/app/lib/*"을 이어준다.
- 실행하고자 하는 Main Class 이름을 "package.className" 형태인 "gracefulsoul.HelloDockerApplication"로 정의한다.

# 정리
- 위에서 하나씩 살펴본 JAVA 애플리케이션 경량화 Docker Conatiner는 MSA 구성에 있어서 아주 기본적인 서비스 빌드 방법의 하나를 살펴보았다.
- 애플리케이션을 돌리기 위한 컨테이너는 동작에 필요한 최소한의 리소스를 이용한 컨테이너 경량화는 배포 크기의 감소와 성능 향상, 비용 감소 등의 이점이 있으므로 선택이 아닌 필수이다.

# Reference
[^Dockerizng]: [Spring-Boot-Docker_Springio-Guides](https://spring.io/guides/gs/spring-boot-docker){:target="_blank"}
[^Multi-Stage-builds]: [Multi-Stage-builds-Docker](https://docs.docker.com/build/building/multi-stage/){:target="_blank"}
[^Amazon_Crretto_JDK]: [Amazon-Crretto](https://aws.amazon.com/corretto){:target="_blank"}
[^Binutils]: [Binutils](https://www.gnu.org/software/binutils/){:target="_blank"}
[^Jdeps]: [Jdeps_Oracle-Document](https://docs.oracle.com/en/java/javase/21/docs/specs/man/jdeps.html){:target="_blank"}
[^Jlink]: [Jlink_Oracle-Document](https://docs.oracle.com/en/java/javase/21/docs/specs/man/jlink.html){:target="_blank"}
[^Alpine_Linux]: [Alpine_Linux-Wiki](https://en.wikipedia.org/wiki/Alpine_Linux){:target="_blank"}
※ Sample Code는 [여기](https://github.com/GracefulSoul/lightweight-jdk-docker){:target="_blank"}에서 확인 가능합니다.