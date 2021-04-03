---
title: "JavaScript"
excerpt: "JavaScript 대한 설명"
last_modified_at: 2021-04-02T20:10:00
header:
  image: /assets/images/javascript/javascript.png
categories:
  - JavaScript
tags:
  - Programming
  - JavaScript

toc: true
toc_ads: true
toc_sticky: true
---
# JavaScript
- 가벼운 Interpreter 또는 JIT Compile 프로그래밍 언어이다.
- First-Class Functions를 지원한다.
- Prototype 기반, 다중 패러다임 스크립트 언어이다.
- 동적이고 Command, [Object-Oriented Programming(OOP)](../../paradigm/oop), [Functional Programming(FP)](../../paradigm/fp) 스타일을 지원한다.
- 변수 자료형이 선언되지 않는다.(Dynamic Typing, Loosely Typed)

# First-Class Functions, 일급 함수
- 매개변수로 제공이 가능하다.

```js
function sayHello() {
   return "Hello, ";
}
function greeting(helloMessage, name) {
  console.log(helloMessage() + name);
}
// Pass `sayHello` as an argument to `greeting` function.
greeting(sayHello, "JavaScript!");
```

- 함수가 함수를 반환할 수 있다.

```js
// Using a variable.
const sayHello = function() {
   return function() {
      console.log("Hello!");
   }
}
const myFunc = sayHello();
myFunc();
```

```js
// Using double parentheses.
function sayHello() {
   return function() {
      console.log("Hello!");
   }
}
sayHello()();
```

- 변수에 할당이 가능하다.

```js
const foo = function() {
   console.log("foobar");
}
// Invoke it using the variable.
foo();
```

# Library
## [JQuery](https://jquery.com/)
- 이벤트 처리, CSS 애니메이션 및 Ajax 뿐만 아니라 HTML Document Object Model(DOM)트리 탐색 및 조작을 단순화하도록 설계된 JavaScript Library이다.

## [React](https://reactjs.org/)
- User Interface 또는 UI Components를 구축하기위한 Open Source, Front-End, JavaScript Library이다.

# Framework
## [Bootstrap](https://getbootstrap.com/)
- Responsive Mobile-First Front-End Web 개발을 위한 무료 오픈 소스 Framework이다.

## [Angular.js](https://angularjs.org/) / [Angular](https://angular.io/)
- JavaScript에 정적 타입 개념을 추가한 신형 언어인 [TypeScript](https://www.typescriptlang.org/) 기반 오픈 소스 Web Application Framework이다.
- Angular 1.x 버전은 Angular.js, Angular 2 버전 이상부터 Angular로 불린다.

## [Vue.js](https://vuejs.org/)
- User Interface 및 Single-Page Application(SPA)을 구축하기위한 오픈 소스 Model-View-ViewModel Front-End JavaScript Framework이다.
- 선언적 렌더링 및 구성요소의 구성에 초점을 맞추어 점진적으로 적응이 가능한 아키텍처를 제공한다.

# [ECMAScript](http://www.ecma-international.org/)
- JavaScript를 이루는 코어 스크립트 언어이자 표준([ECMA-262](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/))이다.

# Reference
- [Wiki-JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)