---
layout: post
title: "[Next.js] Prisma & MySQL 시작하기 🌸"
subtitle: #부제목
categories: [Next.js]
tags: [넥스트, TIL]
---

## What is Prisma ? 🌱

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbRptLk%2FbtsugjDHrMF%2F8NIEjX2zP60x4k8TuaVE10%2Fimg.jpg)

> <https://www.prisma.io/>

**`Prisma`** 란,<br>
Node.js 와 TypeScript 에서 사용할 수 있는 데이터베이스 툴킷<br>
차세대 `ORM` **(Object Relational Mapping)** 프레임워크이다.<br>

SQL 코드를 쓰지 않고,<br>
Javascript(**typescript** 도 가능) 코드를 작성하여 데이터베이스를 수정할 수 있도록 연결해주는 서비스 이기도하다.<br>

### ORM ?

**`Prisma`** 는 ORM 이지만,<br>
기존 ORM 과 근본적으로 다른 ORM 이며,<bR>
발생하는 여러 문제는 Prisma 를 통해 해결할 수 있다고한다.<br>

> <https://www.prisma.io/docs/concepts/overview/prisma-in-your-stack/is-prisma-an-orm>

`ORM` 은,<br>
DB데이터 (Schema) 를 객체 (Object) 로 매핑해주는 역할을 하여,<br>
모델링된 객체와 관계를 바탕으로 **SQL 을 자동으로 생성** 해 주는 도구라고 한다.

---

## init 🌼

먼저,<br>
**`Next.js`** 앱을 `npx create-next-app` 명령을 통해 설치 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKV9TH%2FbtsugTSELmt%2F8tYWApH5UBo7dIC82LRXV0%2Fimg.jpg)

> 각 옵션은 취향 존중 !

`npx` 명령을 통해 `next.js` 앱(13 ver) 을 설치 했다면,<br>
아래와 같은 파일구조를 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FScwKr%2FbtsuGzefwRJ%2FFlHVdBxX3J7O1XShPaxLs0%2Fimg.png)

---

### Prisma 🌝

설치한 `Next` 앱으로 진입하여 `Prisma` 를 설치 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIRNg3%2FbtsugUjJKIZ%2FfAsaEP3qFL60TKnOvyJjM1%2Fimg.png)

설치한 Prisma 를 init(초기화) 하여 파일구조에 `Prisma` 와 `.env` 가 생성됨을 확인한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FceHU5e%2FbtsuGhq1SZE%2FzCtbKWSyNvk7z1YLUPqKZK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNeoDZ%2FbtsuGl71mBl%2F07vfGroNSE2ry6f4GfP2q0%2Fimg.png)

#### DB 설정 ⛅️

생성된 `Prisma` 디렉토리를 확인 해 보면,<bR>
`schema.prisma` 파일이 존재하는데,<bR>
여기에서 데이터베이스 (DB) 연결정보를 추가 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcjSwhc%2FbtsuqA5Wrla%2FxYHDeLsIf9Yg6EAKIIska0%2Fimg.jpg)

> Defalut DB 는 `PostgreSQL` 로 지정되어있다.

`PostgreSQL` 을 `MySQL` 로 변경 해 주고 저장 !

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FocDx9%2Fbtsut5x65NY%2FWlMc1ztDkPK7R6eZBCTI4k%2Fimg.png)

`datasource db` 에도 정의되어있듯,<br>
`env` 에서 `DATABASE_URL` 을 불러온다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkAidi%2FbtsuJcvV2Py%2F3fYKJ4kzEE9LUtkECvV5K0%2Fimg.jpg)

`.env` 파일에서 DB 연결정보를 추가 해 준다.

```
DATABASE_URL="mysql://username:password@localhost:3306/myDatabase"
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FburQUm%2FbtsuIB3G51z%2FubHv4kZydUZCivE2aE2n11%2Fimg.png)

> 포트번호 뒤에는 실제 사용할 테이블 명을 지정해준다.

이제 데이터 모델을 설정 해 주어야하는데,<br>
`schema.prisma` 에 아래와 같이 모델을 정의 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTkMXl%2FbtsvvCUNnI0%2FBNQDeQ7pKtgYzKdUb6nkWk%2Fimg.png)

지정한 모델을 마이그레이션 명령어를 통해 실제 사용될 DB 와 동기화 작업을 해 주어야 한다.

```
yarn prisma migrate dev --name init
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Felbk6a%2FbtsvnivRA1O%2FQbT8j0OGAiB1xu0HpC2W8K%2Fimg.png)

> 만약 에러 ❌ 가 발생한다면 !?

👇👇👇<br>

마이그레이션 명령어를 실행했더니,<br>
`generators` 가 실행되지 않는다는 에러가 발생했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FF5mLv%2FbtsvmzdwToQ%2FaUvAyd9qa31VkC31AcneQ0%2Fimg.png)

메세지에 출력된대로 `prisma/client` 를 설치 해 준다.

```
yarn add @prisma/client
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIgjrb%2Fbtsvdsz0h1c%2F4o9dA0hxuXa2rWqQAwRVm0%2Fimg.png)

다시 마이그레이션 명령어를 실행하면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Felbk6a%2FbtsvnivRA1O%2FQbT8j0OGAiB1xu0HpC2W8K%2Fimg.png)

`prisma` 파일트리에서 마이그레이션 된 SQL 파일을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdqT7GH%2Fbtsvnbi6GY7%2F3WRYGTECoJZtmCpEzHpjx0%2Fimg.png)

☝️☝️☝️<br>
(이건 DB 에서도 확인 가능 !)

---

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2FKRr%2Fbtsvargrfxf%2F0aVOcZwXz82JoFggo2EvOK%2Fimg.png)

`root` 이름의 localhost:3306 기본 포트로 열린 커넥션에 접근 해 보면,<br>
`.env` 에 정의한 `next_mariaDB` DB 가 생성됨을 확인할 수 있다.<br>
그 아래에는 마이그레이션 때 지정한 `notice` 테이블이 존재한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcuMBNP%2FbtsviRL6tb9%2Fr9vxoOgqEic3aj3PDiRhEK%2Fimg.png)

해당 포스팅을 통해<br>
데이터베이스에 `Prisma` 를 사용하여 접근 및 제어 해 볼 수 있었고,<br>
다음 포스팅에서는 서버 없이,<br>
`Prisma Client` 를 설치하여 DB 를 조작하고, CRUD 의 작업 과정을 담아보려한다.

---

## Reference 🌊

> <https://defineall.tistory.com/853><br><https://jake-seo-dev.tistory.com/171><br><https://velog.io/@iamhayoung/prisma-schema><br><
