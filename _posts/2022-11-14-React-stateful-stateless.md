---
layout: post
title: "[React] 부모, 자식 컴포넌트간의 데이터 이동"
subtitle: #부제목
categories: React
tags: [리액트, 프로젝트, TIL]
---

### 로직
다음과 같이 버튼 `WeatherButton` 을 클릭하게 되면,<br>
해당 지역에 따른 날씨 정보가 `WeatherBox` 에 출력되는 로직을 구현하려 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDEsnK%2FbtrYdiwqSOK%2F9IKjs0HVNNUWCicXxLuBK1%2Fimg.png)

먼저 버튼에 `onClick` 이벤트를 부여하여 함수 내부에 이벤트를 정의해주었고,<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLYCnu%2FbtrYkFp1UBI%2FJKoOzSNBJLjukJfBqHtOIK%2Fimg.png)

변화하는 값을 제어하기 위해 `useState` Hooks 를 생성해주었다. 
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FegBPM7%2FbtrYe0oW7xm%2FDKaWq1tXMhzoJLrXJuf9E0%2Fimg.png)

### 문제 발생
---

문제는<br>
url 을 통해 받은 데이터를 `WeatherBox` 에 전달해 주어야 하는데,<br>
리액트는 단방향 통신이기때문에<br>
데이터를 부모 컴포넌트인 `WeatherBox` 에 보내줄 수가 없었다.

리액트는 부모 컴포넌트에서 자식 컴포넌트로만 데이터를 전달 할 수 있다.<br>

이를 통해 데이터 흐름을 추적하기는 더 쉽지만,<br>
같은 형제끼리 데이터를 주고받기는 힘들다는 단점이 있다.

> 즉, 위에서 아래로만 값을 전달해 줄 수 있는 리액트

### 문제 해결
---

자식 컴포넌트에 존재하는 모든 State 를<br>
부모 컴포넌트인 `App.js` 로 옮겨주어 모든 State 를 관리할 수 있게 해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcU6FxD%2FbtrYqSb7e5D%2FMmWPb1gzRKHFoRclXFkJT0%2Fimg.png)

> 즉, `WeatherButton` 은 어떤 State 도 갖고있지 않다.

그리하여 `WeatherButton` 컴포넌트에 `setCity` 를 Props 해 준다.

> 함수도 Props 가 가능하다 !

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fr6z0k%2FbtrYqz47GqX%2Fvz3JLCq61OWcXpuCczMgh0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcyY0R3%2FbtrYqu3Tp9n%2FFkkv9D1SRWA1kWAP5k0Imk%2Fimg.png)

버튼을 클릭했을 때 값이 변하는지 확인하기위해<bR>
**useEffect** 를 생성해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGdDHY%2FbtrYqSb9eoQ%2FsG2PJrpokxnrscuovWD7Xk%2Fimg.png)

> useEffect 는 컴포넌트의 **update** 를 주시하는 Hooks 이다.<br>
즉, `city` State 를 주시하고 있다가 `city` 가 바뀔 경우 **useEffect** 함수가 호출된다.

![](https://blog.kakaocdn.net/dn/11u1a/btrYr9qRqBg/F1349gnVQ1Y50ck6diSAM1/img.gif)
<br>
<br>
각각의 컴포넌트에서 State 를 생성해 들고 있었던 경우였었는데,<br>
자식 컴포넌트에서 부모 컴포넌트로 데이터를 보내야 하는 상황이었다.

이를 해결하기 위해 모든 State 는 부모 컴포넌트인 `App.js` 로 보내주고,<br>
나머지 컴포넌트에서는 Props 로 받은 데이터를 보여주는 형태로 구현했다.

> **stateful** Component : 모든 State 를 들고있는 컴포넌트<bR>
**stateless** Component : State 없이 Props 와 같이 받은 데이터만 보여주는 컴포넌트