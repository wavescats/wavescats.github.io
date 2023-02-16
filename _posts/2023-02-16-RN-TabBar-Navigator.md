---
layout: post
title: "[React-Native] Tab Navigator 를 사용해 화면 구성하기"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, 프로젝트, TIL]
---

다음과 같이 TabBar 를 모두 구성한 뒤의 모습이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcdb9Ac%2FbtrZz1zrnvu%2F58VtaGmpjg23h8kf7YjBmK%2Fimg.png)

### Navigator
버튼을 눌렀을때 보여지는 화면에 구분을 하고싶다.

#### Navigation 의 종류
- Stack Navigator
- Tab Navigator
- Draw Navigator

이 중,<br>
해당 프로젝트에서는 **Tab Navigator** 를 사용할 것이다.<br>
<br>
Navigation 이 분리 된 이유로는,<br>
원래 하나의 패키지에 모두(Stack, Tab, Draw) 포함되어 있었지만,<br>
Stack 과 Tab 만을 사용하는 경우 Draw 는 사용하지 않아<br>
이는 필요없는 패키지로 구분되어 전체 크기에 영향을 끼치게 되었다.<br>
때문에, 이를 보완하기 위해 패키지를 분리하게 되었다고 한다.

#### 패키지 설치
```bash
npm install @react-navigation/native --save
```

> expo 앱에서 생성한 프로젝트일 경우 의존성 있는 패키지들을 추가 설치해 주어야한다.

```bash
npx expo install react-native-screens react-native-safe-area-context
```

#### 사용
```bash
import { NavigationContainer } from '@react-navigation/native'
```

공식 문서를 참고하여 확인 해 보니,<br>
`App.js` 가 `return` 되어 실행되는 부분에<br>
`<NavigationContainer>` 를 추가하여 사용하면 된다고 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbr8cHN%2FbtrZD2wYDMj%2FoMPO2ccSzcKXvxdAWTgp8K%2Fimg.png)

---
### Tab navigation
공식문서를 살펴보면, Tab navigation 은,<br>
모바일 앱 하단에서 주로 볼 수 있으며 클릭하여 화면 전환을 할 수 있도록 하는 탭 바 임을 알 수 있다.

#### 패키지 설치
```bash
npm install @react-navigation/bottom-tabs
```

#### 사용
```bash
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdQp8k%2FbtrZGhCCaxk%2FFw4K6tIkqewoo254fpoEh0%2Fimg.png)

![](https://blog.kakaocdn.net/dn/bXLYsF/btrZH2kv6bz/1KOiLksHMeG0n6g5LAGJc1/img.gif)


### 적용
- App.js

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCliwu%2FbtrZIfrizoG%2Fx1uFNiKMyJId6JdKG22vI1%2Fimg.png)

- src/navigation/Tab.jsx

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOam0z%2FbtrZJWYyLur%2FZVxiyvHeK5lcTTQKA0SRWK%2Fimg.png)

> `headerShown: false` 옵션은 상단 상태바를 제거하는 옵션이다.

- 결과

![](https://blog.kakaocdn.net/dn/bEdhU6/btrZK1E8eD0/2wuyNTzkWNRbe8O0ToeYB0/img.gif)

<br>
넵.. 왜 초기 구성과 이미지가 다르냐구요?<br>
싹 갈아 엎었기 때문이죠 🌞😭<br>
<br>
덕분에 Navigator 의 사용 방법에 대해 완벽하게 숙지하게된 프로젝트였다고 합니다 👏👏

### Reference
> <https://reactnavigation.org/docs/getting-started><br><https://reactnavigation.org/docs/tab-based-navigation/>
