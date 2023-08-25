---
layout: post
title: "[Typescript] React.FC 란 ? 💨"
subtitle: #부제목
categories: Typescript
tags: [타입스크립트, TIL]
---

## 개요 👋

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDpEA7%2FbtssbloU1Dh%2F5aq6cz8wT8tASAsFeLzFh1%2Fimg.jpg)

이번 포스팅에서는 프론트엔드 포지션에서 가장 많이 사용하는<bR>
`React` 프레임워크와 안정성을 위해 사용하는 `TypeScript` 를 사용하여<br>
간단한 컴포넌트를 구현해보고자한다.

---

### What is FC ?

**`FC` 는 `Function Component` 의 약자**로,<bR>
React 의 함수 컴포넌트를 정의할 때 사용되는 타입이다.<br>
이 타입은 함수 컴포넌트가 받을 수 있는 **props 의 타입을 제네릭으로** 받아, 타입 안정성을 높일 수 있다.<Br><br>

기본적으로 `React.FC` 는,<br>
**`children` 이라는 props 를 자동으로 추가**한다.

```javascript
// 1
type ComponentsType = React.FC<MyProps>;

// 2
type ComponentsType = (
  props: Myprops & { children?: ReactNode }
) => ReactElement;
```

두 코드는 같은 의미를 가지고 있는 코드이다.

---

#### 장점

`React.FC` 의 장점은<br>
컴포넌트가 **함수형 컴포넌트임을 명시**하여 보다 직관적으로 확인할 수 있으며,<br>

> 협업 시 해당 컴포넌트를 공유한다면,<br>
> props 에 **어떤 값이 전달되는지** 쉽게 파악이 가능하다.

**자동으로 `children` 이라는 프로퍼티를 받을 수 있으므로,**<br>
**별도로 `children` 을 타입 정의에 추가할 필요가 없다.**<Br>

또한 props 에 대한 타입을 명시할 수 있어,<br>
잘못된 타입의 props 를 전달하는 실수를 컴파일 타임에 디버깅 할 수 있다.<br>

#### 단점

반면에 단점으로는,<br>
`defaultProps` 와 호환이 되지 않을 수 있고,<br>
`children` 을 자동으로 추가하기에<br>
`children` 을 받지 않아야 하는 컴포넌트에서 **별도의 타입을 지정**하여 사용해야한다.

> `defaultProps` 는 클래스 컴포넌트에서 주로 사용함.<br> > `children` 을 받지 않아야 하는 컴포넌트에서는 **`React.FC` 를 사용하지 않고 직접 props 타입을 명시**해준다.

즉, `Optional Children`.<br>
말 그대로 `Children` 을 옵셔널하게 가지고 있다는 것이다.

```javascript
export const Hello: React.FC<HelloProps> = ({ name }) => {
  return <h1>Hello olleh! my name is {name}</h1>;
};

const App = () => (
  <>
    <Hello name="suzi">
      <span>{"I have children"}</span>
    </Hello>
  </>
);
```

위 코드를 보면,<bR>
`Hello` 컴포넌트는 `children` 을 렌더링 하는 부분이 없음에도<br>
`App` 컴포넌트에서 에러 없이 작동한다.<br><br>

이는 타입스크립트를 사용하면서 혼란을 야기할 수 있는 부분이므로,<br>
해당 컴포넌트에 `children` 의 존재가 가능한지 여부를 확인하는 로직이 추가되면<br>
가독성, 유지보수 측면에서 좋을 것 같다.<Br><br>

---

`defaultProps` 가 호환이 되지 않는다 라는 말은,<br>
즉, **`React.FC` 에서는 `defaultProps` 를 사용하지 못한다** 라는 말 이다.

> `defaultProps` 란 -> props 의 default 값을 설정해주는 방법이다.

```javascript
export const Hello: React.FC<HelloProps> = ({ name }) => {
  return <h1>Hello olleh! my name is {name}</h1>;
};

Hello.defaultProps = {
  name: "minsu",
};
```

```javascript
export const Hello: FC<HelloProps> = ({ name = "minsu" }) => {
  return <h1>Hello olleh! my name is {name}</h1>;
};
```

두 코드의 예시가 있다.<br>
첫 번째 코드의 경우 `defaultProps` 속성을 사용하여 기본값을 지정해주고있다.<bR>
`name` 에 props 가 전달되지 않을 경우 `default` 로 정의한 'minsu' 가 기본값으로 사용된다.<br><br>

두 번째 코드의 경우,<br>
함수형 컴포넌트의 파라미터에서 직접 기본값을 설정하고있다.<br>
`name` 에 props 가 전달되지 않을 경우 직접 기본값으로 지정한 'minsu' 가 기본값으로 사용된다.<br><br>

두 코드의 차이점으로는<br>

1. `defaultProps` 기본값을 정의하는 설정이 필요 없는 두 번째 코드가<br>
   보다 간결하여 가독성을 향상시킬 수 있다.<br>
2. TypeScript 를 사용 할 경우 두번째 코드가 타입 추론에 보다 유리할 수 있다.<br>
   기본값이 명시적으로 매개변수에 지정되었기 때문에 TypeScript 가 더 정확한 타입 추론이 가능하다.

> React 에서 `defaultProps` 는 미래에 **deprecated 될 가능성**이 있으므로,<br>
> 두 번째 방식이 더 안전한 로직을 구현하는데 좋을 것 같다.

---

### FC 예시 💾

```javascript
import React, { FC } from "react";

interface MyProps {
  name: string;
  age: number;
}

const MyComponent: FC<MyProps> = ({ name, age, children }) => {
  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
      <div>{children}</div>
    </div>
  );
};

export default MyComponent;
```

해당 예시의 코드는 `MyProps` 라는 `TypeScript` 인터페이스를 선언하고,<br>
`name` 이라는 문자열 타입과,<br>
`age` 라는 숫자 타입의 프로퍼티를 가진다.<br>

`MyComponent` 라는 이름으로 함수형 컴포넌트 (`FC`) 임을 명시하고,<br>
`MyProps` 인터페이스를 따르는 `props` 를 받는다.<br>

`FC<MyProps` 를 사용하면 `children` 이라는 props 도 자동으로 포함된다.

---

## Reference 🌊

> <https://shape-coding.tistory.com/entry/TypeScript-ReactFC%EC%97%90-%EC%82%AC%EC%9A%A9%EC%97%90-%EB%8C%80%ED%95%B4-%EC%83%9D%EA%B0%81%ED%95%B4%EB%B3%B4%EA%B8%B0><br><https://story.pxd.co.kr/1650><br><https://velog.io/@apro_xo/React-React.FC%EC%9D%98-%EB%8B%A8%EC%A0%90%EA%B3%BC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95>
