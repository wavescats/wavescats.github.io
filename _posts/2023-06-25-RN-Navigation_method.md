---
layout: post
title: "[React-Native] Navigation 을 통한 화면 이동 시 뒤로가기 기능 구현하기"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, TIL]
---

### 개요

네비게이션을 활용한 페이지 구현을 한다면,<br>
뒤로가기 기능은 가령 필수적인 요소로 사용되어야 한다고 본다.<br><br>
이번 포스팅에서는<br>
모바일 앱에서 구현한 `Stack Navigator` 에<br>
이전 화면을 보여주기 위한 메소드를 정리하고자 한다.

---

### React-Navigation ?

React-Native 에서 사용하는 화면 이동을 위한 라이브러리 이다.<br>
`Stack`, `BottomTab`, `Drawer` 등 앱 개발시 많이 사용되는<br>
화면 이동에 대해 각 플랫폼 환경에 맞도록 쉽게 변환 해 주도록 설정되어있다.

> <https://reactnavigation.org/>

React-Navigation 의 구성 요소로는,<br>
Navigator 와 Screen 의 조합으로 이루어져 있으며,<br>
`Navigator` 는 Navigation 이 어떤 구조로 되어있는지 나타내는 컴포넌트 이다.<br>
`Screen` 은 말 그대로 화면을 그리는 컴포넌트 이다.

### goback

> React-Native Navigator 관련 라이브러리 설치 생략

먼저,<br>
Screen 컴포넌트로 구현한 화면을<br>
로그인 페이지인 Signin 컴포넌트에 Props 를 통해 넘겨주어 구현한 페이지 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWUDob%2Fbtsl0lXPD1p%2FHkvuj5MBHSSBZwNJJaVJdK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcYICk0%2Fbtsl2nz5LHy%2FxCf1NfB8FGQztPDVP66tFk%2Fimg.png)

여기 로그인과 회원가입 기능을 담고있는 두 컴포넌트가 있다.<br>
회원가입 페이지에서<br>
하단의 **'이미 계정이 있으신가요?'** 란을 누르게 되면<br>
로그인 페이지로 이동하게 되며,<br>
Back 버튼이 생성된다.

![](https://blog.kakaocdn.net/dn/bECwtr/btsl6MToOMz/ckk3zppDqhp8kKGgCENOSk/img.gif)

이를 구현한 코드로는<br>
`Naivigation` 의 메소드로<bR>
`goBack` 과 `canGoBack` 를 사용하였다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHlcBO%2Fbtsl1ANtEP6%2FswLaNvWk4oy3C4P6hsSn7k%2Fimg.png)

생성한 `Back` 이라는 Text 에<bR>
`onPress` 기능을 부여하고<br>
`onPressBackButton` 함수를 생성하여 넣어주었다.<br>
함수에는 goBack 함수만이 들어가있으며<br>
참조 또한 동일한 값을 가진다.<br><Br>

![](https://blog.kakaocdn.net/dn/bIiZbc/btsl9u52YbM/HFyO8FP4IzEuuF57zYu4A0/img.gif)

단,
로그인 페이지에서 생성된 Back 버튼을 누르게 되면<br>
이전의 회원가입 페이지로 이동하게 되는데<br>
첫 페이지인 회원가입 페이지에서<br>
Back 버튼이 활성화가 되어있고,<br>
이를 Press 하게된다면<br>
더 이상 뒤로 갈 화면이 없기 때문에 **에러**가 발생할 것이다.
<br><br>
이를 방지하기 위해 `canGoBack` 함수를 사용하였다.

---

### canGoBack

위에서 발생할 에러를 대비하여<br>
`canGoBack` 함수가 제공되고 있다.<br><br>
해당 함수의 기능은<br>
뒤로가기 버튼을 눌렀을 경우,<br>
이전화면으로 돌아갈 수 있는지의 유무를 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHlcBO%2Fbtsl1ANtEP6%2FswLaNvWk4oy3C4P6hsSn7k%2Fimg.png)

`goBack` 과 `canGoBack` 은<br>
`useNavigation` 에서 제공하는 메소드로 정의하고,<br>
구현한 로그인 페이지와 회원가입 페이지에서 사용할 것이다.<br>
<br>
`canGoBack` 함수는<br>
Navigation 히스토리에 이전 페이지가 있는지 확인하고,<br>
뒤로 이동할 페이지의 여부를 나타내는 부울 값을 반환한다.<br><br>
첫 페이지인 회원가입 화면에서는<br>
더 이상 뒤로 갈 화면이 없을 뿐더러<br>
이동한다면 에러가 발생할 것 이므로 Back 버튼을 없애 줄 것이며,<br>
한 페이지 들어간 로그인 화면에서는<br>
Back 버튼을 활성화 시켜<bR>
이전 화면인 회원가입 페이지로 이동하게끔 조건을 부여했다.

![](https://blog.kakaocdn.net/dn/bIiZbc/btsl9u52YbM/HFyO8FP4IzEuuF57zYu4A0/img.gif)

---

### pop & popToTop

<br>
- pop

`pop` 함수는 `goback` 함수와 동일한 기능을 갖고 있다.<br><br>
단,<br>
`goBack` 함수와 다른 점으로는<br>
히스토리로 남아있는 스택의 기록을 제거 한다는 차이가 있다.

> pop 스택 맨 위 화면을 제거하고 그 아래 화면으로 이동.

<br>
- popToTop

쌓여있는 스택의 첫 번째 화면으로 이동하는 기능을 갖고 있다.<br>
pop 함수와 마찬가지로<bR>
첫 번째 화면을 제외한 모든 화면을 스택에서 제거하고<br>
초기 상태로 돌아가는 기능을 담고있는 함수이다.
