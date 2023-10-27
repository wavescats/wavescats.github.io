---
layout: post
title: "[React] 🔥 Firebase 를 활용한 웹 호스팅 추가하기 (배포) 🚀"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL, 파이어베이스]
---

## 개요 📣

로컬 서버에서 개발한 프로젝트를,<br>
호스팅을 통해 도메인을 얻어 외부에서의 접근을 허용하는 것을 배포(`Deploy`)라고 한다.<br>
대표적인 호스팅 서비스로는 `Netlify`, `Vercel`, `AWS`, `Github Pages` 등 이 있지만,<br>
이번 포스팅에서는,<br>
Google 에서 제공하는 `Firebase` 를 통한 호스팅 처리를 정리하고자 한다.

---

### 프로젝트 생성 🎉

`Firebase` 웹 호스팅 생성 및 배포하기 작업 순서는 크게 아래와 같이 진행된다.<br>

1️⃣ `Firebase` 프로젝트 생성<br>
2️⃣ `Firebase` 호스팅 설정<br>
3️⃣ `Firebase` 초기화<br>
4️⃣ `Firebase` 배포 및 확인

> <https://console.firebase.google.com/>

먼저 해당 URL 에서 새로운 `Firebase` 프로젝트를 생성 해 준다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FukI1V%2FbtszjriLTYX%2FKXsz5DJ316oyYNvaMa2tvK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZpd5d%2Fbtszk41jACi%2F6X0k9zqoacxydkljmlZoAK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAj4Y5%2FbtszmzfEJ66%2FIo1UV1l8zrGbkQK1iHFZk0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcXZS57%2FbtszgzoKkcr%2FTbN8JQuZrivI1F4PJWyGu1%2Fimg.png)

---

### install 🔮

우리는 `웹 앱`을 배포하려고 하니,<br>
생성한 프로젝트의 `프로젝트 개요` 화면에서 `웹` 버튼을 클릭 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7i967%2FbtszlJiwJ1d%2Ff3N2iHh7zs0i2ttsD7IBz0%2Fimg.png)

앱 닉네임을 설정 해 준뒤 호스팅 체크박스도 체크 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbdulfq%2FbtszlJv43GE%2FbFWgQ1ywt8oNo9ewAV0HCk%2Fimg.png)

`npm` 을 사용하여 프로젝트에서 `firebase` 모듈을 설치 해 준다.

```
npm install firebase
```

```
yarn add firebase
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYtFXb%2Fbtszjsbh11g%2FLfIFSKPzSjt2WkCUyImQLK%2Fimg.png)

> **`firebase SDK`** 는 추후 모듈을 초기화 할 때 사용되므로 클립보드에 저장 해 놓자

다음으로 아래 명령어를 통해<br>
`Firebase` 로 생성한 프로젝트 관리, 배포, DB 관리 등 을 할 때 사용되는 모듈을 전역으로 설치 해 준다.

```
npm install -g firebase-tools
```

```
yarn global add firebase-tools
```

---

### init 💾

프로젝트 터미널에 `firebase login` 을 실행하여,<br>
프로젝트와 생성한 프로젝트를 연결할 준비를 한다.

> 해당 명령어를 실행하면, 새 창으로 google 로그인 화면이 실행된다.

- 이미 명령어를 실행하여 로그인 된 상태

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcRWQ7n%2FbtszlJv5b1D%2FE2a097ske8JSt0GPBfLumK%2Fimg.png)

> 만약 Local 에 연결된 구글 계정을 변경하고 싶다면<br>`firebase logout` 명령으로 연결을 끊어줘야 한다.

---

```
firebase init
```

해당 명령어를 실행하면 아래와 같은 화면을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlyHZZ%2FbtszlYfAsFA%2Ff8InHBNPW6jCaAFddl6Iq1%2Fimg.png)

> `Hosting: Configue files for Firebase Hosting …` 을<br>`스페이스 바` 를 눌러 선택 후 Enter

앞서 생성한 프로젝트를 선택 해 준다.
`Select a default Firebase project for this directory:`

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgmeZZ%2FbtsziOTdQJR%2FRXCKk85KX8Y1JEIpW6hXe0%2Fimg.png)

> `Vite` 로 생성한 앱일 경우 `npm run build` 혹은 `yarn run build` 명령을 실행 시<br>`dist` 폴더가 생성된다.<br>
> (React 의 경우 `build` 폴더 생성)

> Are you ready to proceed? (Y/N)<br>**👉 진행여부 Y**<br><Br>
> What do you want to use as your public directory?<br>**👉 dist 라고 적어준다**<br>**(npm run build 로 나온 파일을 사용하기 때문에)**<br><br>
> Configure as a single-page app (rewrite all urls to /index.html)? (Y/N)<br>**👉 SPA 일경우 index.html 을 기본으로 보여주겠다는 여부 Y**<br>**(리액트이기 때문에 SPA)**<br><br>
> Set up automatic builds and deploys with GitHub? (Y/N)<br>**👉 GitHub로 자동 빌드 및 배포 설정 N**<br><br>
> File build/index.html already exists. Overwrite? (Y/N)<br>**👉 이미 생성된 index.html을 덮어쓰는여부 N**<br>**(덮어쓰면 리액트로 build 된 파일이 초기화되기 때문에 N)**

`init` 설정이 완료되면 Hosting 을 하기 위한 파일과 폴더가 생성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtElb7%2FbtszgYBVQJt%2FQn99IJ3aMI0Hd5hck12Aj1%2Fimg.png)

---

`build` 명령어를 실행하지 않고 `firebase deploy` 명령어만을 실행하면,<br>
배포가 진행되며 생성된 `Hosting URL` 주소로 접속할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUBJSZ%2FbtszlYmmyv9%2FKsaqg7zwMaWsGqNt3Bjl2K%2Fimg.png)

생성된 호스팅 주소로 접속 시 아래와 같은 화면이 출력된다면,<br>
호스팅(배포) 에 성공 한 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdfV4KG%2FbtszhsCLYcA%2F5H0jsKrbg7ywvLwAn9zcPK%2Fimg.png)

> 작성된 코드를 반영시키려면,<br>`build` 명령어를 실행하고 다시 `firebase deploy` 명령으로 적용시키면 된다.

---

### Error ❌

만약 `404` 에러 `Page Not Fount` 가 뜬다면,<br>
`firebase.json` 파일을 수정 해 준다.

![](https://velog.velcdn.com/images/-__-/post/715286b7-e392-4e3b-afa7-1b72fa3b1c55/image.png)

```
{
  "hosting": {
    "public": "build",
    "ignore": ["firebase.json", "**/.*", "**/node_modules/**"],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

---

### 배포 확인 ✔️

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBibUf%2Fbtszl05xQnT%2FsngGePKXQrFY2eBILAeUh0%2Fimg.png)

> 도메인과 함께 성공적으로 Deploy 된 상태를 확인할 수 있다.

---

## Reference 🌊

> <https://wavescats.github.io/react/2022/10/21/react18.html><br><https://firebase.google.com/docs/hosting?hl=ko><br><https://firebase.google.com/docs/hosting/quickstart?hl=ko><br><https://lxxyeon.tistory.com/38><br><https://velog.io/@hippohami/Firebase-%EC%9B%B9-%ED%98%B8%EC%8A%A4%ED%8C%85-%EC%84%A4%EC%A0%95-%EB%B0%B0%ED%8F%AC-%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95>
