---
layout: post
title: "[React] JS 파일과 JSX 파일의 차이 🌊"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

## 개요

프로젝트 및 코드를 작성하다보면,<br>
JS 파일의 형태와 JSX 형태의 파일을 마주친 적이 있었다.<br>
<br>
JS 는 자바스크립트 언어로 구성되어있음을 인지하고있었는데,<br>
과연 **그럼 JSX 파일은 뭘까 ⁉️** 라는 궁금증에서 출발하려한다.

---

### 파일 확장자 ☑️

- JS
  - JavaScript XML 의 약자

<br>

- JSX
  - JavaScript 코드와 함께 XML 과 유사한 문법을 사용가능

---

### 문법 🚝

- JS
  - 순수한 JavaScript 코드로 작성됨<br>
    - 기본적인 JavaScript 문법과 구문을 따르며 HTML 로 작성 시 문자열로 작성해야한다

<br>

- JSX

  - JavaScript 의 확장 문법으로,<br>
    HTML 과 유사한 구문을 사용하여 컴포넌트를 작성할 수 있다
    <br>
  - 이를 통해 컴포넌트의 구조와 렌더링을 더 쉽게 구현할 수 있다<br>
  - JavaScipt 코드를 사용하기 위해 중괄호('{}')를 사용

---

### 컴포넌트 정의 🏭

- JS

  - 함수(Function) 나 클래스(Class) 로 정의

- JSX

  - 컴포넌트를 JSX 구문으로 정의하고,<br>
    이를 JavaScript 함수나 클래스로 감싸서 사용한다
    <br>
  - JSX 문법은,<br>
    HTML 과 유사하게 컴포넌트의 구조와 속성을 표현할 수 있다.

---

### 결론 🌅

즉,<br>
JS 는 순수(표준) 자바스크립트 코드로 작성됨을 알수있고,<br>
JSX 는 사용자가 보다 쉽고 직관적이게 리액트 컴포넌트를 만들 수 있는<br>
HTML 식의 문법을 말한다.<br>

> React 프로젝트에서는 주로 JSX 파일을 사용하여 컴포넌트를 작성하고,<br>
> JavaScript 모듈로 사용되어 애플리케이션을 구성한다.

---

### Reference 🏊

> <https://stackoverflow.com/questions/46169472/reactjs-js-vs-jsx><br><https://stackoverflow.com/questions/46169472/reactjs-js-vs-jsx/46169521#46169521><br><https://ko.legacy.reactjs.org/docs/introducing-jsx.html><br><https://legacy.reactjs.org/docs/jsx-in-depth.html#why-jsx><br><https://bo5mi.tistory.com/190>
