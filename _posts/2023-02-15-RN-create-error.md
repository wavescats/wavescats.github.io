---
layout: post
title: "[React-Native] 프로젝트 생성 시 발생한 에러 'npx create-expo-app'"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, Error]
---

### 에러 확인 💥
```bash
npx create-expo-app .
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb36PZm%2FbtrZrc1Gs7F%2FS0USIkpENAIehQzNwVOk11%2Fimg.png)

`npx` 명령어를 사용해 expo app 을 생성하였다.

생성한 앱을 실행하기 위해 `expo start` 를 입력하였다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfHuhS%2FbtrZsFvehRt%2FdzPWKsUgofABL38kpikB61%2Fimg.png)

여기까진 괜찮았지..😩
<br>
오늘도 역시 무탈히 지나가는 일 없이 에러 발생..😭😭

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXjy2w%2FbtrZrfKOXlE%2F8BHgXuRPzzwQQXKCVRDV30%2Fimg.png)

앱을 실행 시키고 QR 코드를 iPhone 에서 실행하자<br>
bundling 메세지와 함께 에러 메세지가 반긴다.

에러를 살펴보면,<br>

> Error: Problem validating fields in app.json.<br>
• Field: slug - 'slug' must match pattern "^[a-zA-Z0-9_\-]+$".

app.json > slug 부분에 정규표현식 외에 사용되는 무엇인가 존재하여 발생하는 에러인것같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgEjtD%2FbtrZqzC7Evh%2F6AujjAEApdCgxlxNaS10Hk%2Fimg.png)

### 에러 해결 ✨
아마 프로젝트 이름에서 에러가 발생하는것같다.
프로젝트 이름에 사용된 `.` 을 제거 후 다시 실행해보면,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdojXkK%2FbtrZlYXOE4e%2FBQ7M8GyVKHwzwq7P6kAwfK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwAMdN%2FbtrZqz4fOA1%2F4C9XkaXvBDaB8BnQHZ2kw1%2Fimg.png)

에러 없이 깔끔한 실행을 할 수 있다 ! 😁