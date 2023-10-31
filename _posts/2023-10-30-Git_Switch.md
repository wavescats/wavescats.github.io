---
layout: post
title: "[Git] Switch 명령어를 통해 로컬환경에 브랜치 가져오기 💭"
subtitle: #부제목
categories: Git
tags: [Github, TIL]
---

## 개요 💨

현재, 깃허브(Github) 에 협업을 위해 레포지토리와 브랜치를 생성하고,<br>
이를 작업하기 위해 로컬 환경에 `git clone` 한 상황이다.

---

### 저장소 가져오기 💾

먼저,<br>
로컬 환경에 깃허브 레포지토리를 가져올 경로를 확인한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbqxa36%2FbtszvjcII40%2FyabxB6KjYYWxdxUMqhOaU1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbllZom%2FbtszmAfLJWx%2FEFd4RWjGNkYW3oIXEoKqD0%2Fimg.png)

`git clone` 은 완료 되었고,<br>
깃허브 저장소를 보면 GUI 로 생성한 브랜치가 `main`, `develop`, `pair01`, `pair02` 가 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoGO4L%2FbtszuFG6o12%2F73bbZcYELVXoN1B17rTqr1%2Fimg.png)

`clone` 한 경로에서 브랜치를 확인 해 보니 `main` 브랜치 밖에 확인이 되지 않는다 😞

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fq8Pc4%2FbtszlYgFNC0%2Ffr49DPh1fHO2GyqC2EFtLK%2Fimg.png)

이 때,<br>
`git switch` 명령어를 입력하고 `tab` 키를 누르게 되면,<br>
아래와 같이 생성되어있는 브랜치들을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrpYGZ%2Fbtszl0MkMqo%2FjKE5MWBR9O9S7o6U06kbf0%2Fimg.png)

> **단, 모든 브랜치들을 로컬 환경에 불러오는 작업을 해 주어야 한다.**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVXIeB%2FbtszkotTXFb%2FZkuqycINPkzhHkL490Gltk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVXIeB%2FbtszkotTXFb%2FZkuqycINPkzhHkL490Gltk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FE2c4C%2Fbtszl0yOqst%2FbrQRq10GV5AywbKPSxtAIk%2Fimg.png)

다시 `git branch` 명령으로 브랜치 목록을 확인 해 보면,<br>
레포지토리의 상태와 `fetch` 한 것을 확인할 수 있다 😁

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb77dx8%2Fbtszk3bHKSL%2Ft75yRFKpI5cDpGWQjcCqC1%2Fimg.png)

> **역시 공식문서가 최고다..** <br><https://git-scm.com/docs/git-switch>

---

### Reference 🌊

> <https://jake-seo-dev.tistory.com/99><br><https://git-scm.com/docs/git-switch><br><https://fe-j.tistory.com/entry/git-checkout-%EC%99%80-git-switch-%EC%B0%A8%EC%9D%B4>
