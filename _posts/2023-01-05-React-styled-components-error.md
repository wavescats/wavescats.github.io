---
layout: post
title: "[React] Styled-Components 설치 에러"
subtitle: #부제목
categories: React
tags: [리액트, Error]
---

### 에러 확인
---

클론코딩 진행중에 발생한 에러이다.<br>
순조롭게 따라 진행 중 **styled-components** 를 사용하기 위해 `npm install` 을 입력했다.
<br>
먼저, 강의 영상에서와 같이 yarn 명령어를 통해 설치하려했지만,<br>
아래와 같이 yarn 에 대한 패키지가 설치되어 있지 않아 진행되지 않았다.

```bash
yarn add styled-components
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCrNw8%2FbtrXXxTc7Je%2F9r4xKv0K2xb3SzuPzYC2Wk%2Fimg.png)

그래서 대체 방법으로 npm install 을 사용했다.

```bash
npm install styled-components
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsDxnw%2FbtrXV02ITH2%2FQX1v5frtEdWIDLV4ChwKVk%2Fimg.png)

?????? 에러 발생 😱<br>

구글에 찾아보니,<br>
react 의 버전과 설치하고자하는 패키지의 버전이 일치하지 않아 발생하는 에러라고 한다.

```bash
npm install --verbose
```
```bash
npm install -g yarn
```

> -g 옵션은 전역 (어느 디렉토리에서도 가능하게) 으로 설치하겠다는 옵션.

#### 명령어 재 실행
---

```bash
yarn add styled-components
```
```bash
--legacy-peer-deps
```
구글에 검색해보니 이 명령어를 실행시키라는게 제일 많았다.
(외쳐 갓 구글..✨)

하지만 아무리 해도 안됨..😥


### 에러 해결
---

제일 간단했던건데 미처 생각지 못한 부분이 있었다.<br>

이 에러는 종속성 문제인데,<br>
버전이 달라 종속성에 문제가 생기더라도 버전관계를 무시하고 설치하면 되었다.

위 명령어가 패키지 트리를 빌드할 때<br>
**npm**이 **peerDependencies**를 완전히 무시하도록 하는 명령어 인데,<br>
어떤 패키지를 설치할 때 옵션을 부여할지 명시해주지 않았던 것이다..😮

```bash
npm install styled-components --legacy-peer-deps
```

다음과 같이 설치할 패키지를 명시하고,<br>
뒤에 옵션을 추가하니 정상적으로 설치가 되었고, <br>
**import** 하여 사용할 수 있었다.


### 230225 추가
`styled-components` 를 `react-native expo` 앱 에서 설치할 때의 에러이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmsHYC%2Fbtr0AyjrwA4%2FHSKpwkulOiJtotDL2u8gSK%2Fimg.png)

이전에 발생한 에러와 똑같다.
<br>
에러 메세지를 한번 살펴보자.
<br>
```
npm ERR!   react@"18.1.0" from the root project
npm ERR!   peer react@">= 16.8.0" from styled-components@5.3.6
npm ERR!   node_modules/styled-components
npm ERR!     styled-components@"*" from the root project
```
설치하고자 하는 `styled-components@5.3.6` 모듈은 `react@">=16.8.0` 에 의존한다.<br>
그러나,<br>
root project 에는 `react@">=18.1.0` 버전이 설치되어 있다.
<br>
<br>
메세지 아래에 에러 해결방법에 대해 제공하고 있다.<br>
command 입력 시 `--force` 옵션이나 `--legacy-peer-deps` 를 붙여 실행하면,<br>
위에서 발생한 의존성 에러를 해결 할 수 있다고.

- `npm install --force`

**로컬에 다운로드 이력이 존재하더라도 다시 온라인에서 다운로드 받는다.**

- `npm install --legacy-peer-deps`

**6 버전 이하에서 동작하던 것 처럼 peerDependencies 를 무시하고 설치한다.**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSs9O5%2Fbtr0H7LBEX1%2FUn5KKQiLDoVupwpi8T65kK%2Fimg.png)

### Reference
> <https://velog.io/@whdms3368/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-styled-components-unable-to-resolve-dependency-tree-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0>

> <https://stackoverflow.com/questions/65802896/installing-styled-components-failed-in-react-native>