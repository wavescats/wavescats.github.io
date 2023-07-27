---
layout: post
title: "[React-Native] App 의 종류와 특징 (네이티브, 크로스 플랫폼, 하이브리드) 📱"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, TIL]
---

## 개요

프론트엔드 포지션으로 개발을 입문한지 9 개월차,<br>
단순히 `State` 만 치며 웹 페이지만 구성하다보니,<br>
**웹 앱** 이란걸 알게되었고,<br>
**하이브리드 앱**과 **네이티브 앱** 등등 너무나도 궁금한 것들이 많아졌다 !<br>
이 포스팅에선 다양한 모바일 앱들의 종류와 차이 ?<br>
등을 내가 알기 쉽게 정리하려고 한다
<br><br>
실제로 회사에서 대표님께서 안드로이드에서 접근 할 수 있는<br>
**네이티브 앱**으로 외주를 맡겼는데<br>
**코틀린**으로 개발된 앱을 받았던 적이 있다<br>
업체 측에서는 원하는 요구사항에 맞게 잘 작업 해 줬는데,<br>
대표님이 원했던 요구사항은 **리액트 네이티브**였던것,,<br>

---

### 네이티브 앱

네이티브 앱 이란,<br>
모바일 기기(태블릿, 스마트폰 등) 에서 실행되는 앱으로<br>
주로 `Android` 기기에서는 `Java`, `Kotlin` 으로 개발되며,<br>
`ios` 기기에서는 `Objective-C`, `Swift` 로 개발된다<br><br>

네이티브 앱은 운영체제와 하드웨어에 직접 접근할 수 있어<br>
다른 앱과 다르게 비교적 최적화된 성능을 제공하지만,<br>
특정 플랫폼에 종속되어 있다는 단점이 있다.<br><br>
즉,<br>
`ios`, `Android` 두 플랫폼 모두 지원하는 앱을 만들고 싶다면,<br>
각각의 언어로 개발하고<br>
서로 다른 플랫폼에서 지원하는 앱스토어에 배포하여 사용자에게 제공하는 형태로 구현되고있다.<br><br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxB6H1%2FbtsoEp87qm4%2FKiW53W2VCtLoT6SWKMUkmK%2Fimg.png)

이러한 단점을 극복하기위해<br>
`크로스플랫폼`이 등장했다<br>

---

### 크로스플랫폼

요즘 리액트 네이티브를 공부중인데,<br>
내가 생각하는 리액트 네이티브의 최대 장점은<br>
같은 소스코드로<br>
`Android` 와 `ios` 두 운영체제를 모두 섭렵 가능하다는 점 !!<br>
<br>
즉,<br>
하나의 모바일 앱을 통해 두 운영체제로 개발해야하는 번거로움을<br>
`React-Native` 를 통해 해소할 수 있다 라는 말이다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcTW9KT%2FbtsozTv73LD%2FxhMvzKAVR2157P3PDuXwEk%2Fimg.png)

> 대표적인 크로스플랫폼 앱 <br>
> AirBnB, Facebook, Instagram

---

### 웹 앱

웹 앱,<br>
말 그대로 모바일의 형태를 가진 웹 사이트를 말한다<br>
`웹 앱` 은 모바일 기기(단말기)의 종류에 영향받지 않고,<br>
모든 기기에서 같은 형태의 컨텐츠를 볼 수 있는 웹 사이트를 말한다.<br><br>
대게 반응형 웹 (Responsive Web) 으로 구현 하는 경우를 많이 봤었던것 같다.<br>

> ex) Chrome, Safari 등 마켓플레이스에서 설치하여 앱에 접근하는 형태가 아닌,<br>
> 브라우저에서 접근 가능한 형태

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdg4gvy%2FbtsoDIgFsOM%2FQrTV2aGADpmdjG39Nwu4U0%2Fimg.png)

---

### 하이브리드 앱

하이브리드 앱에 대한 정의를 잘 내리지 못하고 있던 찰나,<br>
기업 측의 멘토분이셨던 홍경태 대표님께서 열정적인 설명을 통해 이해시켜주셨다<br><br>

내가 이해한 하이브리드 앱을 간단하게 설명하자면,<br>
모바일 서비스로 구현한 앱에서 지원하지 않는 기능등을<br>
`Webview` 등의 기술을 통해 모바일 기기에서 구현한 것처럼 하는 행위? 기능?<br>
<br>
사실 하이브리드 앱의 원리는 간단한 것이었다<br>
네이티브 앱 혹은 크로스플랫폼 앱으로 구현한 서비스를 만들어<br>
화면 안에 컨텐츠를 직접 그리지 않고 `Webview` 라는 요소를 통해<bR>
사용자에게 보여주는 기능을 말하는것이다<br>
`Webview` 는 지정한 URL 로 접근하여 웹 앱 형태로 구현된 웹 사이트를<br>
모바일 기기 화면에 출력하는 것이다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbpWYBE%2FbtsozTv8v1u%2F0RZ616eGR92ccqxgvkkzck%2Fimg.png)

---

## Reference 🌊

> <https://hongong.hanbit.co.kr/%EB%AA%A8%EB%B0%94%EC%9D%BC-%EC%95%B1-%EC%A2%85%EB%A5%98%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EC%95%B1-%ED%81%AC%EB%A1%9C%EC%8A%A4-%ED%94%8C%EB%9E%AB%ED%8F%BC-%EC%9B%B9-%EC%95%B1-%ED%95%98/><br>
