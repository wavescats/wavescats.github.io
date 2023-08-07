---
layout: post
title: "[Vue.js] Vue.js 와 Express 서버 연결 시 포트 충돌 해결하기(feat. Port 란?)"
subtitle: #부제목
categories: [Vue.js]
tags: [뷰js, TIL, Error]
---

## 개요

`Vue.js` 는 기본적으로 8080 포트를 사용한다.<br>
하지만,<br>
`Node.js`의 `Express` 프레임워크에는 기본 포트번호가 없다.<br>
즉, `Express` 애플리케이션을 실행할 때 포트번호를 직접 지정해주어야한다.

---

### Port

개발자들 사이에는 특정 포트번호를 사용하는 일종의 관행이 있다.<br>

> 로컬 개발 환경에서는 주로 `3000`, `8000`, `8080` 포트를 사용한다.

이는, 단순한 관행일뿐 실제 서비스 환경에서는 이런 번호로 설정하지 않는다.<br><Br>

그렇다면,<br>
포트(Port) 번호는 원하는 숫자를 임의로 넣어도 무관한가 ?<br>

> 원하는 포트번호를 자유롭게 사용해도 되지만, 아래 유의사항이 있으니 참고하자 !

**1. 잘 알려진 포트 (Well-Known Ports)**

- 0 - 1023 번 포트는,<br>
  특정한 서비스에 할당되어있는 잘 알려진 포트이다.
- HTTP 는 80 번 포트, HTTPS 는 433 포트를 사용하므로<br>
  다른 용도로 사용하는 것은 일반적으로 권장하지 않는다.

**2. 등록된 포트 (Registered Ports)**

- 1024 - 49151 번 포트는,<br>
  특정한 서비스에게 등록되어있을 수 있는 포트이므로 가능한 피하는 것이 좋다.

**3. 동적 및 사적 포트 (Dynamic or Private Ports)**

- 49152 - 65535 번 포트는,<br>
  동적 및 사적 포트로 사용하기 위해 예약되어 있다.<br>
  **개발 환경에서는 주로 이 포트를 사용**하게 된다.

**4. 기본적으로, 두 개의 애플리케이션은 동시에 같은 포트를 사용할 수 없다.**<br>
즉, 사용하려는 포트가 다른 프로세스에 의해 사용중인 경우 **포트 충돌**이 발생한다.

---

## Client

개요에서 언급한 바와 같이<br>
`Vue.js` 는 기본적으로 `8080` 포트를 사용한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVFV1v%2Fbtsqj20hl5N%2Fmgdywv5kpJHtoIklC1pD80%2Fimg.png)

`yarn run serve` 명령으로 프로젝트를 실행하게되면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdafebA%2Fbtsqd4jCJBQ%2FSkXXBIkuspeRNxufR17Vdk%2Fimg.png)

다음과 같은 화면을 볼 수 있다.

---

## Server

클라이언트 측에서 요청한 정보를 서버에서 받아 데이터베이스에 적재하기 위해<br>
`Express` 를 사용하여 서버를 구축했다.<br>

```javascript
const express = require("express");
const cors = require("cors");
const bodyParser = require("body-parser");

const app = express();
// Express 의 Default Port 는 5000 이지만,
// 관례를 따라 개발 시에 주로 사용되는 Port 로 변경
const PORT = 8080;

app.use(cors());
app.use(express.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.listen(PORT, () => {
  console.log(`open server : ${PORT}`);
});
```

이렇게 간단히 작성된 코드를 `nodemon` 으로 서버를 실행하게되면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxyCKw%2FbtsquiN16ri%2FMIw22cY54Ixkg5LGweOgJK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbqNBE%2FbtsqodN3eRA%2Fel7ndkOU6Gj1V4361A1210%2Fimg.png)

다음과 같이 `Cannot GET/` 이라는 텍스트와 함께,<br>
Title 에는 Error 가 출력됨을 볼 수 있다.<br><Br>

---

### 에러 해결

이를 해결하기 위해<br>
`Vue.js` 의 Default Port 번호를 임의로 변경 해 주려고한다.<br><br>
`package.json` 에서<br>
`Scripts` 부분의 애플리케이션을 실행하는 명령어에<br>
임의의 포트 번호를 부여하고 저장하면 변경된 포트번호로 서버가 실행된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbd2QMC%2Fbtsqh4czEfn%2F7JNkSfOLokVOswdv6mKaL0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FP5rOh%2Fbtsqtvty5cC%2FGJdCPTaDQRz2ndk8D0izo1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTmoTb%2FbtsqrNO3p5c%2FdxITwbeNJeaKYq22wR4kCK%2Fimg.png)

그럼 이제 정상적으로 `Client` 와 `Server` 가 연결 되어<br>
에러메세지가 사라진 형태를 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOrD29%2Fbtsqd4DYvRe%2Fy7yVwY3df6rZAZJoJFXH30%2Fimg.png)

### Reference 🌊

> <https://gocoder.tistory.com/2582><br><https://donggoolosori.github.io/2020/12/06/nodejs-server/><br><https://m.blog.naver.com/kangminser88/221146020394>
