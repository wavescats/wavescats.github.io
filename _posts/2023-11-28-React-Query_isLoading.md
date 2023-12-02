---
layout: post
title: "[React] 서스펜스와 리액트쿼리를 활용하여 로딩화면 구현하기 (Feat. Skeleton UI 💀)"
subtitle: #부제목
categories: React
tags: [리액트, 서스펜스, 리액트쿼리, TIL]
---

## 개요 🔔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9Jfrs%2FbtsAXgNKUUi%2FYiB4frV40StpsOgqODNKbk%2Fimg.png)

`리액트 서스펜스(React Suspense)` 는,<br>
앱에서 비동기적으로 데이터를 처리하고 관리하기 위해 사용하는 리액트의 새로운 기능이다.<bR>
서스펜스는 `React 16` 에서 처음 선보이고,<br>
`React 18` 에서 정식으로 추가 된 기능이라고 한다.

---

### Why Suspense ❓

사용자에게 구현한 웹 페이지를 보여주기 위한 UI/UX 개선사항으로 스켈레톤 UI 를 접하고,<br>
이를 구현하기 위해<bR>
삼항연산자를 통해 `LoadingComponent` 를 불러오는 형태로 진행했다.<br>

하지만,<br>
서스펜스를 사용하면 코드가 훨씬 직관적으로 리팩토링이 되며,<br>
코드 스플리팅을 통해 웹 성능(최적화) 에도 유의미한 영향을 끼칠 수 있었다.

서스펜스의 사용 방법은 아래와 같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdw4KfK%2FbtsA2sGThP2%2FtfjJJrzeX7xeokh7UiQRqk%2Fimg.png)

레이아웃을 담당하는 컴포넌트 하위에<br>
서스펜스를 사용하여 비동기 데이터 로딩을 처리하는 로직이 담겨있다.<br>

`<Comment />` 컴포넌트를 비동기적으로 로딩하며,<br>
로딩 중에는 `<Spinner />` 컴포넌트가 표시된다.

> `fallback` 옵션은 서스펜스 컴포넌트에서 사용되는 옵션 중 하나로,<br>코드 스플리팅이나 데이터 로딩을 처리할 때<br>로딩 중에 보여줄 컴포넌트나 요소를 저장하는데 사용된다.<br><br>즉, **서스펜스 컴포넌트는 비동기적으로 로딩되는 컴포넌트를 기다리며**<br>**로딩중일 때 사용자에게 어떤 내용을 보여줄지 `fallback` 을 통해 정의**한다.

---

## React-Query 🌸

`React-Query` 에는 서스펜스와 유사한 `isLoading` 이 있다.<br>
`isLoading` 은, `useQuery` 훅을 사용할 때 발생하는 상태 중 하나로<br>
데이터를 비동기적으로 가져오는 동안의 로딩 상태를 나타낸다.<br>

`useQuery` 훅을 사용하면, 데이터를 가져오는 동안 제공하는 주요 상태가 있다.

- data<br>
- isLoading<br>
- error<br>

`isLoading` 의 경우, 데이터를 가져오는 동안 `true` 로 설정되며<br>
데이터를 모두 불러오거나, 에러가 발생하면 상태가 `false` 로 변경된다.

```javascript
import { useQuery } from "react-query";

function MyComponent() {
  const { data, isLoading, error } = useQuery("myData", fetchDataFunction);

  if (isLoading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>Error: {error.message}</p>;
  }

  // 여기에서 data를 사용하여 UI를 렌더링합니다.
  return <div>{data}</div>;
}
```

이 코드는 `useQuery` 로 데이터를 가져오는 중인지 여부를 `isLoading` 을 통해 확인하고,<br>
해당 상태가 `true` 라면, 로딩 메세지가 출력된다.<br>

> 에러가 발생한 경우도 동일 !

데이터가 성공적으로 잘 불러와졌다면 `data` 객체를 출력한다.

---

### Suspense vs isLoading ❔

두 방법 모두 비동기적으로 **데이터를 가져오고 있는 동안** 처리하는 기능을 담당하고있다.<br>

- **Suspense**

```javascript
import React, { lazy, Suspense } from "react";

const LazyComponent = lazy(() => import("./LazyComponent"));

const MyComponent = () => {
  return (
    <Suspense fallback={<LoadingSpinner />}>
      <LazyComponent />
    </Suspense>
  );
};
```

`React` 의 `Suspense` 경우 비동기 데이터를 **로딩하는 동안 대기할 때** 사용한다.<br>
코드에서 사용된 것처럼,<br>
`lazy` 로딩을 통해 컴포넌트를 `import` 하여 대기하고,<br>
이를 `fallback` 옵션에서 컴포넌트를 호출하여 `Suspense` 중 보여질 컴포넌트를 명시하고 있다.

---

- **isLoading**

```javascript
import { useQuery } from "react-query";

const MyComponent = () => {
  const { data, isLoading, error } = useQuery("myQueryKey", fetchDataFunction);

  if (isLoading) {
    return <LoadingSpinner />;
  }

  if (error) {
    return <ErrorComponent />;
  }

  return <DataComponent data={data} />;
};
```

`React-Query` 가 제공하는 `useQuery` 는,<br>
비동기 데이터를 가져오고 있는동안 `isLoading` 이라는 상태를 제공한다.<br>
이 상태는 데이터가 로딩 중 인지의 여부를 `boolean` 으로 뱉어낸다.

> 위 예시 참조 !!

두 개념 모두 비슷하지만 정리하자면,<br>

`React-Query` 의 `isLoading` 은<br>
데이터가 **로딩 중 인지 여부를 확인**하는데 사용되고,<br>

`React` 의 `Suspense` 는,<br>
비동기 작업 중 **대기하는 동안 특정 컴포넌트나 리소스를 지정**하는데 사용된다.<br>

해당 코드는 두 기법을 사용한 간단한 예시이다.

```javascript
import { Suspense, useState, useEffect } from "react";

const MyComponent = () => {
  const [data, setData] = useState(null);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    try {
      const response = await fetch("https://api.example.com/data");
      const result = await response.json();

      setData(result);
      setIsLoading(false);
    } catch (error) {
      console.error("Error fetching data:", error);
      setIsLoading(false);
    }
  };

  return (
    <div>
      <Suspense fallback={<LoadingSpinner />}>
        <AsyncComponent data={data} />
      </Suspense>

      {isLoading && <LoadingSpinner />}
    </div>
  );
};
```

이 코드에서 `Suspense` 는, `AsyncComponent` 가 데이터 로딩이 완료 될 때 까지 기다리도록 하고,<br>
`isLoading` 은, 데이터가 로딩 중인지의 여부를 관리한다.

> **즉,<br>`React-Query` 에서 제공하는 `isLoading` 은 👇<br>비동기 데이터를 가져오고 있는 동안 `isLoading` 을 사용하며,<br>이 속성은 데이터가 로딩 중인지 여부를 나타낼때 사용 !!!<br><Br>`React` 에서 제공하는 `Suspense` 는 👇<br>비동기 데이터를 로딩하는 동안 대기할 때 사용하며,<br>`React.lazy` 와 함께 사용되어 코드 스플리팅과 같은 비동기 작업에서 컴포넌트를 기다리게 한다.<br>`Suspense` 를 사용하여 코드 스플리팅된 컴포넌트나 데이터를 로딩하는 컴포넌트를 대기할 때 사용한다.**

---

### 차이점 🎭

얼핏 보면 두 기능은 비동기 데이터를 불러오기 이전의 작업을 처리하는 용도로 사용되어,<br>
다소 비슷하다고 느껴질 수 있지만, **두 기능은 서로 다른 용도**를 가진 기능들이다.

- **isLoading**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fxljup%2FbtsBinlsSTZ%2F6JKEWRSl2rB8ktDLVCxzw1%2Fimg.png)

`React-Query` 의 `isLoading`<br>

- 👩‍🦰 **목적**<br>
  비동기 데이터를 가져오는 동안의 데이터 로딩 상태를 관리하고,<br>
  해당 상태에 따라 UI 를 업데이트 하는 데 사용.
- 🧒 **활용**<br>
  `useQuery` 훅을 사용하여 데이터를 비동기로 가져올 때 사용하며,<br>
  `isLoading` 속성을 통해 데이터가 로딩 중인지의 여부를 확인할 수 있다.

---

- **Suspense**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F99SIQ%2FbtsBgJJmbYQ%2Fk4JUGTk5XbE8SU64j5jG5k%2Fimg.png)

- 👨 **목적**<br>
  비동기 작업 중, 대기하는 동안 특정 컴포넌트나 발생하는 리소스를 처리하는 데 사용.<br>
  코드 스플리팅과 함께 사용하여 **필요한 컴포넌트를 필요한 때만 렌더링** 하는데 목적을 둠.
- 👴 **활용**<br>
  `React.lazy` 와 함께 사용하여, 코드 스플리팅된 컴포넌트를 비동기적으로 불러오거나,<br>
  `React.Suspense` 컴포넌트를 통해 **대기중에 특정 컴포넌트를 렌더링** 할 때 사용.

---

이렇게 두 기능의 차이를 다시 한 번 정리해 봤는데,<br>
역시 비슷해 보인다..😫<br>

하지만,<br>
두 기능은 각각 **데이터 로딩**과 **데이터 처리**에 관련하여 다른 측면에 중점을 둔 기능들 이므로<br>
엄연히 다른 기능(목적)을 갖고 있다고 말할 수 있다.<br>

> **오늘도 새로운 지식 잘 먹었다 !**

---

## Reference 🌊

> <https://www.loginradius.com/blog/engineering/react-code-splitting-with-lazy-suspense/><br><https://www.daleseo.com/react-suspense/><br><https://yiyb-blog.vercel.app/posts/react-query-loading-state><br><https://stackoverflow.com/questions/75401477/reasons-for-using-isloading-or-isfetching-in-react-query>
