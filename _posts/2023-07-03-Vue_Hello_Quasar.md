---
layout: post
title: "[Vue.js] Quasar 프레임워크로 프로젝트 초기 세팅하기 💘"
subtitle: #부제목
categories: [Vue.js]
tags: [뷰js, TIL]
---

### 개요

Quasar 은 Vue.js 기반의 프레임워크로,<br>
다양한 플랫폼에서 애플리케이션을 개발할 수 있도록 구현되어있다.<br><br>

해당 포스팅에서는,<br>
Quasar CLI 를 사용하여<br>
Quasar 앱을 생성하는 과정을 정리하고자 한다.

### yarn

yarn 으로 설치 할 경우

> <https://yarnpkg.com/><br> `yarn global add @quasar/cli`

---

### npm

npm 으로 설치 할 경우

> <https://nodejs.org/en><br> `npm install -g @quasar/cli`

---

두 패키지 매니저 중 하나를 선택하여<br>
Quasar 명령어를 입력 받을 수 있도록 CLI 를 설치 해 준다.
<br><Br>
나는 yarn 으로 CLI 를 설치하려 했지만,<br>
로컬에 yarn 이 설치되어 있지 않아 npm 으로 설치를 진행 해 주었다.

---

### 설치 과정

- Quasar CLI 가 설치되어 있지 않아 create 명령어를 인식하지 못하는 경우

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FARHxA%2FbtsmfL8TooG%2Fu683XQGYNDCKoQ2Cn2CHlK%2Fimg.jpg)

- yarn 으로 CLI 를 전역으로 설치하는 경우

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcPQ6vM%2Fbtsmd1Rxd6Q%2Fb2yiZetRgu4K2MYD155pJK%2Fimg.jpg)

- 하지만, yarn Package Manager 가 설치되어 있지 않아 create 명령어를 인식하지 못함.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSaCc8%2FbtsmiEhpsKa%2FWIGu53LOnNyERMejdHpVz1%2Fimg.jpg)

- 이미 설치 되어있는 npm Package Manager 로 변경

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9SZwd%2Fbtsl9vMoz2T%2F0zWQxelUgIlRPFHWQLjRZK%2Fimg.jpg)

> <https://nodejs.org/en><br>

1. 해당 사이트에서 LTS 버전으로 다운로드 진행<br>
2. 환경변수로 PATH 설정 후 진행
   <br><Br>

- npm 명령어를 통해 전역으로 CLI 를 설치하는 경우

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnCGXV%2FbtsmkbMLgqD%2FXrc5mJ6w5Jf9TzWOWKuG6k%2Fimg.jpg)

- create 명령어를 인식하지만, 명령어의 업데이트로 인한 에러

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft0ava%2FbtsmkODxtxq%2FlJAYVKY0rWXvw0ksZLc3z1%2Fimg.jpg)

해당 경우는,<br>
Quasar CLI 의 버전 및 템플릿 변경으로 인해 발생하는 에러이며,<br>
최신 버전의 Quasar CLI 에서는 `quasar create` 대신<br>
`yarn create quasar` or `npm init quasar` 을 통해<br>
Quasar 프로젝트를 생성할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZo2Cf%2FbtsmfMfIuSf%2FmzQSw9bxx442JiSb1R8b30%2Fimg.jpg)

---

### Reference

> <https://nodejs.org/en><br><https://yarnpkg.com/><br><https://malwareanalysis.tistory.com/532><br><https://programforlife.tistory.com/69>
