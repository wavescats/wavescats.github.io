---
layout: post
title: "[React-Native] onPress 함수를 props 로 자식 컴포넌트에서 Toggle 하기"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, TIL]
---

카카오톡 친구 목록을 클론코딩 중이다.<br>

다음과 같이 친구 목록들이 나열되어 있을 때,<br>
버튼을 클릭 시 친구 목록이 숨겨지는 Toggle 을 구현하려 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb0G3Xn%2Fbtr0Axq7dHE%2FGzZQnksPadQ7YgeJUjEB70%2Fimg.jpg)

먼저,<br>
부모 컴포넌트에서 친구 목록을 보여주기 위한 State 를 생성했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbw7Wjr%2Fbtr0DWjxthe%2F1B1bt9Y3R7pijHKfzb05Uk%2Fimg.png)

하단에는 버튼을 클릭 시 `setIsOpened` State 가 `false` 로 변경되는 함수를 생성해 주었다.

이를 자식 컴포넌트에서 사용할 수 있도록 props로 보내줄 것이다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpVY6E%2Fbtr0IFui2TW%2FGDCm6EcuA1hNSrza9UaYFk%2Fimg.png)

자식 컴포넌트인 `Body2` 에서는,<br>
버튼에 `onPress` 이벤트를 주었고,<br>

아이콘에는
props 로 내려받은 `isOpened` 가 true 일땐 **up** false 일땐 **down** 이 되는 옵션을 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb4zqbp%2Fbtr0ANHqhgu%2FRsbfeItPmuoqyLg6rpPNd1%2Fimg.png)

여기에 이벤트를 추가해 아이콘이 **down** 이 되었을 경우,<br>
친구 목록이 보여지는 이벤트를 추가하려한다.

---

### 삼항 연산자
삼항연산자를 활용해,<br>
props 로 내려받은 `isOpened` 가 true 일 때 아래 `ScrollView` 구문을 실행시키고 false 라면 null 을 return 하는 로직이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcysLLd%2Fbtr0H7kiTOg%2FogVpgJjV0abW1Lww8STwTk%2Fimg.png)

### if 문

if 문을 활용해<br>
`isOpened` 가 true 가 아닌 상태라면 null 을 return 해 주고,<br>
그게 아니라면 `ScrollView` 구문을 실행하는 로직이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc1oxBb%2Fbtr0AxYYZKJ%2Fn9CMcgzPVwSQ2WiZ7GFblk%2Fimg.png)


### && 연산자
`props.isOpened` 가 && (true) 일 때 아래 구문을 랜더링 하라는 로직이다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbORFEw%2Fbtr0HSt5WOR%2FrYG1PgM9yekKk7Vr7H7bL0%2Fimg.png)

&& 연산자는<br>
값이 false 라면 && 이전에 멈추기 때문에 return false 가 되고,<br>
true 라면 && 이후의 값을 체크한다.

> false && 2 = false<br>
true && 2 = true

> 두 방법 중 **가독성** 측면에서 바라봤을 때는,<br>
첫 번째 줄에서 return 되는 부분을 첫 줄에서 확인할 수 있기 때문에<br>
두 번째 방법인 **if 문을 활용한 방식**이 조금더 나아 보이는것 같다.

### 결과

![](https://blog.kakaocdn.net/dn/tD0P4/btr0KSmpxMf/tfirmXeAx0KBmXy4esm9UK/img.gif)