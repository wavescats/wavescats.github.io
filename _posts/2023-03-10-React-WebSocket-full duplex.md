---
layout: post
title: "[React] WebSocket 을 활용한 실시간 채팅 기능 - 1"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL, WebSocket]
---

## 개요
이전 포스팅에서 `WebSocket`을 활용해 back 과 front 를 연결하고,<br>
메세지를 보냄으로써 연결이 잘 되었는지 확인 해 보았다.<br>
<br>
이번 포스팅 에서는, <br>
서로 다른 웹 브라우저에서 메세지를 보내고 받는 실시간 채팅 기능을 구현해 보고자 한다.

---

## 개발환경
작업 툴은 `vscode`를 사용하며,<br>
웹 브라우저는 `chrome`과, `Microsoft Edge`로 진행한다.

## UI
이전에 생성한 `home.pug`에서 간단한 UI 를 그려 확인 해 보자.<br>
<br>

아직은 비어있지만 메세지를 받으면 리스트 형태로 받을 `ul`태그를 생성해준다.<br>
그 아래 `form`태그를 부모 태그로 두고,<br>
그 아래 텍스트를 입력할 수 있는 `input`태그와,<br>
작성한 메세지를 보낼 수 있는 `button`태그를 생성한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdjdNnB%2Fbtr3QyGuBIh%2FMKnLyWyhpUa76wRm9B7rv0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWoQLt%2Fbtr3Lq24ww8%2FCRfoLDEGqPNWTUWpGTtG11%2Fimg.png)

## 데이터(텍스트) 전송

`html` 코드가 작성된 태그를 `Client.js`에서 가져온다.<br>
```js
const MessageList = document.querySelector('ul')
const MessageForm = document.querySelector('form')
```

event listener 를 `MessageForm`에 추가한다.

```js
function handleSubmit(event){
    event.preventDefault()
    const input = MessageForm.querySelector('input')
    // console.log(input.value) // console 창에 input 영역에 입력한 텍스트를 출력
    socket.send(input.value) // front form 영역에서 서버로 데이터 전송
    input.value = "" // 빈 값을 정의하여 send button 을 클릭 시 내용을 비워줌
}

MessageForm.addEventListener('submit', handleSubmit)
```

다음과 같이 코드를 작성한 뒤,<br>
`console.log(input.value)`의 주석을 풀면 브라우저 콘솔 창에 입력한 텍스트가 출력 되지만,<br>
`socket.send` 명령어를 통해 입력한 텍스트를 `Server.js`에 보내준다.

![](https://blog.kakaocdn.net/dn/d1gBVa/btr3U2GFMEI/TernC8UuzQ1hcqHD4CwCHK/img.gif)

> `input.value`를 빈 문자열로 정의하여 텍스트를 입력 후 버튼을 클릭 시 input 영역을 비워줌. 

### 에러
front 에서 보낸 데이터(텍스트)를 server 터미널에 출력할때,<br>
다음과 같이 출력이 된다면 아래와 같은 형태로 재 랜더링 하여 다시 데이터를 보내주도록 하자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFqy66%2Fbtr3IDvho5M%2FbqAjaMImbGh28hdUcSZAnk%2Fimg.png)

```js
console.log(message.toString('utf8'))
```

이는 맥 사용자 이외의 윈도우에서 해당하는 에러인듯하다..<br>
(본인이 윈도우 사용자 )

---

`Server.js`의 터미널에 user 가 front 에서 입력한 텍스트가 잘 출력이 됨을 확인 했다.<br>
이제 user 가 보낸 메세지를 다시 user 에게 보내줄 수 있도록 `socket.send` 함수를 사용한다.<br>
즉, <br>
front 영역에서 보낸 데이터를 server 를 거쳐 다시 front 에 띄워준다는 말이다.

```js
socket.send(message)
```

이 때도 마찬가지로 콘솔 창에 다음과 같이 출력 된다면,<br>
`'utf8'`옵션을 추가하여 다시 랜더링 해 주자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FepE7et%2Fbtr3SxU0ghn%2FYuOFeEwJTJEG0OhqYya4kk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbio9l5%2Fbtr3SICeMlM%2FE6nLvdGLN16uwteo7AGXL1%2Fimg.png)

> 1 번은 front 콘솔에 출력되는 메세지<br>
2 번은 server 콘솔에 출력되는 메세지

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbReMOf%2Fbtr3XW607qX%2FVMdxFxqkwFPBDkjnp4tptK%2Fimg.png)

---

## 다른 웹 브라우저 간의 통신
`input`영역 안에 텍스트를 입력 후 버튼을 클릭하면,<br>
메세지를 전송하고 받는 기능을 구현 했다.<br>
<br>
여기까지의 기능을 chrome 에서 테스트 했지만,<br>
다른 웹 브라우저인 Microsoft Edge 에서 다시 테스트 해 보도록 하자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjiCws%2Fbtr3TI9Duan%2FyIG3Pi4XMjVEcKcZ4K5QXK%2Fimg.png)

역시나 chrome 에서 텍스트를 보내면 chrome 브라우저 에서만 받을 수 있고,<br>
Edge 에서 보낸 텍스트는 Edge 브라우저 에서만 받을 수 있었다.<br>
<br>
즉, 한 개의 서버가 서로 다른 브라우저로부터 데이터를 받고있고,<br>
받은 데이터에 각각 답장(반환)을 해 주고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCCDF2%2Fbtr34aSUelA%2FZuWyAIwwF6Vz53CSxGXy21%2Fimg.png)
    
<br>

이번에는 **한쪽의 브라우저에서 텍스트를 보내면,**<br>
**다른 웹 브라우저에서도 데이터를 받을 수 있는 기능**을 구현하려 한다.
<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkNoe8%2Fbtr37BuRdFO%2FInvbIWsVQkYzmohZoqgfLk%2Fimg.png)

해당 코드는 Chrome 과 Edge 두 브라우저에 연결 되었을때 실행되는 코드이다.<br>
```js
wss.on('connection', (socket) => {
    console.log('Connection to Browser 💌')
    socket.on('close', () => console.log('Disconnected to Browser ❌'))
    socket.on('message', (message) => {
        socket.send(message.toString('utf8'))
    })
})
```
해당 코드로 인해 두 브라우저 모두<br>
서버가 연결되었다는 메세지와 함께 새로운 메세지를 받을 수 있다.<br>
즉,<br>
같은 코드로 두 개의 브라우저가 연결 되었다는 의미이다.<br>
<br>
아니, 어쩌면 두 개 이상의 브라우저가 연결이 될지도 모른다.<br>
<br>
그렇기에 먼저,<br>
다수의 브라우저들을 데이터베이스로 받을 수 있게 빈 배열을 생성해준다.
```js
// 두 개의 브라우저가 담겼다면,
const otherBrowser = [] // ex) [1, 2, ...]
```
빈 배열이 담긴 `otherBrowser`는, <br>
누군가 서버에 연결을 시도한다면 그 connection 을 담는 역할을 한다.

```js
// 브라우저들이 연결 되었을 때 `otherBrowser`에 넣어줌
otherBrowser.push(socket) 
---
// 메세지 영역의 함수
// 터미널에 "Buffer 68 65 6c 6c 6f 20 66 72 6f ..." 이 출력되어 utf-8 로 렌더링 해줌
otherBrowser.forEach((aSocket) => aSocket.send(message.toString('utf8')))
```

해당 코드로 인해 임의의 브라우저에서 받은 메세지를 <br>
socket 이 있는 모든 곳에 전달해 줄 수 있게 된 것이다.<br>

![](https://blog.kakaocdn.net/dn/1MI9d/btr34UoDLWR/3YtYkurfGGBXy6DzDN8ylK/img.gif)

## Reference
> <https://nomadcoders.co/noom/lectures/3096>