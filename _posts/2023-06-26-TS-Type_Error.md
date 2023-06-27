---
layout: post
title: "[Typescript] Type 을 지정하지 않아 발생하는 에러 해결방법"
subtitle: #부제목
categories: [TypeScript]
tags: [리액트 네이티브, 타입스크립트, Error, TIL]
---

### 에러 확인

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdQDXi8%2FbtslwpfhLBh%2F5cTKOmvwknGNjEbKu2NATK%2Fimg.jpg)

Stack Navigation 을 사용하여<br>
구현한 컴포넌트를 불러오는 과정에서 발생한 에러이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw2Uu9%2FbtslCI5A5uQ%2FgOeEcyxMtxQFzOOkaZk3pk%2Fimg.jpg)

불러올 해당 컴포넌트의 초기 세팅을 마치고,<br>
`export default` 를 통해<br>
다른 곳에서도 해당 컴포넌트를 import 가능한 상태이다.

에러 메세지를 살펴보자.

> Type '"Signin"' is not assignable to type '"Signup"'

해당 메세지를 직역 해 보면,<br>
Signin Type 을 Signup 타입에 할당할 수 없다고 한다.

---

### 에러 해결

Type 이 정의되어 있는 파일에서 에러를 살펴보자

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbe1TXU%2FbtslAmJc9Ae%2FEbESIdgikVnCK1TK3TfpUK%2Fimg.jpg)

Stack 에서 사용할 Type 으로 Signup 은 undefined 로 정의되어있었지만,<br>
Signin 의 Type 은 정의되어 있지 않아 추가로 정의 해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbudHF8%2FbtslB2ctH8W%2F9xyKCAvKaHlkyFSAGik6Gk%2Fimg.jpg)

---

#### 다른 방법

타입이 별도로 정의되어 있는 파일을 생성하여 관리하는것이<br>
유지보수 및 가독성 측면에서 우수한 성능을 보이지만,<br>
<br>
조금 더 직관적으로 알아볼 수 있도록<br>
**인라인 형태로 Type 을 지정할 수도 있다.**

```javascript
<Stack.Screen name="Signup" component={SignupScreen as undefined} />
<Stack.Screen name="Signin" component={SigninScreen as undefined} />
```

---

### Reference

> <https://okky.kr/questions/1258371><br><https://leehyungi0622.github.io/2021/04/23/202104/210423-Typescript_TIL-2/>
