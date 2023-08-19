---
layout: post
title: "[React-Native] image 라이브러리를 사용하여 다른 사용자들의 프로필 이미지 관리하기 🌁"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, TIL]
---

## 개요

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyrEdJ%2FbtsrtguFacF%2Fa7BnffeF6M0dPUT74nVKkk%2Fimg.png)

다음과 같이 구현된 컴포넌트에<br>
등록된 사용자 프로필 이미지를 보여주려고 하는데,<br>
<br>
내 정보가 아닌,<br>
`FlatList` 로 구현된 다른 유저들의 정보에<br>
프로필 이미지를 관리하는 컴포넌트를 구현하고,<br>
프로필 이미지가 없는 경우<br>
파란 박스 안에 사용자 이름의 첫 글자를 가져와<br>
이미지 대신 넣어주는 기능을 구현하고자 한다.

---

### 이미지 컴포넌트 구현

등록된 이미지를 크게, 확대하여 볼 수 있도록<br>
`react-native-image-viewing` 라이브러리를 설치하여 적용하려고 한다.

![](https://blog.kakaocdn.net/dn/dcsFV9/btsrqEbZi7L/BsR12ktYX0blvB5G4oX77K/img.gif)

> <https://github.com/jobtoday/react-native-image-viewing>

<br>
#### Installation
---

```
yarn add react-native-image-viewing
```

or

```
npm install --save react-native-image-viewing
```

라이브러리를 설치 했다면,<br>
유저 프로필이미지를 관리하는 컴포넌트를 생성해준다.<br>

> 해당 컴포넌트는 `ChatScreen` 과 `HomeScreen` 에서 재사용 할 예정

---

#### Profile

> 정의하는 `Profile` 컴포넌트를 `UserPhoto` 컴포넌트에서 재사용한다.

```javascript
<TouchableOpacity disabled={onPress == null} onPress={onPress}>
  <View style={containerStyle}>
    {imageUrl ? (
      <image source={{ url: imageUrl }} style={imageStyle} />
    ) : text ? (
      <Text style={textStyle}>{text}</Text>
    ) : null}
  </View>
</TouchableOpacity>
```

`imageUrl` 이 있는 경우,<br>
기존의 이미지를 보여준다.<Br>
이미지가 없는 경우 텍스트가 있는지 확인하고,<br>
텍스트가 있다면 컴포넌트에 보여주고<br>
이미지와 텍스트 둘 다 없는 경우라면 `null` 을 보여주는 삼항연산자를 통한 조건이다.<br><Br>

---

### UserPhoto

#### Props

- 앞서 정의한 `Profile` 컴포넌트를 Props 로 불러와 재사용한다.

```javascript
return (
  <Profile
    size={size}
    style={style}
    imageUrl={imageUrl}
    onPress={() => {}}
    text={name?.[0].toUpperCase()} // 이름이 소문자일 경우 대문자로 치환
    textStyle={nameStyle}
  />
);
```

#### 미리보기 기능

- 이미지를 클릭(UserPhoto) 할 경우 미리보기 기능 구현

```javascript
import React, { useState } from "react";
import ImageView from "react-native-imageviewing";

const [viewerVisible, setViewrVisivle] = useState(false);
// imageUrl 이 있는경우 uri 에 imageUrl 을 넣어주고, 없으면 빈 array
const images = useMemo(
  () => (imageUrl != null ? [{ uri: imageUrl }] : []),
  [imageUrl]
);

return (
  <>
    <ImageView
      images={images}
      imageIndex={0}
      // 미리보기 상태의 유무
      visible={viewerVisible}
      // true 로 변경된 visible 을 false 로 변경 -> 이미지를 닫는 요청이 들어올 경우 setViewrVisible State 를 false 로 변경 -> (false 상태 이므로) ImageView 컴포넌트가 닫힘
      onRequestClose={() => setViewrVisible(false)}
    />
  </>
);
```

#### onPress

- 미리보기 onPress 함수

```javascript
import React, { useCallback } from "React";

const showImageViewer = useCallback(() => {
  setViewerVisible(true);
}, []);

return (
  <Profile
    size={size}
    style={style}
    imageUrl={imageUrl}
    onPress={showImageViewer}
    text={name?.[0].toUpperCase()} // 이름이 소문자일 경우 대문자로 치환
    textStyle={nameStyle}
  />
);
```

#### 예외처리

`images` 에 뭔가 들어있는 경우에만 실행 -> `showImageViewer`<br>
`images` 에 뭔가 들어있지 않은 경우 -> undefined

```javascript
onPress={images.length > 0 ? showImageViewer : undefined}
```

---

### HomeScreen

앞서 구현한 `UserPhoto` 컴포넌트를 `HomeScreen` 컴포넌트에 붙이는 과정이다.<br>

다른 유저들의 정보가 나열되어있는 `FlatList` 내부를 살펴보면,<br>
유저 이름과 이메일이 그려지는 영역이 있는데,<br>
해당 부분과 `UserPhoto` 의 영역을 분리하기 위해 `View` 요소로 감싸준다..

```javascript
<View>
  <Text style={styles.otherNameText}>{user.name}</Text>
  <Text style={styles.otherEmailText}>{user.email}</Text>
</View>
```

그리고, `UserPhoto` 컴포넌트를 `View` 요소 상단에 배치한다.<br>

```javascript
<Profile
  style={styles.userPhoto}
  onPress={user.profileUrl}
  imageUrl={user.name}
/>
```

각 위치에 `imageUrl`, `name` 파라미터를 전달 해 주면<br>
다음과 같이 화면에 각 요소들이 세로로 정렬된 모습을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfH5b4%2FbtsrvWYB4hv%2F429ughHb53bmWKFoWvjTI0%2Fimg.png)

분리한 `UserPhoto` 와 `View` 컴포넌트의 위치를 조정하기 위해
부모로 감싸져있는 `TouchableOpacity` 에 `style` 을 추가 해 준다.

```javascript
import { StyleSheet, View, Text, TouchableOpacity } from "react-native";

<TouchableOpacity
  style={styles.userListItem}
  onPress={() => {
    // 각각의 유저들만의 채팅창 구현을 위해 파라미터를 넘겨줌 => 타입으로 userId, other 지정
    navigate("Chat", {
      userIds: [me.userId, user.userId],
      other: user,
    });
  }}
>
  <UserPhoto
    style={styles.userPhoto}
    imageUrl={user.profileUrl}
    name={user.name}
  />
  <View>
    <Text style={styles.otherNameText}>{user.name}</Text>
    <Text style={styles.otherEmailText}>{user.email}</Text>
  </View>
</TouchableOpacity>;

export default HomeScreen;

const styles = StyleSheet.create({
  userListItem: {
    backgroundColor: Colors.LIGHT_GRAY,
    borderRadius: 12,
    padding: 20,
    flexDirection: "row",
    alignItems: "center",
  },
});
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQX1lr%2FbtsrrT9b1DB%2FoaKJfL0B7ovSumFxGsc58k%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmhcm6%2FbtsrDJqmoAV%2FSpyusr8rnpzCe4AKakbiek%2Fimg.png)

---

- 최종 코드

```javascript
import React, { useMemo, useState, useCallback } from "react";
import { StyleProp, TextStyle, ViewStyle } from "react-native";
import ImageView from "react-native-image-viewing";
import Profile from "../HomeScreen/Profile";

// Props 선언 -> Profile 이미지 등록할때와 동일
interface UserPhotoProps {
  size?: number;
  style?: StyleProp<ViewStyle>;
  imageUrl?: string;
  name?: string;
  nameStyle?: StyleProp<TextStyle>;
}

const UserPhoto = ({
  size = 48,
  style,
  imageUrl,
  name,
  nameStyle,
}: UserPhotoProps) => {
  // ImageView 를 보여줄지 말지에 대한 State
  const [viewerVisible, setViewrVisible] = useState(false);

  const images = useMemo(
    // imageUrl 이 있는 경우 uri 에 imageUrl 을 넣어주고 없는 경우 빈 배열
    () => (imageUrl != null ? [{ url: imageUrl }] : []),
    [imageUrl]
  );

  const showImageViewer = useCallback(() => {
    setViewrVisible(true);
  }, []);

  return (
    <>
      <Profile
        size={size}
        style={style}
        imageUrl={imageUrl}
        // 보여줄 이미지가 있을 경우 showImageViewer 함수를 실행하여 true 로 변경, 아닐경우 undefined -> 작동 x
        onPress={images.length > 0 ? showImageViewer : undefined}
        // User name 의 첫 글자 index 가져오기 -> UpperCase 로 소문자일 경우 대문자로 치환
        text={name?.[0].toUpperCase()}
        textStyle={nameStyle}
      />
      <ImageView
        images={images}
        imageIndex={0}
        visible={viewerVisible}
        // 닫는 요청이 들어올 경우 State 를 false 로 변경
        onRequestClose={() => setViewrVisible(false)}
      />
    </>
  );
};

export default UserPhoto;
```

> 이미지가 없을 경우,<br>
> 사용자가 지정한 **`name` 의 첫 글자를 가져오는 부분**은 아직 미 구현
