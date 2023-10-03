---
layout: post
title: "[React-Native] 안드로이드 스튜디오 애뮬레이터 API Level 과 관련된 SDK 에러 💧"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, TIL, Error]
---

## 개요 👂

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqyLzr%2FbtswpYDmZje%2F7v7hhy9Iwlm7MBv75pHYkK%2Fimg.png)

**`npx react-native init '프로젝트명'`** 으로 React-Native 앱을 생성하고,<br>
생성한 앱을 실행했을 때 마주친 에러를 기록하려한다.

---

### init 🌟

**`개요`** 에서 사용한 프로젝트 생성 명령어를 사용하여 프로젝트를 생성해 준다.

> **`template`** 옵션을 주어 TypeScript 로 초기화 해 준다 ❗️

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyRzMy%2FbtswPUtkI71%2FYquhBmaNRIxugPOgkoNDtK%2Fimg.png)

생성한 프로젝트 경로로 이동하여 **`.code`** 명령어를 통해 새 창에서 VSCode 를 연다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQVHIj%2FbtswBEkcKqu%2FAkzm3KQKkU7qBLw1wAAK41%2Fimg.png)

---

### Error 💥

여느때와 같이 **`yarn run android`** 명령어를 통해 생성한 앱을 실행 하면,<br>
지정된 애뮬레이터가 실행되며 RN 앱이 실행되어야하는데<br>
아래와 같은 에러가 발생했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsEZ2V%2FbtswUU7LAWe%2FiA4mYsnr7cb43n9IoAARAk%2Fimg.png)

에러를 살펴보면,<br>
**`/android/app/build.gradle`** 에 정의되어있는 플러그인을 실행하기 위한 클래스를 찾을 수 없다.<br>
이러하니... 기존의 내역이 남아있는 캐시를 지워라 ? 라는 형태의 메세지 인것같다.<br>

> 만약, 해당 에러를 마주쳤다면 아래 1️⃣, 2️⃣, 3️⃣ 번을 시도 해 보자 ❗️<bR>

**1️⃣ 캐시 제거**

Android 프로젝트 디렉토리로 이동한 다음,<br>
**`./gradlew clean`** 명령을 실행하여 Gradle 캐시를 삭제하고, 다시 React Native 앱을 실행 해 보자.

```
cd android
./gradlew clean
```

**2️⃣ Gradle 버전 업데이트**

Android 프로젝트의 build.gradle 파일에서 사용 중인 Gradle 버전을 확인하고<br>
**`build.gradle`** 파일 내용 중에 아래 부분을 찾아서 Gradle 최신 버전을 확인하고 업데이트 한다.

> 최신 버전은 **`Gradle`** 공식 웹 사이트에서 확인할 수 있다 👇👇👇<br><https://gradle.org/releases/>

```
dependencies {
    classpath("com.android.tools.build:gradle:버전_업데이트_필요")
}
```

**3️⃣ React-Native 앱 재설정**

나도 이 방법을 적용 해 보았는데,<br>
React Native 앱의 **`./node_modules`** 와 Gradle 캐시를 모두 지우고 다시 설치하는 방법이다.

```
rm -rf node_modules/
yarn install
cd android
./gradlew clean
cd ..
react-native run-android
```

---

두 번째로는,<br>
프로젝트에 정의되어있는 **`compileSdkVersion`** 이 애뮬레이터의 버전과 일치하지 않는다고 한다.<br>
이 에러를 먼저 해결 해 보도록 하자.

**`android/build.gradle`** 을 열어보면,<br>
아래와 같은 **`buildscript`** 를 확인할 수 있는데,<br>
정의되어있는 버전을 **`31`** 로 수정 해 준다.

> 원래 **33** 으로 지정되어있었음 ❗️

이 **`31`** 은 어디서 알았냐면,<br>
안드로이드 스튜디오에 **`Virtual Device Manager`** 에서 생성한 애뮬레이터의 버전에서 확인했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIBaTp%2Fbtswkp81RlK%2FFDqxhReolAeMfaKy5DS2H1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcMXbIC%2FbtswcNCp2jJ%2Fu8jCuvvoIHoq1TG5ZQ6Nf1%2Fimg.png)

> API Level 이란 ❓<br>
> 공식문서 참조 👇👇👇<br><https://developer.android.com/guide/topics/manifest/uses-sdk-element?hl=ko>

해당 버전을 수정 해 주고,<br>
**`yarn run android`** 명령으로 다시 앱을 실행 해 보면 정상적으로 애뮬레이터와 연결이 됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc4xFGS%2FbtswarGvVCw%2FikK26Gv5kdEYKGKTNLgutK%2Fimg.png)

---

## Reference 🌊

> <https://developer.android.com/guide/topics/manifest/uses-sdk-element?hl=ko><br><https://stackoverflow.com/questions/59163464/could-not-find-implementation-class-for-plugin-error-when-using-plugin-java-gra><br><
