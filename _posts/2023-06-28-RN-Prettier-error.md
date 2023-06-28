---
layout: post
title: "[React-Native] Navigation Hook 사용 시 Prettier Extentions 주의사항 및 해결방법 💘"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, Error, TIL]
---

현재 구현한 모바일 화면이다 ✨

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQWdof%2FbtslC1Zucn2%2F0zyr6BfjtOC81fJPr5kFjk%2Fimg.png)

하단의 다른 유저 정보가 담긴 Area 를 클릭 시,<br>
추가로 생성 해 놓은 `Chat Screen` 으로 이동하게끔<br>
`onPress` 함수를 사용하여 `useNavigation` 훅으로 기능을 구현할 계획이다
<br>
<Br>

기본 구조를 갖춘 `Chat Screen` 이다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnNypj%2FbtslJHlm6ck%2FLpwtpHKFUCQbWeqHQKGV41%2Fimg.png)

이 컴포넌트를 로그인이 된 경우에만 보여주어야 하기 때문에,<Br>
조건문이 들어있는 Stact Navigate 내부에 컴포넌트를 추가 해 준다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpvBn8%2FbtslKjYATYY%2FQk7y6PRk1yTG2WJZ5KRkpK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbETWEy%2FbtslCI0d2By%2FmfUO7YeL8BopN6vZjHPJK0%2Fimg.png)

그리고,<br>
버튼을 누른 경우 해당 컴포넌트를 보여주어야 하므로,<br>
`Home Screen` 에 비워져 있던<br>
`onPress` 함수에 `navigate` 함수를 채워주었다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcaTlFA%2FbtslLhlFIp2%2Fif8YOM0Kkk18NxDJb3ge21%2Fimg.png)

해당 기능을 사용하기 위해<br>
`useNavigation` 훅을 선언 해 주어야 한다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fqrlhs%2FbtslCHUv3aM%2FJGMkcRUa3n5sdogJw1WUv0%2Fimg.png)

---

### 에러 확인 💥

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcxfTMk%2FbtslJ9orNFS%2FswzmoKDFDesHp7o7tIUXl1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbv5MOR%2FbtslJGfJLRv%2FNhKUTvVOEFJ0F0rYykok9k%2Fimg.png)

음...<br>

해당 에러 메세지를 살펴보면,

> Error: A navigator can only contain 'Screen', 'Group' or<br>
> 'React.Fragment' as its direct children (found ';').<br>
> To render this component in the navigator,<Br>
> pass it in the 'component' prop to 'Screen'.

이 에러는,<br>
Navigator 컴포넌트에 올바른 자식 컴포넌트가 사용되지 않아<br>
발생하는 에러라고 한다.<br>
Children 으로는<br>
`Screen`, `Group`, `React.Fragment` 만이 사용될 수있다고 한다 🌞

---

### 에러 해결 🌅

에러 메세지를 다시 살펴보면,

> 'React.Fragment' as its direct children (found ';').

Fragment 내부에 세미콜론이 존재하여 발생하는 에러인듯하다 🚀

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbETWEy%2FbtslCI0d2By%2FmfUO7YeL8BopN6vZjHPJK0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnBjni%2FbtslDEDet5a%2FNZqfy0kObg4UpS30GLKfgK%2Fimg.png)

![](https://blog.kakaocdn.net/dn/EmFQ0/btslC1kWkjy/B5tm3SSqj5NK9u94YfrGf0/img.gif)

해당 부분에 대해 에러가 발생한 이유로는<Br>
코드 작성 시 세미콜론을 입력 해 주지 않았지만,<br>
VSCode 확장 기능으로 설치했던<br>
Prettier 때문에 발생한 에러였다
<br>
<br>
Prettier 는 Code Formatter 기능을 담고 있는 Extention 으로<br>
자동 줄 바꿈, 세미콜론 등의 자동 포맷 기능을 갖고 있다<br>
<br>
Extention 의 기능을 통해<br>
보다 간편히 코드를 작성 할 수 있었지만,<br>
해당 기능을 통해 에러가 발생할 수도 있음을 알고나니<br>
`양날의 검` 인것같아 코드를 작성 할 시 유의해야 할 부분인것같다

---

#### Reference 🌊

> <https://stackoverflow.com/questions/62494561/error-a-navigator-can-only-contain-screen-components-as-its-direct-children><br><https://github.com/react-navigation/react-navigation/issues/9578><br><https://www.appsloveworld.com/reactjs/100/34/a-navigator-can-only-contain-screen-group-or-react-fragment-as-its-direct><br><https://reactnavigation.org/docs/screen/><br><https://source--react-navigation-docs.netlify.app/docs/stack-navigator/>
