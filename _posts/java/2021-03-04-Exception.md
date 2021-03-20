---
title: "Java Exception"
excerpt: "Java Exception에 대한 설명"
last_modified_at: 2021-03-04T19:45:00
header:
  image: /assets/images/java/java.png
categories:
  - Java
tags:
  - Programming
  - Java
  - Exception

toc: true
toc_ads: true
toc_sticky: true
---
# Error
- 런타임 시, 시스템 혹은 가상머신에서 비정상적인 상황으로 인해서 발생하는 심각한 수준의 오류이다.
- 개발자가 사전에 예측하여 처리할 수 없기 때문에, 오류에 대한 처리를 신경쓰지 않아도 된다.
- 대표적으로 StackOverflowError, OutOfMemoryError 등이 존재한다.

# Exception
- 런타임 시, 개발자가 잘못 구현한 로직(코드) 혹은 사용자의 잘못된 조작에서 발생하는 오류이다.
- 개발자가 사전에 예측하여 처리할 수 있기 때문에, 예외를 구분하여 그에 맞는 대처를 할 수 있다.
- 대표적으로 IOException, NullPointerException 등이 존재한다.

## Checked Exception & Unchecked Exception

| | Checked Exception | Unchecked Exception |
|:--------|:--------|:--------|
| 예외 처리 | 명시적 예외 처리 | 생략 가능 |
| 확인 시점 | 컴파일 단계 | 런타임 단계 |
| 예외 발생 시, 트랜잭션 처리 | Rollback 수행 | Rollback 미수행 |
| 대표 예외 | Exception 클래스의 자식(서브) 클래스 | RuntimeException 클래스의 자식(서브) 클래스 |
|| IOException | RuntimeException |
|| SQLException | NullPointerException|
|| InterruptedException | ClassCastException |

# 예외 처리
## 방법
### 예외 복구
- 예외 상황을 파악하고 문제를 해결해서 정상 상태로 돌려놓는 방법이다.
- 재시도를 통해 복구하는 방법이 있다.

### 예외처리 회피
- 예외 처리를 직접 담당하지 않고, 호출한 쪽으로 던져 회피하는 방법이다.
- throws 키워드를 이용하여 예외를 전달하는 방법이 있다.

### 예외 전환
- 예외 회피와 비슷하게 메서드 밖으로 예외를 던지지만, 그냥 던지지 않고 적절한 예외로 전환해서 넘기는 방법이다.
- 사용자 정의 Exception을 생성하여 해당 클래스로 throws 키워드를 이용하여 전달하는 방법이 있다.

## 핸들링
# try ~ catch block
- try ~ catch 블록을 이용하여 예외가 발생하는 부분을 감싸고 예외가 발생하면, 적절한 방법으로 처리한다.

```java
public class FileService {
  public List<String> usingTryCatch() {
		List<String> rows = new ArrayList<>();
		// You must declare the InputStreamReader, BufferedReader class outside the try~catch syntax so it can be used and closed.
		InputStreamReader inputStreamReader = new InputStreamReader(FileService.class.getClassLoader().getResourceAsStream("music.txt"));
		BufferedReader bufferedReader = null;
		try {
			bufferedReader = new BufferedReader(inputStreamReader);
			String line;
			while ((line = bufferedReader.readLine()) != null) {
				rows.add(line);
			}
			return rows;
		} catch (IOException e) {
			e.printStackTrace();
		} finally { // Must close the InputStreamReader, BufferedReader class.
			try {
				inputStreamReader.close();
				bufferedReader.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		return null;
	}
	public List<String> usingTryWithResources() {
		List<String> rows = new ArrayList<>();
		try (InputStreamReader inputStreamReader = new InputStreamReader(FileService.class.getClassLoader().getResourceAsStream("music.txt"));
			 BufferedReader bufferedReader = new BufferedReader(inputStreamReader);) {
			String line;
			while ((line = bufferedReader.readLine()) != null) {
				rows.add(line);
			}
			return rows;
		} catch (IOException e) {
			e.printStackTrace();
		} // Even if you don't use the Finally keyword, the BufferedReader closes automatically.
		return null;
	}
}
```
- usingTryCatch 메서드의 경우 InputStreamReader와 BufferedReader를 종료하는 close() 메서드를 호출하기 위해서 finally 구문을 사용해야 하는데 scope의 문제로 try~catch 구문 밖에 변수를 선언하여야 사용하는 불편함이 존재한다.
- usingTryWithResources 메서드의 경우 JDK 1.7부터 지원하는 try-with-resources 구문을 사용하여 소괄호 안에 정의한 변수들은 AutoCloseable 인터페이스를 상속받아 구현되어 있어, 구문 종료 이후 자동으로 리소스 관리를 해준다.

# throws
- 메서드 내부에서 발생하는 Exception을 호출한 메서드로 전달한다.
- 예외처리 회피에 사용되는 방법이다.

```java
public class FileService {
  ...
	public List<String> usingThrows() throws IOException { // Pass the IOException to the caller.
		List<String> rows = new ArrayList<>();
		try (InputStreamReader inputStreamReader = new InputStreamReader(FileService.class.getClassLoader().getResourceAsStream("music.txt"));
			 BufferedReader bufferedReader = new BufferedReader(inputStreamReader)) {
			String line;
			while ((line = bufferedReader.readLine()) != null) {
				rows.add(line);
			}
			return rows;
		}
	}
}
```

# throw
- 메서드 내부에서 발생하는 Exception을 적절한 Exception으로 전환하여 호출한 메서드로 전달한다.
- 예외 전환에 사용되는 방법이다.

```java
public class FileException extends RuntimeException {
	private static final long serialVersionUID = -7903712172617310856L;
	public FileException(String message) {
		super(message);
	}
	public FileException(Throwable cause) {
		super(cause);
	}
	public FileException(String message, Throwable cause) {
		super(message, cause);
	}
}
public class FileService {
  ...
	public List<String> usingThrow() { // Pass the IOException to the caller.
		List<String> rows = new ArrayList<>();
		try (InputStreamReader inputStreamReader = new InputStreamReader(FileService.class.getClassLoader().getResourceAsStream("music.txt"));
			 BufferedReader bufferedReader = new BufferedReader(inputStreamReader)) {
			String line;
			while ((line = bufferedReader.readLine()) != null) {
				rows.add(line);
			}
			return rows;
		} catch (IOException e) {
			throw new FileException("An error occurred while loading the file.", e);
		}
	}
}
```

※ Sample Code는 [여기](https://github.com/GracefulSoul/Sample/tree/master/src/main/java/gracefulsoul/java/exception)에서 확인 가능합니다.
