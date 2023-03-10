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

Server 단에서 `console.log(socket)`을 찍고,<br>
브라우저에서 새로고침을 해 보면 아래와 같이 socket 에 담긴 정보를 터미널에서 확인할 수 있다.

![](https://blog.kakaocdn.net/dn/dMuCgK/btr292oK8Fo/fBqFxjnWMk5cKW3Ua6neFk/img.gif)


### Message Event
위 단계를 거쳐 `socket`에 담긴 정보를 확인 해 보았으니,<br>
Server 단에서 서버가 연결 되었을때 메세지를 보내,<br>
Client 단에서 메세지를 받아보도록하자.

```javascript
// server.js
wss.on('connection', (socket) => {
    console.log('Connection to Browser 💌')
    socket.send('hello !!!') // socket 으로 데이터 전송
}) 
```

```javascript
// client.js
// 서버가 구동되었을때의 이벤트
socket.addEventListener('open', () => {
    console.log('Connection to Server ✅')
})

// 서버에서 메세지를 send 했을때의 이벤트
socket.addEventListener('message', (message) => {
    console.log('Just got this: ', message.data, '서버에서 보낸 메세지 !')
})

// 서버를 껏을때의 이벤트
socket.addEventListener('close', () => {
    console.log('Disconnected to Server ❌')
})
```

코드를 확인 해 보면,<br>
먼저, `server.js`에서 send 메소드를 통해 `hello !` 라는 메세지를 `socket` 에 보냈으며<br>
이를 `client.js` 에서 `addEventListener`를 통해 메세지를 받을 수 있다.
`socket`에서 제공하는 `Event` 는 4 가지로,<br>
`open`, `message`, `error`, `close` 를 제공하고 있다.<br>
<br>

첫 번째 이벤트는,<br>
`open` Event 를 사용해 `socket` 이 `open` 되었다면,<br>
브라우저에 연결되었다는 메세지를 출력하는 로직이다.<br>
<br>
두 번째 이벤트는,<br>
`message` 이벤트를 사용해 Server 단에서 보낸 메세지를 받는 로직이다.<br>
<br>
세 번째 이벤트는,<br>
`close` 이벤트를 사용해 `ctrl + c` 를 사용해 서버를 종료 했을때,<br>
브라우저에서 확인할 수 있는 메세지가 담긴 로직이다.
<br>
<br>
이를 브라우저에서 확인 해 보면,<br>
메세지 이벤트에 대한 결과가 콘솔 창에 출력되고 있다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd3Pqji%2Fbtr3aLAmNlR%2FVR3v1UOYzheIytOekghdhK%2Fimg.png)

우리는 서버 단에서 `hello !!!`라는 메세지를 보냈고,<br>
그 이외의 정보는 필요 없기에 `message.data`를 통해 필요한 정보만 가져오면 될것이다.

이와 동시에 서버가 실행 되었기 때문에,<br>
Server 단에서 `console.log` 를 통해 보낸 메세지가 터미널에 출력 될 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F04ETc%2Fbtr3ccqA2tw%2FzaUY6MzCkgndEVBdLfSrqK%2Fimg.png)

마지막으로 서버를 `ctrl + c`를 통해 종료 시,<br>
브라우저에서 `close` 이벤트가 담긴 로직이 실행 될 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FI0WG5%2Fbtr3az1ekWk%2F8zGDkLACegWe6P6oKCpmMK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6IVLF%2Fbtr3dTRlwWP%2FXX3mrod7TXQ8HNQmB3oZa1%2Fimg.png)

---

## 회고
WebSocket 을 활용해,<br>
Server 와 Client 사이에 간단한 메세지 주고받기를 실습 해 봄으로써<br>
실시간 채팅 서비스를 개발해볼 예정을 갖고있다.

### Reference
> <https://nomadcoders.co/noom/lectures/3096><br><https://developer.mozilla.org/en-US/docs/Web/API/WebSocket/WebSocket><br><https://www.npmjs.com/package/ws><br>