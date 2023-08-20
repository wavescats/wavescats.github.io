---
layout: post
title: "[React-Native] HTTP 요청 시 Axios 와 Fetch 의 차이 (feat. HTTP 요청이란 ?)💬"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, TIL]
---

## 개요 🌅

백엔드 서버와 HTTP 통신을 `axios` 라이브러리를 사용하여 한 경험이 있다.<br>
리액트에서는 자체 내장되어있는 `fetch` 를 사용하여 별도의 설치 없이 사용 가능했었지만,<br>
<br>
실은 이 둘의 기능은 같다고 할 수 있다.<br>
이번 포스팅에서는 두 기능의 차이점과 간단한 예시를 통해<bR>
두 기능의 차이를 적어보려한다.

---

### Axios vs Fetch 💌

`axios` 와 `fetch` 는 모두 웹 브라우저 또는 `Node.js` 환경에서<br>
`HTTP` 요청을 보내고 받는데 사용되는 `Javascript` 라이브러리 이다.<br>

`axios` 란,<br>
웹 브라우저, `Node.js` 를 위한 `Promise API` 를 활용하는 `HTTP` 비동기 통신 라이브러리이다.<br>

두 라이브러리 모두 HTTP `GET`, `POST`, `PUT`, `DELETE` 등의 요청을 보낼 수 있지만,<br>
각 기능이 갖고있는 약간의 차이점이 있다.

---

#### HTTP ❔

`HTTP` 요청 (HTTP Request) 이란,<bR>
클라이언트 (웹 브라우저, 모바일 앱 등) 가<br>
웹 서버에 데이터를 요청하거나 서버로 데이터를 전송 하는데 사용되는 메세지를 말한다.<br>
`HTTP` 요청은 `HTTP` 프로토콜을 사용하여 전송되며,<br>
이를 통해 웹 페이지, 이미지, 비디오 등의 리소스를 다운로드하거나<br>
폼 데이터를 서버에 전송 (submit) 할 수 있다.

**1️⃣. `HTTP` 메서드 (Method)**

- 요청의 종류를 나타내는 동작으로, `GET`, `POST`, `PUT`, `DELETE` 등이 있다.
  - `GET` -> 서버에 데이터를 요청하여 가져오는 데 사용한다. (읽기 기능)
  - `POST` -> 서버에 데이터를 보내 리소스를 생성하거나 업데이트 하는데 사용한다. (쓰기 기능)
  - `PUT` -> 서버의 리소스를 업데이트하거나 대체하는데 사용한다.
  - `DELETE` -> 서버의 리소스를 삭제(제거)하는데 사용한다.

**2️⃣. 헤더 (Headers)**

- 요청에 대한 부가 정보를 나타내는 메타데이터이다.
  - 요청을 보내는 사용자의 브라우저 정보
  - 콘텐츠 타입
  - 인증 토큰

**3️⃣. 본문 (Body)**

- 요청과 함께 전송되는 데이터이다.
  - `POST` 혹은 `PUT` 요청과 같이 서버에 데이터를 보낼 때 사용된다.

> `HTTP` 요청을 보내는 경우,<br>
> 웹 서버는 요청을 처리하고 응답 (HTTP Response) 을 클라이언트로 돌려 보낸다.<br>
> 응답 (res) 에는 요청에 대한 결과 정보, 요청한 데이터, 상태코드 등이 포함된다.

---

#### Axios

**1️⃣. Error Handling**<br>
`HTTP` 오류 상태코드 (404, 500 등) 를 반환하는 경우,<br>
`axios` 는 자동으로 에러를 발생시킨다.

**2️⃣. JSON Parsing**<br>
JSON 형식을 갖춘 응답 데이터가 자동으로 파싱된다.

**3️⃣. Browser Support**<br>
더 오래된 브라우저에 대한 지원을 제공하며, ES5 를 사용하여 구현된다.

**4️⃣. TimeOuts**<br>
요청 시간 초과를 설정할 수 있다.

**5️⃣. Interceptors**<br>
요청 및 응답 인터셉터를 제공하여<bR>
전역 수준에서 요청과 응답을 변형하거나 로깅하는데 유용하다.

**6️⃣. Cancellation**<br>
요청 취소 토큰을 사용하여 이미 진행중인 `HTTP` 요청을 취소할 수 있다.

**7️⃣. Progress Monitoring**<br>
업로드 및 다운로드의 진행 상황을 모니터링 할 수 있는 기능을 제공한다.

**8️⃣. Server-Side Rendering (SSR)**<br>
`Node.js` 환경에서도 작동하므로 서버측 렌더링을 지원한다.

---

#### Fetch

**1️⃣. Error Handling**<br>
`HTTP` 오류 상태 코드를 반환하는 경우, `fetch` 는 에러를 발생시키지 않는다.<br>
대신, 응답 객체를 반환하고 개발자가 응답 객체의 `'ok'` 속성을 확인하여<br>
요청이 성공했는지 확인해야할 필요가 있다.

**2️⃣. JSON Parsing**<br>
`json()` 메서드를 사용하여 수동으로 응답 데이터를 `JSON` 으로 파싱해야한다.

**3️⃣. Browser Support**<br>
최신 브라우저에서 지원되지만,<BR>
일부 더 오래된 브라우저에서는 `fetch` 를 지원하지 않을 수 있다.<br>
이러한 경우 `폴리필` 을 사용하여 `fetch` 기능을 추가할 수 있다.

**4️⃣. TimeOuts**<br>
요청 시간 초과를 설정할 수 있는 기능이 없지만, 이를 대체(해결) 할 수 있는 방법이 존재한다.

**5️⃣. Interceptors**<br>
해당 기능 제공 x

**6️⃣. Cancellation**<br>
`AbortController` 객체를 사용하여 요청을 취소할 수 있다.

**7️⃣. Progress Monitoring**<br>
해당 기능 제공 x

**8️⃣. Server-Side Rendering (SSR)**<br>
브라우저 기반 API 이기 때문에,<br>
`Node.js` 환경에서 `fetch` 를 사용하기 위해선 별도의 라이브러리를 사용해야한다.

---

### 사용 예시 🔐

#### `Axios`

마찬가지로 `React-Native` 환경에서<br>
`axios` 를 사용하여 `GET` 요청을 보내는 예시이다.

> `axios` 는 별도의 패키지 이므로, 사용하기 전 설치가 필요하다

```
npm install axios
or
yarn add axios
```

설치 한 후에는 아래와 같이 `axios` 를 사용하여 `GET` 요청을 보낼 수 있다.

```javascript
import axios from "axios";

axios
  .get("https://api.example.com/data")
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```javascript
const getUser = async () => {
  try {
    const response = await axios.get(`/user?name=TEST`);
    console.log(response); // API 호출 정상
  } catch (ex) {
    // API 호출시 에러 발생
  }
};
```

`POST` 요청을 보낼 경우,<br>
아래와 같이 `post` 메소드를 사용하여 본문에 데이터를 추가할 수 있다.

```javascript
import axios from "axios";

axios
  .post("https://api.example.com/data", {
    key1: "value1",
    key2: "value2",
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```javascript
const createFeed = async (feedItem: FeedItem) => {
  try {
    const response = await axios.post(`/feed`, { ...feedItem });
    console.log(response); // API 호출 정상
  } catch (ex) {
    // API 호출 시 에러 발생
  }
};
```

---

#### `Fetch`

아래는 `fetch` 를 사용하여 `React-Native` 환경에서<br>
별도의 라이브러리 설치 없이 `GET` 요청을 보내는 예시이다.

```javascript
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

```javascript
const getUser = async () => {
  const response = await fetch(`/user?name=TEST`)
    .then((result) => result.json())
    .catch((result) => {
      /* 에러 발생 */
    });
  console.log(response); // API 호출
};
```

`POST` 요청을 보낼 경우,<br>
아래와 같이 `method` 와 `headers` 를 설정하여 본문에 데이터를 추가할 수 있다.

```javascript
fetch("https://api.example.com/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    key1: "value1",
    key2: "value2",
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

---

두 예시의 차이를 보면,<br>
`Axios` 는 data 의 속성을 다루고,<br>
`Fetch` 는 body 의 속성을 다룬다.<br<Br>

`Fetch` 의 경우 `response` 를 받는다고 바로 사용할 수 없고,<br>
`.json` 메서드를 사용하여 값을 사용할 수 있었다.<br>

반면에 `Axios` 의 경우,<br>
위와 같은 과정이 생략되고 바로 값을 받아 사용가능한 형태를 지원한다.<br><br>

마지막으로 `TypeScript` 에서의 `Axios` 는,<br>
`generic` 을 통한 Typescript Type 추론이 재활용을 통해 가져올 수 있어 비교적 간편하다는 장점이 있다.

---

### Reference 🌊

> <https://velog.io/@eunbinn/Axios-vs-Fetch><br><https://tlsdnjs12.tistory.com/26><br><https://kofearticle.substack.com/p/korean-fe-article-axios-vs-fetch>
