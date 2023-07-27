---
layout: post
title: "[React-Native] Firebase-Firestore 기간 만료로 인한 권한 에러 💫"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, Error, TIL]
---

## 개요

`React-Native` 로 채팅 앱을 `Firebase` 를 사용하여 구현하던 중,
갑자기 발생한 에러로 인해 채팅방이 불러와 지지 않는 에러가 발생했다 😱

- 에러가 발생한 화면

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnQqeV%2Fbtso5W0YlLj%2Fhyf4WXAoI1rPqMCQxJA4zk%2Fimg.png)

- 에러가 발생하기 전 화면

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVdOsl%2FbtsoiZXjbSF%2FtCgPWb3cAAf8g8oCbvVOHK%2Fimg.png)

---

### 에러 확인 😈

Firebase 의 해당 프로젝트를 살펴보니<br>
채팅방이 생성되어 있는데,<br>
화면에 출력이 되지 않는 상태인것같았다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcJP3xQ%2Fbtso6ScyrZO%2FvTxS6rt3zW2qBhPsOMU4AK%2Fimg.png)

Firebase 프로젝트를 생성하면 메일로 수신됨이 문득 떠올라<br>
메일함을 열어보니<br>
Firebase 측에서 발송된 메일이 와 있었다 💌

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTyJRS%2FbtsoXy0QpQc%2FiibTaq7ko7pzliYkmAwdsk%2Fimg.png)

---

### 에러 해결 😇

해당 메일을 확인하면서 프로젝트를 생성 할 때,<br>
테스트모드 (30일) 로 지정하여 생성한 기억이 났고<br>
하단의 `규칙수정` 버튼을 통해<br>
사전에 지정한 규칙을 수정 해 주었다

- Before

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbq7r6G%2Fbtso09tnjOa%2F6tPhO3cgzPGloDWfKuMzt1%2Fimg.png)

- After

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9qxuA%2Fbtso8zp7ox9%2FkMwhW4GSBtEiwZKMj8nBM1%2Fimg.png)

---

에러를 수정하고 node 로 실행된 터미널에서<br>
`r` 을 통해 앱을 reroad 하니<br>
에러가 없어지고 화면이 정상적으로 출력됨을 확인했다 !

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fnzzjm%2Fbtso1uc6UHd%2FJXc7vYkfRmtiI4wipRqM2K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTFnfF%2Fbtso6jhocqL%2FGSwEGYiwsz2HjWpRTRk5I0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHqeAe%2Fbtso7h4ttAp%2FgmFNQyjiPfSGNUivKqK3k0%2Fimg.png)

---

### Reference 🌊

> <https://stackoverflow.com/questions/54479483/get-error-firestore-the-caller-does-not-have-permission-to-execute-the-specif><br><https://bocoder.tistory.com/85><br><https://firebase.google.com/docs/reference/kotlin/com/google/firebase/firestore/FirebaseFirestoreException.Code>
