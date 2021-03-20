---
title: "Java Design Pattern - Chain of Responsibility Pattern"
excerpt: "Java를 이용하여 Design Pattern - Chain of Responsibility Pattern에 대해 설명합니다."
last_modified_at: 2021-03-20T11:10:00
header:
  image: /assets/images/designpattern/behavioral/chainOfResponsibility.png
categories:
  - DesignPattern
tags:
  - Programming
	- Java
  - DesignPattern
  - Behavioral Patterns

toc: true
toc_ads: true
toc_sticky: true
---
# [Design Pattern](../designpattern)
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Behavioral Patterns, 행위 패턴
- 객체간의 상호작용과 책임을 중시하는 패턴이다.
- 한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하면서 객체 사이의 결합도를 최소화하는 것에 중점을 두는 패턴이다.

# Chain of Responsibility Pattern
- 한 요청을 두 개 이상의 객체에서 처리하고 싶을 때 사용하는 패턴이다.

# Example
```java
public abstract class AbstractLogger {

	public static int INFO = 1;
	public static int DEBUG = 2;
	public static int ERROR = 3;

	protected int level;

	// Next element in chain or responsibility.
	protected AbstractLogger nextLogger;

	public void setNextLogger(AbstractLogger nextLogger) {
		this.nextLogger = nextLogger;
	}

	public void logMessage(int level, String message) {
		if (this.level <= level) {
			write(message);
		}
		if (nextLogger != null) {
			nextLogger.logMessage(level, message);
		}
	}

	abstract protected void write(String message);

}
public class ConsoleLogger extends AbstractLogger {

	public ConsoleLogger(int level) {
		this.level = level;
	}

	@Override
	protected void write(String message) {
		System.out.println("Standard Console::Logger: " + message);
	}

}
public class ErrorLogger extends AbstractLogger {

	public ErrorLogger(int level) {
		this.level = level;
	}

	@Override
	protected void write(String message) {
		System.out.println("Error Console::Logger: " + message);
	}

}
public class FileLogger extends AbstractLogger {

	public FileLogger(int level) {
		this.level = level;
	}

	@Override
	protected void write(String message) {
		System.out.println("File::Logger: " + message);
	}

}
```

- 일정 Level에 해당하는 Logger 클래스를 찾아 Logging을 위한 AbstractLogger 추상 클래스를 정의한다.
- Console, Error, File 별 Logging을 위한 각 클래스를 정의하고, 각 Logging 방식에 대한 write 메서드를 구현한다.

```java
public class ChainPatternMain {

	private static AbstractLogger getChainOfLoggers() {

		AbstractLogger errorLogger = new ErrorLogger(AbstractLogger.ERROR);
		AbstractLogger fileLogger = new FileLogger(AbstractLogger.DEBUG);
		AbstractLogger consoleLogger = new ConsoleLogger(AbstractLogger.INFO);

		errorLogger.setNextLogger(fileLogger);
		fileLogger.setNextLogger(consoleLogger);

		return errorLogger;
	}

	public static void main(String[] args) {
		AbstractLogger loggerChain = getChainOfLoggers();

		loggerChain.logMessage(AbstractLogger.INFO, "This is an information.");
		loggerChain.logMessage(AbstractLogger.DEBUG, "This is an debug level information.");
		loggerChain.logMessage(AbstractLogger.ERROR, "This is an error information.");
	}

}
```

- Error 수준의 경우 ErrorLogger를 호출하고, Debug 수준의 경우 FileLogger, Info 수준은 ConsoleLogger를 호출하도록 선언한다.
- ErrorLogger가 호출되면 다음에는 FileLogger를 호출하도록하고, FileLogger가 호출되면 다음에는 ConsoleLogger를 호출하도록 연결한다.
- 위의 설정이 적용된 Logger를 AbstractLogger로 받아 각 Logging Level 별 Log 메시지를 출력해본다.

# Source
[GitHub-Chain of Responsibility](https://github.com/GracefulSoul/Sample/tree/master/src/main/java/gracefulsoul/designpattern/behavioral/chainOfResponsibility)