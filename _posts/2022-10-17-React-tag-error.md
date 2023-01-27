---
layout: post
title: "[React] Document input 태그 오류"
subtitle: #부제목
categories: Error
tags: [리액트]
---

### 에러 확인
---
부트스트랩을 이용하여 HTML 파일을 수정하던 중,<BR>
알 수 없는 에러로 인해 렌더링이 되지 않는다.
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5a5793d2-b3fa-463a-9df9-967ed702d7a6/input_%EC%98%A4%EB%A5%98.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T180042Z&X-Amz-Expires=86400&X-Amz-Signature=f63952041e1cd7422437e6aab92f52a30a888556afa2fb0d08fc6d977de53624&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22input%2520%25EC%2598%25A4%25EB%25A5%2598.PNG.png%22&x-id=GetObject)

### 에러 해결
---
리액트에는 <br>
<span style='background-color: #ffdce0; color: #808080;'> '모든 태그는 열리면 닫는 태그가 있어야 한다' </span> 라는 규칙이 존재한다.

> input 태그에 닫는 태그가 존재하지 않음.

html 문서 내에서는 무관했을 부분이었을테지만,<br>
리액트로 전환하는 과정에서는 지켜줘야 하는 규칙이 있음을 알게되었다.

### Reference
> <https://sir.kr/qa/59262>
