---
layout: post
title: "[React] Cannot read properties of undefined (reading 'xxx')"
subtitle: #부제목
categories: Error
tags: [리액트, 프로젝트]
---

### 에러 확인
---

프로젝트 진행 시 아마 가장 많이 마주쳤던 에러 메세지 였던 것 같다.
```
Uncaught TypeError: Cannot read properties of undefined (reading 'temp')
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUMQqL%2FbtrYszQExF3%2FMgYdSMES4rj2a7cIzJKKP0%2Fimg.png)

에러를 살펴보면,
> {cod: '400', message: 'Noting to geocode'}

이 에러는 **useEffect** 관련 에러인데,<br>
**useEffect** 는 처음 렌더링 시 특정 작업을 실행할 수 있도록 하는 Hooks 이다.<br>

코드의 작동 순서는 위에서 아래로 내려가기에<br>
먼저 `getCurrentLocation` 함수가 실행이 된다.<br>
차순으로 `getWeatherByCity` 함수가 실행 되는데,<br>
이 **Effect** 는 `city` 를 기준으로 Weather 를 가져오는데,<br>
`city` 를 담고있는 State 의 초기 값은 아무것도 없는 "  " 빈 값이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYqGq8%2FbtrYpmFcrhD%2FZxJTNlDLFWCVKh95eEleYk%2Fimg.png)

때문에 `getCurrentLocation` 함수는 호출이 되었지만,<br>
`getWeatherByCity` 함수를 호출하는 과정에서<bR>
url 에 빈 값이 담긴 `city` 를 호출 했기에 에러가 발생한 것이다.<br>


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyeiXI%2FbtrYmvPYlB6%2FYEHw0zKCP5oOsHHVyoDfgK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAKu9o%2FbtrYqTh6xWw%2FKuXfGZzayxW2o7Q6sH6fOK%2Fimg.png)

> 이 부분을 주석 처리 해 주면 정상적으로 렌더링이 된다.

### 에러 해결
---

그런데,<br>
`getWeatherByCity` 함수를 주석 처리 한다면 State 로 받는 각 지역별 `city` 의 값은 어떻게 가져올까 ??

간단하다.<br>
두개로 분리된 **useEffect** 를 조건을 걸어 하나로 합쳐주면 된다.

단,<br>
상황에 맞게 `getCurrentLocation` 과 `getWeatherByCity` 가 호출이 되게끔 말이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcaqeMy%2FbtrYrTu4IEO%2FZU46VfJzWnVVEUa9XWzNX0%2Fimg.png)


### Reference
> <https://stackoverflow.com/questions/46877169/error-400-nothing-to-geocode-with-openweathermap-api>