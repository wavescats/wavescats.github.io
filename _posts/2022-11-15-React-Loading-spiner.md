---
layout: post
title: "[React] UI 에 Loading-Spinners 효과 주기"
subtitle: #부제목
categories: Project
tags: [리액트, 프로젝트]
---

지역별 현재 날씨 정보를 불러오는 과정에서 사용하는 효과이다.<br>

데이터를 불러오는 과정에서 API 가 호출되는 사이에 약간의 딜레이가 존재한다.<br>
이 UI 적인 부분을 Loading-Spinner 를 추가하여<br>
사용자에게 약간의 인내하는 시간을 기대할 수 있을것 같다.

### Reference
> <https://www.npmjs.com/package/react-spinners>

```
npm install --save react-spinners
```

설치가 완료 되면,<Br>
아래 Usage - Example 부분을 참고하여 내 코드에 넣어주면 된다.

```
import ClipLoader from "react-spinners/ClipLoader";
```

그리고,<br>
`ClipLoader` 컴포넌트를 가져 올 것이다.
```
    <ClipLoader 
        color = { color } 
        loading = { loading } 
        cssOverride = { override } 
        size = { 150 } 
        aria-label = "Loading Spinner" 
        data-testid = "loader" 
    />
```

각각의 정보에 대한 설명도 공식문서를 참조하면 알 수 있다.

먼저, loading Props 는 Boolean Type 임을 알 수 있고,<br>
만약 `false` 라면 아무것도 보이지 않는다.

이는 변화하는 값 이기 때문에 **useState** Hooks 를 생성해 줄 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9OO2p%2FbtrYtRZCxcR%2FdSUdz6WVAPMQH9sviswXsK%2Fimg.png)

현재는 **State** 값을 true 로 주었기 때문에 화면에서 스피너가 계속 도는 것을 확인할 수 있다.

![](https://blog.kakaocdn.net/dn/dsP3t0/btrYyTWYIvm/iGchbHqBE3Xqb2tfhIZeGk/img.gif)


### 코드의 사용
---

이제 이 스피너를<br>
지역을 바꿨을 때 데이터를 불러오는 과정에서 사용하면 된다.

`getWeatherByCurrentLocation` 과 `getWeatherByCity` 에<br>
fetch 가 되기 전과 데이터를 불러온 후에 setLoading 을 넣어주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fct5tZ7%2FbtrYzp8Z8Wx%2FYvEoGnORauVSGHNxPLU05k%2Fimg.png)

![](https://blog.kakaocdn.net/dn/bE2Ozd/btrYAl5V5M5/YHSk0BLR0xOGeCEkgDUmu0/img.gif)

### 문제점 
---

스피너의 동작은 잘 확인 했다.<br>
다만, UI 적인 부분에서 스피너가 나온 순간 `ContentBox` 가 아래로 움직이는 모습이 보인다.

#### 해결
---

이 부분을 스피너가 등장하는 순간에는 `ContentBox` 가 보이지 않게끔 설정하려한다.

삼항연산자를 활용해 <br>
`loading` 이 **true** 일 경우 `ClipLoader` 가 보여지고,<br>
**false** 일 경우 `ContentBox` 가 보여지게

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6iPOV%2FbtrYzpuEcNX%2FJB2Xd9twroaq85sHA9iKkk%2Fimg.png)

![](https://blog.kakaocdn.net/dn/bTgRWV/btrYzqf0ePu/ZmzuTfTykWwIYX5sxXMA8K/img.gif)