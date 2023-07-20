---
layout: post
title: "[React-Native] 특정 라이브러리 설치 후 Android 빌드 시 SDK 에러 해결방법"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, TIL, Error]
---

## 개요

아래와 같이 React-Native 를 사용하여<br>
실시간 채팅이 가능한 모바일 서비스를 제작중인 과정이다<br>
<br>
여러명의 사용자를 관리하기 위해<br>
파이어베이스 Authentication 을 사용하여
회원가입 기능을 추가하였고,<br>

출력된 `내 정보` 란에서 프로필 이미지를 추가하려한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVdOsl%2FbtsoiZXjbSF%2FtCgPWb3cAAf8g8oCbvVOHK%2Fimg.png)

---

## 설치

해당 기능을 구현하기 위해 설치한 라이브러리는<br>
<br>
`Image-Crop-Picker`<Br>

프로젝트에 사용한 패키지 매니저로는 `yarn` 을 사용했기 때문에,<br>
해당 명령어를 통해 라이브러리를 설치 해 주었다.

```bash
yarn add react-native-image-crop-picker
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXYgsr%2FbtsohYRPL9L%2FIrVn3cFaKaqOt3Kx86zxkK%2Fimg.jpg)

라이브러리 설치가 완료되면<br>
`android/app/build.gradle` 의 경로로 접근하여<br>
해당 부분을 추가 해 줌으로 인해 라이브러리를 제어 할 수 있다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB7Nye%2Fbtsoe1WJRfQ%2Fp9RA190uRHkff4S7jUUufK%2Fimg.png)

---

### 에러확인

여느 때와 같이<bR>
`yarn run android` 명령을 통해 안드로이드 스튜디오 애뮬레이터를 실행시킨다<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcnBVdq%2FbtsogXMF762%2F4s86dU1ApGkSgKKfL06M30%2Fimg.jpg)

**엥 ?**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqkzUJ%2Fbtsog0bqhLD%2FFhPb5pfCIPYiLVnBobKnM0%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLfXVg%2Fbtsofs7JNPF%2FCVOO5BAY2AVfwIdJ6FtK70%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcRj0xD%2FbtsohXZHq0x%2FwoRRMpJVRmMzJke9zwUdy1%2Fimg.jpg)

심지어 실행중이던 애뮬레이터도 종료되며 튕겨져 나온다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhOpmV%2FbtsofoYp6TP%2FPkC5MH3y7EONQ6ElGUVoo0%2Fimg.jpg)

---

#### 제거

`Package.json` 에 추가 된 해당 라이브러리를 확인하고,<br>
지움 -> 저장 -> `yarn install` 과정으로 패키지를 적용시킨다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuVEK7%2FbtsohpWuWnv%2Fbavz2h8bKQoIx8J1OlkpTk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAa5N9%2FbtsogYSmNNB%2FoKuaVvWWvav6FYfyP9JrLK%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDDQPc%2Fbtsoe2H7fks%2FG5WITZgGkHXALGKkkvGVKK%2Fimg.jpg)

---

#### 실행

해당 라이브러리를 제거 후 다시 앱을 실행하니 정상적으로 구동된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmSShb%2FbtsokDzLXAg%2FYz7NGxYlMItzaEi0POnbmk%2Fimg.jpg)

확실히 라이브러리와 해당 프로젝트가 충돌하는 것 같다.<br>
<br>

---

**다시 설치..**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb4R0JG%2FbtsoiYKQABW%2FlVBht1Iukx76XjqOHFUk5k%2Fimg.jpg)

**실행**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc52k9a%2Fbtsoi0aNT0J%2F9QybdtpEhHpWHOTsprdUr1%2Fimg.jpg)

**검색하여 찾아본 결과**
yarn 패키지매니저를 통해 저장된 캐시를 제거하는 명령어를 실행하여<br>
의존성 패키지를 효율적으로 관리하기 위해 아래 명령어를 실행한다고 한다.

```bash
yarn start --reset-chche
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWtRhb%2FbtsofNXWtuN%2FdpOWEMcB6uJRZZFEyFoVtk%2Fimg.jpg)

하지만,,<br>
<br>
모든 과정을 거쳐도 앱이 실행되지 않는것은 동일했다..

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc52k9a%2Fbtsoi0aNT0J%2F9QybdtpEhHpWHOTsprdUr1%2Fimg.jpg)

---

### 에러 해결

위 과정에서 겪었듯,<br>
설치된 라이브러리와 앱을 실행하는 프로젝트가 충돌하고있는상황같아<br>
해당 라이브러리를 지원하는 깃허브 페이지의 문서를 다시 한번 살펴보았다.<br>
Docs 에 미처 확인하지 못했던 부분이 있었는데,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkH5fe%2FbtsoeH5nYkU%2FBSrSCYriT8KE9bgKwpK0F1%2Fimg.png)

> 1. `React-native` 의 버전이 0.60 이상일 경우<br>
>    라이브러리의 버전을 0.25.0 이상으로 설치하고,<br>
>    그게 아니라면 0.25.0 이하 버전을 설치해라<br>
> 2. `React-native-image-crop-picker` 의 버전이 0.39.0 이상이라면<br>
>    Android CompileSdkVersion 의 버전을<br>
>    33 이상으로 설정해라

`Package.json` 에서 라이브러리가 설치된 버전을 확인 해 보니,<br>
0.40.0 인데 이 경우 Docs 에 있는대로 세팅한다면<br>
android CompileSdkVersion 의 버전을 33 으로 수정해야 할것 같았다.

> Android CompileSdkVersion 은<br> > `android/app/src/debug/AndroidManifest.xml` 경로에서 수정하면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuVEK7%2FbtsohpWuWnv%2Fbavz2h8bKQoIx8J1OlkpTk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FygMl6%2FbtsogZ4D7pI%2FbnafqdafkrixTT9oYMyvY1%2Fimg.png)

---

해당 부분을 수정 후 `yarn run android` 명령으로<br>
앱을 실행시키니 에러가 해결됨을 확인할 수 있었다..

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmSShb%2FbtsokDzLXAg%2FYz7NGxYlMItzaEi0POnbmk%2Fimg.jpg)

---

패스트캠퍼스 디스코드는<br>
질문글을 남기면 답변을 한달 뒤에 달아준다...<br>
<br>
그냥 뭐... 그렇다고.. ㅎㅎ

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdhheUL%2FbtsofrnvmES%2FkqNmtwKL5uGPD95Us2ATH0%2Fimg.png)

---

## Reference 🌊

> <https://github.com/ivpusic/react-native-image-crop-picker><br><https://0biglife.tistory.com/entry/React-Native-Cropping-for-Image-Picker><Br><https://velog.io/@ysh616/react-native-crop-picker-%EC%98%A4%EB%A5%98-%EA%B8%B0%EB%A1%9D>
