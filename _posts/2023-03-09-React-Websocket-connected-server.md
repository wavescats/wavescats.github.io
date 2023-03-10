---
layout: post
title: "[React] WebSocket 을 활용한 서버간의 통신"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL, WebSocket]
---

## 개요
WebSocket 을 활용하여 Backend 와 Frontend 를 연결하고,<br>
연결이 잘 되었는지 Message 를 보내 확인해보려한다.

## WebSocket
> <https://developer.mozilla.org/en-US/docs/Web/API/WebSocket/WebSocket>

먼저, 공식문서를 참조하여 Server 에 WebSocket 서버를 생성한다.

- 라이브러리 설치
```bash
npm i ws
```
> <https://www.npmjs.com/package/ws>

---

라이브러리를 설치 후 서버를 생성할때,<br>
WS 서버와 Express 서버 둘 다 작동하기 원한다면 아래와 같이 서버를 생성 해 주면 된다.

- http://localhost:3000
- ws://localhost:3000

```javascript
import http from "http"
import Express from "express"
import WebSocket from "ws"

const app = Express()
const server = http.createServer(app)
const wss = new WebSocket.Server({ server })
```

> Express 는 WS 를 지원하지 않음

후에, 서버 단 에서 연결이 잘 되었는지 터미널에서 확인하기 위해 console.log 를 보내준다.

```javascript
const handleListen = () => console.log(`Listening on http://localhost:3000`)
server.listen(3000, handleListen)
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFKEbB%2Fbtr3aruX2l8%2F4wvCKukgCDeNNMdPx172j1%2Fimg.png)

---

### Connection
Server 에서 WebSocket 서버를 생성 해 주었다면,<br>
실시간 통신을 위해 클라이언트 영역과의 연결을 해 주어야 한다.

```javascript
// server.js
// on 메소드는 connection event 를 기다림
wss.on('connection', (socket) => {
    console.log(socket)
}) // 익명함수 socket 은 connection 이벤트가 발생 했을 경우 socket 을 받음
```

```javascript
// client.js
const socket = new WebSocket(`ws://${window.location.host}`)
```

Server 단에서 `console.log(socket)` 을 찍고,<br>
브라우저에서 새로고침을 해 보면 아래와 같이 socket 에 담긴 정보를 터미널에서 확인할 수 있다.

![](https://blog.kakaocdn.net/dn/dMuCgK/btr292oK8Fo/fBqFxjnWMk5cKW3Ua6neFk/img.gif)

### Reference
> <https://nomadcoders.co/noom/lectures/3096><br><https://developer.mozilla.org/en-US/docs/Web/API/WebSocket/WebSocket><br><https://www.npmjs.com/package/ws><br>