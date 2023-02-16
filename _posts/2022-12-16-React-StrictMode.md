---
layout: post
title: "[React] 콘솔 창에서 같은 결과가 중복되어 출력되는경우"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

아래와 같이 **console.log** 를 찍어 보았을 때,<Br>
같은 결과가 중복되어 출력된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIsY8A%2FbtrX9E7fSvs%2FsagXNxvWKqZ6t6BHDUPKG1%2Fimg.png)

index.js 에서 코드를 살펴보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuhR7J%2FbtrYj2yzRgd%2F85ODkiz9Hw10W2Oq2o3MfK%2Fimg.png)

#### Reference
- StrictMode 가 뭘까?
> <https://velog.io/@sweet_pumpkin/%EB%AC%B4%EC%9E%91%EC%A0%95-%EB%94%B0%EB%9D%BC%ED%95%98%EA%B8%B0-%EC%95%84%EB%8B%88-%EC%99%9C-%EC%BD%94%EB%93%9C%EA%B0%80-%EB%91%90-%EB%B2%88-%EC%B6%9C%EB%A0%A5%EB%90%98%EB%8A%94-%EA%B1%B4%EB%8D%B0-React-StrictMode>

Reference 를 참고한 결과,<br>
App 을 감싸고 있는 StrictMode 를 제거해 주면 된다고 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAh4t4%2FbtrYjykexmo%2FS4HLXsHkHbNHMp3XzeiY2K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdmkwWS%2FbtrYiU9bp08%2FzJRKyY0bSIKNKk13DBeDZK%2Fimg.png)