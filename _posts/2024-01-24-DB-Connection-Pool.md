---
layout: post
title: "[DataBase] 커넥션 풀 vs 단일 커넥션 (Connection Pool vs Single Connection) (Feat. MySQL) 🔌"
subtitle: #부제목
categories: [DataBase]
tags: [TIL, DB, MySQL]
---

## 개요 🙋

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4GPS0%2FbtsD0Gwk5dF%2FxE6WBYhJj1rgXkm1WmyHkk%2Fimg.jpg)

보통 프로젝트를 진행하다보면,<br>
설계된 **`API`** 를 호출하기 위해 로직을 작성하는데<br>
그 로직 안의 내용은 보통 아래와 같을것이다.

```JavaScript
const db = require('../loaders/db');

module.exports = {
  getBrandData: async () => {
    const connection = await db();
    const [rows] = await connection.query(
      'SELECT brand_name, name, caffeine FROM brand'
    );
    connection.end();
    return rows;
  }
};
```

로직을 살펴보면,<br>
외부에 정의된 데이터베이스초기화 로직을 불러와 **`connection`** 변수에 비동기로 담아 사용한다.

**`DB`** 에 접근이 성공하게되면,<br>
쿼리문을 날려 명령을 수행한 뒤 불필요한 리소스 낭비를 방지하기 위해 **`DB`** 의 연결을 해제한다.

이와 같은 방식을 **`단일 커넥션`** 이라고 하며,<br>
각 클라이언트 또는 사용자에 대해<br>
하나의 데이터베이스 연결(**`createConnection`**) 만을 유지하는 방식의 개념을 갖는다.

그럼 이와 반대되는 개념인 **`커넥션 풀`** 에 대해<br>
장, 단점을 알아보고 이를 로직에 적용해 보고자 해당 포스팅을 시작한다.

---

### 단일 커넥션 (Single Connection) 👼

위에서 간략하게 설명했듯,<br>
단일 커넥션의 경우 작은 규모의 프로젝트에서 주로 채택되는 방식이다.

**장점** 👍

- **간단한 구현**<br>
  👉 작은 규모의 애플리케이션에서는 그에 상응하는 간단한 구현이 가능하다.
- **적은 리소스**<br>
  👉 연결을 생성하고 필요한 만큼만 사용 후 즉시 닫을 수 있음
- **간단한 코드**<br>
  👉 커넥션 관리가 간단하여 코드가 간결해짐

**단점** 👎

- **동시 접속**<br>
  👉 동시에 많은 접속이 발생 할 경우 유연한 대체가 불편하다.
- **생명주기 관리**<br>
  👉 트랜잭션의 생명주기가 다양하고 길어질 경우 커넥션을 효과적으로 관리하기 어려움.

### 커넥션 풀 (Connection Pool) 💫

**장점** 👍

- **동시 접속**<br>
  👉 여러 사용자의 동시 접속을 효과적으로 처리 가능.
- **리소스**<br>
  👉 미리 생성된 커넥션을 재 사용하여 발생하는 오버헤드를 감소시키고 리소스에도 유의미한 영향을 끼침
- **연결 지속**<br>
  👉 장기적인 연결을 통해 트랜잭션 간 효율적인 데이터 전송 가능

**단점** 👎

- **복잡성**<br>
  👉 커넥션 풀의 구현 및 관리는 상대적으로 복잡할 수 있다.
- **리소스**<br>
  👉 미리 생성된 커넥션들이 항상 메모리를 차지하고 있음
- **오버헤드**<br>
  👉 일부 상황에서는 커넥션 풀 자체의 오버헤드가 발생할 수 있음.

> 오버헤드란 ❓<br>**`Task`** 를 처리하기 위해 사용되는 추가적인 비용이나 리소스를 말한다.<br>기본 작업의 수행을 위한것이 아닌,<br>시스템 & 프로세스를 관리하고 유지하기 위한 부가적인 요소에서 발생하는 것을 말한다.

장 단점을 확인 해 봤으니,<bR>
두 방법을 코드로 구현 해 보며 확인 해 보도록 하자 ✅

---

### Example 💌

#### createConnection 🔌

```JavaScript
require('dotenv').config();
const mysql = require('mysql');
const {
  DB_HOST,
  DB_PORT,
  DB_USER,
  DB_PASSWORD,
  DB_SCHEMA
} = require('../config/index');

const conn = async () => {
    mysql
        .createConnection({
          host: DB_HOST,
          port: Number(DB_PORT),
          user: DB_USER,
          password: DB_PASSWORD,
          database: DB_SCHEMA
        })
        .connect(err => {
          err ? console.log(err) : console.log('DB_CONNECTED');
        });
};

module.exports = conn;
```

가장 기본적인 방법으로 구현된 DB 와 연결하는 로직이다.<bR>
**`Callback`** 함수를 사용하기 위해 **`MySQL2`** 모듈을 사용하였고,<br>
**`createConnection`** 메서드를 호출하여 **`MySQL`** 에 대한 커넥션을 생성 해 주었다.

```JavaScript
const db = require('../loaders/db');

module.exports = {
  getBrandData: async () => {
    const connection = await db();
    const [rows, fields] = await connection.query(
      'SELECT brand_name, name, caffeine FROM brand'
    );
    connection.end();
    return rows;
  }
};
```

분리된 코드를 불러와<br>
생성된 **`DB`** 에 연결 및 사용 후 **`end`**, **`destory`** 등으로 커넥션을 제거하여 사용한다.

이와같이 단일 커넥션을 채택하여 사용했을 경우,<bR>
위의 단점에서도 언급했듯<br>
커넥션을 삭제하고 재 생성됨에 따라 발생하는 **`handshake`** 비용,<br>
프로세스 혹은 스레드 비용이 증가한다는 **단점**이 존재한다.

---

#### createPool 💫

커넥션 풀은 **미리 필요한 수 만큼 커넥션을 생성** 해 놓고,<br>
**사용 후 반납**하는 개념이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpuDg7%2FbtsD4Iss3UP%2FP5gnoq8iI7kkHOxutwJtp1%2Fimg.png)

이를 통해 단일 커넥션과는 다르게<br>
커넥션을 다시 생성하는데 사용되는 비용이 소비되지 않는다는 장점이 있다.

```JavaScript
const conn = async () => {
  const connection = await mysql.createPool({
    host: DB_HOST,
    port: Number(DB_PORT),
    user: DB_USER,
    password: DB_PASSWORD,
    database: DB_SCHEMA,
    connectionLimit: 10
  });
  return connection;
};

module.exports = conn;
```

**`async/await`** 을 사용하여 **`MySQL2`** 모듈의 **`Promise`** 기능을 활용했다.

위 로직과 차이점은,<br>
**`connectionLimit`** 옵션을 추가함으로 서버에 가해지는 부하를 줄일 수 있는 점 이다.

> **`connectionLimit: 10`** 은,<br>동시에 최대 10 개의 연결만 허용하겠다는 의미이며<bR>11 번 째 요청은 **`Pending`** 되어 동시에 접근하는 연결을 분산시킬 수 있다.

하지만,<br>
**`Pool`** 을 너무 적게 생성 해 놓으면 대기시간 (**`Pending`**) 이 발생할 수 있고,<bR>
너무 많이 생성 해 놓으면 메모리(리소스) 낭비가 크다는 단점이 있다.

```JavaScript
exports.getCoffeeInfoSum = async ({ getReq }) => {
  const conn = await db();
  const getConn = await conn.getConnection();
  const params = [getReq];
  const sql = `
  SELECT SUM(caffeine)
  FROM post
  WHERE user_id = ?
  `;
  const [row] = await getConn.query(sql, params);
  getConn.release();
  return row;
};
```

마찬가지로 분리된 코드를 불러와<br>
생성된 **`DB`** 에 **`getConnection`** 메서드를 사용하여<br>
가져온 커넥션에 쿼리문을 날리고 **`release`** 메서드를 통해 연결된 커넥션을 풀 에 반납하여 사용한다.

> **`getConnection`** 는,<br>**`MySQL`** 커넥션 풀 에서 새로운 연결을 가져오는 메서드 이다.<br>

---

### 결론 🤹‍♂️

**`Node.js`** 환경에서 **`MySQL`** 모듈을 사용하여 **`DB`** 에 접근하는 두 가지의 방법을 살펴봤는데,

**작은 규모**의 애플리케이션이나<bR>
간단한 작업에서는 **단일 커넥션**으로 구현하는 것이 보다 효율적인 부분이 있으며

**대규모** 애플리케이션이나<br>
웹 서버, 데이터베이스에 잦은 요청이 요구된다면,<br>
**커넥션 풀** 을 사용하여 성능을 최적화 할 수 있을 것 같다.

단,<br>
커넥션 풀은 **대부분의 상황에서 권장**되는 방법이다.

클라이언트가 동시에 서비스에 접근하거나 웹 앱의 경우와 같이 많은 수의 요청이 들어오는 상황에서<br>
**자원을 효율적으로 관리하고 성능을 최적화**시킬 수 있기 때문이다.

이 글을 정리하며,<bR>
실제 단일 커넥션으로 구현되어있던 로직을 👉 커넥션 풀로 리펙토링하여 사용중 이다.

---

## Reference 🌊

> <https://velog.io/@wngud4950/MySQL-%EB%8B%A8%EC%9D%BC-Connection-VS-Connection-Pool-%EB%B0%A9%EC%8B%9D%EC%9D%98-%EC%B0%A8%EC%9D%B4><br><https://velog.io/@gwon713/Nodejs-MySQL-DB-connection-pool><br><https://techbless.github.io/2020/01/17/Node-js%EC%97%90%EC%84%9C-Mysql-Connection-Pool-%EC%9D%B4%EC%9A%A9%ED%95%98%EA%B8%B0/><br><https://m.blog.naver.com/collcr/222869575871>
