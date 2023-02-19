---
layout: post
title: "[React-Native] Expo Vector icon 으로 TabBar icon 변경하기"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, 프로젝트, TIL]
---

Tab Navigator 로 구현한 TabBar 이다.
![](https://blog.kakaocdn.net/dn/bEdhU6/btrZK1E8eD0/2wuyNTzkWNRbe8O0ToeYB0/img.gif)

버튼을 눌렀을 경우 현재 위치해있는 컴포넌트 아이콘이 변경되며 파란색으로 변경되며,<br>
아닐 경우 회색으로 유지된다.

화살표 아이콘을 IconLabel 과 같은 의미를 가진 아이콘으로 변경을 하려 한다.

### 아이콘 탐색
> <https://icons.expo.fyi/>

expo 에서 제공하는 Vector icon 이다.<br>
변경하고자 하는 icon 의 이름을 탐색 후 사용하면 된다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4b4J8%2FbtrZPUGmo8R%2FzNRpaBmRtIhZRb4ATVzZCK%2Fimg.png)

> filter 기능을 이용해 원하는 종류의 아이콘만을 탐색할 수 있다.

---

### 코드에 적용하기

다음과 같이 보여지는 `Tab.Screen` 에 options 를 주어 기능을 추가할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBLnPe%2FbtrZK1zrRMi%2FOzPMD6mK8cFQDmP6DGeG8K%2Fimg.png)

먼저,<br>
`tabBarIcon` 함수를 생성하고 매개변수로 `focused` 와 `size` 를 받는다.<br>
`focused` 에 삼항 연산자를 이용하여<br>
클릭 이벤트가 발생했을때 `home` 이 active 가 되며,<br>
그게 아닐경우 아이콘이 unActive 되어 `home-outline` 이 보여지게끔 지정 해 주었다.

#### tabBarLabel
`name='Home'` 대신 `tabBarLabel` 옵션을 추가해도 무관하지만,<br>
이번 프로젝트에서는 이름이 같아 옵션을 주석처리 해 두었다.

#### 아이콘 이름 색상 변경하기
`<Tab.Navigator>` 에 `tabBarOptions` 를 추가하여<br>
`activeTintColor` 아이콘이 클릭 되었을 때 색상을 검정으로,<br>
`inactiveTintColor` 아이콘이 클릭 되지 않았을 때 색상을 회색으로 지정 해 주었다.

- 옵션 추가 전

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvhA41%2FbtrZ0KQheU1%2FUvOHTdgY20QQy60iJ8zYw1%2Fimg.png)

![](https://blog.kakaocdn.net/dn/bAOgSR/btrZNuur4w5/6uyn1PWQU9QUWMeQCEINrK/img.gif)

- 옵션 추가 후

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZuiZN%2FbtrZKoVUs8z%2FR7q6ieHZRznDarKP9t5PkK%2Fimg.png)

![](https://blog.kakaocdn.net/dn/cQ6RdC/btrZR3bY2jk/TDoKbryPqUz8VVn0KmHf80/img.gif)