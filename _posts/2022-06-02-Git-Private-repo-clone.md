---
layout: post
title: "[Git] Private Repo Clone 시 에러"
subtitle: #부제목
categories: Git
tags: [Error, Github]
---

### 에러 확인

과제를 진행하기 위해<br>
GitHub 에 있는 레포지토리를 Clone 하는 과정에서 발생한 에러이다.💫

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn6hmg%2FbtrYTp7UC5O%2FV1I2k1EmPaKy4Lb0TVSqBk%2Fimg.png)

음...😕

정상적으로 로컬에 Clone 이 되지 않은 상황이다.

계정 내 임의의 Public 레포지토리를 Clone 해 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbweRP9%2FbtrYTpz5iN1%2FlzNhF1ZY0NKMG3wNRW7aj0%2Fimg.png)

이건 되는데...😰

---

Private 레포지토리를 Clone 하기 위해 아래와 같은 방법을 시도 해 보았지만,<br>
나에겐 해당사항 없이 처음과 같은 메세지만 볼 수 있었다.😵

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLDTzA%2FbtrYQRSvt1o%2F3RDtkwbsUlyUOKCV4gxQzK%2Fimg.png)

이 에러를 해결하기에 앞서 전제 조건으로,<br>
본인은 이 실습 전에 ***깃허브 토큰***을 발급 받아 **사용했던 이력**이 있었고,<br>

발급한 토큰의 **기간이 만료**가 되어있던 상태였으며,<br>
만료된 토큰은 **이미 로컬에 등록**되어 있는 상태였다.

### 에러 해결
---

새로 발급받은 **Personal access tokens** 키를<br>
<br>
(윈도우 기준)<br>
제어판 - windows 자격증명관리자 - git:http://github.com - 편집 - 암호 변경(토큰 키 입력)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fch90Kv%2FbtrYRRc9czG%2FYtF80fw6Nm3hlDldGmUiR0%2Fimg.png)

터미널을(git bash를) 재 부팅 시킨 뒤 다시 클론 명령어를 입력 했더니,<br>
정상적으로 클론이 됨을 확인 할 수 있었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzBu0K%2FbtrYUuOqGWE%2F012Fx76hbwikR0S8rcE0x1%2Fimg.png)