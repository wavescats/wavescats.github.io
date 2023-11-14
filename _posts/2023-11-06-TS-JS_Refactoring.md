---
layout: post
title: "[Typescript] 바닐라로 구현된 프로젝트를 타입스크립트로 리펙토링하기 ⚡"
subtitle: #부제목
categories: Typescript
tags: [타입스크립트, 프로젝트, TIL]
---

## 개요 🔔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcaduot%2FbtsAfAmvyii%2F23Z3W0pHJdyqHesvEvGiFk%2Fimg.png)

<U>멋쟁이사자처럼 프론트엔드 테킷 스쿨 플러스 (이하 FESP)</U> 에서 진행한,<br>
바닐라 자바스크립트 `Todo App` 프로젝트를<br>
타입스크립트로 리펙토링 하는 과정을 포스팅 하려고한다.<br>

해당 과정에서는 `Vite` 와 `ESLint` 등 이 사용되며,<br>
`Axios` 라이브러리를 사용하여 HTTP 요청을 처리한다.

---

### Axios ⚡

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNWFoG%2FbtszSJD3SdB%2FAiZWR9ofi2IzWE8JksHOfK%2Fimg.png)

먼저, 기존의 HTML 파일 내부 `Script` 문에 심어주었던 `Axios` 를 주석 처리하고,<br>
해당 라이브러리를 프로젝트 경로에 설치 해 준다.

```
npm i axios
```

```
yarn add axios
```

사용하고자 하는 코드 내부에 `import` 하여 `axios` 를 사용한다.

```
import axios from "axios"
```

먼저, 공통된 엔드포인트에 `HTTP` 요청을 진행하므로<br>
모듈화 인스턴스를 생성 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbXmb2I%2FbtszQCd719a%2F11Bhdp3ESMwsagUkjArm7K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeEjWN3%2FbtszWE9zfp4%2FqTnK92cbWdjUJVjYuvbc3k%2Fimg.png)

공통된 요청을 보내는 엔드포인트 인스턴스를 `TodoList.js` 파일에서 사용할 것인데,<br>
기존의 `defaultInstance` 를 제거 후,<br>
생성한 인스턴스를 `import` 하여 사용한다.

---

### Refactoring 💌

`.js` 확장자를 가진 파일을 `.ts` 확장자로 변경 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsVcow%2FbtszZnscUb8%2FjPzjiiVOG3GXWJxtD78ydk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsC6vA%2FbtszWGM6OTE%2Fq9Zo1soJrh6STMeekfbcFK%2Fimg.png)

> 확장자를 변경하자마자 발생하는 에러...

#### 목록 불러오기 🔮

- `TodoList.ts`<br>

파일 명 그대로 생성한, 생성된 Todo 목록을 조회 할 수 있는 페이지이다.<br>
먼저 DB 에 저장된 데이터를 불러오기 위해<br>
`getData` 함수를 정의하고,<br>
사전에 생성한 인스턴스(`defaultInstance`) 에 `get` 비동기 요청을 보내 사용한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdnD0sf%2Fbtsz6NzjIQD%2FnqhiXow1akD0g9CrFI3VC0%2Fimg.png)

---

#### 목록 상세보기 💫

- `TodoInfo.ts`<br>

`getData` 함수에서 요청한 `data` 에는 객체 형태의 데이터를 담고 있다.<br>
Typescript 에서는 해당 변수의 값이 `null` 또는 `undefined` 일 수 있음을 고려하여<br>
`!` 나 `?` 와 같은 문법을 사용한다.<br>
해당 변수에서 `!` (단언 연산자) 를 사용할 경우,<br>
`data`는 항상 존재할 것이라고 확신할 때 `detailInfo` 변수에 값이 할당된다.

> 만약, `data` 의 값이 `null` 혹은 `undefined` 일 경우에도 로직이 계속 실행되어야 한다면<br>옵셔널 체이닝 기법을 사용하면 조금 더 안전하게 로직을 작성할 수 있다 ✅

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdfQz9%2FbtsAjgA2zDO%2FlTW0Ck8h3BLpxA6Y75fYp1%2Fimg.png)

```typescript
const detailInfo = data?.item;
```

---

#### 목록 추가하기 💨

- `TodoRegist.ts`<br>

해당 코드는 `DOM` 을 사용하여 HTML 에서 `<body>` 요소를 찾고,<br>
그 요소의 클래스 속성을 변경하는 코드이다.<br>

`TodoRegist` 함수에서도 마찬가지로<br>
`TodoInfo` 와 동일하게 `!` (단언 연산자) 를 사용하여<br>
선택된 `<body>` 요소가 `null` 혹은 `undefined` 일 경우 발생하는 런타임 에러를 방지한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FI9JYD%2FbtsAmA6uN79%2FSllj4FCGWCNAcmqmuGpKik%2Fimg.png)

그리고, 공통된 인스턴스(`defaultInstance`) 에 `POST` 요청을 보내 DB 를 수정한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGpu8g%2FbtsAm3tNe5Q%2FJ7XcE1UmH0uADe1HT1AxZ0%2Fimg.png)

```typescript
registerBtn.addEventListener("click", async function () {
  if (titleInput.value === "" || contentInput.value === "") {
    alert("할 일과 내용을 입력해주세요");
    return;
  }
  await defaultInstance
    .post(`/todolist`, {
      title: titleInput.value,
      content: contentInput.value,
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
  location.href = "/";
});
```

---

### Error 💥

**타입스크립트**는 친절하게 변수명을 잘못 입력 한 경우에도 `에러 메세지`로 알려준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRstPh%2FbtszZjXEYVK%2FAXQvGjepaabqZ1LuOQerQk%2Fimg.png)

### 회고 👀

해당 프로젝트는,<br>
`Javascript` 프로젝트를 👉 `Typescript` 로 리펙토링 하는 프로젝트 였다.<br>
해당 프로젝트를 통해
자바스크립트로 작성된 코드를 타입스크립트를 활용하여<br>
보다 엄격하게 관리하고, 발생하는 에러를 최소화 하여 관리할 수 있는 효율적인 코드를 작성하는 방법을 익힐 수 있었다.

> 생각보다 리펙토링 할 부분이 없어서 (?) 비교적 쉬웠다 (?)

## 소스코드 ✔

👇👇👇<br>
<https://github.com/likelion-plus/todolist-js/tree/develop/02.typescript/todoapp>

---

## Reference 🌊

> <https://github.com/likelion-plus/todolist-js/tree/develop/02.typescript/todoapp><br><https://velog.io/@rgfdds98/JS-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-TS-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0><br><https://typescript-kr.github.io/pages/intro-to-js-with-ts.html><br><https://www.nextree.io/typescript-vs-javascript/>
