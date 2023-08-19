---
layout: post
title: "[React-Native] JSX 문법 에러 발생시 해결방법 (Feat. return)"
subtitle: #부제목
categories: [React-Native]
tags: [리액트, 리액트 네이티브, Error, TIL]
---

### 에러 확인 💥

다음과 같이<br>
저장된 사용자들의 정보를 가져오는 State 인 `LoadingUsers` 가 있고,
React-Native 에서 제공하는<br>
로딩 컴포넌트인 `ActivityIndicator` 가 담긴 함수가 있다.
<br>
<Br>
만약,<br>
`loadingUsers` 가 있다면 `renderLoading` 함수를 불러오고,<br>
그게 아니라면 `Null` 을 출력하는 형태를 구현하려 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fu87S0%2FbtslClbJ9nH%2Fcvf0IVYIiLPsNAGxOkdqn1%2Fimg.png)

에러를 살펴보면,<br>

> No overload matches this call.<br>
> Overload 1 of 2, '(props: ViewProps | Readonly<ViewProps>): View', gave the following error.<br>
> Type 'void | Element' is not assignable to type 'ReactNode'.<br>
> Type 'void' is not assignable to type 'ReactNode'.<br>
> Overload 2 of 2, '(props: ViewProps, context: any): View', gave the following error.<br>
> Type 'void | Element' is not assignable to type 'ReactNode'.<br>

해당 에러는,<br>
React 컴포넌트에서 반환하는 JSX 내부의 일부 구문의 형태가<br>
올바르게 작성되지 않은 경우 발생하는 에러라고한다.

먼저,<br>
`ActivityIndicator` 가 항상 보이게끔<br>
`loadingUsers` 자리에 `true` 로 변경 해 주어 확인 해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbj6qHB%2FbtslGBLjhny%2FZyP4L1NdOPjANPYYGJXYwk%2Fimg.png)

음...... 😥<br>
<br>
`renderLoading` 함수를 확인 해 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbSiH9F%2FbtslCIdtxLN%2F1AG4HV3kcxA3PWF80ra6rk%2Fimg.png)

음....... 😩

---

### 에러 해결 ✨

에러 메세지와 작성된 코드를 다시 확인 해 보았더니,<br>
컴포넌트가 반환하는 메서드에서 JSX 문법이 틀리게 작성되어있었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdgcgMk%2FbtslDEPpw38%2FGGtjR0YsnK8rPg5n89NCW0%2Fimg.png)

이는,<br>
모든 함수나 렌더링 메서드는 JSX 를 반환해야하는데,<br>
무엇을 반환할지에 대한 부분이 명시가 되어있지 않았던 상태이다.<bR>
<br>
반환하고자 하는 `View` 컴포넌트를 `return` 문을 통해 반환 하여 사용하니<br>
정상적으로 `ActivityIndicator` 가 보여지는 것을 확인할 수 있었다 👍

- True 일 경우 (항상 보여지게)
  ![](https://blog.kakaocdn.net/dn/xzuHE/btslCa2Azj9/pLS1kIF2vNMZ5S30Q0wVVK/img.gif)

- 조건을 통해 배열을 불러오기 전에만 보여지는 경우
  ![](https://blog.kakaocdn.net/dn/GXxwH/btslCILk7sd/bqkRDIMQQFZU33wNxNf3P1/img.gif)

---

#### Reference 🌊

> <https://stackoverflow.com/questions/58449813/react-typescript-error-no-overload-matches-this-call><br><https://dubaiyu.tistory.com/307><br><https://kyounghwan01.github.io/blog/dev-report/error-report/React/>
