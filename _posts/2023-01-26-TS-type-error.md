---
layout: post
title: "[Typescripts] Parameter 'xxx' implicitly has an 'any' type"
subtitle: #부제목
categories: Error
tags: [타입스크립트]
---

### 에러 확인
---

이미지 갤러리를 클론코딩 하던중 발생한 에러이다.<br>

이미지를 Drag & Drop 하여 추가하기 위해<br>
react-dorpzone Hooks 를 가져와 사용했다.
<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJwsrr%2FbtrXGnxXjdZ%2FThU5K4zzMF7csIxifLub20%2Fimg.jpg)

코드를 작성하고 실행하니 다음과 같은 에러 메세지를 출력한다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fe6f65f1-da45-44c6-bffb-75a0d489649e/Parameter_acceptedFiles_implicitly_has_an_any_type2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T102841Z&X-Amz-Expires=86400&X-Amz-Signature=cd2d1472328b92622c646a6b1539112a17a78e64796896147dfdf8c4ea0cdfca&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Parameter%2520%27acceptedFiles%27%2520implicitly%2520has%2520an%2520%27any%27%2520type2.JPG.jpg%22&x-id=GetObject)


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

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1d976c97-b17f-4cee-ae48-ef222e0331b8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T102940Z&X-Amz-Expires=86400&X-Amz-Signature=3e51c27d705730accd927deb60b4d4d80594d511d6a03407d6d59cce46969fdf&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)


### Reference
---

> <https://velog.io/@edie_ko/React-TypeScript-JavaScript%EC%97%90%EC%84%9C-TypeScript%EB%A1%9C-%EB%B3%80%ED%99%98-%EC%97%90%EB%9F%AC-%EC%84%A0%EB%AC%BC-%EC%84%B8%ED%8A%B8>

> <https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html>

> <https://pottatt0.tistory.com/m/entry/React-Typescript-typeScript%EC%97%90%EC%84%9C-%EA%B0%9D%EC%B2%B4-key%EC%97%90-%EC%A0%91%EA%B7%BC%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95ERROR-Element-implicitly-has-an-any-type-because-expression-of-type-string-cant-be-used-to-index-type>