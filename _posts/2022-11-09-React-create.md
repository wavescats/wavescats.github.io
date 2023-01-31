---
layout: post
title: "[React] 프로젝트 생성 시 발생한 에러 'npx create-react-app'"
subtitle: #부제목
categories: Error
tags: [리액트]
---

### 에러 확인
---

새로운 프로젝트를 위해 npx 명령어를 입력하던와중 에러가 발생했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWShNq%2FbtrXGTDAx3T%2FHZXUZK4y8Ksm5fHsg5hATK%2Fimg.jpg) 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcOWFbO%2FbtrXHBJwcRG%2FlAgCFgG9OlbO4DaqC5Okh0%2Fimg.jpg)


에러를 살펴보면,<br>

> *name can no longer contain capital letters

npm이 사용하는 명령어의 일부이거나 프로젝트명에<br>
대 소문자 또는 특수기호를 입력하지 말라는 뜻 이다.
<br>

아마, 프로젝트를 생성하기 전<br>
프로젝트를 위한 빈 디렉토리를 생성하고 명령어를 입력해서 발생했던 실수인것같다.
<br>

> 생성하는 리액트 프로젝트명에는 대문자나 특수기호가 포함되어있는지 꼭 확인하자.

<br>
<br>

### 에러 해결
---

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEyJeK%2FbtrXHXFhyKn%2F0VrEoneHCRgbAbmSeZvYNK%2Fimg.jpg)

프로젝트명을 소문자로 변경하니 정상적으로 실행됨을 알 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmVKuT%2FbtrXJ2ZSK9Z%2FD6GLoMNWgAtpUMzWjVQK70%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcAdGLr%2FbtrXHPHtom9%2Fiq1ngvoKAgBuOGJkvqa0I1%2Fimg.jpg)