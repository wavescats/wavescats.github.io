---
layout: post
title: "[React] Vite 앱에서 .env 환경변수 관리하기 (Feat. Firebase 🔥)"
subtitle: #부제목
categories: React
tags: [리액트, Vite, TIL]
---

## 개요 🔔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlVcJQ%2FbtsBxWfCBpO%2FMi2hkuWl6QoeRzsEOMvOa0%2Fimg.png)

프로젝트를 진행하다보면 주로 사용하는 **`파이어베이스`**나,<br>
**`소셜 로그인`** 등의 기능을 구현할 때가 있다.

이 때,<br>
사용되는 **`App key`** 는 고유한 암호와 같은 역할을 하는데,<br>
소스코드를 **`Github`** 에 올릴 때 **`App Key`** 도 포함하여 같이 올리는 경우가 빈번히 있다.

실제 현업에서는 이를 **`.env`**(환경변수) 파일에 정의하여<br>
위와 같은 **`Key`** 를 보안상의 이유로 인해 숨겨야 한다고 한다.

**`React`** 환경에서 **`.env`** 파일에 정의하여 사용하는 형태로 구현했지만,<br>
**`Vite`** 환경이라 그런지 에러가 발생하더라.

그리하여 해당 포스팅 에서는 **`Vite`** 환경에서 **`.env`** 파일을 사용하여<br>
**`App Key`** 와 같은 고유한 정보를 숨긴 채 로직을 수행하는 과정을 담아보려한다.

---

## 환경변수란 ❔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpbHe5%2FbtsBvpwuVEq%2F6043hXq0By6DUALZuDIuB0%2Fimg.png)

환경 변수란 **`Environment Variable`** 라고 하며,<br>
관련된 환경변수는 **`dotenv`** 파일에 정의하여 로직에 사용하곤 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlSFcO%2FbtsBuzlvZx2%2FWRcplsgA62KBxL6ONhcy90%2Fimg.png)

환경 변수는<br>
운영체제나 소프트웨어에서 사용되는 값으로, 시스템 전체(global) 에서 공유되는 변수이다.<br>
주로 시스템 설정, 실행 환경, 사용자 환경 등과 관련된 정보를 저장하는데 사용된다.

사용방법으로는 대게 대문자로 표시되며,<br>
운영 체제에 따라 설정하는 방법이 상이할 수 있다.

> 명령 줄이나 스크립트에서는 주로<br>**`$VARIABLE_NAME`** 또는 **`%VARIABLE_NAME%`** 과 같은 형식으로 참조한다.

---

## Vite ⚡

개요 에서 언급했듯,<br>
**`파이어베이스`** 사용하기 위해 **`App Key`** 를 발급받고, 이를 로직에서 불러와 사용하는 경우가 생겼다.

**`Vite`** 또한 **`React`** 기반이기에, 아래와 같이 사용했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0osRN%2FbtsBvqokP2F%2FqMDzXdleIhuoHIL2KW2Tjk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEgt5E%2FbtsBynEpCCq%2FMTCPkdDd4MMH3zSanXDARK%2Fimg.png)

### 에러 발생 🚫

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZxKRJ%2FbtsBxUibqCN%2Fz6URSxVCknP0Sw9UaklC90%2Fimg.png)

**`process is not defined`** 에러가 발생했다.

기존의 환경변수 사용법 으로는,<br>

1️⃣ 루트 디렉토리에 **`.env`** 파일을 생성하고,<br>
2️⃣ 변수명이 **`REACT_APP_`** 으로 시작하는 변수를 생성하고<br>
3️⃣ 로직에서 **`process.env.변수명`** 으로 호출하여 사용

> 변수에 들어가는 값은 문자열("") 로 감싸거나 띄어쓰기를 주지 말기 ❗❗

위 과정으로 사용했지만,<br>
**`Vite`** 환경에서는 조금, 아주 조금 사용방법이 달랐다.

---

### 에러 해결 ✔

1️⃣ 루트 디렉토리에 **`.env`** 파일을 생성<br>
2️⃣ **`VITE_`** 으로 시작하는 변수 생성<br>
3️⃣ **`import.meta.env.변수명`** 으로 호출하여 사용

> 문자열("") 로 감싸도 허용 가능 ❗❗

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc5LlFg%2FbtsBtHxIKPk%2Fx8oZX18DmfEz3HddaCVLTk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fxf5KS%2FbtsByAKsRul%2F7a2uwiECBcMai7jKA4RfCK%2Fimg.png)

> **`VITE_`** 를 붙이지 않은 변수명은 검색되지 않아 다시 위와같은 에러가 발생할 수 있다 😫

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fsldo0%2FbtsBurawwR2%2Ft5wmZEOEIhZUfRRtNrrJX0%2Fimg.png)

에러를 해결하고<br>
해당 기능을 구현하기 위해 사용한 **`Firestore`** 를 **`console.log`** 로 찍어보니<br>
해당 **`App Key`** 가 **`__private`** 의 형태로 숨겨진 채 브라우저 콘솔에 출력되고 있다.

마지막으로,<br>
설정을 모두 마친 **`.env`** 파일은 **`Github`** 에 올라가면 안되기 때문에<br>
**`gitignore`** 에 반드시 추가 해 주어야 한다.

> #<br>.env

---

## localhost 😎

**`파이어베이스`** 를 사용하려면 승인된 도메인만이 인증을 받을 수 있다.

하지만,<br>
**`Vite`** 는, **`127.0.0.0:5173`** 과 같은 형태로 앱이 실행되기 때문에 도메인을 추가 해 주어야 한다.

이를 해결 해 주기 위해 도메인을 추가하지 않고,<br>
프로젝트를 실행하는 명령어를 수정함으로 간단히 해결할 수 있었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvfSfh%2FbtsBuamBKQr%2FIkS84cVuJEVRGYaKSa9D50%2Fimg.png)

---

## Reference 🌊

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxdipM%2FbtsBubrRw3w%2FsEC0G6jNHovV9nbRUP5iR0%2Fimg.png)

> <https://ko.vitejs.dev/guide/env-and-mode.html><br><https://velog.io/@tmdgp0212/TIL230316-using-.env-on-vite><br>
