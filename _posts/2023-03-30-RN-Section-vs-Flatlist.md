---
layout: post
title: "[React-Native] Section-List 와 Flat-List 의 차이"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, TIL]
---

## 개요

다음과 같이 버스 운행 정보가 담긴 앱을 구현하려 한다.<br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFHM2x%2Fbtr6TmKcpOB%2FqKg5jqmn19bC4qYR2udXj0%2Fimg.png" width="200" height="400">

해당 서비스는 3 가지 Section 으로 구분되어 있는데,<br>

- 간선버스
- 지선버스
- 직행버스

해당 UI 를 `Flat-List` 를 사용하여 구현 하려한다면,<br>

각각의 (버스 번호가 담긴) 아이템이 시작되는 첫번째를 알아내어,<br>
그 위에 Section 을 추가해야하는 번거로움을 맞닥드리게 된다.

이와 같은 상황에 `Section-List` 컴포넌트를 사용하면,<br>
조금 더 간단하게 구현할 수 있다.

## Flat-List

UI 를 `Flat-List` 로 구현하려면,<br>
`FlatList` 안에 `data` 라는 props 를 받고 그 안에 배열을 넣어주어 구현할 수 있다.<br>
하지만,<br>
작성된 코드를 보면 알 수 있듯 각각의 Section 을 구분 짓기엔 다소 어려움이 보인다.

```JS
<View style={{ flex: 1 }}>
    <Text style={{ fontSize: 30, fontWeight: "bold" }}>FlatList</Text>
    <FlatList
        data={[
            { busNum: 146 },
            { busNum: 360 },
            { busNum: 740 },
            { busNum: 3412 },
            { busNum: 1100 },
            { busNum: 1700 },
        ]}
        renderItem={({ item }) => <Text>{item.busNum}</Text>}
    />
</View>
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcubOh%2Fbtr610F9EEv%2Fxu8kWluIEDjvqPLUx4ozik%2Fimg.png)

## Section-List

이번엔,<br>
앞서 구현한 `FlatList` 를 `SectionList` 를 사용하여 코드를 리펙토링 한 형태이다.<br>
<br>

먼저,<br>
각각의 Section 을 담당하는 `title` 이 존재하고,<br>
`data`는 각 Section 안에서 반복되는 데이터의 리스트의 형태이다.<br>
`data`는 `FlatList` 와 같은 역할을 갖고 있다.

```JS
<View style={{ flex: 1 }}>
    <Text style={{ fontSize: 30, fontWeight: "bold" }}>SectionList</Text>
    <SectionList
        sections={[
            {
                title: "간선버스",
                data: [{ busNum: 146 }, { busNum: 360 }, { busNum: 740 }],
            },
            {
                title: "지선버스",
                data: [{ busNum: 3412 }],
            },
            {
                title: "직행버스",
                data: [{ busNum: 1100 }, { busNum: 1700 }, { busNum: 740 }],
            },
        ]}
        renderSectionHeader={({ section: { title } }) => <Text>{title}</Text>}
        renderItem={({ item }) => <Text>{item.busNum}</Text>}
    />
</View>
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUW6dN%2Fbtr61hhlFpj%2Fkvk6avmFqjkmKZhpkeqcTK%2Fimg.png)

## 회고

`Flat-List`와 `Section-List` 모두 각자가 갖고 있는 장점이 있으며,<br>
다음과 같은 UI 를 구현할 때는,<br>
`Section-List` 컴포넌트로 구현하는게 `Flat-List` 로 구현하는 형태 보다 조금 더 나아보인다.<br>
<br>
두 컴포넌트 모두<br>
담고있는 props 의 형태를 제외하고는 사용법이 동일하기 때문에<br> 상황에 맞는 컴포넌트를 사용할 수 있을것 같다.
<br>

단,<br>
`Section` 에 사용되는 `title` 을 render 하기 위해서는<br>
`renderSectionHeader` props 을 사용하여 렌더링 하여야 한다.

```JS
renderSectionHeader={({ section: { title } }) => <Text>{title}</Text>}
renderItem={({ item }) => <Text>{item.busNum}</Text>}
```

## Reference

> <https://reactnative.dev/docs/flatlist><br><https://reactnative.dev/docs/sectionlist><br><https://velog.io/@djaxornwkd12/React-Native-FlatList%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90><br><https://greatpapa.tistory.com/149>
