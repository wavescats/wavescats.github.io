---
layout: post
title: "[React] Authenticated is not a function - createContext"
subtitle: #부제목
categories: React
tags: [리액트, Error]
---

## 에러 확인

리액트에서 클레이풀을 활용한 E-Commerce 페이지를 구현중에 발생한 에러이다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FokFc6%2Fbtr8ay12x8m%2FZTS8rkKXUv95oQKntq8pUK%2Fimg.png)

상품의 정보가 담긴 데이터가 배열로 잘 불러와지지만,<br>
화면에 렌더링이 되고 있지 않은 상태이다.<br>

에러를 보기 전에 터미널에 어떤 메세지가 출력되고 있는지 확인 해 보니
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVPDAe%2Fbtr753aJCr9%2FK4fQixh8ih88zHSD6cDKCk%2Fimg.png)

> `Line 55:11:  'AuthContextData' is assigned a value but never used`

55 번째 줄에 작성된 `AuthContextData` 가 선언은 되었지만,<br>
값이 할당되지 않았다는 메세지가 출력되어있다.

## 에러 해결

코드를 살펴보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdiitJu%2Fbtr8axvh2va%2F00Js6xNE0VAwHbP6uTqb8K%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F26mDP%2Fbtr7267pPVL%2Fny7T1r0ZkzxyNYW5pdaS8k%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmVI5N%2Fbtr73Qb4Rzi%2FPuOOnPCk1HqzoSpqwM5nyk%2Fimg.jpg)

실제로 해당 코드에서,<br>
`isAuthenticated` 함수가 `AuthContext.Provider` 컴포넌트에 제대로 전달되지 않아 <br>
`isAuthenticated is not a function` 에러가 발생한 것이다.<br><br>

함수들이 담긴 `AuthContextData` 가 할당되어있지만,<bR>
호출이 되지 않아 그 안에 담긴 함수들 또한 실행되지 않는 상황이 발생한 것이다.<br><br>

현재는 `<AuthContext.Provider value>` 부분에서,<br>
`value props` 에 객체를 전달 해 주어야 하는데<br>
현재는 객체의 키 이름만 전달 해 주고 있는 상황이다.<br>
따라서,<br>
`AuthContextData` 객체를 `value` 의 props 로 값을 전달 해 주면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNWTtm%2Fbtr76ZZ8O2h%2FZFyyzk2HNTHKKsb8G1a3C1%2Fimg.jpg)

사용된 Provider 는 Context 를 구독하는 컴포넌트들에게 Context 의 변화를 알리는 역할을 갖고 있는데,<br>
`AuthContext` 에 Value 로 `AuthContextData` 객체가 전달되어,<br>
하위 컴포넌트에서 해당 함수와 데이터를 전달하여 사용할 수 있다.

## 코드 리펙토링

또 다른 측면에서 바라보았을 경우에는,<br>
Clayful 라이브러리에서<br>
Customer 클래스에 `isAuthenticated` 함수가 없기 때문에 발생한 경우이다.<br>
Clayful 라이브러리의 Customer 클래스는<br>
고객 정보를 관리하기 위한 클래스로, `isAuthenticated` 함수 대신 get 함수를 제공한다.<br>

따라서,<br>
get 함수를 사용하여 고객 정보를 가져와서 로그인 상태를 확인할 수 있다.

```JS
const isAuthenticated = () => {
    var Customer = Clayful.Customer;

    var options = {
        customer: localStorage.getItem('accessToken'),
    };

    Customer.get(options, function (err, result) {
        if (err) {
            // Error case
            console.log(err.code);
            setIsAuth(false);
            return;
        }

        var data = result.data;

        if (data.id) {
            setIsAuth(true);
        } else {
            setIsAuth(false);
        }
    });
};
```

변경된 코드에서 `Customer.get()` 함수를 사용하여 고객의 정보를 가져오고,<br>
가져온 정보를 통해 로그인 상태를 확인한다.<br>
만약,<br>
가져온 정보에 `id` 속성이 존재한다면 로그인 상태로 간주한다.

## Reference

> <https://velog.io/@mujaen/ReactContext-%ED%98%84%EC%97%85%EC%97%90%EC%84%9C-%EC%93%B8-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C><br>
