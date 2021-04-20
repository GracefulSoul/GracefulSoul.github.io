---
title: "Java Design Pattern - Front Controller Pattern"
excerpt: "Java를 이용하여 Design Pattern - Front Controller Pattern에 대해 설명합니다."
last_modified_at: 2021-03-27T14:50:00
header:
  image: /assets/images/designpattern/other/frontController.png
categories:
  - DesignPattern
tags:
  - Programming
  - Java
  - DesignPattern

toc: true
toc_ads: true
toc_sticky: true
---
# [Design Pattern](../designpattern){:target="_blank"}
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Front Controller Pattern
- 모든 요청이 단일 핸들러로 처리되도록 중앙 집중식 요청 처리 메커니즘을 제공하는 데 사용된다.
- 이 핸들러는 요청의 인증/권한/로깅 또는 추적을 수행한 다음 요청을 해당 핸들러로 전달할 수 있다.

# Example
```java
public class HomeView {

	public void show() {
		System.out.println("Displaying Home Page");
	}

}
public class StudentView {

	public void show() {
		System.out.println("Displaying Student Page");
	}

}
```

- View의 역할을 할 HomeView와 StudentView를 구현한다.

```java
public class Dispatcher {

	private StudentView studentView;
	private HomeView homeView;

	public Dispatcher() {
		this.studentView = new StudentView();
		this.homeView = new HomeView();
	}

	public void dispatch(Request request) {
		if (Request.STUDENT.equals(request)) {
			this.studentView.show();
		} else {
			homeView.show();
		}
	}

}
```

- Dispatcher를 통해 Request에 대한 View를 제공하도록 처리한다.

```java
public class FrontController {

	private Dispatcher dispatcher;

	public FrontController() {
		this.dispatcher = new Dispatcher();
	}

	private boolean isAuthenticUser() {
		System.out.println("User is authenticated successfully.");
		return true;
	}

	private void trackRequest(Request request) {
		System.out.println("Page requested: " + request.name());
	}

	public void dispatchRequest(Request request) {
		// Long each request.
		trackRequest(request);
		// Authenticate the user.
		if (isAuthenticUser()) {
			dispatcher.dispatch(request);
		}
	}

}
```

- FrontController에서는 Request에 대한 권한 관리와 로깅을 수행한다.

```java
public class FrontControllerPatternMain {

	public static void main(String[] args) {
		FrontController frontController = new FrontController();
		frontController.dispatchRequest(Request.HOME);
		frontController.dispatchRequest(Request.STUDENT);
	}

}
```

- Request를 통해 각 요청을 수행해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/frontController){:target="_blank"}에서 확인 가능합니다.