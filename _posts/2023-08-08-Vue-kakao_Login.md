---
layout: post
title: "[Vue.js] 카카오 소셜로그인 구현하기 (feat.Express)"
subtitle: #부제목
categories: [Vue.js]
tags: [뷰js, TIL]
---

## 개요

서비스를 이용하려면,<br>
사용자의 정보를 바탕으로 사용자 인증을 구현해야 할 때가 있다.<br>
대표적인 예로 `google` 로그인이 있을것이며,<br>
각종 소셜 로그인이 있을테지만<br>
이번 포스팅 에서는 카카오플랫폼을 활용한 소셜 로그인을 `Client` 에서 구현하고,<br>
`Server` 측 에서 다시 `Client` 측으로 보내주는 간단한 로직을 구현하여 기록하고자 한다.

---

## 카카오 Process

아래의 Process 는 Kakao Developer 에서 제공하는 Docs 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIFe8p%2FbtsqBoOPElL%2FYAPCeNWVW2CIYYsUJY8Q01%2Fimg.png)

해당 로직을 내가 이해한 대로 간단히 요약하자면,<br><br>

1. 클라이언트에서 카카오서버에 요청을 보내어<br>
   요청을 보낸 사용자가 카카오 서버에 있는 사용자 인지 유무를 판별한다.

2. 카카오 서버에 있는 사용자라면 인가코드와 함께 토큰을 발급해주고

3. 등록한 Redirect URI 로 페이지를 이동시켜준다 -> 이 때 토큰이 필요 !

---

해당 로직을 모두 구현하고자 하면,<br>
프론트엔드 혹은 백엔드 모두 **혼자 구현이 가능**하다고 한다.<br>
하지만 그렇게 될 경우 `cors` 에러가 발생할 경우가 있다고 하니,<br>
**`인가코드 받기`** 혹은 **`토큰 받기`** 를 기준으로 역할을 나누는 것이 좋을 것 같다.<br><br>

만약 이 로직을 혼자 구현한다면 아래와 같은 로직으로 구현 될 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxXT0z%2FbtsqBGV02t5%2FlSEe9PmfdGt5nwFoNfrPD1%2Fimg.png)

이 로직을 `Client` 는 `Vue.js` 로 구현 해 볼 것이며,<br>
`Server` 는 `Node.js` 프레임워크인 `Express` 를 사용하여 `Axios` 로 통신을 할 예정이다.

---

### Client

- 전체 코드

```javascript
<template>
    <a @click="loginWithKakao">
        <img src="./../assets/kakao_login_medium.png" />
    </a>
</template>

<script setup>
import axios from 'axios';
import server from './../config/server.json';

const loginWithKakao = () => {
  window.Kakao.Auth.login({
    scope: 'profile_nickname, profile_image, account_email, gender',
    success: getProfile,
  });
};

const getProfile = (authObj) => {
  console.log('authObj', authObj);
  window.Kakao.API.request({
    url: '/v2/user/me',
    success: (res) => {
      const kakao_account = res.kakao_account;
      console.log('kakao_account', kakao_account);

      // kakao_account 를 받은 login 함수를 사용
      login(kakao_account);
      alert('로그인 성공');
    },
  });
};

const login = async (kakao_account) => {
  try {
    const response = await axios.post(server.url + `/api/login`, { kakao_account });
    console.log(response.data.message); // Login successful
  } catch (error) {
    console.error('Login failed', error);
  }
};
</script>
```

카카오에서 제공하는 **`Kakao.Auth.login` 함수를 사용하기 위해**서는,<br>
`index.html` 에 SDK scripts 를 `head` 태그 내부에 삽입 해 주어야 한다.

```javascript
const loginWithKakao = () => {
  window.Kakao.Auth.login({
    scope: "profile_nickname, profile_image, account_email, gender",
    success: getProfile,
  });
};
```

해당 함수에서 사용된 `scope` 는 4개의 인자를 받는데,<br>
이 값은 로그인 시 사용되는 동의항목의 ID 값 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqE5ZB%2FbtsquBV6FnT%2FVQjRTgcHAoZGZ5EF4WEsrK%2Fimg.png)

```javscript
const getProfile = (authObj) => {
  console.log('authObj', authObj);
  window.Kakao.API.request({
    url: '/v2/user/me',
    success: (res) => {
      const kakao_account = res.kakao_account;
      console.log('kakao_account', kakao_account);

      // kakao_account 를 받은 login 함수를 사용
      login(kakao_account);
      alert('로그인 성공');
    },
  });
};
```

`getProfile` 함수에서는<br>
`window` 함수를 통해 **카카오 서버로부터 인가코드를 성공적으로 받았을 경우**<br>
authObj 라는 파라미터를 받을 수 있는데,<br>
이 값을 `console.log` 로 찍어 보면 로그인에 사용된 정보를 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbafpPD%2Fbtsqvg42Czv%2FLBLB4vOgi62e7DgF3xFsRk%2Fimg.png)

이 파라미터를 가지고 카카오에서 제공하는 API 를 활용하여 서버측에 전송할 데이터를 가공할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmTQ9V%2FbtsqB1Z3mjD%2FO5dRUg8r49iQuYIeBd6uwK%2Fimg.png)

이제 가공된 데이터를 서버측에 보내주어야 하는데,<br>
이 데이터는 **비동기적으로 처리**되기때문에<br>
`async - await` 문으로 작성할 수 있다.

```javascript
const login = async (kakao_account) => {
  try {
    const response = await axios.post(server.url + `/api/login`, {
      kakao_account,
    });
    console.log(response.data.message); // Login successful
  } catch (error) {
    console.error("Login failed", error);
  }
};
```

위 코드를 보면<br>
비동기로 작성된 `login` 함수를 `getProfile` 함수가 참조하는것을 알 수 있다.<br><br>

`Server` 측으로 `/api/login` 주소로 요청을 보내면,<br>
`Server` 에서는 요청한 값이 담긴 URL 을 받을 엔드포인트를 지정 해주면 서버측 콘솔에 `kakao_account` 의 값이 출력될것이다.<br>

`server.url` 에 담긴 값은 import 한 url 을 호출하는 형태로 되어있다.

```javascript
// ./server.json
{
    "url": "http://localhost:8080"
}
```

Client 측에서 작성된 전체 코드를 보면,<br>
요청한 값을 로컬스토리지에 저장하는 로직이 담겨있지 않음에도 불구하고<br>
kakao\_ 라는 이름의 `key`, `value` 가 저장 됨을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJIo1Z%2FbtsqCab7C1c%2Fg7SbkE4pG85NGqn0mHMnq0%2Fimg.png)

이 값은 아마 `index.html` 에 심어놓은 SDK 에<br>
**자체적으로 내장되어있는 함수**가 존재하리라고 예상하는 바 이다.

### Server

- 전체 코드

```javascript
const express = require("express");
const cors = require("cors");
const bodyParser = require("body-parser");

const app = express();
const PORT = 8080;

app.use(cors());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json()); // body-parser 미들웨어 사용

app.post("/api/login", function (req, res) {
  console.log(req.body); // 클라이언트로부터 받은 결과 값
  // DB 설계 로직 작성

  // 응답 -> 클라이언트
  res.json({ message: "Login successful" });
});

app.listen(PORT, () => {
  console.log(`open server : ${PORT}`);
});
```

생각보다 `Server` 측 코드는 `Client` 보다 비교적 간단하다.<br>

```javascript
const express = require("express");
const cors = require("cors");
const bodyParser = require("body-parser");
```

먼저,<br>
`express`, `cors`, `body-parser` 를 사용하기에 앞서<br>
패키지 명령어로 해당 **모듈들을 설치** 해 준다.

```
npm i express cors body-parser
```

> 한줄로 설치 명령어를 작성하여 동시에 설치가 가능하다.

설치된 모듈들은 `require` 명령어로 불러올 수 있다.

> Client 에서는 `require` 가 아닌 `import` 를 사용했지만,
> 일맥상통하다.

```javascript
const app = express();
const PORT = 8080;
```

`require` 로 불러온 모듈을 변수에 담아 선언 해 준다.

```javascript
app.use(cors());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json()); // body-parser 미들웨어 사용
```

변수 `app` 에 담긴 `express` 를 사용하여<br>
지정한 모듈을 사용하겠다는 `use` 명령어를 선언 해 준다.

---

#### body-parser

> body-parser 모듈은<br> > `Client` 측에서 POST 요청으로 보낸 **`Request data`** 의 **`body`** 로 부터<br>
> 파라미터를 편리하게 추출할 수 있는 모듈이다.

```javascript
{
  userID : "힝",
  password : "나도몰라"
}
```

다음과 같은 데이터를 body 에 담아 POST request 를 보낸다면,<br>
`Server` 측 에서 `Express` 를 사용하여 POST request 를 처리하는 방법은 아래와 같다.

```javascript
var express = require('express')
var app = express()
app.post('/profile', function(req, res) => {
  console.log(req.body)
})
```

만약,<br>
`body-parser` 라이브러리가 없는 경우,<br>
`console.log(req.body)` 라인에서 undefined Error 를 볼 수 있을것이다.

> `req.body` 는 `body-parser` 를 사용하기 전에는<br>
> default 값 으로 Undefined 가 설정 되기 때문이다.
> <br><br>
> 해당 에러를 해결하기 위해 `body-parser` 라이브러리를 설치한다.

```bash
npm i body-parser
```

```javascript
var express = require('express')
var bodyParser = require('body-parser')

var app = express();

app.use(bodyParser().json())

app.post('/profile', function(req, res) => {
  console.log(req.body)
})
```

이제 `console.log` 를 통해 req.body 에 담긴 값을 json 형태로 확인할 수 있을것이다.

---

다시 `Server` 측 코드로 돌아와서,<br>

```javascript
app.post("/api/login", function (req, res) {
  console.log(req.body); // 클라이언트로부터 받은 결과 값
  // DB 설계 로직 작성

  // 응답 -> 클라이언트
  res.json({ message: "Login successful" });
});
```

해당 로직은 `Client` 에서<br>
`/app/login` 의 URL 로 POST 요청을 보낸 값을 확인할 수 있는 로직이다.

> POST 로 보낸 값은 `req.body` 에 담김

`req` 는 request 의 약자이며,<br>
`res` 는 response 의 약자이다.

정상적으로 `Client` 에서 요청한 값이 불러와졌다면,<br>
아래 로직인 `res.json` 에 작성된 `message` 를 Console 창에 출력한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FG9geh%2FbtsqBG3sER3%2FYcjATXKnJvl0UQkA3bN6PK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlOaH7%2FbtsqD5HQudH%2FcK6Za0FHLkspDMMOge8tKK%2Fimg.png)

---

여기까지 클라이언트와 카카오서버, 로컬 서버와의 통신을<br>
간단하게 구현 해 보았는데<bR>
이제 이 로직에서 **`jwt`, `uuid` 혹은 `nanoid` 라이브러리를 사용**하여<br>
요청한 값을 해쉬 형태로 암호화 하여 **DB 에 저장**하는 형태로 구현 해 볼 예정을 갖고있다.

---

### Reference 🌊

> <https://velog.io/@wi4020/node.js-%EB%B0%B1%EC%97%94%EB%93%9C-%EC%B9%B4%EC%B9%B4%EC%98%A4-%EC%86%8C%EC%85%9C-%EB%A1%9C%EA%B7%B8%EC%9D%B8-A-Z-1><Br><https://stackoverflow.com/questions/52998987/parsing-error-unexpected-token-expected><br><https://medium.com/@chullino/1%EB%B6%84-%ED%8C%A8%ED%82%A4%EC%A7%80-%EC%86%8C%EA%B0%9C-body-parser%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%A9%EB%8B%88%EB%8B%A4-%ED%95%98%EC%A7%80%EB%A7%8C-body-parser%EB%A5%BC-%EC%93%B0%EC%A7%80-%EB%A7%88%EC%84%B8%EC%9A%94-bc3cbe0b2fd>
