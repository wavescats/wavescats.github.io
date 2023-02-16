---
layout: post
title: "[React] webpack / npm run build 시 발생한 오타 에러"
subtitle: #부제목
categories: React
tags: [리액트, Error]
---

### 에러 확인
---

webpack 을 활용해 프로젝트 구현을 마치고 <br>
`npm run build` 를 입력했을때의 출력창 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqMANJ%2FbtrXH72swaq%2FLzJcoo1R8TwMwpXSRwYKI1%2Fimg.png)

프로퍼티 Plugins 가 뭔지 알 수 없다는 ? 의미인것같다.

Reference를 확인해보니 다음과 같은 에러는 오타인 경우가 대부분인것같다.


**수정 전**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoRWoB%2FbtrXJWyRsO3%2F5IgKCg7GQAzkhtX9MqyWsk%2Fimg.png)

**수정 후**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbu54Rb%2FbtrXIPfUoEk%2F4wLTrVNjaayJwVRXd3B1Z1%2Fimg.png)

### 에러 해결
---

> Plugins → plugins 로 변경 (대문자 → 소문자)


`npm run build`
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpLZyT%2FbtrXH7VF2Bh%2Fmy7HfcrKesR1G5Rck8e6k0%2Fimg.png)


### Reference
> <https://inkor.tistory.com/m/143>

> <https://www.inflearn.com/questions/24678/npx-webpack-%EC%97%90%EB%9F%AC%EB%B0%9C%EC%83%9D%ED%95%A9%EB%8B%88%EB%8B%A4-%EB%8F%84%EC%99%80%EC%A3%BC%EC%84%B8%EC%9A%94>