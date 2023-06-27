---
layout: post
title: "[React-Native] WebView 를 통해 카카오 지도 API 불러오기 💌"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, 카카오, TIL]
---

## 개요 🔮

React-Native 앱에서 카카오 지도 API 를 불러오려 한다.<br>
하지만,<br>
카카오 개발자문서에는 React-Native 전용 문서를 제공하지 않는다 👽

> Android -> java, Kotlin<br>
> ios -> Swift

그래서 이번 프로젝트에서는<br>
웹 문서를 참고하여 서버를 띄우고,<br>
이를 React-Native-Webview 라이브러리를 통해 불러오려고한다.

---

## React 🌐

```bash
npx create-react-app [프로젝트명]
```

해당 명령어로 react 앱을 생성해 준다.<br>
<br>
공식 문서를 참조하여 순서대로 API 를 사용하기 위한 키를 발급받는다 🔑

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdc4SIT%2Fbtsihc4zAmP%2FH7toikIBo8WVuBPGmBsRr1%2Fimg.png)

> <https://apis.map.kakao.com/web/guide/>

플랫폼에는 생성한 React 앱을 실행한 `http://localhost:3000` 을 추가 해 준다.
<br>
<br>
React 앱에는 지도 정보를 화면에 출력하기 위해<br>
해당 script 를 `public/index.html` 에 넣어 주고,<br>
발급받은 키를 입력해준다.

```html
<script
  type="text/javascript"
  src="//dapi.kakao.com/v2/maps/sdk.js?appkey=발급받은 APP KEY를 넣으시면 됩니다."
></script>
```

지도를 띄우기 위해 `useEffect` 훅으로 해당 함수를 감싸준다.

```javascript
var container = document.getElementById("map"); //지도를 담을 영역의 DOM 레퍼런스
var options = {
  //지도를 생성할 때 필요한 기본 옵션
  center: new kakao.maps.LatLng(33.450701, 126.570667), //지도의 중심좌표.
  level: 3, //지도의 레벨(확대, 축소 정도)
};

var map = new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴
```

그리고 아래 `return` 문에는 지도를 출력하기 위해 `div` 태그를 사용한다.

```javascript
<div id="map" style="width:500px;height:400px;"></div>
```

### 에러

해당 코드를 작성 한 뒤 앱을 실행시켜 보면,<br>
`Uncought ReferenceError : kakao is not defined` 라는 에러 메세지가 출력된다.<br>
<br>
이 에러를 해결하기 위해 `function` 밖에서 window 선언이 필요하다.

```javascript
const { kakao } = window;
```

---

### 전체 코드

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcLxadX%2FbtsiqWfY5e2%2FKp1VVNxbV8RS54VfUaQSk1%2Fimg.png)

### 배포

React 앱을 깃허브에 Push 하고,<br>
레포지토리를 Netlify 에 배포하여 어디서나 사이트에 접근 가능하도록 구현하고자 한다.<br>
<Br>
배포 방법은 **Reference 를 참조**

#### 배포 시 에러 🚫

Netlify 에 React 앱을 배포하고,<br>
생성된 url 로 접근 하였더니<br>
Page Not Found 에러로 지도 api 가 출력이 되지 않는다..😵<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbr9D5V%2Fbtsis78YrpA%2FSLhOJ7CBnKopcKwkOgeJqK%2Fimg.png)

React 앱에서는 정상적으로 출력되는데....😭😭

1. React 앱에 파일 생성
   public/ 에 \_redirects 파일을 생성하고,<br>
   아래 코드를 입력 해 준다.

```
/* /index.html 200
```

> 모든 접근을 허용 (200번대 상태코드) 하겠다는 의미

2. Build Command 설정
   배포 시 레포지토리 선택 후 아래에 있는 Build setting 에<br>
   Build Command 를 입력하는 칸이 있다.
   default 값이 `npm run build` 인데,<br>
   앞에 `CI= ` 를 붙여주어<br>

```
CI= npm run build
```

로 바꾸어 저장 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fzagyn%2FbtsiuNhlDif%2FIdORbGev2VNGveJML8KGok%2Fimg.png)

본인의 경우 2번 째 방법을 통해 에러가 해결 되었다 ✨

---

## React-Native 📲

React-Native 에서는<br>
Webview 라이브러리를 사용하여<br>
React 앱에서 배포한 웹 사이트를 화면에 출력하는 형태를 구현하고자 한다.

### 설치

```bash
npm i react-native-webview
```

해당 설치 명령어를 입력하였을 경우 의존성 문제로 설치가 되지 않는 경우가 있다.<br>
<br>
이 경우 `--peer-legacy-deps` 명령을 통해 강제로 설치할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeCEHKB%2Fbtsit0nMJbf%2F3D4u569WTfc5dokOcyt8fk%2Fimg.png)

### 최종 코드

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcihEyl%2FbtsiuLw2yzX%2FltfVOkDp2sUJ8yJk8mTv6K%2Fimg.png)

해당 url 에는 Netlify 에 배포한 React 앱의 주소를 넣어주며,<br>
이 때, Netlify 의 주소도 카카오 플랫폼에 등록 해 주어야 한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJTjpA%2FbtsiqTKB5gm%2FPva38857YmIrHkGyOH4IQK%2Fimg.png)

### 결과

![](https://blog.kakaocdn.net/dn/SC7tU/btsisRk04Hh/lFH56DoDsj0nMEuagaKRi0/img.gif)

## Reference

> <https://apis.map.kakao.com/web/guide/><br><https://clolee.tistory.com/77><br><https://kimcomdong.tistory.com/entry/Deploy%EC%9A%B0%EC%97%AC%EA%B3%A1%EC%A0%88-%EB%A7%8E%EC%9D%80-React-netlify-%EB%B0%B0%ED%8F%AC-Page-Not-Found-%EC%99%80-Deploy-Failed%EC%9D%98-%ED%96%A5%EC%97%B0><br><https://velog.io/@remon/React-Netlify%EB%A1%9C-%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0><br><https://docs.netlify.com/routing/redirects/#syntax-for-the-redirects-file>
