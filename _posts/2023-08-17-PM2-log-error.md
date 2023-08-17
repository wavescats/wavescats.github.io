---
layout: post
title: "[Node.js] PM2 log 명령어가 실행되지 않을때 해결방법 💞"
subtitle: #부제목
categories: [Node.js]
tags: [pm2, 백엔드, Error, TIL]
---

## 개요 👋

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmC6xr%2Fbtsrr0FDkBP%2FlUjVr9u9Z2pZqWG8lgcUM1%2Fimg.webp)

**`PM2` 란,**<br>
`Node.js` 애플리케이션을 위한 고급, 생산 중심의 프로세스 관리자 라고한다.<br><br>

`PM2` 는,<bR>
데몬화, 클러스터링, 로깅, 로드 밸런싱 등 다양한 기능을 제공한다.<br>

**1️⃣ 데몬화**<br> - 애플리케이션을 데몬화 하여 백그라운드에서 실행할 수 있다.

**2️⃣ 클러스터링**<br> - 애플리케이션을 여러 개의 프로세스로 분산하는 클러스터링을 지원한다.

**3️⃣ 로드밸런싱**<br> - 애플리케이션에 들어오는 요청을 여러개의 프로세스에 고르게 분산시킨다.

**4️⃣ 자동 재시작**<br> - 애플리케이션에 오류가 발생하며 자동으로 재시작한다.

**5️⃣ 로깅**<br> - 애플리케이션의 로그를 쉽게 모니터링하고 관리할 수 있다.

**6️⃣ 모니터링**<br> - 애플리케이션의 메모리 사용량, CPU 사용량 등 성능 지표를 모니터링 할 수 있다.

---

### 에러 발견 💥

`pm2 log 1` 의 명령어를 실행하면<bR>
id 값이 1 인 프로세스로 요청한 log 가 콘솔창에 출력되어야 하지만,<bR>
다음과 같이 에러가 발생해 `log` 가 출력되지 않는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrfAVq%2Fbtsrq93VZQ0%2F8eF7xJwwPFiiClzGJAgWsK%2Fimg.png)

---

### 에러 해결 ✨

```
pm2 reload <app_name|id|'all'>
```

본인의 경우 API 를 호출하는 부분에서 에러를 마주쳤기 때문에,
<Br>
**재 시작 할 id 값을 명시**하여 `reload` 해 주었다.

```
pm2 reload 1
```

> 위에 `reload` 명령어가 정의되어있듯,<br>
> 프로세스의 `name` 이나 `id` 혹은<br>
> 고유한 값인 `pid` 값도 가능할 것이라 예상하는 바 이다.

위 명령어를 통해 `PM2` 에서 **실행중인 프로세스를 재 시작** 할 수 있다.<br>

해당 명령어는,<br>
기존 프로세스를 중지 시키고 새 프로세스를 시작하는 대신<br>
그레이스풀 리로드를 수행하여 **기존 연결을 유지**하면서 애플리케이션을 **재시작** 할 수 있다.<bR>
이를 통해 **서비스 중단 시간 없이** 애플리케이션을 업데이트 및 재시작을 할 수 있다.

---

`reload` 를 통해 프로세스를 재 시작 했다면,
`pm2 list` 명령어를 통해<br>
현재 데몬의 형태로 실행되고있는 프로세스들의 상태를 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FS1sJK%2Fbtsrh076afO%2FzTCcmxHfnrrihYxSrQ9ke1%2Fimg.png)

이후,<br>
다시 `pm2 log 1` 명령어를 실행하면<bR>
해당 API 에 요청을 보낸 log 가 정상적으로 출력된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcTGdXC%2FbtsrgsYnLKb%2F7KYPTtvnBtvNocQSzFMbg1%2Fimg.png)

---

### Reference 🌊

> <https://inpa.tistory.com/entry/node-%F0%9F%93%9A-PM2-%EB%AA%A8%EB%93%88-%EC%82%AC%EC%9A%A9%EB%B2%95-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0-%EB%AC%B4%EC%A4%91%EB%8B%A8-%EC%84%9C%EB%B9%84%EC%8A%A4><br><https://gareen.tistory.com/59><br><https://velog.io/@sinclebear/PM2-Log-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95>
