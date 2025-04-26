---
title: "Docker Entrypoint로 실행된 Shell Script에서 Application으로 SIGTERM을 전송하는 방법"
excerpt: "Docker Entrypoint로 실행된 Shell Script에서 Application으로 SIGTERM을 전송하는 방법"
last_modified_at: 2025-04-26T20:50:00
header:
  image: /assets/images/java/sending-docker-sigterm-from-shell-to-application.png
categories:
  - Java
tags:
  - Programming
  - Docker
  - ENTRYPOINT
  - Shell Script
  - SIGTERM
  - Graceful Shutdown

toc: true
toc_ads: true
toc_sticky: true
---
# 개요
- Dockerfile을 만들다 보면, ENTRYPOINT[^Docker_Docs_Dockerfile_ENTRYPOINT]에 단순 application을 실행하는 로직 외 다양한 로직을 실행하기 위해서 Shell Script를 실행하는 경우가 있다.
- 이 경우, Docker를 종료하려고 SIGTERM을 전송하면 Shell Script로 전송되기 때문에 Application에서는 정상적으로 SIGTERM을 전달받지 못해서 Graceful Shutdown이 수행되지 않고 SIGKILL에 의해서 서비스는 강제 종료된다.
- 위의 상황들을 해결하기 위한 기본적인 방법인 Shell Script로 전달된 SIGTERM을 Application으로 전달하는 방법을 설명한다.

# run.sh
```sh
#!/bin/sh

# Send SIGTERM to the application.
term_handler() {
  if [ $pid -ne 0 ]; then
    kill -SIGTERM "$pid"
    wait "$pid"
  fi
  exit 143 # 128(External) + 15(SIGTERM)
}

# Setup the trap for the SIGTERM.
trap 'kill ${!}; term_handler' SIGTERM

# Start application.
java org.springframework.boot.loader.launch.JarLauncher &
pid="$!"

# Wait the signal.
while true; do
  # Check if process is still running.
  kill -0 "$pid" 2>/dev/null
  if [ $? -ne 0 ]; then
    echo "Process $pid is not running. Terminating the container."
    term_handler
  fi
  # Signal confirmation interval.
  sleep 5
done
```
- Apline Linux에서도 정상 동작 가능하도록 bash가 아닌 sh로 실행 가능하게 shebang[^Shebang]을 "/bin/sh"로 정의한다.
- term_handler 함수는 pid가 존재하면 pid로 SIGTERM을 전송 후 완료되기 까지 pid 프로세스를 기다리는 작업을 수행하고 마지막으로 143 코드로 스크립트 실행을 종료한다.
  - 143의 의미는 외부 요청 수행을 의미하는 128에, SIGTERM을 의미하는 15를 더한 값으로 차별화 시킨 값이다.
- tarp 명령어를 통해 SIGTERM을 받았을 때, term_handler 함수를 수행한다.
- java 명령어로 어플리케이션을 수행하면서, pid 변수에 실행된 pid를 저장한다.
- 5초마다 수행 프로세스가 진행 중인지를 검증하고, 프로세스 종료된 경우 스크립트 실행을 종료하여 현재 실행 중인 컨테이너 또한 종료한다.

# Dockerfile
```sh
... omitted ...

# Copy run.sh and change mode to 755
COPY ./run.sh /
RUN chmod 755 /run.sh

... omitted ...

# Run application
ENTRYPOINT [ "/bin/sh", "/run.sh" ]
```
- 위에서 정의한 run.sh 파일을 컨테이너 내부로 이동시킨 후, 실행에 문제 없게 755 권한을 부여한다.
- ENTRYPOINT로 컨테이너 실행 시, run.sh 쉘 스크립트를 실행하도록 정의한다.

# 부가 설명
- Docker Compose를 이용하여 종료하게 되는 경우엔 컨테이너 Graceful Shutdown을 위한 stop_grace_period[^stop_grace_period] 옵션과 Spring Boot의 Graceful Shutdown[^Graceful_Shutdown] 설정을 유연하게 조절하여야 한다.

# 정리
- Docker Container는 컨테이너 실행에 수행되는 CMD 혹은 ENTRYPOINT 설정으로 실행된 프로세스의 상태와 직접적인 관계가 있지만, Shell Script 등을 활용한 간접적인 Application 실행의 경우 Signal을 주요 Application에 중계해야 정상적인 상태를 동기화 할 수 있다.

# Reference
[^Docker_Docs_Dockerfile_ENTRYPOINT]: [Docker-Docs-Dockerfile-ENTRYPOINT](https://docs.docker.com/reference/dockerfile/#entrypoint){:target="_blank"}
[^Shebang]: [Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)){:target="_blank"}
[^stop_grace_period]: [Docker-Compose-stop_grace_period](https://docs.docker.com/reference/compose-file/services/#stop_grace_period){:target="_blank"}
[^Graceful_Shutdown]: [Spring-Boot-Graceful-Shutdown](https://docs.spring.io/spring-boot/reference/web/graceful-shutdown.html){:target="_blank"}
※ Sample Code는 [여기](https://github.com/GracefulSoul/lightweight-jdk-docker){:target="_blank"}에서 확인 가능합니다.