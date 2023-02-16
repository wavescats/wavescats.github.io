---
layout: post
title: "[React] 구글 폰트 적용하는 법 (다운로드 x)"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

### 폰트 적용
아래 링크에서 원하는 폰트를 찾아 우측 태그를 찾아<br>
index.html 의 head 영역 내부에 넣어준다.

> <https://fonts.google.com/specimen/Do+Hyeon?subset=korean&noto.script=Kore>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FccYqbg%2FbtrX1w9jBVK%2FWJgxroyXtzLEHTL6eS4LZ0%2Fimg.png)

해당 코드를 폰트가 적용되었으면 하는 부분에 넣어준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrjX3p%2FbtrX4kTA4Ht%2FG8pccZJPYFf8Wb2JStrtMk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcvvieB%2FbtrX3uvFui7%2FxqKiSCshVTzHQSfAN2zjXK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPPQ0s%2FbtrX1ReivIz%2FY7YUhqQ3FCAQlj6MRakkgk%2Fimg.png)

### 부트스트랩으로 가져온 버튼의 폰트 변경
---

폰트를 다운로드해서 적용하는 경우,<br>
버튼에 인라인 형태로 적어주면 된다. **(카멜 케이스)**

```
<Button style={{ fontFamily : "Do Hyeon" }}>테스트 시작하기</Button>
```