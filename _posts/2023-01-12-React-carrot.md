---
layout: post
title: "[React] npm i 로 패키지 설치 시 캐럿의 유무"
subtitle: #부제목
categories: TIL
tags: [리액트]
---

npm package.json 에서 패키지의 버전을 관리하다 보면<br>
~1.0.1 이나 ^12.1.2 과 같은 것을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdv5VHf%2FbtrXK86SZFb%2F4hqWEDf9Ar6PVEVUJKKJmK%2Fimg.png)

위 명령어로 prettier 를 설치 해 주었다.<br>
가만히 보니 다른 패키지들과 다른 점이 보인다.<br>
바로 버전 앞에 ^ 모양이 없다.

이는 캐럿 이라는 단어로<br>
패키지가 업데이트 되었을 때 (`npm i` 등)<br>
마이너 버전에 한해 업데이트를 허용한다는 의미이다.
<br>
<br>
즉, 업데이트를 원하지 않을 경우 옵션을 추가하여 캐럿이 없이 패키지 설치가 가능하다.<br>
`—save-exact` 옵션을 추가하지 않고 설치하게 되면 캐럿이 추가된다.