---
layout: post
title: "[React] Styled-Components 설치 에러"
subtitle: #부제목
categories: Error
tags: [리액트]
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

### Reference
> <https://velog.io/@whdms3368/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-styled-components-unable-to-resolve-dependency-tree-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0>

> <https://stackoverflow.com/questions/65802896/installing-styled-components-failed-in-react-native>