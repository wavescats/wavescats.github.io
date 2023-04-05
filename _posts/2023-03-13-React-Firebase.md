---
layout: post
title: "[React] Firebase 를 활용한 회원가입 기능 및 DB 관리"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL, 파이어베이스]
---

## 개요

Firebase 는 Google 에서 개발한 클라우드 기반 백엔드 플랫폼으로,<br>
모바일 및 웹 애플리케이션 개발 시 조금 더 쉬운 기능과 서비스를 제공하고 있다.

## 사용이유 ?

개발자가 어플리케이션을 개발하고 운영하는데 필요한 다양한 서비스를 제공하여<br>
생산성을 높이고 유지보수를 간편하게 해 주는 플랫폼 이다.
<br>

- Fast (쉬운 개발)
  - 제공하는 서비스를 이용하여
- 안정성
  - serverLess 아키텍쳐를 사용하기 때문에 유지보수 및 확장성에 용이함.
- 실시간 데이터베이스
  - 데이터의 변경사항을 실시간으로 감지하여 동기화 가능.
- 호스팅
  - CDN 을 활용하여 보다 빠르게 애플리케이션을 구축하며 정적 파일을 호스팅 할 수 있는 서비스를 제공.
- 쉬운 배포
  - Firebase CLI(Command Line Interface)를 사용하여 로컬에서 개발한 애플리케이션을 쉽게 배포가능.
- 확장성
  - 서버리스 아키텍처를 사용하기 때문에 트래픽이 증가하더라도 추가적인 리소스를 필요로하지 않고 확장할 수 있음.

> 아래는 **기초 환경 설정**이기 때문에 이미 알고 있다면 다음으로 이동 가능

---

## Firebase 설정

<https://firebase.google.com/?hl=ko>
<br>
이름을 지정하여 프로젝트를 생성한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvyTLI%2Fbtr8eWXj61E%2FuAz8Q1kBD4mE36y7PczQZ1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FF5AOJ%2Fbtr745OuHcw%2FBKiVDuG92Wvs5lLsUd5quK%2Fimg.png)

(생성 후)<br>
간단한 회원인증관리를 하기 위해<br>
Authentication - 이메일 / 비밀번호 를 선택한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXmI3B%2Fbtr753iIcjL%2FpyRxsk3iYF67lj6rp3t5r1%2Fimg.png)

### Realtime Database

'한국' 지역이 없기 때문에 아시아에 속해있는 '싱가포르' 로 지정한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fr47p1%2Fbtr77PRJ3o6%2Fs6eLALgogHcn6OUIVm3kvk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrAFkM%2Fbtr8f3aLvec%2FUz6QSGcrY6tKMfFUFieDyk%2Fimg.png)

### Storage

Realtime Database 와 마찬가지로,<br>
아시아 지역을 설정 해 준다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbK7o7z%2Fbtr8h9gXIxf%2Fjj6xJvJtEfv8gRehPzu360%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsBKAm%2Fbtr8axJ1bDE%2Fbvj1ZwgjGXm88okjutyYkK%2Fimg.png)

### 코드에 추가하기

'프로젝트 개요' 에서<br>
생성한 프로젝트로 접근하여 웹 앱에 추가할 추가 정보를 입력 해 준다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcXCVBI%2Fbtr8f147hG8%2FsuYhq4cZOb7vtj5YxKMhsk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5KkXi%2Fbtr745VjmXa%2Fr5IUWJ1dYJO96aVr5Khty0%2Fimg.png)

다음으로,<br>
코드 에디터에 firebase 환경을 추가해 주어야 하기 때문에,<br>

```js
npm i firebase
```

npm 명령어를 사용하여 설치 해 준다.

아래 있는 제품의 SDK 부분은 firebase 디렉토리를 생성해 하위 파일에 넣어 준다.<br>
`/firebase/index.js`

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtiPhX%2Fbtr752xhvYz%2FAab0NqnsXv2BRcEleY4RkK%2Fimg.png)

SDK 키를 추가 했다면, CLI 를 추가로 설치 해 준다.

```js
npm install -g firebase-tools
```

배포는 생략.

---

## 적용

회원가입 UI 를 구현했다는 가정 하에 진행.<br>
회원가입 로직이 작성되어 있는 상단에 Firebase 와 관련된 정보를 import 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaCrlz%2Fbtr8axXKmb5%2FqCUqUhDhhdCvWzg4Ng371K%2Fimg.png)

`postUserData` 를 생성해 Firebase 에 생성될 유저정보를 입력 해 준다.<br>
인증 정보를 위해 `getAuth()`, 입력받는 값으로 email, password

> Promise 객체로 값을 입력받기 때문에,<br>
> async await 방식을 사용해 비동기 처리로 전환

해당 과정을 거치게 되면,<br>
firebase 에는 새로운 유저가 생성되고, <br>
회원 가입과 동시에 로그인 상태로 변경된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHK1yg%2Fbtr8aw5CPQc%2FHYKKbCVxF9RMydKxHVVAtK%2Fimg.png)

가입한 유저의 정보를 Firebase RealTime DB 에 저장하기 위해,<br>
아래 정보를 import 해 준다.

```js
import { getDatabase, ref, set } from "firebase/database";
```

유저의 정보가 저장되고자 하는 경로를 입력 해 준다.

```js
await set(ref(getDatabase(), "users/" + user.uid), {
  // 경로 지정
  name: user.displayName,
  avatar: user.photoURL,
});
```

name 은 회원 가입 시 유저가 설정한 이름이고,<br>
avatar 는 회원 가입 시 생성되는 프로필 이미지이다.

---

<localhost:3000/join> 으로 접근 했을 때의 보여지는 회원가입 페이지 이다.<br>
test, test@test.com 으로 순차적으로 입력 후 회원가입을 진행하게 되면
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbh2XRf%2Fbtr8eW4q3i3%2FzcwWjmFc2P2n4YpKpfBHHk%2Fimg.png)

설정한 네비게이션 기능으로 인해 /Main 페이지로 이동하게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdavbQd%2Fbtr77gJct8s%2FBItuLOhA5CwoYJAXW8CRuk%2Fimg.png)

그리고, Firebase 를 확인 해 보면<br>
Authentication 내역에 방금 생성한 test 에 대한 정보가 기록되어 있다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdqO87Y%2Fbtr8iZMjYiM%2FFbUwqh1FphUei8Vv9rhQs0%2Fimg.png)

Realtime DB 에도 마찬가지로,<br>
지정해 주었던 /users 경로 아래에 생성한 유저들의 정보가 담기고 있음을 확인할 수 있다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeJJPE8%2Fbtr8gVjv3Hq%2F9WCBiWUcY3ZKY4KBQPeZHK%2Fimg.png)

### Avatar

유저 정보에 Avatar 를 넘겨주고 있는데,<br>
이는 간단히 보면 '프로필 이미지' 로,<br>
유저가 생성한 이메일 값을 `md5` 라는 함수를 사용해 암호화 된 해시 값으로 생성해 준다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdkeqX%2Fbtr8f2Dh8y7%2FTHmAxSq74RJm7JfPKGWDJ1%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKqlvJ%2Fbtr8kIpSNwV%2Fyk4kNaNoqVqyX3TrLzMsr0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEwaQB%2Fbtr8i83yBdb%2FcjjP2UACfSVZHYYxfzHkw0%2Fimg.png)

## Reference

> <https://ko.gravatar.com/site/implement/images/>
