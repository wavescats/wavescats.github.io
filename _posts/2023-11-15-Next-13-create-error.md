---
layout: post
title: "[Next.js] Next.js 앱을 13 버전으로 다운그레이드하기 🔽"
subtitle: #부제목
categories: [Next.js]
tags: [넥스트, Error, TIL]
---

## 개요 💬

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxGhXi%2FbtsAreaGl6Y%2FgHCs691K1lo2GvkTJ71dDk%2Fimg.png)

<U>멋쟁이사자처럼 프론트엔드 테킷 스쿨 플러스 (이하 FESP)</U> 에서 진행한,<br>
`Next.js` 를 활용하여 날씨 앱을 만드는 과정 중<br>
초기 세팅에서 발생한 에러에 대한 내용을 포스팅 하려고한다.

---

### 앱 생성 💫

`Next.js` 앱을 생성하기 위해 아래 명령어를 실행한다.

```
npx create-next-app [프로젝트 명]
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDAyIQ%2FbtsAouLXbWh%2Ffuzzmyz8kPZ0B11ywqi1I0%2Fimg.png)

---

### Error

#### 버전 에러 💥

`npx` 명령어로 앱을 생성하고 실행하면 아래 에러가 발생할 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFWSlO%2FbtsAmyhfZ4O%2FGvKx9kMTr6HFbkjZdMbKW0%2Fimg.png)

`./node_module` 에 종속성 패키지가 누락되었을 가능성이 있어<br>
`./node_module` 과 `package-lock.json` 파일을 제거 후 다시 `npm install` 명령을 실행한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb1uU7V%2FbtsAmFnaVjt%2FU7tiEISViLm1vx4xAjtV10%2Fimg.png)

이 에러(경고)는 `npx` 로 `Next.js` 앱을 생성하면<br>
최신 비전인 14 버전의 보일러플레이트가 생성되고,<br>
기존에 전역으로 설치되어있는 `node.js` 의 버전과 호환되지 않아 발생하는 에러(경고)이다.<br>

`package.json` 을 확인하여, 현재 설치되어있는 `next` 의 버전을 확인하고,<br>
13 버전으로 다시 설치를 하여 종속성을 추가해준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEZfS5%2FbtsAmFgopyP%2FtAtqYj75sEIgKKK9GX1KWk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdVittK%2FbtsAkvrwPt0%2FFny5IkC1z0WlETUGfqWn90%2Fimg.png)

공식 문서에도 해당 부분에 관련된 사항이 명시되어있다.

> <https://nextjs.org/blog/next-14><br>`Node.js` 의 최소 버전은 18.17 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcMwmaA%2FbtsAnCwPw6c%2FaRuIUGk4XeNb59ppEkCFk1%2Fimg.png)

하지만 이미 13.0.0 버전의 Next 앱을 생성 했으니 계속 진행한다 ⚡

---

#### next.config.js 💢

`npm run dev` 명령으로 설치된 13 버전의 Next 앱을 실행하니 에러 메세지가 변경됬다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcnqTOi%2FbtsAkusNAbS%2FHsukIltOO6DgmnoU9Vszl0%2Fimg.png)

> `no exported configuration found`

해당 에러는 `next.config.js` 파일에 올바른 구성요소가 설정되어 있지 않다는 에러이다.<br>
현재는 아래와 같이 빈 객체를 내보내고 있는데,<br>
이 설정을 초기에 앱을 생성 할 때 설정한<br>
`app` 디렉토리로 실행한다는 `true` 로 설정 후 해당 기능을 활성화 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4Zoz8%2FbtsAri5n1vi%2F6bqktRGyYyIVwH6kMT2Yo1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJd6Ng%2FbtsAmz8qoY8%2FE1ww6hnoAOkUgXlnfrVUK1%2Fimg.png)

---

#### Google Font 🤬

모든 설정이 끝나고 다시 `npm run dev` 명령으로 앱을 실행하니 에러 메세지가 또 변경되었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLKE7v%2FbtsArxuv1Cn%2FpmAojvIt1WjlaAQNVHd3KK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPrkhi%2FbtsAsz6G4MQ%2FZ0ZyQ4bxiuo88B1NkBsPSK%2Fimg.png)

설치되지 않은 종속성 라이브러리인 `@next/font/google` 를 설치하기 위해 아래 명령어를 실행했다.

```
npm install @next/font-google
```

```
yarn add @next/font-google
```

해당 라이브러리를 설치 해 주었지만, 여전히 같은 에러가 발생하여<br>
에러가 발생하는 파일에서 특정 부분을 주석 처리 해 주니 스타일이 적용되지 않은 채 렌더링이 됬다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJeDf9%2FbtsAmEWgSge%2FD4g0vqrQpFHlY3khkOcKX0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FK22uc%2FbtsAqLUktJe%2FKvCPQmbrIP2VKGq8pzVsuk%2Fimg.png)

아직 해당 에러는 원인과 해결방법을 찾지 못했지만,<br>
<U>`Next.js` 의 13 버전과 14 버전에서의 호환성 문제로 발생한 것이 아닐까 ?</U> 라고 예상한다..😥

---

## Reference 🌊

> <https://medium.com/codex/next-js-13-google-fonts-5e0e50e031c6><br><https://www.npmjs.com/package/next-google-fonts><br><https://upmostly.com/next-js/how-to-add-google-fonts-to-your-next-js-app>
