---
layout: post
title: "[React] Zero-Runtime CSS in JS (Feat.최적화)"
subtitle: #부제목
categories: React
tags: [리액트, Zero-Runtime, CS, TIL, 프로젝트]
---

## 개요 🔔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F85ZqL%2FbtsCP272CLV%2FvkjVOaEQiGMgTZ41ZTmr81%2Fimg.webp)

해당 포스팅에서는 프론트엔드 직군에서 빼 놓을 수 없는 `최적화` 에 대한 관계가 있는,<br>
`CSS` 에 대해 정리 해 보고자 한다.

---

## Zero-Runtime 🚫

`Zero-Runtime` 이란,<br>
특정 기술이나 라이브러리를 사용할 때 **런타임 코드가 최소화** 되거나 **필요하지 않은 상태**를 의미한다.

### 런타임 ❓

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAtsYL%2FbtsCN6bT3P3%2FiDLxsRaVY6m4p9Eurn2Uy0%2Fimg.png)

**런타임**이란,<br>
프로그램이 실행되고 있는 동안의 시간을 의미한다.<br>
런타임은 프로그램이 실행되고 종료될 때 까지 계속되며<bR>
컴퓨터의 하드웨어와 상호작용하는 작업을 수행하는 동안의 모든 활동을 포함한다.

`JavaScript` 에서의 런타임은,<br>
**브라우저에서 실행되는 경우** 브라우저의 `JavaScript` 엔진을 의미하며<br>
**서버 사이드에서 실행되는 경우** `Node.js` 와 같은 환경을 가리킨다.

---

제로 런타임은 **`UX`** 에 유의미한 영향을 끼치며,<br>
번들 사이즈를 줄일 수 있고,<br>
만약 런타임 코드가 작거나 없다면 서비스를 보다 효율적으로 제작할 수 있다.<br>
이를 통해 **초기 로딩속도** 를 향상시키고 사용자 경험을 향상시킬 수 있다.

`Zero-Runtime` 이라는 용어는 주로 `CSS-in-JS` 라이브러리 중에서<bR>
**런타임 오버헤드**를 최소화 하거나 없애는 방식을 강조할 때 사용한다.<br>
이를 통해<br>
**번들 사이즈**를 줄이고 **초기 로딩속도**를 개선하여 웹 애플리케이션의 **성능을 향상**시키는데 유의미한 영향을 끼친다.

---

## CSS in JS 💛

먼저, `CSS in JS` 라고 하면 가장 먼저 떠오르는 것은 **`Styled Component`** 일 것이다.<br>
`Styled Component` 는 **`Zero-Runtime` 특징**을 가지기도 하며,<br>
`React` 뿐만 아니라 다른 프레임워크와도 호환되며 현존하는 생태계에 자연스레 동화되며<br>
다양한 확장성 또한 제공하는 점에서 대표적인 라이브러리로 꼽힌다.

`CSS in JS` 와 반대되는 개념으로 `CSS in Module` 이 있는데,<br>
아래 사진을 참고 해 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnbeS2%2FbtsCP45Snz8%2FpOXRcD1yk3fDfIByOSAA3K%2Fimg.png)

만약, 보다 효율적인 유지보수를 위해 모든 `Style` 을 모듈화 하여 생성했다면<br>
위 사진과 같이 셀 수 없이 생성되는 모듈이 많아질 것으로 예상된다.<br>

이를 보완하기 위해 `CSS in JS` 방식을 보다 선호하는 추세이며<br>
마찬가지로 **빌드 타임에 생성된** `JavaScript` 파일을 불러옴으로 인해<br>
여러 모듈을 생성하고 관리하는 과정에서 발생하는 사소한 문제를 해결할 수 있다.

> `CSS in Module` 은 스타일을 부여한 `Class` 가 **중복되게 생성되는 문제**를 막아준다.<bR>
> 이를 통해 **유지보수**에 용이하고,<br>
> 모듈화 된 `CSS` 가 분리된 `React` 컴포넌트와 잘 어우러진다는 장점이 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F18f0x%2FbtsCWLcHZ5g%2FDp6bOoT19LpfYvU7CeNta0%2Fimg.png)

---

`Styled Componet` 는,<br>
각 컴포넌트 내부에 `CSS` 를 적용하고 이를 컴포넌트 화 함으로 인해<br>
별도로 `CSS` 파일을 불러올 필요 없이 `JS` 에서 바로 스타일을 입힐 수 있고,<br>
컴포넌트에 정의한 스타일이 **다른 컴포넌트에 오염**이 되지 않는다는 장점이 있다.

하지만, `Styled Component` 혹은 `Emotion` 과 같은 `CSS in JS` 라이브러리의 경우<br>
**개발자 경험은 크게 상승**시키지만,<br>
빌드 시간에 모든 스타일을 계산하여 생성하는 것이 아니라<br>
런타임에 **동적으로 스타일을 계산하여 추가**하기 때문에<br>
**번들 크기가 증가**하고<br>
**렌더링 속도가 저하**되어 UX 에 유의미한 영향을 끼친다는 단점이 있다.

대부분의 경우 문제가 발생하진 않지만,<br>
스타일이 복잡할 경우 런타임에 성능 이슈가 발생할 수도 있다.

---

## 대안 ❔

### Tailwind 🌫

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcaPzfZ%2FbtsCTz40miD%2F8Ok2RwIqUjDg0XXht5zPTk%2Fimg.png)

테일윈드는 `CSS in JS` 방식은 아니지만,<br>
`HTML` 클래스에 직접 스타일을 적용하는 방식으로<br>
**빌드 타임에 미리 정의되어있는 스타일을 통해** 디자인을 빠르게 구성할 수 있고, 커스터마이징이 가능하기에<br>
별도의 스타일 시트나 스타일 블록이 필요하지 않아<br>
보다 간결해진 문서의 구조를 유지할 수 있다.

> `Tailwind` 또한, 런타임에 CSS 를 생성하지 않는 `Zero Runtime` 의 특성을 가지고 있다.

다만,<br>
일부 개발자는 문서에 작성된 스타일 코드로 인해 **문서를 빠르게 파악하기 어렵다**는 단점이 있고<br>
코드가 가로로 길게 나열된다는 부분을 선호하지 않는 개발자들도 존재한다.

### Panda CSS 🐼

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSNhsa%2FbtsCOGKYgqf%2FdaMPk56lJ0ImDwQnu4cbQK%2Fimg.png)

`Panda CSS` 는 최근 진행한 프로젝트에서 도입한 `CSS` 라이브러리로,<br>
위에 작성된 라이브러리, 프레임워크의 가능한 모든 단점들을 보완하여 나온 라이브러리 이다.<br>

`Panda CSS` 또한 `Tailwind` 와 동일하게<br>
**런타임에 `CSS` 를 생성하지 않는다는 `Zero Runtime` 특성**을 가지고 있지만<br>
미리 정의해둔 스타일을 적용하는 것이 아니기에 **`Atomic` 하지 않다**는 차이가 있다.

또한, `Styled Component` 의 문법을 지원히여 앞선 이슈들을 해소할 수 있었다.

다만,<br>
비교적 다른 라이브러리들에 비해 나온지 얼마 되지 않아 **자료가 별로 없다**는 단점이 있었다.

---

## 마무리 하며... 🤔

해당 포스팅을 작성하며 내가 지금 뭘 작성하고 있는지? 🙄<br>
쓰면서도 모르겠는 부분이 생기기도 했고,<br>
비교적 다른 포스팅들에 비해 많은 시간이 소요된 포스팅 인것같다.

이를 빗대어 표현 해 보자면,<br>
그만큼 UI 뿐만 아니라 UX 부분 또한 상당 시간 고려해야하는 부분이며<br>
이를 해소하기 위해 등장한 `CSS` 들이 다양하지만<br>

그 중에서 프로젝트 진행 시 채택할 수 있는 라이브러리의 폭도 넓어진 것 같다.<br>

- 프로젝트의 규모 및 팀 구성
- 컴포넌트 기반 vs 페이지 기반
- 개발자의 선호도

이 밖에도 여러 가지로 선택할 수 있는 기준은 다양하겠지만,<br>
단순히 기능 구현에만 초점을 두어 공부했던 본인을 다시금 돌아볼 수 있게끔 만들어준 포스팅 이라고 생각한다.

---

## Reference 🌊

> <https://velog.io/@daymoon_/CSS-CSS-in-JS-vs-CSS-in-CSS><br><https://velog.io/@lucas/CSS-IN-JS%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A5%BC-%EC%8A%A4%ED%83%80%EC%9D%BC%EB%A7%81%ED%95%B4%EC%A4%84-%EC%88%98-%EC%9E%88%EB%8A%94%EA%B0%80><br><https://velog.io/@daymoon_/CSS-CSS-in-JS-vs-CSS-in-CSS><br><https://fe-developers.kakaoent.com/2022/220210-css-in-kakaowebtoon/?fbclid=IwAR10q4zhGGIdjdd7l9VyDC9Xn0AU0UkoGeDmTyoWotpt6cxn4T6WHLMPkGg><br><https://velog.io/@kbs2082/React-Styled-Component%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90><br><https://www.javascriptstuff.com/what-are-css-modules/>
