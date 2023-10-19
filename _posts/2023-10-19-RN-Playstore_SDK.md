---
layout: post
title: "[React-Native] 안드로이드 스튜디오 애뮬레이터에 구글 플레이스토어 앱 추가하기 📱"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, PlayStore, TIL]
---

## 개요 ⏰

개발자라면,,<br>
아니 컴퓨터를 사용하는 사용자의 **대부분이 윈도우 사용자 일거라 예상하며** 이 포스팅을 작성한다.<br>
나도 윈도우 개발환경을 사용하면서,<br>
디바이스는 ios 를 사용하고 있는데,<br>
**React-native** 에서 **ios 개발은 Mac 💻 으로만 가능**하다는 점이 아쉬웠다.<br>
하지만,<br>
나와 같은 케이스를 위해 **안드로이드 스튜디오 애뮬레이터**를 사용하여<br>
윈도우 개발환경에서 Android 디바이스를 구동하여 앱을 빌드 할 수 있다.<br>

이번 포스팅 에서는,<br>
애뮬레이터를 구동시켰을 때, 대게 **`Play Store`** 가 없었던 경우가 다반수였던것같다.<br>
아니, 실제로 필요가 없었다.<br>
특정 앱을 설치하기 위해 애뮬레이터에서 `Play Store` 에 접근하여야하는데,<br>
어떻게 하면 `Play Store` 를 추가할 수 있을까 ? 에서 시작하려 한다.

---

## Virtual Device Manager 📱

초기 화면에서,<br>
우측 옵션을 클릭하여 `Virtual Device Manager` 로 이동한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNuvwJ%2FbtsyQPJ6zty%2Fs8hNmUtBwor9ILqOQDkRYk%2Fimg.png)

해당 애뮬레이터의 옵션을 클릭하여 `Show on Disk` 를 선택하면,<br>
파일 탐색기가 실행되는데,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbXKV5W%2FbtsyMNmHjzy%2FfLKhzSDaN5IMC22yxrsIHk%2Fimg.png)

`config.ini` 파일을 편집기로 실행하여 아래와 같이 수정하여 저장한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcy41wx%2FbtsyLoOJ0qE%2FEHcCRXANBWTaXqWm4DU9N0%2Fimg.png)

```
PlayStore.enabled = true
image.sysdir.1 = system-images\android-31\google_apis_playstore\x86_64\
```

저장하고 `Device Manager` 를 새로고침 하면 아래와 같이 경고 아이콘이 표시되는데,<br>
해당 이미지 파일을 찾을 수 없다고 하니,<br>
`SDK Manager` 에서 **필요한 이미지를 다운로드** 받아주도록 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbndUX1%2FbtsyPUFach6%2FQkFC8gDXvMq0kJCmM2YEr1%2Fimg.png)

---

## SDK Manager 🔮

다시 초기 화면으로 돌아와 옵션 버튼을 클릭하여 `SDK Manager` 로 접근한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcWO4sZ%2FbtsyLtieBZ5%2Fb5o1fJnCMgjaVCL3T4EIlK%2Fimg.png)

첫 번째 탭 `SDK Platforms` 에서 하단의 `Show Package Details` 체크박스를 체크하면,<br>
**특정 API Level 별로 정리하여 보여주는 것 같다.**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSqXEj%2FbtsyQSNBaZW%2FsvDQFtfrnpHVvYIrbvPkCK%2Fimg.png)

원하는 System image 를 선택하여 `Apply` 버튼을 클릭하면,<br>
`SDK Component installer` 가 열리며 다운로드가 진행된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbULvR%2FbtsyNt2CCGD%2FGzKSDYd8FGuFn26GHdipiK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcB5N7i%2FbtsyNqrgtH0%2FQtMGUvg7we7dKRZA6iKo7k%2Fimg.png)

---

### 생성 및 실행 🏄

위 두 과정을 모두 마쳤다면,<br>
**새로 `Device` 를 추가하여 `Play Store` 를 지원하는 기기를 생성**한다.

> 위 이미지에서 `Pixel XL` 을 선택하여 설정을 마쳤는데,<br>
> 해당 디바이스는 `Play Store` 를 지원하지 않는 기기였다 ..😨

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUafnR%2FbtsyMMuBEox%2FNsD4k1dIpbQzNO9XJPBdD0%2Fimg.png)

나는 **`Pixel 4` 를 선택하여 디바이스를 생성** 해 주었고,<br>
해당 기기를 실행 해 보면 다음과 같이 홈 화면에 `Play Store` 가 생성됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fyi1fZ%2FbtsyLNU046g%2FOrp5X3Zfsmdh92kdKTora0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDHcw2%2FbtsyPT7jYLz%2FNNjlOhjCDPTEGq39VNcbD0%2Fimg.png)

> 실제 디바이스와 같이 앱 다운로드 하는 과정도 모두 동일하다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbs4FM8%2FbtsyPT0zhPp%2FRy1EAXhH10F9nCz06nFPfK%2Fimg.png)

---

## Reference 🌊

> <https://bada744.tistory.com/112><br><https://ccusean.tistory.com/entry/Android-Virtual-Devices-%EC%97%90-Play-Store-%EC%B6%94%EA%B0%80%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95><br><https://developer.android.com/studio/run/managing-avds?hl=ko><br><https://aspring.tistory.com/entry/Android-App-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%8A%A4%ED%8A%9C%EB%94%94%EC%98%A4-AVD-%EC%84%A4%EC%B9%98>
