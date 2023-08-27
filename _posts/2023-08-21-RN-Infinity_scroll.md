---
layout: post
title: "[React-Native] 유튜브 API 를 활용하여 무한 스크롤 구현하기 (feat. A to Z )"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, 무한 스크롤, TIL]
---

## 개요 ⏰

이번 포스트는 유튜브 API 를 활용하여<br>
계속해서 렌더링되는 데이터들을 무한스크롤을 통해 `React-Native` 환경에서 구현 해 볼 예정이다.

![](https://blog.kakaocdn.net/dn/GjG7d/btsrH7erUmF/Qe95qRflyd3OxgEHO3Gxf0/img.gif)

---

### init 🌅

먼저 `/` 루트 경로에서 아래 명령을 실행하여 `React-Native` 프로젝트를 생성 해 준다.

```
npx react-native init [프로젝트명]
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FekVeDP%2FbtsrEznPH3b%2FD7Fg0LzhDyCSfbHyHy7zQK%2Fimg.png)

생성된 프로젝트는 `yarn` 혹은 `npm` 명령을 사용하여<br>
안드로이드 스튜디오 애뮬레이터를 통해 실행할 수 있다.

```
yarn run android

or

npm run android
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoAiO9%2FbtsrARDxqd9%2FV9CIqtaCsgxvIBJUTyQlp1%2Fimg.png)

> 초기 실행 시 앱을 애뮬레이터에 설치하는 과정이 존재하므로,<bR>
> 시간이 다소 소요될 수 있다.

---

### App.tsx 🚢

생성된 프로젝트를 실행하여 보면 아래와 같은 화면을 볼 수 있는데,<br>
이는 최 상위 부모 컴포넌트로 `App.tsx` 를 불러와 화면에 띄워주는 방식인데,<br>
별도의 컴포넌트를 생성하여 import 해 주는 방식으로 렌더링 하면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbnbrig%2FbtsrS392sVy%2F7Kn2gP7WP9bK0hiatkrBHk%2Fimg.png)

---

### Components 🚀

`/` 루트 경로에 `/src` 디렉토리를 생성하여 필요한 컴포넌트를 제작하려고한다.<br>

---

#### TypeListItem

컴포넌트를 제작하기에 앞서,<br>
클리이언트에서 사용할 데이터들의 타입을 먼저 선언해주려한다.

```javascript
// Type 정의
export type TypeListItem = {
    title: string // 제목 텍스트
    thumbnail: string // URL
    publishedAt: string // ex) "2022-06-15T12:31:57Z"
    viewCount: number // 조회수
    channelTitle: string // 채널명
}
```

---

#### ListItemView

함수형 컴포넌트`(FC)`를 제작하여 `item` 의 정보를 화면에 출력하는 컴포넌트이다.

```javascript
import React from "react";
import { TypeListItem } from "./TypeListItem";
import { Image, Text, View } from "react-native";

export const ListItemView: React.FC<{ item: TypeListItem }> = (props) => {
  return (
    <View>
      <Image style={{ height: 200 }} source={{ uri: props.item.thumbnail }} />
      <View
        style={{
          paddingHorizontal: 12,
          paddingVertical: 12,
          flexDirection: "column",
        }}
      >
        <Text style={{ fontSize: 16 }}>{props.item.title}</Text>
        <Text style={{ fontSize: 12 }}>
          {/* 특수문자 ' · ' */}
          {props.item.channelTitle} · 조회수 {props.item.viewCount} /{" · "}
          {props.item.publishedAt}
        </Text>
      </View>
    </View>
  );
};
```

> 인라인형태로 스타일을 지정한게 마크다운 문법에 적용이 되지 않는다.. 😭

`props` 를 매개변수로 받고,<br>
그 안에 정의된 `item` 은 `TypeListItem` 의 타입을 따른다.<br>

높이가 200 으로 고정된 `URI` 는,<br>
`props.item.thumbnail` 로 부터 이미지 URL 을 가져와 화면에 표시한다.

---

#### ListView (더미)

해당 컴포넌트는,<br>
더미데이터를 가진 배열을 `FlatList` 를 활용하여<br>
각 항목을 `ListItemView` 를 통해 렌더링하는 컴포넌트이다.

```javascript
import React, {useState} from 'react';
import {TypeListItem} from './TypeListItem';
import {FlatList} from 'react-native';
import {ListItemView} from './ListItemView';

export const ListView: React.FC = () => {
  const [list] = useState<TypeListItem[]>([
    {
      title: 'TITLE_01',
      thumbnail:
        'https://docs.expo.dev/static/images/tutorial/background-image.png',
      publishedAt: '2023-08-22',
      viewCount: 100,
      channelTitle: 'CHANNEL TITLE 01',
    },
    {
      title: 'TITLE_02',
      thumbnail:
        'https://docs.expo.dev/static/images/tutorial/background-image.png',
      publishedAt: '2023-08-22',
      viewCount: 200,
      channelTitle: 'CHANNEL TITLE 02',
    },
    {
      title: 'TITLE_03',
      thumbnail:
        'https://docs.expo.dev/static/images/tutorial/background-image.png',
      publishedAt: '2023-08-22',
      viewCount: 300,
      channelTitle: 'CHANNEL TITLE 03',
    },
  ]);

  return (
    <FlatList
      data={list}
      renderItem={({item}) => <ListItemView item={item} />}
    />
  );
};
```

`useState` 훅을 사용하여 `list` 의 상태를 초기화 한다.<br>
이 상태의 초기 값에는 `TypeListItem[]` 타입의 배열로, 목록에 표시할 데이터를 담고 있다.<br>
각 객체는 `title`, `thumbnail`, `publishedAt`, `viewCount`, `channelTitle` 속성을 가진다.<br>

`FlatList` 컴포넌트를 사용해서 정의한 데이터를 렌더링한다.<br>
`data` 에는 `FlatList` 가 렌더링 할 데이터(`list`) 를 지정한다.<bR>
`renderItem` 에는 각 아이템을 어떻게 렌더링 할 것인지를 지정하며,<br>
여기서는 `ListItemView` 컴포넌트를 사용한다.

---

#### App.tsx

불필요한 코드를 제거한 상태로 `SafeAreaView` 영역 내부에<bR>
더미 데이터가 담긴 `ListView` 컴포넌트를 불러온다.

```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 */

import React from "react";
import { SafeAreaView, StatusBar, useColorScheme } from "react-native";
import { Colors } from "react-native/Libraries/NewAppScreen";
import { ListView } from "./src/ListView";

function App(): JSX.Element {
  const isDarkMode = useColorScheme() === "dark";

  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };

  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={isDarkMode ? "light-content" : "dark-content"}
        backgroundColor={backgroundStyle.backgroundColor}
      />

      <ListView />
    </SafeAreaView>
  );
}

export default App;
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbqHXZo%2Fbtsr62QabnI%2FHelbl2noQrcRfuXkr0CjxK%2Fimg.png)

---

#### useData

Youtube API 를 사용하여,<br>
컴포넌트에 더미가 아닌 실제 데이터를 불러오기 위한 컴포넌트이다.<br>
`ListView` 컴포넌트에서 불러오는 더미데이터를 모두 지우고,<br>

```javascript
const { data, loadData } = useData();
```

해당 코드를 입력하여 실 데이터를 불러온다.

> `data` 와 `loadData` 는 커스텀 훅을 사용하여 가져옴 ❗️

`loadData` 는 `useEffect` 를 사용하여 호출하고, 의존성 배열에도 추가.

- ListView.tsx

```javascript
import React, { useEffect } from "react";
import { TypeListItem } from "./TypeListItem";
import { FlatList } from "react-native";
import { ListItemView } from "./ListItemView";
import { useData } from "./useData";

export const ListView: React.FC = () => {
  const { data, loadData } = useData();

  useEffect(() => {
    loadData();
  }, [loadData]);

  return (
    <FlatList
      data={data}
      renderItem={({ item }) => <ListItemView item={item} />}
    />
  );
};
```

- useData.ts

`axios` 라이브러리를 사용하여<br>
Youtube API 를 요청하고, 데이터를 화면에 보여주는 로직을 구현하려한다.

```
npm install axios or yarn add axios
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F50rdg%2FbtsrZjx5MoW%2FDmcQkT1jKLyOmz2uajMgv1%2Fimg.png)

> <https://console.cloud.google.com/apis/api/youtube.googleapis.com/metrics?hl=ko&project=test-467a4>

위 경로로 접근하여 `Youtube Data API v3` 를 사용할 수 있는 API 키 🔑 를 발급받는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb1ygWx%2Fbtssbj5E1R5%2FsK2se1LEO5rTYwoO065Mw0%2Fimg.png)

```javascript
import { useCallback, useState } from 'react'
import { TypeListItem } from './TypeListItem'
import axios from 'axios'

// 동일한 config 값 들을 가지고있는 axiosInstance
const axiosInstance = axios.create({
    baseURL: 'https://www.googleapis.com/youtube/v3/', // 주로 서버 URL == host
})

const API_KEY = 'api_key'

export const useData = () => {
    const [ data, setData ] = useState<TypeListItem[]>([])

    const loadData = useCallback(async() => {

        try {
            // baseURL 로 get 요청 => '/video' 엔드포인트로 요청, 파라미터로는 호출할 때 사용되는 config(매개변수) 값
            const videoResults = await axiosInstance.get<{
                kind: 'youtube#videoListResponse';
                etag: string;
                nextPageToken: string;
                prevPageToken: string;
                pageInfo: {
                  totalResults: number;
                  resultsPerPage: number;
                };
                items: {
                    kind: 'youtube#video';
                    etag: string;
                    id: string;
                    snippet: {
                      publishedAt: string;
                      channelId: string;
                      title: string;
                      description: string;
                      thumbnails: {
                        [key: string]: {
                          url: string;
                          width: number;
                          height: number;
                        };
                      };
                      channelTitle: string;
                      tags: string[];
                      categoryId: string;
                    };
                    contentDetails: {
                      duration: string;
                      dimension: string;
                      definition: string;
                      caption: string;
                      licensedContent: boolean;
                      regionRestriction: {
                        allowed: [string];
                        blocked: [string];
                      };
                      contentRating: {
                        mpaaRating: string;
                        tvpgRating: string;
                        bbfcRating: string;
                        chvrsRating: string;
                        eirinRating: string;
                        cbfcRating: string;
                        fmocRating: string;
                        icaaRating: string;
                        acbRating: string;
                        oflcRating: string;
                        fskRating: string;
                        kmrbRating: string;
                        djctqRating: string;
                        russiaRating: string;
                        rtcRating: string;
                        ytRating: string;
                      };
                    };
                    statistics: {
                      viewCount: number;
                      likeCount: number;
                      dislikeCount: number;
                      favoriteCount: number;
                      commentCount: number;
                    }
                }[]
            }>('/videos', {
                params: {
                    key: API_KEY,
                    part: 'snippet, contentDetails, statistics',
                    chart: 'mostPopular',
                    // 국가코드
                    regionCode: 'KR',
                },
            })

            const videoData = videoResults.data
            setData(videoData.items.map(( item ) => ({
                title: item.snippet.title,
                thumbnail: item.snippet.thumbnails.high.url,
                publishedAt: item.snippet.publishedAt,
                viewCount: item.statistics.viewCount,
                channelTitle: item.snippet.channelTitle,
            })))
        } catch(ex) {
            console.log(ex)
        }

    }, [])

    return {
        data,
        loadData,
    }
}
```

해당 API 를 사용하기 위해 `key` 값을 매개변수로 넘겨주고,<br>
필수 파라미터로 정의되어있는 `part` 를 같이 넘겨준다.<br>
필수로 넘겨주는 매개변수에는 여러 속성이 존재하는데,<br>
`snippet`, `contentDetails`, `statistics` 을 지정해준다.<br><br>

요청을 하게되면 데이터가 `EN` 으로 들어오기 때문에<br>
한국 데이터를 불러오기 위해 국가코드(`regionCode`) 를 지정해주었다.

---

#### ListView (최종)

`Custom Hook` 을 통해 데이터를 불러오고,<br>
`FlatList` 를 사용하여 데이터를 렌더링하는 컴포넌트이다.<br>
사용자가 스크롤을 하여 출력된 `ListItem` 목록의 끝에 도달하면 `loadMoreData` 함수가 호출된다.

```javascript
import React, { useEffect } from "react";
import { TypeListItem } from "./TypeListItem";
import { FlatList } from "react-native";
import { ListItemView } from "./ListItemView";
import { useData } from "./useData";

export const ListView: React.FC = () => {
  const { data, loadData, loadMoreData } = useData();

  useEffect(() => {
    loadData();
  }, [loadData]);

  return (
    <FlatList
      data={data}
      renderItem={({ item }) => <ListItemView item={item} />}
      onEndReached={loadMoreData}
      // 마지막에 가까운 지점
      onEndReachedThreshold={0.1}
    />
  );
};
```

`useData` 라는 `custom hook` 을 호출하여 각 인수들을 가져온다.<br>
`data` 는 목록에 표시할 데이터가 정의되어있고,<br>
`loadData` 는 데이터를 초기로 로드하는 함수이다.<br>
`loadMoreData` 는 이후 컴포넌트에서 정의할 함수인데,<br>
스크롤이 끝난 경우 새로운 데이터를 불러오는 로직이 담겨있는 함수이다.<br>

`useEffect` 훅을 사용하여,<br>
컴포넌트가 마운트 될 때 `loadData` 함수를 호출하여 초기 데이터를 로드한다.

`FlatList` 에는 데이터를 어떤 형태로 가져올 것인지 파라미터를 지정해주는데,<bR>
`data` 는 표시할 데이터,<br>
`renderItem` 은 각 항목을 어떻게 렌더링 할 것인지,<br>
`onEndReached` 는 목록의 끝에 도달했을 때 호출될 함수,<br>
`onEndReachedThreshold` 목록 끝에 얼마나 가까워야 `onEndReached` 함수가 호출될지 정하는 임계값 ? 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Frj0YO%2FbtssaANkIq3%2Fk2BtzvH7LEj96CkoIWK9qk%2Fimg.png)

---

### FIX 🔨

![](https://blog.kakaocdn.net/dn/bDopJe/btsr4YhnUm3/p8OImLbZsxwSe22KgvEJTK/img.gif)

다음과 같이 Youtube API 를 사용하여 실 데이터를 화면에 출력을 했지만,<br>
스크롤이 끝난 경우,<br>
계속되는 스크롤을 통해 새로운 데이터를 `reload` 하여 불러오는것을 목표로 했었다 💦<br><br>

하지만 위 이미지를 보면,<br>
스크롤이 끝난 경우 새로운 데이터를 불러오기는 하지만,<br>
이전 데이터를 지우고 새로운 데이터가 불러와 지는 형태로 구현이 되어있다.

---

#### Concat

`concat` 은 문자열이나 배열을 연결할 때 사용하는 함수이다.<br>
즉, `useData` 컴포넌트 내부에 정의되어있는<br>
실 데이터를 불러오는 `setData` State 에 `concat` 함수를 사용하여<br>
이전 데이터가 담긴 배열 뒤에 새로운 데이터 배열을 이어서 가져올 수 있도록 구현했다.

- Before

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnZphl%2FbtssgFBrL9P%2FRnB4FakAQIGNpam8Lc3CvK%2Fimg.png)

- After

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuhfWl%2Fbtssbi6JGgB%2FCwz7VkXZdElLzU4c9RhM2k%2Fimg.png)

![](https://blog.kakaocdn.net/dn/x36HD/btsr5YIqoHm/QYcFdzgce6nktRpuAkzWak/img.gif)
