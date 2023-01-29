---
layout: post
title: "[Git] Commit & Push 중 에러"
subtitle: #부제목
categories: Error
tags: [Github]
---

여느 때와 같이 수정 사항을 푸시하기 위해 파일을 추가하고 커밋과 푸ㅅ.. 응?

<br>

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2b0356e8-ca76-4d8a-9ae6-376ff0b3701a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T173948Z&X-Amz-Expires=86400&X-Amz-Signature=1b33fc7f6a47aa7602f316f5ccca90b5d477c64aeeb34df9183c51fb98d38631&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 에러 확인
---

처음 보는 에러가 날 반긴다.


> error: pathspec '[FIX] typeError' did not match any file(s) known to git

에러를 구글에 검색 해 보니,<br>
**브랜치가 업데이트 되지 않아 생기는 에러라고 한다.**

<br>
먼저 status 로 스테이징 영역을 확인해본다.<br>
수정한 파일은 정상적으로 올라갔는데, 다른 파일들이 올라가지 않았다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/430e7abb-0279-424d-bda1-593d1be49b96/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T174131Z&X-Amz-Expires=86400&X-Amz-Signature=3bd012814576f23d82415ba3441fb7dc67e745736a4f09774e45b442cb1da0f5&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

혹시 vscode 의 setting.json 파일을 건드려<br>
이전 버전과 충돌이 생긴건아닐까 싶어 검색한 해결책을 실행해본다.

```
$ git remote update
$ git fetch
or
$ git remote update
$ git checkout [브랜치명]
```

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b203fab6-a5bc-465b-a36c-274544e7f53d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T174243Z&X-Amz-Expires=86400&X-Amz-Signature=b60d3343593ce73c91a8cbfd4a731a3762e43b3aa039f270408c6a640b2af574&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9dd54b15-d180-44ab-8063-d40d507f324b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T174257Z&X-Amz-Expires=86400&X-Amz-Signature=8c7f961040ae70bfa956d14d35b56e421339794d0d3fb09d136c0dc7ab63e566&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

??? <br>
똑같다..😱<br>
나아진게 없다...😭😭😭

<br>

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2f42aa52-1258-4589-9d00-0bfb71399786/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T174450Z&X-Amz-Expires=86400&X-Amz-Signature=38f3f840073b4346edf4896bf42cec74a69f4418e3f4a2afa5306b0f065feca7&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

아무런 반응이 없다...😩
<br>
<br>

### 에러 해결
---

에러의 원인은..<br>
커밋 메세지 작성 시 **-m 옵션을 추가하지 않았다.**

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8b4d0fb3-d7cb-455a-aa13-b84f21ece3ad/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T174706Z&X-Amz-Expires=86400&X-Amz-Signature=a3a22c8e41f2714e38390dbd9d4f0acf7b04cb04eddf99d1fbc23eaf97b305f0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)


### Review
---

매일 하는 커밋 이었기에 어이가 없었지만,<br>
사소한 부분에 실수로 인해 에러가 발생하니 꼼꼼히 살펴 보는 것도 책임임을 알게 되었다.

### Reference
---

> <https://fomaios.tistory.com/entry/%ED%95%B4%EA%B2%B0%EB%B2%95-error-pathspec-did-not-match-any-files-known-to-git>