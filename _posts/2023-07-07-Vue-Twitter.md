---
layout: post
title: "[Project] Twitter 앱 (Vue.js) 🐦"
subtitle: #부제목
categories: [Project]
tags: [뷰js, 프로젝트]
---

## [Project] Toy 프로젝트 회고 🚝

## 🐦 Twitter

해당 서비스는 Twitter 를 클론한 프로젝트로<br>
게시물을 생성 및 조회하며<br>
원하는 게시물에 좋아요 기능을 통해<br>
유저들의 반응을 확인할 수 있는 서비스 입니다.

---

### PipeLine 🔮

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fsrxye%2FbtsmRr3bFaU%2FvUDp0HSdqrOolc7AkX7RxK%2Fimg.png)

### 프로젝트 구성 🌱

#### 프로젝트 기간 (7/3 ~ 7/7)

- Front-end
  `Vue.js` 프레임워크인 `Quasar` 로 웹 페이지 UI/UX 구성
  <br>
- Back-end
  `firebase` 의 `Firestore` 로 유저 및 게시물 DB 관리

---

#### 기능소개 🔨

`Home` 탭과 `About` 탭으로<br>
두 페이지를 라우팅 기능을 활용하여 구성했지만,<br>
현재는 단일 페이지 구성으로<br>
최대한 Twitter 와 유사하게 구성하려 기획하였습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdELRVz%2FbtsmRoL8tH1%2F8bKeukn9TPqblEqnkkWgKK%2Fimg.png)

반응형 사이즈로 1024px 이하이거나,
모바일 환경에서 실행 시 UI 가 변경되도록 설정하였습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnJX5G%2FbtsmQqxkx7n%2FqL6UOezmQyRg8KX1vOiRt0%2Fimg.png)

![](https://blog.kakaocdn.net/dn/bDHJup/btsmRsA0YP9/TeDUNz3HH7Glgw9050BKr0/img.gif)

**Post**
Firestore 를 통해 게시물을 생성할때마다 문서를 추가하고,<br>
제거 시 실시간으로 DB 에 반영되도록 구현하였습니다.

**Like**
UI 에서 하트 이모지를 클릭 시 Toggle 되어<br>
색깔이 변경되며 이를 Firestore 에서도 실시간 반영되게 구현하였습니다.

![](https://blog.kakaocdn.net/dn/csWhCq/btsmYMyxVTK/5AKomdMKTBKiQqgqwewD10/img.gif)

---

> Github 소스코드<br> > <https://github.com/wavecats/Twitter_App>

---

#### 개발회고 💡

새로 입사한 기업에서<br>
React 가 아닌 Vue.js 로 프로젝트를 진행하고 있어<br>
Vue.js 를 공부하던 중<br>

`instagram` 을 제작한 기업인<br>
`meta` 에서 새로운 탈 중앙 소셜 미디어 플랫폼인 '스레드(Threads)' 가 출시하였고,<br>
이에 감명을 받아<br>
Twitter 앱을 클론 해 보는 Toy Project 를 진행했습니다.<br>

---

#### 아쉬웠던 점 & 보완해야 할 사항

**DateTime**

새로운 게시물 작성 시 `date-fns` 라이브러리를 사용하여<br>
`"3 minute ago"` 형태로 구현하려 했지만<br>
생각한대로 잘 되지 않아 추후 개선해야 할 부분으로 남겨두었습니다.<br>
<br>
**Authentication**
유저들의 DB 를 관리하기 위하여<br>
회원가입 및 로그인기능을 추가할 계획을 갖고있습니다.<br>
사용자의 편의를 위하여 소셜 로그인 기능을 추가하려고 합니다.

---

### Reference 🌊

> <https://youtu.be/la-0ulfn0_M<br><br><https://date-fns.org/><br><https://firebase.google.com/docs/firestore/using-console?hl=ko&authuser=0><br><https://about.instagram.com/ko-kr/blog/announcements/introducing-threads-app>
