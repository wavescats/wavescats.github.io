---
layout: post
title: "[React] Cannot read properties of undefined (reading 'xxx') - 1"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, Error]
---

### 에러 확인
사이드 프로젝트로 청첩장 앱을 개발하던 중 생긴 에러이다.

`App.js` 에서 `data.json` 파일을 import 하여 데이터를 props 로 넘겨주어<br>
`Area1.jsx` 에서 데이터 url 을 props 하여 화면에 뿌려주는 과정을 진행하고 있었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcxJ9Bm%2Fbtr1pWX0NXi%2FCvGEKRzGpTOU1z5V1f1qj0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcomC4j%2Fbtr1EfvjtRT%2FrKdVj7hrASz0sYWinxW5yk%2Fimg.png)

어제까지만 해도 에러 없이 정상적으로 실행되어<br>
Git Hub 에 Push 까지 마친 상태였지만,<br>
오늘 다시 앱을 실행 해보니 아래와 같은 에러가 콘솔창에 보여지고 있었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAtJqx%2Fbtr1MoR5PRv%2FOC6R5bblIFyr2LbRUzJbI0%2Fimg.png)

에러를 확인 해 보니,<br>
이전에 포스팅 했던 에러와 같은 에러였다.

> <https://wavescats.github.io/react/2022/11/14/React-properties-of-undefined-error.html>

리액트에서 가장 자주 보는 오류 메시지로<br>
('') 안의 값이 정의되지 않아 불러올 수 없을 때 발생한다고 한다.<br>

`img1` 의 값은 `data.json` 에 정의되어 있다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC3hee%2Fbtr1I9BmZdy%2FaBvuvgQ33eKC8OR1fdFPPk%2Fimg.png)

주소를 Ctrl + 클릭 하여 접속 해 보니 이미지가 정상적으로 불러와 지는걸 보아,<br>
다른 곳에서 에러가 발생한 것 같다.
<br>

---

### 에러 해결
`App.js` 에 정의되어 있는 `useEffect` 때문에 발생한 에러였다.<br>
코드를 살펴보면,<br>
<br>

`useEffect` 는,<br>
`setLandingPage` 가 `JsonData` 를 받아 렌더링 시 빈 배열을 뱉어내는 형태로 구현되어 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FddZFQk%2Fbtr1uejQG4c%2FwOqoUnV6mat81a6tltRuJk%2Fimg.png)

빈 배열의 의미는,<br>
이펙트에 리액트 데이터 흐름에 관여하는 어떠한 값도 사용하지 않겠다는 뜻으로<br>
실제로 값이 사용되어야 할 때 버그를 일으키는 주된 원인 중 하나로 꼽히기도 한다.
<br>

즉,<br>
해당 프로젝트에서 원했던 요구사항은<br>
페이지 랜더링 시 한번에 별다른 조건 없이 모든 데이터를 보여주기만 하면됐엇기에<br>
`useState` 나 `useEffect` Hooks 를 사용할 필요가 없었다.

---

### 어제는 됐는데 오늘은 안될때 ?
`useEffect` Hooks 를 사용하여<br>
작성한 로직대로 페이지 렌더링 시 요구사항을 화면에 뿌려주는 작업까지 마친 뒤<br>
Git Hub 에 push 를 했지만,<br>
<br>
오늘은 안됐던 이유는,<br>
`useEffect` 구문이 실행되어 에러가 발생한 것 같다.

#### 그럼 어제는?
로컬 서버가 켜져있는 상태(이미 렌더링 되어있는 상태) 로 이미지 데이터를 불러왔기에<br>
`useEffect` 가 실행되지 않은 상태로 화면에 뿌려졌던것 같다고 추측하는 바 이다.

---

### Reference
> <https://velog.io/@nemo/react-error-cannot-read-property><br>
<https://overreacted.io/ko/a-complete-guide-to-useeffect/>
