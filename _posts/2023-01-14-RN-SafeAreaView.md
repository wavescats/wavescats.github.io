---
layout: post
title: "[React-Native] SafeAreaView 를 활용해 expo 앱에 그리기"
subtitle: #부제목
categories: TIL
tags: [리액트 네이티브]
---
### 에러도 아닌것이 뭔가 이상한거..😇

expo 앱을 설치 후,<br>
화면에 보이는 `View` 영역에 생성한 컴포넌트를 보여주려 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FO9Oy2%2FbtrZuCebxug%2FquwnKOkO4wzZLWyiUF28nK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw390G%2FbtrZo80uH8I%2FsEiVzxa9t8mJeWP1gyEqz0%2Fimg.png)

코드를 작성 후 `expo start` 명령어를 통해 앱을 실행시키면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7CV96%2FbtrZqGCCgR2%2FwkMVwIekHCzH9NWSmwaZZK%2Fimg.png)

왼쪽 위 상단에 작성한 텍스트가 표시되고 있다.<br>
이 부분을 검색 해 보니 **'노치 영역'** == **'상단바'** 라고 한다.

어떻게 하면 노치 영역에서 벗어난 영역에 컴포넌트가 시작될 수 있을까?

### SafeAreaView ✨
---
바로,<br>
부모의 최 상단 컴포넌트를 안전한 영역부터 그리게 해 주는 `SafeAreaView` 를 이용할 것이다.

다음과 같이 `View` 영역을 `SafeAreaView` 로 바꾸어 렌더링 해 주면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc0ThGR%2FbtrZrzv0BjR%2FiM8ydPN1l75Kmcd7VPVQ8k%2Fimg.png)

노치 영역을 벗어난 이후부터 컴포넌트가 그려짐을 볼 수 있다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FH0iGe%2FbtrZrT8NDr2%2FnQe6xp9SZyaVKDxvVSSdIk%2Fimg.png)

마찬가지로 노치 영역은 상단 뿐만 아니라 하단에도 존재했다.
`StyleSheet` 에 `justifyContent: 'flex-end'` 스타일을 추가 해 주면,<br>
작성한 컴포넌트가 하단(==**홈 인디케이터**)에서 렌더링 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F48Vh2%2FbtrZsEDy2sn%2FrC0e4WeNzghVTcvgKEHsC0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlHzO4%2FbtrZttu2QBf%2FkabjxHrRSyKb6iK5g0NhG0%2Fimg.png)

이 또한,<br>
`SafeAreaView` 를 이용하여 컴포넌트를 감싸주면, <br>
**홈 인디케이터** 영역 이후부터 그려지게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAWLvm%2FbtrZrzbIXZ9%2F0TPk81cytGEOKzRfFKGro1%2Fimg.png)

### iPhone-X-Helper
---
`SafeAreaView` 를 이용하여 자동으로 노치 영역을 제외하여 그릴 수도 있지만,<br>
다른 방법으로는 `react-native-iphone-x-helper` 라이브러리를 이용하여<br>
노치 영역의 높이를 구하여 `margin` 이나 `padding` 을 주는 방법도 있다.

```bash
npm i react-native-iphone-x-helper --save
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHLJ5Q%2FbtrZtqkLO7f%2F7slNHaA68G6ic8pAC7u4y0%2Fimg.png)

`react-native-iphone-x-helper` 에 `getStatusBarHeight` 와 `getBottomSpace` 을 이용하면,<br>
상단과 하단의 노치 영역에 해당하는 높이를 구할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbdw0v5%2FbtrZuDc7Ttb%2F9FRmV75PMfKoAnqcp2okkk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZNARx%2FbtrZqGQfwFp%2Fk0yJyDf4CokLBtM052Kx1K%2Fimg.png)

구한 값을 토대로 `paddingTop`, `paddingBottom` 을 주어도 되지만,<br>
변수를 불러와 스타일에 적용시켜보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft7JCQ%2FbtrZrAaBwq1%2FLFNYKGKk4uBejXOJM8n7Pk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmlSuO%2FbtrZrYh1TwQ%2FtxNiOPefBgiCUiU2moGBy0%2Fimg.png)

> `SafeAreaView` 를 사용하지 않고도 노치 영역 이후부터 컴포넌트가 그려진다.


### Reference
> <https://trend21c.tistory.com/2236><br><https://devport.tistory.com/11><br><https://github.com/ptelad/react-native-iphone-x-helper>