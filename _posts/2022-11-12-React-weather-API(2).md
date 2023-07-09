---
layout: post
title: "[Project] 날씨 기반 API 를 활용한 프로젝트 - 2 (OpenWeather API) 🌞"
subtitle: #부제목
categories: Project
tags: [리액트, 프로젝트]
---

## UI 제작

---

**_Reference_**
![](https://files.cdn.thinkific.com/file_uploads/523761/images/0ac/c3c/3d3/1648395289245.jpg)
**<https://bitna-weather.netlify.app>**

먼저,<br>
각각의 Element 들을 제작하기보다 Bootstrap 을 활용하여 UI 를 제작하려 한다.

```bash
npm install react-bootstrap bootstrap
```

### Bootstrap 과 React-Bootstrap 의 차이

**_Bootstrap은 상태값과 클래스를 사용하고,<br>
React-Bootstrap은 function과 hooks를 사용한다._**

> React-bootstrap 은 리액트에 최적화 되어있으며 컴포넌트에 초점을 맞춰 제작되어<br>
> 가독성이 좋고 다양한 애니메이션 구현시 더 유용하다.

Reference 를 보면,<br>
body 태그 안에 두개의 컴포넌트가 구현되어있음을 예상할 수 있다.

---

## React-Bootstrap 의 사용

npm 을 통해 라이브러리를 설치 했다면,<br>
다음과 같이 원하는 컴포넌트에 import 하여 적용시킬 수 있다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcZXrSY%2FbtrY8jufnyH%2Fbr7k8Qnz0cq85j4bJqnKwk%2Fimg.png)

단, React-Bootstrap 에서 제공하는 가상의 CSS 를 먼저 import 해 주어야 한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVpj1x%2FbtrZagql731%2FIxjUjYFU2V6QlcHdBssKD1%2Fimg.png)

---

## Styled Component

Styled Component 를 활용해<br>
별도의 css 파일을 생성하지 않고 각각의 컴포넌트에 스타일을 삽입하려한다.

```bash
npm install --save styled-components
```

### Styled Component 사용 이유?

- css 파일을 밖에 두지 않고 컴포넌트 내부에 넣기 때문에<br>
  css가 전역으로 중첩되지 않도록 만들어준다 ✨

- 생성한 class 를 까먹고 중복해서 스타일을 부여하는 작업이 줄어든다 🔥

- 컴포넌트에 부여한 스타일이 다른 JS 파일에 적용되지 않는다 🌊

프로젝트를 작업하다 보면 원하지 않는 부분에 Style 이 적용되는 경우가 있다.<br>
`export` 를 하지 않는 한,<br>
스타일을 부여한 컴포넌트에서만 **모듈화** 되어 다른 컴포넌트에 영향을 끼지치 않는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FboohX4%2FbtrY1l0kgJu%2FACOHaQzKCkfrTbd5QhG7J1%2Fimg.png)

> 이 부분이 가장 마음에 들어 Styled-Component 를 사용한다 !

---

## Flex-box

컴포넌트를 생성하면 왼쪽 상단에 아이템들이 보여지는걸 확인 할 수 있다.
이를 가운데로 옮기기 위해 스타일을 부여할 것이다.<br>

`display: flex`<br>
`justify-content`<br>
`align-items: center`<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fci1bVG%2FbtrZbRi5IDU%2FguT4idlQaA3Ue0M798XHs1%2Fimg.png)

### 에러 💥

음.. 아이템들이 가로 정렬은 되었는데, 세로 정렬이 되지 않는다..😥<br>
`align-items` 속성이 적용이 되지 않은걸까..?😕

#### 에러 해결 🎶

개발자도구를 열어 확인 해 본 결과,<br>
컴포넌트를 담은 `div` 태그의 높이가 **'아이템의 높이 만큼 만'** 으로 적용되어 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd4CsA3%2FbtrZa2rUYil%2FhEtQE9KefaQyp9foKXYuyk%2Fimg.png)

이 `div` 의 높이를 `height: 100vh` 로 늘려주어 화면 전체의 높이를 갖도록 Style 을 적용해주자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGhwSd%2FbtrY7L5e8pD%2FvntKGcIIhhwszqGeOsY0Nk%2Fimg.png)

---

가운데 정렬은 모두 마쳤지만,<br>
`div` 태그 안에 담긴 각각의 컴포넌트들이 한 선상에 위치하고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGhwSd%2FbtrY7L5e8pD%2FvntKGcIIhhwszqGeOsY0Nk%2Fimg.png)

이는 앞서 부여한 Style 인 `display: flex` 때문이다.<br>

> flex-box 는 아이템들을 flexible 하게 컨트롤 하기는 쉽지만,<br>
> 모든 아이템들은 가로 정렬의 속성을 **Default** 하게 갖는다.

이를 해결하기 위해,<br>
`flex-direction: column` 을 추가 해 주자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcrmAYY%2FbtrY8jufF2N%2FALT1Cf2P56iUCyfXePr1P0%2Fimg.png)
