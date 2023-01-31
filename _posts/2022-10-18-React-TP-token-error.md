---
layout: post
title: "[React] [팀 프로젝트] 페이지 이동 시 토큰의 부재로 인한 에러"
subtitle: #부제목
categories: Error
tags: [리액트]
---

### 에러 발생
---
> TypeError - Cannot read properties of undefined

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVSkqF%2FbtrXFtLW5Kd%2FfSW65yP2xrfJfd9oNCyZn0%2Fimg.png)

url 에서 community 경로로 진입 시 해당 구간에서의 오류가 발생했다.

> email(key) : cookie.token.email(value)

email 에 해당하는 value 부분이 정의되지 않는다는 오류이다.

### 에러 확인
---
해당 오류를 살펴보니,<br>
토큰을 통해 로그인 한 사용자에 한해 게시판 기능을 이용할 수 있게끔 작성해놨는데, 

입력된 이메일이 없으니 발행된 토큰이 없고, 페이지에서는 요청을 거부한 것이다.

> 팀원이 작성중인 로그인, 회원가입 정보를 아직 Git 에서 Pull 하지 않음


### 에러 해결
---
> 오류가 발생한 구간 주석 처리 진행

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYEDCQ%2FbtrXJgxmRxC%2FY719bSBtABxE4EoaUp9qK0%2Fimg.png)
<br>

정상적으로 페이지가 랜더링 됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcNqvhk%2FbtrXIzKItzM%2FCvZU97nME723UK4YTjoB4k%2Fimg.png)

> 이후 CRUD 에 적용되는 토큰이 아직 없기 때문에<br> 
모든 구간 주석 처리 진행


### Review
---
프로젝트의 협업을 위해 Git 을 사용하여 버전을 관리하였는데,<br>
현장에서 작업하는 와중에서도<br>
소통의 부재로 인해 가볍기도하지만 무거운 에러를 직면하게 되었다.

<br>
다시금 협업 시 소통의 중요성에 대해 깨닫게 되었다.