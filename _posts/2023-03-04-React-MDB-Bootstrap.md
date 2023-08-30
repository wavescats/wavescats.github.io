---
layout: post
title: "[React] MDB Bootstrap 을 활용한 앱 스타일링 🎨"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL]
---

### 개요 👋

프로젝트를 진행하다보면 **사용자를 위한 UI** 는 필수적으로 고려해야 하는 사항이다.<br>
웹 서비스를 제작 해 보았다면 **Bootstrap** 을 들어보았을것이다.

### Bootstrap 🌟

**Bootstrap** 은 웹 서비스를 보다 쉽게 제작 할 수 있게 도와주는 프레임워크로<br>
**CSS** 와 **JS** 로 제작되어 있다.
<br>
하지만 대게 HTML 파일로 제작되어 있어
<br>

React 앱에 가져오게 되면 무수히 많은 `className` 지옥을 경험할 수 있다.
<br>
이를 보완하기 위해 React-Bootstrap 을 사용한다.

### React-Bootstrap 💥

**React-Bootstrap** 은,<br>
기존의 Bootstrap 의 `className` 을 제거하고<br>
독자적인 Element 를 가진 형태로 구성되어 있어 코드가 간단해진다는 장점이 있다.

### MDB-Bootstrap 🔥

이번 프로젝트에서 UI 를 디자인 하기 위해 채택한 라이브러리이다.<br>
기존에 사용했던 **React-Bootstrap** 보다 선택할 수 있는 UI 가 다양하다고 느꼈다.

#### 설치 💜

```
npm i mdb-react-ui-kit
```

> <https://mdbootstrap.com/docs/react/getting-started/installation/>

#### 적용 💛

index.html 파일 head 영역에 css 파일을 추가 해 준다.

```
<link
    href="https://cdnjs.cloudflare.com/ajax/libs/mdb-ui-kit/6.2.0/mdb.min.css"
    rel="stylesheet"
/>
```

Static Gallery 컴포넌트를 불러와 사용할 것이다.

> <https://mdbootstrap.com/docs/react/extended/gallery/>

`App.js` 에서 `Jsondata` 를 불러와 해당 컴포넌트에 `Props` 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbeYnzn%2Fbtr1UuMU8HX%2F2LgkcUfjxoAxZi4KM6KJjk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbxLhh%2Fbtr1XPJl5Kh%2FMFfysLPXL9yK7EtHX3byz0%2Fimg.png)

해당 컴포넌트에서 받아올 데이터를 넣어준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRV5mu%2Fbtr1TSUQ1rI%2FdibMWUPvVaztKKXEljvYJ1%2Fimg.png)

> 테일윈드 스타일로 css 속성이 적용되어 있다.

#### 결과 💚

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJKgB9%2Fbtr1KvFObYP%2F3q8KJnPMh2SahOweptbDi1%2Fimg.png)

### Reference

<https://dsc-sookmyung.tistory.com/189><br>
<https://itfresh.tistory.com/6>
