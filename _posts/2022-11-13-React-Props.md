---
layout: post
title: "[React] Props 를 활용한 Weather 데이터 호출 시 에러"
subtitle: #부제목
categories: React
tags: [리액트, Error]
---

### 에러 확인
---

변화하는 값을 관리하기 위해 useState Hooks 를 사용할때 발생한 에러이다.
<br>
먼저, State 값에 빈 값을 정의하기 위해 **null** 값을 부여하고<br>
> 초기 값은 모르기 때문에 null 지정

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbV7J16%2FbtrYchiix92%2F85KyN3BErlhU76U41X1zRk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdC6GPK%2FbtrYao2Xgdr%2FrHwKeQW1ilQNdy8nu0cAxK%2Fimg.png)

Weather 데이터를 생성한 컴포넌트인 WeatherBox 에서 보여주어야 하기 때문에<br>
Props 를 사용해 weather 데이터를 WeatherBox 에 보내준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTVuDQ%2FbtrX3rNFw2n%2FQb6Uo9HtlVmozwHzSo8K6K%2Fimg.png)

여기서, Props 라는 object 안에서 weather 데이터를 가져오기 위해<br>
ES6 문법인 Destructuring 을 사용하여 넘겨준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFqopT%2FbtrX6ovCbet%2FHDCceWOnWS9UuGJhyvWdc1%2Fimg.png)

데이터를 확인 해 볼까?
<br>
가져온 weather 데이터에서 필요한 정보는,<br>
name 과 온도를 나타내는 temp 일 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fvjn42%2FbtrX3tEOrfi%2FbYN3fDA5XG5Kv7XivHsRhk%2Fimg.png)

name 의 값을 가져온다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOhHzz%2FbtrYdjmLcwv%2FPKI9xxo7c5NGqh19ungJ4k%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdqxYOT%2FbtrX6hwDdKx%2Fhxdtno3l5h3xIMeQJkUREk%2Fimg.png)
**?!** <br>

에러와 함께 화면에 보여지는 UI 들이 모두 사라졌다.
<br>
<br>
에러를 살펴보면,<br>
**'weather 의 값이 null 이라 name properties 를 불러올 수 없다'** 고 한다.

### 에러 해결
---

이유는 간단했다.<bR>
useEffect 의 영향을 받아 에러가 발생한 것이었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fca3JSZ%2FbtrX33sn9Wd%2Fvst0wKVEvq2tyFa6OdumM0%2Fimg.png)

useEffect Hooks 는 맨 처음 UI 가 렌더링 된 후 실행이 되는데,<br>
그 때 당시의 weather 의 값은 null (초기값) 상태이므로<br>
WeatherBox 에서 weather.name 을 보여주고 싶지만 null 이기때문에 에러가 발생한 것이다.
<br>
<br>
이를 `삼항 연산식` 혹은 `조건부 렌더링` 문법을 통해 수정해 주면 된다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1dH8n%2FbtrX6pae4GL%2FkjHIPeWGvQV34yT62cjHD0%2Fimg.png)

> weather 가 참일경우(=값이 있을경우) .name 을 보여줘 !

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFJ8qS%2FbtrX2XMPFhB%2FtQvvSfQNuJuHlb5mavwrY0%2Fimg.png)