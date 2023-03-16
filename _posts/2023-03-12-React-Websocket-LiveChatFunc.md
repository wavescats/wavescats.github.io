---
layout: post
title: "[React] WebSocket 을 활용한 실시간 채팅 기능 - 2"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL, WebSocket]
---

## 개요
이전 포스팅에선,<br>
서로 다른 웹 브라우저 환경에서 실시간으로 메세지를 보내고 받는 기능을 구현했다.<br>
<br>
이번 포스팅에서는 상대방 혹은 자신이 보낸 메세지들을<br>
채팅 기능과 유사하게 메세지를 보낸 사람이 누구인지와<br>
받은 메세지들을 리스트형태로 화면에 출력하는 로직을 구현해 보고자 한다.

```js
a : text
b : text
a : text1
...
```

---

## UI
이전 포스팅에서 `home.pug`에 `ul` 태그를 생성해 두었다.<br>
그 아래에 메세지를 받을 경우 리스트형태로 쌓일 수 있게 `li`태그를 생성한다.<br>
`li`태그는 `front.js` 영역의 MessageEvent 영역에 다음과 같이 추가 해 준다.
```js
const li = document.createElement('li') // 새로운 메세지를 받으면 요소 생성
li.innerText = message.data // message.data 를 li 안에 담음
MessageList.append(li) // li 를 MessageList 안에 추가해줌
```
> `li`를 `MessageList`에 append 해 줌으로써 메세지를 Front 영역의 화면에서 볼 수 있다.

다음과 같이 익명의 상대가 보낸 메세지를 리스트 형태로 출력 해 준다.

![](https://blog.kakaocdn.net/dn/yKNQq/btr36GcCq4E/VmXLUBkfAnWaDxDVv0LVp0/img.gif)


## userName 지정
`home.pug`에서 `form`태그를 하나 더 생성 해 준다.<br>
`placeholder`에는 아이디를 입력하고 저장할 수 있는 버튼을 생성 해 준다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuPYtw%2Fbtr34MSalNc%2FpqGTUEcwBeF5GaGo6EUgqK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxviJJ%2Fbtr34LZ12vx%2FUK7vgSRqqIPOi2aHkk6KCK%2Fimg.png)

생성한 아이디를 Server 로 보내야 하는데,<br>
고려해야할 사항으로는,<br>
1. Server 는 Message 들을 구분하지 못한다.
- 메세지를 보낼 때 입력받은 그대로를 출력하기 때문.
2. 메세지를 구별 해 주어야 함.
- 누가 어떤 메세지를 보냈는지 ?
- 아이디를 저장하기 위한 메세지 일 수도 있으며, 텍스트로 구성된 메세지 일 수도 있음.

> `Server.js`의 Message 함수는 모든 메세지를 포함하고 있기 때문

먼저,<br>
`home.pug`의 `form`태그에 Id 를 부여 해 준다.
```js
    form#id
        input(type="text", placeholder="아이디를 입력하세요", required)
        button save 
    ul
    form#message
        input(type="text", placeholder="텍스트를 입력하세요", required)
        button send 
```
`Client.js`에서 정의한 `MessageForm` 을 Id 가 부여된 `#message` 로 변경 해 준다.<br>
그리고 Id 와 Message 를 구분하기 위해 `IdForm` 을 추가로 생성 해 준다.

```js
const MessageList = document.querySelector('ul')
const MessageForm = document.querySelector('#message')
const idForm = document.querySelector('#id')
```

생성한 idForm 에 `addEventListener`를 넣어준다.<br>
(함수 `handleIdSubmit` 생성)

```js
function handleIdSubmit(event){
    event.preventDefault()
    const input = idForm.querySelector('input')
    socket.send(input.value) // send 메소드는 string 타입만을 받을 수 있음
    input.value = ""
}

idForm.addEventListener('submit', handleIdSubmit)
```

---

### JSON
위의 로직대로 실행 해 보면,<bR>
아이디를 입력하고 버튼을 누르게 되면 메세지 형태로 리스트에 추가가 된다.<br><br>
우리가 원하는 것은 아이디는 따로 서버에 저장이 되며,<br>
저장된 아이디가 보내는 메세지만 리스트에 담기는 형태일 것이다.<br>
<br>

때문에,<br>
`JSON` 의 형태를 가진 2개의 Type 으로 id 와 메세지를 구분지을 수 있었으면 좋겠다.<br>
```js
{
    type: "id",
    payload: "a"
},

{
    type: "message",
    payload: "hello"
}
```

`Client.js`에 함수를 생성 해 준다.<br>
```js
// 메세지 전송을 위한 함수 생성
function makeMessage(type, payload){
    const msg = { type, payload }
    return jSON.stringify(msg) // JavaScript Object 를 String 으로 변환해주는 메소드
}

// 적용
function handleSubmit(event){
    event.preventDefault()
    const input = MessageForm.querySelector('input')
    socket.send(makeMessage('new message', input.value))
    input.value = ""
}
// 적용
function handleIdSubmit(event){
    event.preventDefault()
    const input = idForm.querySelector('input')
    socket.send(makeMessage('id', input.value))
}
```

`makeMessage`함수를 생성해<br>
기존에 존재했던 `handleSubmit` 과 `handleIdSubmit` 에 적용하면,<br>
서버에 메세지를 전송 할 때마다 string type 을 전송 해 줄 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FohEFv%2Fbtr38Kf9xe3%2F50kRNAjQEl0nfXiXsho121%2Fimg.png)

다음과 같이 객체 형태로 출력이 되었는데,<br>
이는 Server 가 JavaScript Object 를 읽을 수 없어 String 형태로 출력이 되고있다.

> 다른 언어로 해당 로직을 구현하려면 새로 작성을 해야하지만,<br>
String 타입으로 보내주었기 때문에 Server 에서는 다양한 언어로 로직을 구현할 수 있다.

우리는 JavaScript 로 구현할 것이기 때문에,<br>
Object 형태로 받은 String 을<br>
JavaScript Object 의 형태로 변환 해주어야 Type 을 눈으로 확인 할 수 있다.<BR>

---
### .parse
앞서 JavaScript Object 를 String 으로 변환해주는 메소드로 `.stringify`를 사용했었다면,<br>
반대로 String 을 JavaScript Object 로 변환 해 주는 작업이 필요할 것이다.<br>
<bR>
우리는 `.parse` 메소드를 사용하여 JSON 형태의 String 을 JavaScript Object 로 변환 해 줄 것이다.

`Server.js`의 메세지 영역에 아래 코드를 추가하고 메세지를 전송 해 보자.
```js
const parsed = JSON.parse(message)
console.log(parsed, message.toString('utf8'))
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHh94q%2Fbtr4gU26VVy%2Fj7y0Zo0TXO43qEcJOw6akK%2Fimg.png)

첫 번째로 출력된 것이 JavaScript Object 이고,<br>
두 번째로 출력된 것이 String 임을 확인할 수 있다.<br>

우리가 사용할 것은 JavaScript Object 이기 때문에 `parsed` 를 잘 기억 해 두자.<br>

---

로직을 작성하여 메세지를 보내 작동이 잘 되는지 테스트 해 보도록 하자.
```js
// Server.js
socket.on("message", (message) => {
    const parsed = JSON.parse(message)
    if (parsed.type === "new_message") {
        otherBrowser.forEach((aSocket) => aSocket.send(parsed.payload))
    } else if (parsed.type === "id") {
        console.log(parsed.payload)
    }
})
```
![](https://blog.kakaocdn.net/dn/Aulbq/btr4kQrNZoY/Nf6DnByuc3n4cx0Y0et6Hk/img.gif)

예상했던 대로,<br>
**Id 를 입력했을 때는 메세지가 리스트에 출력되지 않고,**<br>
**메세지를 입력했을때만** 리스트에 출력됨을 확인할 수 있었다.<bR>