---
layout: post
title: "[React] Document input 태그 에러"
subtitle: #부제목
categories: React
tags: [리액트, Error]
---

### 에러 확인
---
부트스트랩을 이용하여 HTML 파일을 수정하던 중,<BR>
알 수 없는 에러로 인해 렌더링이 되지 않는다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbiSVmY%2FbtrXHXyxOvg%2FkWzYu8XLCFcgoAiZqnxN3k%2Fimg.png)

### 에러 해결
---
리액트에는 <br>
<span style='background-color: #ffdce0; color: #808080;'> '모든 태그는 열리면 닫는 태그가 있어야 한다' </span> 라는 규칙이 존재한다.

> input 태그에 닫는 태그가 존재하지 않음.

html 문서 내에서는 무관했을 부분이었을테지만,<br>
리액트로 전환하는 과정에서는 지켜줘야 하는 규칙이 있음을 알게되었다.

### Reference
> <https://sir.kr/qa/59262>
