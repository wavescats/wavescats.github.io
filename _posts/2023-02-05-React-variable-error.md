---
layout: post
title: "[React] ReferenceError: 'xxx' is not defined ❌"
subtitle: #부제목
categories: React
tags: [리액트, MongoDB, Error]
---

### 에러 확인

CRUD 중 C (Create) 부분에서 발생한 에러이다.<br>
다음과 같이 게시물 생성을 하기 위해 내용을 작성하고 생성 버튼을 누르자 에러가 발생했다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOoezc%2FbtrYMO7nFfV%2FyJkHZmVkY7wpTthclBn2S0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F74Mex%2FbtrYIcoJCwd%2FLGaoXsnx9p1nmA9lKdqm10%2Fimg.png)

**MongoDB Compass** 에도 입력한 데이터가 들어오지 않는다.

---

에러 메세지를 확인 해 보면 `Member` 가 정의되어 있지 않다고 한다.

```
ReferenceError: 'Member' is not defined
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F02NBS%2FbtrYIPsVt0G%2FDFea8EMXeEOyBfKEZBKo21%2Fimg.png)

먼저,<br>
코드에서 `Member` 가 정의된 부분을 찾아가보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAfZkn%2FbtrYH1AEy0a%2FSNg4FOahdxYU55NF6hVO71%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FccRcJ2%2FbtrYIOAOQA4%2FikEX50A03EPB9aYYHEYG4K%2Fimg.png)

### 에러 해결

---

E-mail 로 로그인 한 사용자의 데이터를<br>
Schema 로 받는 값으로 `Member` 라 정의 해 놓았는데,<br>
정작 사용하고자 하는곳에서는 `User` 로 정의 해 놓았던 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCfJvV%2FbtrYIxF3wEH%2F9F10pnUtCcdA20zglXHKsK%2Fimg.png)

DB 는 요청하고자 하는 사용자의 데이터를 반환 해 주는데,<br>
입력된 데이터가 다른 경우 에러 메세지를 반환 해 준다.

```
ReferenceError: 'Member' is not defined
```

`User` 로 선언된 변수를 `Member` 로 수정 해 준 뒤,<br>
다시 게시물 생성을 진행 해 보니 정상적으로 생성됨을 확인 할 수 있었다.

> 변수명 재 선언

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdc43ji%2FbtrYJbbqyhJ%2FcfAc9ltKmexTrHoN8qoOIK%2Fimg.png)

> 콘솔 창 확인

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRJBWn%2FbtrYMXQNm7T%2Fx6r6uuLJIS8BwlxU4tMZiK%2Fimg.png)

> 터미널 확인

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc9fczD%2FbtrYIxF3wG2%2FaklHPhxdOaJY4UUvEG2zv1%2Fimg.png)

> DB 확인

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvONGx%2FbtrYH1m8Tjh%2FBQeAVl3lrFRKCeAt6TmYY1%2Fimg.png)
