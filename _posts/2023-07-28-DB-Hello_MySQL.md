---
layout: post
title: "[DataBase] MySQL 에 지도 RestAPI 를 활용하여 데이터 적재하기 (Vue.js) 🐦"
subtitle: #부제목
categories: [DataBase]
tags: [뷰js, TIL, DB]
---

## 개요

이번 포스팅 에서는 이전에 `MongoDB` 를 활용하여<br>
서버와 클라이언트가 통신했던 로직을 레퍼런스로 삼아,<br>
`MySQL` 에 요청한 데이터를 적재하는 로직을 구현 해 보려한다.

---

### What is SQL ?

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwjS1T%2Fbtspl7IIHpj%2FXwaTktJWwViY92KranEI6K%2Fimg.jpg)

`MySQL` 은 데이터베이스 오픈소스 중 가장 많이 사용되는<br>
관계형데이터베이스(RDBMS) 이다.<br>

`MySQL` 은 SQL(Structured Query Language) 문법을 사용하고,<br>
웹 애플리케이션을 위한 데이터베이스로 주로 사용된다.<br>
이를 통해 사용자는 데이터를 생성, 조회, 업데이트, 삭제(CRUD) 를 할 수 있고,<br>
쿼리를 통해 데이터 관계를 조사할 수 있다.

> 보통 실무에서는 쿼리문을 날린다 or 때린다 라고도 표현한다.

`MySQL` 이 사용된 대표적인 프로젝트로는<br>
WordPress, Facebook, Twitter 등 이 있다.

---

#### MongoDB vs MySQL

두 데이터베이스는 NoSQL 과 관계형(RDBMS) 의 차이를 가지고 있다.<br>
각자의 시스템을 사용하여 다양한 용도로 활용할 수 있지만,<br>
구조와 데이터를 처리하는 방식에서 약간의 차이가 있다.<Br><Br>

1. 데이터 구조

   - MongoDB
     **유연한 스키마**를 가진 JSON 과 유사한 문서에 데이터를 저장할 수 있다.
   - MySQL
     **고정된 스키마**를 가지고 있는 테이블에 데이터를 저장한다.<br>
     즉, 각각의 테이블이 어떤 데이터 유형을 가질 수 있는지 정의해야 데이터를 저장할 수 있다.

2. 쿼리 언어

   - MongoDB
     JSON 과 유사한 쿼리 언어를 사용하여<br>
     **JavaScript 를 사용하는 개발자들이 보다 친숙**하게 사용할 수 있다.
   - MySQL
     표준 SQL 문법을 사용하여 보다 **전문적인 기술을 요하는 관리자**와 **개발자**가 필요하다.

3. 스케일링

   - MongoDB
     **수평적으로 스케일링**이 가능하여 데이터를 여러 서버에 **분산**시키는 것이 가능하다.<br>
     이를 통해 대용량 데이터 처리에 적합할 수 있다.
   - MySQL
     **수직적인 스케일링**을 지원하며 빠른 하드웨어를 사용함으로 인해 **성능이 향상**된다.

4. 관계성
   - MongoDB
     **비관계형 데이터**를 주로 다루며,<br>
     관계형 데이터를 다루기에는 조금 제한적인 부분이 있다.
   - MySQL
     테이블 간의 관계를 정의하고 **조인 연산을 수행**할 수 있다.

> 각각의 장점이 존재하므로,<br>
> 프로젝트에 따라 적합한 데이터베이스를 채택하여 사용하는게 올바른 방향이라고 할 수 있다.

---

## 카카오 주소 검색 API 🔔

MongoDB 를 사용하여<br>
카카오 주소검색 API 를 통해 얻은 데이터를 적재 해보았다면,<br>
이번엔 MySQL 을 사용하여 데이터를 적재해보려고한다.<br><Br>
Default Port 는 `3306` 이다.

### Client

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPoKBm%2FbtspmVgod6c%2Ffn3YUy4cuGE7PenwktA2Z1%2Fimg.png)

서버 측에 요청하는 코드는 MongoDB 와 유사하다.<br>
Client 에서 서버로 보낼 데이터를 추출하고,<bR>
서버 측에서는 해당 값들을 받을 준비를 해 주면 된다.

---

### Server

```bash
const mysql = require('mysql')
const cors = require('cors')
const bodyParser = require('body-parser')

const app = express()
const PORT = 8080;

const db = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'a1231234!',
  database: 'testbase'
});

db.connect();

app.use(cors())
app.use(express.json())
app.use(bodyParser.urlencoded({ extended : true }))

app.post('/', (req, res) => {
  const data = req.body
  // 검증 과정 추가
  console.log(data)
  // const query = 'INSERT INTO Address SET ?'
  const query = 'INSERT INTO Address (postcode, roadAddress, jibunAddress, detailAddress, extraAddress) VALUES (?, ?, ?, ?, ?)'
  const valuse = [data. postcode, data.roadAddress, data.jibunAddress, data.detailAddress, data.extraAddress]

  db.query(query, valuse, (error, result) => {
    if (error) {
      console.log('An error occurred:', error);
      res.status(500).send('An error occurred');
    } else {
      console.log('Data inserted successfully:', result);
      res.status(200).send('Data inserted successfully');
    }
  })
})

// Users 테이블을 조회하는 명령어 -> 모든 데이터 선택 / 콜백에는 3개의 매개변수를 받음
db.query('SELECT * from Address', (error, rows, fields) => {
  // 만약 에러가 발생한다면
  if (error) throw error;
  // 에러가 없으면 결과가 rows 에 담김 -> SELECT 문을 통해 조회된 데이터
  console.log('User info is: ', rows);
  // fields 에는 조회된 필드 정보가 담김 -> 필드 이름, 타입 등
});

// 종료
process.on('exit', () => {
  db.end();
});


app.listen(PORT, () => {
    console.log(`open server : ${PORT}`);
});
```

SQL 은 MongoDB 를 연결 할 때와 다르게
Cli 를 통해 데이터베이스를 생성 해 주고,<br>
그 안에 테이블을 생성하고,<br>
테이블 안에 데이터가 담길 필드를 정의 해 주면<br>
클라이언트에서 요청한 값이 DB 에 적재되는 형태로 이루어진다.
<br>
Cli 로 SQL 문을 작성하고,<br>
DB 가 생성 되었는지 GUI 프로그램인 Workbench 로 확인 해 보겠다.
<br>

`+` 버튼을 눌러 Default 값으로 연결정보를 추가하면<br>
root 사용자로 접근할 수 있고,<br>
초기에 설정한 Password 를 입력 시<br>
설계되어있는 데이터베이스로 접근이 가능하다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpKppZ%2FbtspBzKsgTZ%2FbTZGK6gft3It7D9XakRlgK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FP0aoK%2FbtspK4ipOEY%2FINi5YkhGfIkw0CMUqc7dL0%2Fimg.png)

---

#### Database 생성

`command` 창에 `mysql -u root -p` 를 입력하면 mysql cli 가 실행되고<br>
그 아래에서 SQL 문법을 통해 DB 를 관리할 수 있다.

> 만약 이 명령어가 커맨드에서 실행이 되지 않는다면<br>
> `환경변수` 를 키워드로 에러를 해결할 수 있다.

- 데이터베이스 생성

```bash
CREATE DATABASE 데이터베이스명;
CREATE DATABASE testbase;
```

- 생성된 데이터베이스 확인

```bash
SHOW DATABASES;
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fvz4kz%2FbtspFM3z5vR%2FoOCExgyJMC9Tq3Llot3K5K%2Fimg.png)

- 데이터베이스에 진입

```bash
USE 데이터베이스명;
USE testbase;
```

- 테이블 생성

```bash
CREATE TABLE 테이블명(
  필드명1 자료형(크기) NOT NULL AUTO_INCREMENT,
  필드명2 자료형(크기) NOT NULL,
  필드명3 자료형(크기)
---
CREATE TABLE Address(
  // postcode 의 경우 고유한 값 이기 때문에 primary key 로 지정하는게 좋아보인다.
  postcode int NOT NULL,
  roadAddress varchar(100),
  jibunAddress varchar(100),
  detailAddress varchar(100),
  extraAddress varchar(100),
)
);
```

> 각 명령어 끝에는 ; (세미콜론) 을 찍어야 명령어가 실행된다.<BR>
> 세미콜론이 없이 Enter 시 명령어를 계속 작성할 수 있다.

- 테이블 확인

```bash
SHOW TABLES;
```

데이터베이스를 생성하고 선택하지 않으면 다음 명령어를 실행할 수 없다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsEque%2Fbtspxa5fSVl%2F2hLI1zcZjfj2sFL9JhWBE1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdN9o8N%2FbtspGLKeRVF%2FzAHeGWNidqoZOFp0kITTsK%2Fimg.png)

---

#### 확인

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwmTRk%2FbtspsUn8uNv%2F0CkUbXj6nDn5H42B9gXqQ1%2Fimg.png)

---

### Reference 🌊

> <https://poiemaweb.com/nodejs-mysql><br><https://hardner.tistory.com/1><br><https://javakong.tistory.com/67><br><https://wrkbr.tistory.com/526><br><https://www.google.com/search?q=mysql+primary+key+%EC%9D%B8%EB%8D%B1%EC%8A%A4+%EB%B2%88%ED%98%B8%EB%A1%9C+%EC%A7%80%EC%A0%95%ED%95%98%EB%8A%94%EB%B2%95&oq=mysql+primary+key+%EC%9D%B8%EB%8D%B1%EC%8A%A4+%EB%B2%88%ED%98%B8%EB%A1%9C+%EC%A7%80%EC%A0%95%ED%95%98%EB%8A%94%EB%B2%95&aqs=chrome..69i57.18866j0j7&sourceid=chrome&ie=UTF-8>
