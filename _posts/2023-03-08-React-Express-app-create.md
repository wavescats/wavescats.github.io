---
layout: post
title: "[React] Express 앱 10분만에 만들기"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL, Express]
---

## 개요

이번 포스팅은 React 와 Express 를 활용하여 서버와의 통신을 간단하게 구축해보려고한다.

### 라이브러리 설치
- nodemon
```
npm i nodemon -D
```
`nodemon` 은 node monitor 의 약자로,<br>
노드가 실행하는 파일이 속한 디렉터리를 주시/감시하고 있다가<br>
파일이 수정되면 자동으로 애플리케이션을 재시작하게 해 주는 라이브러리 이다.<br>
> 즉, <br>
nodemon 을 활용하면 수정사항을 반영하기 위해 매번 애플리케이션을 재시작 할 필요가 없다.

- Babel
```
npm i @babel/core @babel/cli @babel/node @babel/preset-env -D
```
`Babel` 은 작성한 코드를 컴퓨터가 이해할 수 있도록 변환 해 주는 컴파일러의 역할을 수행한다.<br>
> 즉, 작성한 코드가 다양한 브라우저에서 호환하여 작동하여야 할 때 (크로스 브라우징)<br>`Babel` 을 사용한다.

- Express
```
npm i express
```
`Express` 란 node.js 를 기반으로 만들어진 웹 애플리케이션 프레임워크이다.<br>
> <https://expressjs.com/ko/>

- Pug
```
npm i pug
```
`Pug` 는 Node Express Template Engine 으로,<br>
`Express` 의 패키지 view engine 이다.
<br>
`HTML` 을 `Pug` 문법으로 작성하면 `HTML` 문법으로 변환 해 주는 기능을 갖고 있다.<br>
이를 통해 코드를 간단하게 표현 해 주며,<br>
JS 의 연산 결과를 쉽게 보여주어 코드의 가독성이 향상되는 장점을 갖고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbB9rHl%2Fbtr2Gt7KrFH%2Fw3obGkTBBxt4DQ1Ye2TxCK%2Fimg.png)

---

### 디렉토리 구성
```
├── src/server.js
│
├── bable.config.json
├── nodemon.js
└── .gitignore
```
`src` 폴더를 생성 후 내부에 server.js 파일을 생성 해 주고,<br>
루트 디렉토리에서 나머지 파일들을 touch 명령어로 생성 해 주었다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbansoV%2Fbtr2Oqh42Qw%2FhfP5r5g8DKlU9D8GK8F6lk%2Fimg.png)

먼저,<br>
`babel.config.json` 파일 내부에 코드를 작성하여 컴파일이 가능하도록 설정 해 준다.
```
{
	"presets": ["@babel/preset-env"]
}
```
> `presets` (사전설정)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrhzQL%2Fbtr2O28VomF%2F73CR1Vkoqsk5JES8F3jb5k%2Fimg.png)

다음으로 `nodemon.json` 파일 내부에<br>
exec 명령어를 통해 server.js 를 실행시키기 위해 아래 설정을 입력 해준다.
```
{
    "exec": "babel-node src/server.js"
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdqIBIh%2Fbtr2QLZ3wZJ%2FkYuOyQPgb9a5WwXorGYB50%2Fimg.png)

마지막으로,<br>
`.gitignore` 파일에는 Github 에 Push 할 때 예외 대상을 지정 해 주는 설정을 적어준다.<br>

`/node_modules`

> `/node_modules` 디렉토리를 Github 에 Push 하지 않겟다는 의미

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdsJBSY%2Fbtr2GtfFcpB%2FoksJv46CKsYlbcnNWZI7z1%2Fimg.png)

---

### 서버 실행
먼저 `server.js` 에 설치한 Express 모듈을 import 해 주고,<br>
`const app = Express()` 로 Express 앱을 생성 해 준다.

후에 `app.listen(3000)` 을 통해 서버(3000번 포트) 와 연결 해 준다.<br>

> 서버와 연결이 잘 되었는지 확인하기 위해 `consol.log` 도 작성 해 줌.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb8SeDA%2Fbtr2OQt1UOK%2Fq1bJacnyF7i1hy4Ssl2Vtk%2Fimg.png)

`scripts` 를 실행하기 위해 `npm run dev` 를 터미널에 입력 해 주면,<br>
다음과 같이 `consol.log` 에 작성했던 메세지를 확인할 수 있으며,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBZjOF%2Fbtr2GsVgynV%2FhmNnJ7mSckSNfDcLuLsji1%2Fimg.png)

`localhost:3000` 에 접속 시 페이지를 찾을 수 없다는 에러가 아닌 다음과 같은 메세지가 출력 될 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcxzdL8%2Fbtr2PzMk2hm%2F3hDniiDAhZUWinlSus7g5K%2Fimg.png)

<br>
<br>

이상으로 간단한 Express 앱을 만들어 서버와 통신하는 작업을 마쳤으며,<br>
이후에는 사용자가 눈으로 볼 수있는 Front 영역을 생성 해 보도록 하겠다.


### Reference
> <https://nomadcoders.co/noom/lectures/3074><br><https://velog.io/@wheezy_han/Node.js-nodemon-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%8B%A4%ED%96%89%EB%B0%A9%EB%B2%95><br><https://velog.io/@cks3066/Babel-Babel%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0%EC%99%80-%EC%97%AD%ED%95%A0><br><https://ninjaggobugi.tistory.com/9><br><https://dydals5678.tistory.com/91><br><https://jeonghwan-kim.github.io/series/2019/12/22/frontend-dev-env-babel.html>