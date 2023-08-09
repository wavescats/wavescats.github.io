---
layout: post
title: "[Vue.js] 포스트맨(Postman) 을 사용하여 api 테스트하기 (feat.카카오) 💋"
subtitle: #부제목
categories: [Vue.js]
tags: [뷰js, TIL]
---

## 개요 😊

이전 포스팅에서 구현한 소셜로그인 로직을 사용하여<br>
포스트맨으로 API 테스트를 진행 해 보려고한다.

---

## What is Postman ❓

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdHDaKM%2FbtsqDcnP3Aw%2Fc3VYzFGpnSVGQcYS6e9anK%2Fimg.png)

포스트맨은 API 개발을 위한 협업 플랫폼으로,<br>
개발자가 API 를 테스트, 개발, 문서화, 모니터링 하는 기능을 제공한다.<br>
이 도구는 사용자에게 친숙한 **GUI 를 제공**하여 **HTTP 요청을 보다 쉽게** 확인할 수 있다 💨

1. API 요청 생성
   다양한 HTTP 메서드 (GET, POST, PUT, DELETE 등)을 사용하여 요청을 생성하고 쉽게 수정할 수 있다.

2. 응답 확인
   서버에서 반환된 응답을 확인하고 분석 가능하고,<BR>
   이를 통해 API 의 동작을 빠르게 테스트 및 디버깅 할 수 있다.
3. 자동화 테스트
   스크립트를 작성하여 API 요청과 응답을 자동으로 테스트 할 수 있고,<bR>
   이를 통해 회귀 테스트 및 연속 통합 환경과의 통합이 가능하다.
4. 문서화
   API 에 대한 문서를 생성하고 공유할 수 있으며,<br>
   이를 통해 다른 개발자나 관계자와 협업 시 유용하게 쓰인다.
5. API 모니터링
   서비스 수준계약(SLA) 를 준수하는지 확인하고,<br>
   성능 문제를 식별하기 위해 API를 주기적으로 모니터링 할 수 있다.
6. 협업
   팀원 간에 API 테스트와 컬렉션을 공유하고,<br>
   작업을 동기화 할 수 있어 여러 사람과 협업하는 프로젝트에 유용하다.

위 6가지의 기능은 API 의 전체 생애주기를 관리하고,<br>
개발 과정을 간소화하여 생산성을 향상시키는데 큰 도움을 제공한다.

---

### Server 💌

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

해당 로직을 살펴보면 `"/api/login"` 의 URL 로<br>
클라이언트 측 에서 데이터를 요청하고있다.<br><br>

이때, 여기서 Postman 을 사용하여<br>
해당 URL 이 정상적으로 접근이 가능한 URL 인지 확인해 보려고한다.

> localhost:8080/api/login

```javascript
app.post("/api/login", function (req, res) {
  console.log(req.body); // 클라이언트로부터 받은 결과 값
  // DB 설계 로직 작성

  // 응답 -> 클라이언트
  res.json({ message: "Login successful" });
});
```

이 로직에서 우리가 확인할 수 있는 정보는 res 에 담긴 값으로<br>
지정한 message 인 'Login successful' 이 출력되는 형태를 확인하면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdvSTW3%2FbtsqJBAxEa1%2FZe5J9Wv6qdJWv2Na7Lm7v1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcr68zI%2FbtsqFr6xUGy%2F4pWkeSLgFKOFNXaumrR5Wk%2Fimg.png)

> req.body 에는 `Client` 에서 요청을 하지 않았기 때문에,<br>
> 당연히 빈 값이 담긴 객체가 출력이 될 것이다.

Postman 으로 POST 요청을 보낼 때 마다<br>
서버 측 콘솔에는 **요청받은 값이 없기때문에** 빈 객체가 출력이 된다.<br>

만약 클라이언트 측에서 구현한 전송기능이 담긴 버튼을 클릭했을 경우,<br>
사용자가 입력한 값이 서버측 콘솔에도 보여질 것 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlOaH7%2FbtsqD5HQudH%2FcK6Za0FHLkspDMMOge8tKK%2Fimg.png)

---

### Reference 🌊
