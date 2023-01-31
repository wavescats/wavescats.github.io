---
layout: post
title: "[React] 날씨 기반 API 를 활용한 프로젝트 - 1"
subtitle: #부제목
categories: Project
tags: [프로젝트]
---

## 프로젝트 생성
---

```
npx create-react-app [프로젝트명]
```

`src/app.js` 의 불필요한 부분 제거 후 <br>
`$npm start` 명령어로 앱 실행

## 현재위치 정보 가져오기
---

앱이 ***실행되자마자*** 현재위치에 대한 정보가 필요하므로<br>
`useEffect` Hooks 를 사용

> useEffect 에는 2개의 매개변수가 필요하고,<br>
함수 내부에 원하는 내용을 작성 해 주면 된다.

```
useEffect(() => {함수},[배열])
```

> 현재위치정보 가져오기<br><https://www.w3schools.com/html/html5_geolocation.asp>

위 Reference 를 참조하여 현재위치에 대한 정보를 가져와 보자.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d3b2184f-52c1-478e-b512-e1670e6249cb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T172607Z&X-Amz-Expires=86400&X-Amz-Signature=e1c3382f61c098e698695aeb94de57d67554f07bc45a17cc36a3e3abcd1c655f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5bdf5282-39f1-47ce-851c-31547895200b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T173142Z&X-Amz-Expires=86400&X-Amz-Signature=ac72ae3f99ca49f8c401d40d8fad3298de4b013ccc082f04e2cb38672f839376&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/162f73cb-3bf6-4f86-9607-4181bccf6ff1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T173258Z&X-Amz-Expires=86400&X-Amz-Signature=5fed7d13d289414008edd918b76032dd740291de55d9327bd7c148a3c7be8523&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

> latitude (위도), longitude (경도)

