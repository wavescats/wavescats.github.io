---
layout: post
title: "[Typescripts] Parameter 'xxx' implicitly has an 'any' type"
subtitle: #부제목
categories: Error
tags: [타입스크립트, 프로젝트]
---

### 에러 확인
---

이미지 갤러리를 클론코딩 하던중 발생한 에러이다.<br>

이미지를 Drag & Drop 하여 추가하기 위해<br>
react-dorpzone Hooks 를 가져와 사용했다.
<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJwsrr%2FbtrXGnxXjdZ%2FThU5K4zzMF7csIxifLub20%2Fimg.jpg)

코드를 작성하고 실행하니 다음과 같은 에러 메세지를 출력한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJ5z2v%2FbtrXHPnbrU9%2F8zGEg2w2zlG9DlkUpFUiy1%2Fimg.jpg)


에러를 살펴보면,

> Parameter implicitly has an 'any' type.

직역하면, <br>
매개변수 acceptedFiles 가 암시적으로 any 타입을 갖고있다고 한다.<br>
<br>
<br>

### 에러 해결
---

타입스크립트는 꽤나 까다롭다고 하더라 <br> 
매개변수에 직접 any 타입을 지정해 주었다.<br>

**let 이 아닌 const 임**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqQ7Vg%2FbtrXIivERrm%2F1aixUsJQY2BhEUcdJVqluk%2Fimg.png)


### Reference
---

> <https://velog.io/@edie_ko/React-TypeScript-JavaScript%EC%97%90%EC%84%9C-TypeScript%EB%A1%9C-%EB%B3%80%ED%99%98-%EC%97%90%EB%9F%AC-%EC%84%A0%EB%AC%BC-%EC%84%B8%ED%8A%B8>

> <https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html>

> <https://pottatt0.tistory.com/m/entry/React-Typescript-typeScript%EC%97%90%EC%84%9C-%EA%B0%9D%EC%B2%B4-key%EC%97%90-%EC%A0%91%EA%B7%BC%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95ERROR-Element-implicitly-has-an-any-type-because-expression-of-type-string-cant-be-used-to-index-type>