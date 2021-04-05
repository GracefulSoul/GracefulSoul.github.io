---
title: "JavaScript Asynchronous"
excerpt: "JavaScript 대한 설명"
last_modified_at: 2021-04-05T20:10:00
header:
  image: /assets/images/javascript/asynchronous.png
categories:
  - JavaScript
tags:
  - Programming
  - JavaScript
  - Asynchronous

toc: true
toc_ads: true
toc_sticky: true
---
# Promise
- 자바스크립트 비동기 처리에 사용되는 객체이다.

## 상태
### Pending, 대기
- 비동기 처리 로직이 아직 완료되지 않은 상태이다. new Promise()  함수를 호출하면  대기 상태가 된다.

### Fulfilled, 이행
- 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태이다. 콜백 함수의 인자 resolve를 실행하면 이행 상태가 된다.

### Rejected, 실패
- 비동기 처리가 실패하거나 오류가 발생한 상태이다. 콜백 함수의 인자 reject를 실행하면 실패 상태가 된다.

## Promise Chaining, 프로미스 연결
- then() 메서드를 호출하면 새로운 프로미스 객체를 반환하여 다시 then() 메서드를 이어서 사용 가능하다.

```js
new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000);
}).then(function(result) {
  alert(result); // 1
  return result * 2;
}).then(function(result) {
  alert(result); // 2
  return result * 2;
}).then(function(result) {
  alert(result); // 4
  return result * 2;
});
```

## 오류 처리
- then()을 사용하여 두 번째 인자로 에러를 처리하는 방법.
  - 이 방법으로 호출되면 Uncaught Error가 발생하여, catch()를 이용하도록 한다.
- catch()를 이용하여 에러를 처리하는 방법.

# async, await
- 자바스크립트 비동기 처리 패턴 중 가장 최근에 나온 문법이다.
- 기존 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성 할 수 있도록 해준다.

```js
async function asyncFunction() {
  const data = await asyncMethod();
  // Logic.
}
```

## async
- 비동기 처리를 하는 함수 앞에 async라는 키워드를 사용한다.
- Ex. async function 함수명() {}

## await
- 비동기 처리를 하는 코드 앞에 await라는 키워드를 사용한다.
- Ex. await 함수명()