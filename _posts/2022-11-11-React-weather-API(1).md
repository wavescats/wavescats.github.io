---
layout: post
title: "[React] 날씨 기반 API 를 활용한 프로젝트 - 1"
subtitle: #부제목
categories: Project
tags: [프로젝트]
---

## 프로젝트 생성
---

```
npx create-react-app [프로젝트명]
```

`src/app.js` 의 불필요한 부분 제거 후 <br>
`$npm start` 명령어로 앱 실행

## 현재위치 정보 가져오기
---

앱이 ***실행되자마자*** 현재위치에 대한 정보가 필요하므로<br>
`useEffect` Hooks 를 사용

> useEffect 에는 2개의 매개변수가 필요하고,<br>
함수 내부에 원하는 내용을 작성 해 주면 된다.

```
useEffect(() => {함수},[배열])
```

> 현재위치정보 가져오기<br><https://www.w3schools.com/html/html5_geolocation.asp>

위 Reference 를 참조하여 현재위치에 대한 정보를 가져와 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcaLHbn%2FbtrXOkgeWpY%2FmK7czxOPoYR7TrIKeFpRhk%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcSCbwB%2FbtrXOWMGe2V%2FWtKqwAVtvZxaKiF0pe7eKk%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKCgBn%2FbtrXOvV8sQT%2F6BkUJJzVbCCSq4XE87zua0%2Fimg.png)


> latitude (위도), longitude (경도)

## 현재위치 기반 날씨정보 가져오기
**Current Weather Data** -> **API doc** -> **API call**
> <https://openweathermap.org/current#geocoding>

---


API 를 불러오기 전 함수를 만들어 자리를 만들어주자.

> getWeatherByCurrentLocation 함수 생성

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWiQaz%2FbtrXK8HCSJR%2F2Y0hHt49wE6RNfPcFdRXV1%2Fimg.png)

API url 을 살펴보면 필요한 값들이 적혀있다.<br>
**lat** 의 정보, **lon** 의 정보, **API key**

하지만,<br>
이미 **lat** 과 **lon** 의 값을 구하는 코드를 만들었으니,<br>
그 값을 호출만 해 주면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbX2TO4%2FbtrXPUnlwUv%2FePn8kysksXEhqQ8dzZhmw0%2Fimg.png)

> getCurrentLocation 함수 내부에서 **lat** 과 **lon** 의 값을 가져올때,<br>
getWeatherByCurrentLocation 함수를 호출하고 그 값으로는 **lat** 과 **lon** 을 받는다.

매개변수로 **lat** 과 **lon** 을 주어 <br>
getCurrentLocation 함수가 실행될 때 던져준 값을 캐치한다.<br>

> $ 의 의미는 Dynamic Value 로 변화하는 값을 구할 때 사용한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNpsTQ%2FbtrXPw72LAO%2FPDAk1SZB9rX8fdy2mKC0G0%2Fimg.png)


---
### API 호출 🔮
현재 위치정보가 담긴 url 을 기반으로 API 를 호출해보자 💥

먼저,<br>
url 을 호출해 데이터를 가져올때까지 await 를 통해 기다려달라는 값을 response 에 담아주었다.

> await 을 사용함으로써 비동기적처리를 알수 있다. async - await

> fetch 란, <br>
JavaScript 에서 서버로 네트워크 요청을 보내고 응답을 받을 수 있도록 해주는 매서드이다.

마찬가지로 url 에서 추출한 json 파일을 담아줄 필요가 있다.
response 에서 추출한 json 을 가져올때까지 기다려달라는 값을 data 에 담아주었다.

> API 는 대부분 JSON 파일의 형태를 띄고있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2AdSO%2FbtrXK88KSSK%2FVNe6Fu1Nf4QI4taaFfkplK%2Fimg.png)


---
### 데이터 확인 💥
이제,<br>
가져온 데이터를 확인해 볼 차례이다 🙌🙌<br>
console.log 를 찍어 값을 확인 해 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFaGi1%2FbtrXLr1A89j%2FzUq1tCZ6ikeEUv0reKXbOk%2Fimg.png)


헉스,, 내 신상정보가 담긴 데이터가 보여지고 있다 😱😱 <br>
코딩이란,, API 란,, 정말 심오하며 신기한것,,😎<br>

<br>

다음 포스팅에선,<br>
불러온 데이터를 UI 를 통해 화면에 뿌려주는 작업을 해 보도록 하자 😆