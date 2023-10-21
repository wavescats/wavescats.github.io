---
layout: post
title: "[React] useMemo 와 useCallback 란 ❓"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

## 개요 ✏️

`React` 를 사용한다면,<br>
가장 대표적인 **`Hooks`** 인 **`useState` 와 `useEffect`** 는 이제 익숙 할 것이다.<br>
컴포넌트 내부에서 `props` 나 `state` 를 다루는 기본적인 로직은<br>
**`useState` 와 `useEffect` 만으로도 구현이 가능**하다.<br>

이번 포스팅에서는,<br>
보다 **효과적인 컴포넌트의 렌더링 최적화**를 위해 등장한 `Hooks` 인<br>
`useMemo` 와 `useCallback` 에 대해 정리 해 보려고 한다.

---

### 사전 지식 ✅

1️⃣ 함수형 컴포넌트는 말 그대로 함수 그 자체 이며, `JSX` 형태로 작성된 컴포넌트를 반환하는 함수이다.<bR>

2️⃣ 컴포넌트가 렌더링 된다는 것은 누군가가 그 함수(컴포넌트) 를 호출하여 실행되는 것을 말한다.<BR>
**즉, 함수가 실행될 때 마다 내부에 선언되어 있는 변수나 함수 또한 실행된다.**
<br><br>
3️⃣ 컴포넌트는 자신의 `State` 가 변경되거나, 부모에게서 받는 `props` 가 변경되었을 때 재 렌더링이 된다.<br>

> **하위 컴포넌트에서 최적화를 시켜주지 않으면,**<br>**부모에서 받는 `props` 가 변경되지 않더라도 재 렌더링이 된다.**

---

## useMemo 📝

```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

- Returns a memoized value.

`useMemo()` 는 메모이제이션 된 **값**을 반환한다.

### 메모이제이션이 뭐지 ❓

> 계산 결과를 저장하고, 동일한 입력 값이 다시 전달 될 경우<br>
> 이전에 저장된 결과를 반환하여 계산을 최적화 하는 프로그래밍 기법이다

위 코드에서 `computeExpensiveValue` 함수는 `a` 와 `b` 두 가지의 종속성을 가지며,<br>
이 종속성이 변경될 때만 다시 계산(함수 실행) 한다.<br>
계산된 결과는 `memoizedValue` 에 저장되고 재사용 된다.<br>

**`useMemo`** Hooks 는 위 설명으로 모든 과정을 설명가능하다.<br>
React 앱을 사용하며,<br>
계산 비용이 높은 연산을 **최적화** 하고,<br>
렌더링을 **효율적으로 관리하기 위해** 사용되는 메모이제이션 훅 이다.

---

### 예제 🌟

```javascript
import React, { useState, useMemo } from "react";

function App() {
  const [numbers, setNumbers] = useState([1, 2, 3, 4, 5]);

  // numbers 배열의 합계를 계산하는 함수
  const calculateSum = (numbers) => {
    console.log("Calculating sum...");
    return numbers.reduce((acc, num) => acc + num, 0);
  };

  // useMemo를 사용하여 계산 결과를 메모이제이션
  const sum = useMemo(() => calculateSum(numbers), [numbers]);

  return (
    <div>
      <h1>Sum of Numbers</h1>
      <ul>
        {numbers.map((number, index) => (
          <li key={index}>{number}</li>
        ))}
      </ul>
      <p>Sum: {sum}</p>
    </div>
  );
}

export default App;
```

위 코드는 `useMemo` 훅을 사용하여 `sum` 변수를 계산한다.<br>
`useMemo` 는 `calculateSum` 함수의 결과를 메모이제이션 하고,<br>
의존성 배열에 추가된 **`numbers` 의 값이 변경되지 않는 한, 이전의 결과를 반환한다.**<br>

즉, **`numbers` 배열의 변경이 없다면,**<br>
`calculateSum` **함수가 중복으로 실행되지 않으며,** 계산 결과를 저장(캐싱)하여 성능을 최적화 한다.

---

## useCallback 📡

```javascript
const memoizedCallback = useCallback(callback, dependencies);
```

```javascript
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

- Returns a memoized Callback.

`useCallback()` 은, 메모이제이션 된 **함수**를 반환한다.<br>

`callback` 은 메모이제이션 하려는 대상, 즉 => **콜백 함수** 이며,<br>
`dependencies` 는 의존성 배열로,<br>
이 배열에 포함된 **종속성이 변경될 때만** 새로운 콜백 **함수가 생성**된다.<br>

> 만약 종속성(의존성) 배열이 비어있다면,<br>콜백 함수는 항상 **동일한 결과를 리턴**하는 함수로 유지된다.

사전 지식에도 기재 해 놓았듯,<br>
컴포넌트는 **렌더링 될 때 마다** 내부에 선언되어 있는 표현식(변수, 또다른 함수 등)도 매번 다시 선언되어 사용된다.<br><Br>

이를 보완하기 위하여,<br>
`useMemo` 나 `useCallback` 훅을 사용하여<br>
**불필요한 렌더링을 방지**하고, 계산 비용이 높은 표현식과 콜백 함수를 메모이제이션 하여 방지할 수 있다.<br>

---

### 예제 🌟

```javascript
import React, { useState, useCallback } from "react";
import ChildComponent from "./ChildComponent";

function ParentComponent() {
  const [count, setCount] = useState(0);

  // `increment` 함수를 메모이제이션
  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onIncrement={increment} />
    </div>
  );
}

export default ParentComponent;
```

위 코드는,<br>
`useCallback` 을 사용하여 자식 컴포넌트로 콜백 함수를 전달하는 부모 컴포넌트 이다.<br>

`increment` 함수는,<br>
의존성 배열에 존재하는 `count` 값에 의존하므로,<br>
종속성 배열에 `count` 를 포함시켜 해당 값이 **변경될 때만** (`setCount`) 새로운 함수를 생성한다.

#### 새로운 함수 생성 ❓

새로운 함수를 생성한다는 말은<br>
즉, 매번 렌더링 시 마다 동일한 함수가 아니라 새로운 함수 인스턴스가 생성된다는 것을 말한다.<br>

> `React` 앱은,<br>컴포넌트가 렌더링 될 때 함수 컴포넌트의 모든 코드가 실행된다.

예제에 사용된 `increment` 함수는,<br>
의존성 배열에 포함된 `count` 의 값이 변경되면, 새로운 함수 인스턴스를 필요로 한다.<br>

즉,<br>
`count` 의 값이 변경되면, 새로운 `increment` 함수가 필요하기 때문에<br>
의존성 배열에 담긴 **`count` 값이 변경될 때만 ❕** 새로운 함수 `increment` 가 생성되도록 하여<br>
불필요한 렌더링을 방지하고,<br>
`increment` 함수를 최적화 하여 성능을 향상 시키는 것을 말한다.

---

## Reference 🌊

> <https://youtu.be/uBmnf_k7_r0?si=YrIfAPxIgdZE8Dub><br><https://velog.io/@sunkim/React.memo-useMemo-useCallback-%EC%97%AD%ED%95%A0-%EB%B0%8F-%EC%B0%A8%EC%9D%B4%EC%A0%90><br><https://velog.io/@hang_kem_0531/useMemo%EC%99%80-useCallback%EC%9D%98-%EC%B0%A8%EC%9D%B4><br><https://whales.tistory.com/117><br><https://any-ting.tistory.com/83><br><https://leehwarang.github.io/2020/05/02/useMemo&useCallback.html>
