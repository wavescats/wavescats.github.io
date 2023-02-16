---
layout: post
title: "[Git] Commit & Push 중 에러"
subtitle: #부제목
categories: Git
tags: [Github, Error]
---

여느 때와 같이 수정 사항을 푸시하기 위해 파일을 추가하고 커밋과 푸ㅅ.. 응?

<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcm3Tio%2FbtrXEChOtpJ%2FasZfOPX77LsHCwpUemigVk%2Fimg.png)

### 에러 확인
---

처음 보는 에러가 날 반긴다.


> error: pathspec '[FIX] typeError' did not match any file(s) known to git

에러를 구글에 검색 해 보니,<br>
**브랜치가 업데이트 되지 않아 생기는 에러라고 한다.**

<br>
먼저 status 로 스테이징 영역을 확인해본다.<br>
수정한 파일은 정상적으로 올라갔는데, 다른 파일들이 올라가지 않았다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcSQwFt%2FbtrXHUaZ1nk%2FVKsstJiMkERh86Iv8wKbw1%2Fimg.png)

혹시 vscode 의 setting.json 파일을 건드려<br>
이전 버전과 충돌이 생긴건아닐까 싶어 검색한 해결책을 실행해본다.

```
$ git remote update
$ git fetch
or
$ git remote update
$ git checkout [브랜치명]
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fl5uWp%2FbtrXGnLtCSH%2FK7WKKvk5EKnolT76BFQ1v0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJPbED%2FbtrXFvJNBn1%2FMjZuo8aSEOlt6ck0V1h5nk%2Fimg.png)

??? <br>
똑같다..😱<br>
나아진게 없다...😭😭😭

<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVk7yE%2FbtrXFuD6AqQ%2FoHM3HCijWY0ed7y5DMLdwK%2Fimg.png)

아무런 반응이 없다...😩
<br>
<br>

### 에러 해결
---

에러의 원인은..<br>
커밋 메세지 작성 시 **-m 옵션을 추가하지 않았다.**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNqM0Z%2FbtrXECWrvJI%2FRhkvoIiKsicVKB3YQkMO5k%2Fimg.png)


### Review
---

매일 하는 커밋 이었기에 어이가 없었지만,<br>
사소한 부분에 실수로 인해 에러가 발생하니 꼼꼼히 살펴 보는 것도 책임임을 알게 되었다.

### Reference
---

> <https://fomaios.tistory.com/entry/%ED%95%B4%EA%B2%B0%EB%B2%95-error-pathspec-did-not-match-any-files-known-to-git>