---
layout: post
title: "[DataBase] MongoDB 에 RestAPI 를 활용하여 데이터 적재하기 (Vue.js) 🐸"
subtitle: #부제목
categories: [DataBase]
tags: [뷰js, TIL, DB]
---

## 개요 🌱

이번 포스팅 에서는 카카오 주소 검색 API 를 활용하여<br>
클라이언트와 서버간의 Restful 통신을 구현하고,<br>
추출한 데이터를 `MongoDB` 에 저장해보려고한다.

---

### What is Mongo ?

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZMNvN%2FbtspxbJcbLV%2FxF2XSGiwrMQNiDNLQLoXYK%2Fimg.jpg)

`MongoDB` 는 NoSQL 의 대표적인 데이터베이스로,<br>
관계형 데이터베이스보다 유연하다는 장점을 가지고 있다.<br><br>

기존의 RDBMS(관계형 데이터베이스) 와는 다르게<br>
비정형 데이터를 저장하고 처리하는데 효과적인 데이터베이스이다.<br>

---

#### 특징 🌏

1. 스키마 없는 데이터 모델

   - 보다 유연한 스키마를 제공하여,<br>
     데이터 구조가 다른 문서를 같은 컬렉션에서 저장할 수 있다

   > 빠르게 변하는 데이터를 처리하는 데 유용 할 듯 !

2. 데이터를 Json 형태로 저장할 수 있어 다양한 언어와 호환이 용이하다

3. 수평적 확장

   - 데이터의 빠른 증가에 대응하기 위해 서버에 분산하여 저장할 수 있다

4. 다양한 쿼리 옵션
   - SQL 과 유사한 쿼리 언어와, 인덱싱 및 그래프 처리 등 다양한 기능을 제공한다.

---

### 카카오 주소 검색 API 🔔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPoKBm%2FbtspmVgod6c%2Ffn3YUy4cuGE7PenwktA2Z1%2Fimg.png)

Vue.js 로 간단하게 입력받을 수 있는 폼을 만들고<br>
전송 버튼을 누르게 되면<br>
localstorage 에 입력받은 값이 전송되는 형태의 로직이다.<br>

---

#### Client 🔑

먼저 `./public/index.html` 내부에 SDK 모듈을 심고,<br>
사용자에게 입력받을 수 있는 input 태그에<br>
`v-model` 함수를 사용하여 변수를 선언 해 주고<br>
들어올 값들을 위해 초기화를 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmsEeJ%2Fbtspolzqkgg%2F1k6duwaxfgKK8oxjIAvp01%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFBZl0%2FbtspmfGsCJy%2FYp5ebMbafEZe3xpL1TUPTK%2Fimg.png)

주소 검색 버튼을 눌렀을 때 실행되는 이벤트로는<br>
공식 Docs 에서 제공하는 레퍼런스를 참고했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsN77k%2Fbtspxq7ZSGW%2FuFqM7MGUkzX6V8zTEzkisk%2Fimg.png)

그리고,<br>
데이터가 담긴 각각의 변수를 `this` 를 사용하여 한번 더 감싸고<br>
`formData` 객체로 해당 값들을 묶어 서버로 요청을 보낸다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtEw3H%2FbtspHZBzU9y%2Fp4EPnfRIeLTscYvURsX8AK%2Fimg.png)

`formData`에 담긴 데이터를 서버측에 보내기 위해<br>
`axios` 라이브러리를 사용하여 서버와의 통신을 할 수 있도록 작성했다.

```
axios.post('/', formData)
        .then(response => {
          console.log('서버 ok :', response.data)

        })
        .catch(error => {
          console.log('서버 x :', error)

        })
```

간단한 테스트를 위한 작업이므로,<br>
`/` 루트 경로로 post 요청을 서버로 보낸다

#### Server 🔓

서버는 `Express` 를 사용하여 구축하고,<br>
`cors` 에러를 대비하여 설치 해 준다.<br>
요청한 데이터의 값을 읽을 수 있도록 `body-parser` 도 설치.

- app.js

```bash
const express = require('express')
const cors = require('cors')
const bodyParser = require('body-parser')
const mongoose = require('mongoose')

const app = express()
const PORT = 8080;

app.use(cors())
app.use(express.json())
app.use(bodyParser.urlencoded({ extended : true }))

mongoose.connect('mongodb://localhost:27017')

mongoose.connection.once('open', () => {
  console.log('DB connect seccess')

  dataBase = mongoose.connection.db;

  dataBase = mongoose.dataBase('social')

// DB 에 적재
dataBase.collection('addr').insertOne(postData, (err, result) => {

    if (err) {
        console.error('데이터 삽입 실패:', err);
        } else {
        console.log('저장 완료');
        }
    });
})

// database connect fail
mongoose.connection.on('error', (err) => {
    console.log(err)
})
```

```bash
// get 요청 처리 -> 조회
app.get('/', (req, res) => {
    const postData = req.body;
    console.log('클라이언트에서 온 데이터:', postData);
  });
// post 요청 처리 -> 쓰기
app.post('/', (req, res) => {
  // 클라이언트에서 온 데이터는 req.body에 담겨 있습니다.
  const postData = req.body;
  console.log('클라이언트에서 온 데이터:', postData);

  Data.create(postData)
    .then(savedData => {
    console.log('데이터 저장 성공:', savedData);
    res.status(200).json({ message: '데이터 저장 성공' });
  })
    .catch(err => {
    console.error('데이터 저장 실패:', err);
    res.status(500).json({ error: '데이터 저장 실패' });
  });
});

mongoose.Collection.insert(Data)

app.listen(PORT, () => {
console.log(`open server : ${PORT}`);
})

```

DB 에는 어떤 형태의 데이터를 적재할지에 대한 Schema 와<br>
그 스키마들을 담고있는 모델을 export 해 외부에서 사용 가능하도록 정의한다.<br>

- /models/index.js

```bash
const mongoose = require("mongoose");
const DataSchema = require('./schemas/data')

exports.Data = mongoose.model('Data', DataSchema);
```

- /models/schemas/data.js

```bash
const { Schema } = require("mongoose");

module.exports = new Schema({
      postcode: String,
      roadAddress: String,
      jibunAddress: String,
      detailAddress: String,
      extraAddress: String
    });
```

---

### 확인 🔐

이제 작성한 코드로<br>
클라이언트에서 요청을 보내면 <Br>
서버 (DB) 에서 담긴 데이터를 확인할 수 있을것이다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdWhbmx%2FbtspGKYB34w%2FlOSxLdI7Bb2dguNQIXxm0k%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FN6gpX%2FbtspBzi8Hbb%2FlY3C8bxAOAtZjxKbmu4ZFK%2Fimg.png)
