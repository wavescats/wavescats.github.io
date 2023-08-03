---
layout: post
title: "[React-Native] image 라이브러리를 사용하여 프로필 이미지 등록하기 🌁"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, TIL]
---

## 개요 🌸

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVdOsl%2FbtsoiZXjbSF%2FtCgPWb3cAAf8g8oCbvVOHK%2Fimg.png)

다음과 같이 구현한 원형에<br>
유저를 구분하기 위해 프로필 이미지를 등록하려고 한다.

---

### 홈 컴포넌트 제작 🌱

```javascript
import React, { useCallback } from "react";
import { StyleSheet, TouchableOpacity } from "react-native";
import ImagePicker from "react-native-image-crop-picker";

const HomeScreen = () => {
  // Profile 클릭 시 authProvider 에서 가져온 updateProfileImage 함수 실행 => filepath 는 image 의 path
  const onPressProfile = useCallback(async () => {
    const image = await ImageCropPicker.openPicker({
      cropping: true,
      cropperCircleOverlay: true,
    });
    console.log("image", image);
    await updateProfileImage(image.path);
  }, [updateProfileImage]);

  return <TouchableOpacity style={styles.profile} onPress={onPressProfile} />;
};
export default HomeScreen;

const styles = StyleSheet.create({
  profile: {
    width: 48,
    height: 48,
    borderRadius: 48 / 2,
    backgroundColor: Colors.GRAY,
    marginRight: 10,
  },
});
```

`TouchableOpacity` 를 사용하여<br>
타원을 클릭 시 터치 효과를 낼 수 있는 기능을 붙였다.<br>
<br>
`useCallback` Hooks 를 사용하여<br>
타원을 클릭 시<br>
이벤트가 발생하도록 `onPress` 함수를 생성 해 준다.<br><br>

`onPressProfile` 함수에는,<br>
이미지를 선택할 수 있는 라이브러리인<br>
`react-native-image-crop-picker` 를 사용한다.

```
yarn add react-native-image-crop-picker
```

> <https://github.com/ivpusic/react-native-image-crop-picker>

---

#### Android 설정 🔮

`react-native-image-crop-picker` 라이브러리를 android 에서 build 하기 위해<br>
`android/app/build.gradle` 경로에서<br>
해당 부분을 추가 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaGaOa%2FbtspsGYodDk%2FUezLUtJ1EcCPfR20uEY0nk%2Fimg.png)

해당 모듈을 심어주었다면 패키지를 사용 할 준비가 됬다.

---

#### onPressProfile 👑

설치한 라이브러리를 가져와 `.openPicker` 메소드를 사용한다.<br>
`.openPicker` 메소드는 이미지나 동영상을 선택할 수 있는 메소드이다.<br>
파라미터 값으로는 cropping 옵션을 true 로 주어,<br>
사용자에게 선택한 이미지를 Crop 할 수 있는 기능을 부여한다.<br>
이 함수는 비동기적인 처리를 해야하므로 `async` `awiat` 으로 감싸<br>
해당 Promise 를 처리한다.

```javascript
const onPressProfile = useCallback(async () => {
  const image = await ImageCropPicker.openPicker({
    cropping: true,
  });
  console.log("image", image);
}, []);
```

---

### 실행 🏊

![](https://blog.kakaocdn.net/dn/62NSI/btspOAomdmQ/aiNGExY7b8tzctcAXoMF4k/img.gif)

위 onPress 함수를 정의하면 동영상처럼 콘솔창에 출력은 되지만,<br>
실제 이미지 영역에는 반영이 되지 않을것이다.<br>
`AuthContext` 를 통해 이미지를 실제로 반영하기위해<bR>
Firebase 에서 제공하는 firestore 를 사용하여 로직을 구현 해 보려한다.

---

#### AuthContext 💌

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcJlfDu%2FbtspxpI0uEk%2FUGzUO61Cx4NJYvXSOVW4mK%2Fimg.png)

프로필 이미지를 업데이트를 위한 빈 함수를 정의 해 주고,<br>
들어오는 값의 형태도 지정해준다.

---

#### AuthProvider 💬

- updateProfileImage

```javascript
const updateProfileImage = useCallback(
  async (filepath: string) => {
    const filename = _.last(filepath.split("/"));
    if (user == null) {
      throw new Error("User is undefined");
    }
    if (filename == null) {
      throw new Error("filename is undefined");
    }
    const storageFilepath = `users/${user.userId}/${filename}`;
    await storage().ref(storageFilepath).putFile(filepath);
    const url = await storage().ref(storageFilepath).getDownloadURL();
    await auth().currentUser?.updateProfile({ photoURL: url });
    await firestore().collection(Collections.USERS).doc(user.userId).update({
      profileUrl: url,
    });
  },
  [user]
);
```

먼저, `filepath` 를 살펴보자<br>

보통 파일의 경로를 보면 `aaa/bbb.png` 의 형태로 이루어져있기 때문에<br>
`split` 함수를 사용하여 배열 안의 마지막 파일을 가져와 사용할것이다.<br>
그리고, 이 배열의 값을 가져오기 위해 '\_' `lodash` 를 사용한다.<br>

```javascript
const filename = _.last(filepath.split("/"));
```

<br>

그렇다면,<br>
이미지 파일의 경로를 알아내 가져오는것 까지 완료했다.<br>
이제는, `firebase Stroage` 를 사용하여 가져온 이미지 데이터를 저장하여<br>
해당 사용자가 등록한 프로필 이미지를 DB 에서 꺼내 화면에 보여주면 될것같다.<br>

<Br>
`Storage` 에 저장할 경로를 지정 해 주어야 하는데,<br>
`users` 디렉토리 아래에,<br>
각각의 사용자들이 존재할것이므로 사용자별 디렉토리를 생성하고,<br>
그 유저의 정보를 관리하는 `user.userId` 라는 디렉토리를 만들어<br>
파일이 저장될 경로를 지정해준다.<br>
```javascript
// user 가 null 일 수 도있으니 null 일 경우 에러메세지 출력
if (user == null) {
      throw new Error("User is undefined");
    }
// 만약 filename 이 undefined 일 경우 잘못된 경우이기때문에 에러메세지 출력
if (filename == null) {
      throw new Error("filename is undefined");
    }
const storageFilepath = `users/${user.userId}/${filename}`;
```
<Br>
이 경로에 실제로 파일을 업로드하기위해 storage 를 불러온다.<br>
`ref` 에는 어디에 저장할 지 경로(path) 를 지정해준다.<br>
`putFile` 에는 Original Path -> Local FilePath<br>
이 또한 비동기 처리하여 await 으로 명령을 기다린다.

```javascript
await storage().ref(storageFilepath).putFile(filepath);
```

<br>
업로드한 파일을 유저프로필에 등록하는 로직이다.<br>
앞서 지정해준 `putFile` 에서 다운로드가능한 URL 을 추출해야하는데,<br>
Storage에서 Filepath 를 getDounloadURL 함수를 통해 추출하여 url 이라는 변수에 담아준다.

```javascript
const url = await storage().ref(storageFilepath).getDownloadURL();
```

이제는, 이 url 을 firebase 유저 프로필에 등록하고,<br>
DB 에도 반영할 수 있도록 해야한다.<br>
해당 로직은 이름을 업데이트 할 때와 동일하다.<br>
<br>
DB 의 경로로 접근하고,<br>
특정 필드만 업데이트하기 위해<br>
`setupdate` 가 아닌 `update` 함수로 profileUrl 을 지정해준다.

```javascript
// 프로필 등록
await auth().currentUser?.updateProfile({ photoURL: url });
// DB 저장
await firestore().collection(Collections.USERS).doc(user.userId).update({
      // 해당 url 은 처음에 들어왔을 경우 undefined 일 수도 있어
      // profileUrl? : string 으로 타입 정의
      profileUrl: url,
    });
  },
  // dependencies
  [user]
```

이제 정의한 `updateProfileImage` 함수를<br>
`onPressProfile` 함수에서 버튼을 눌럿을 경우 실행되도록 이벤트를 걸어주면 끝이다 !

```javascript
// Profile 클릭 시 authProvider 에서 가져온 updateProfileImage 함수 실행 => filepath 는 image 의 path
const onPressProfile = useCallback(async () => {
  const image = await ImageCropPicker.openPicker({
    cropping: true,
    cropperCircleOverlay: true,
  });
  console.log("image", image);
  await updateProfileImage(image.path);
}, [updateProfileImage]);
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrZRUU%2FbtspRhwNb0R%2Fn3AIKryqAj3XeLKAJfYdRk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcrANPe%2Fbtsp0SJelDY%2FCks5KLGFZakNMhB4LBMP50%2Fimg.png)

---

### 프로필 컴포넌트 제작 🌱

```javascript
// 프로필 이미지를 담당하는 컴포넌트
import React, {useMemo} from 'react';
import {
  StyleSheet,
  StyleProp,
  ViewStyle,
  TouchableOpacity,
  View,
  Image,
  ImageStyle,
  TextStyle,
  Text,
} from 'react-native';
import Colors from '../modules/Colors';

// 재사용을 위한 Props Optional
interface ProfileProps {
  // 프로필 이미지의 크기
  size?: number;
  // 외부에서 프로필 이미지의 스타일을 변경하게 용이하도록
  style?: StyleProp<ViewStyle>;
  // 프로필을 눌럿을때의 이벤트
  onPress?: () => void;
  imageUrl?: string;
  text?: string;
  textStyle?: StyleProp<TextStyle>;
}

const Profile = ({
  size = 48,
  style: containerStyleProp,
  onPress,
  imageUrl,
  text,
  textStyle,
}: ProfileProps) => {
  const containerStyle = useMemo<StyleProp<ViewStyle>>(() => {
    return [
      // 자체 스타일 container
      styles.container,
      // size 의 값이 변경 될 경우 아래 지정한 값으로 덮어쓰기 => 프로필 원 의 크기 영역
      {width: size, height: size, borderRadius: size / 2},
      containerStyleProp,
    ];
  }, [containerStyleProp, size]);

  const imageStyle = useMemo<StyleProp<ImageStyle>>(
    () => ({width: size, height: size}),
    [size],
  );
  return (
    // onPress 가 넘어오지 않을 경우 버튼이 활성화 되지 않게 disabled
    <TouchableOpacity disabled={onPress == null} onPress={onPress}>
      {/* 프로필 영역을 그려주는 View */}
      <View style={containerStyle}>
        {/* imageUrl 이 있는 경우 Image 컴포넌트를 그려줌 */}
        {/* {imageUrl && <Image source={{uri: imageUrl}} style={imageStyle} />} */}
        {/* imageUrl 이 없는 경우 Text 컴포넌트를 그리고, 아무것도 없는 경우 null */}
        {imageUrl ? (
          <Image source={{uri: imageUrl}} style={imageStyle} />
        ) : text ? (
          <Text style={textStyle}>{text}</Text>
        ) : null}
      </View>
    </TouchableOpacity>
  );
};

export default Profile;

const styles = StyleSheet.create({
  container: {
    backgroundColor: Colors.GRAY,
    overflow: 'hidden',
  },
});
```

![](https://blog.kakaocdn.net/dn/62NSI/btspOAomdmQ/aiNGExY7b8tzctcAXoMF4k/img.gif)

> 일부 과정이 생략되어있음.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ftk3E2%2FbtspVpVo5P8%2FkMly5Mp0KjWgxbZiKw3wyK%2Fimg.png)

컴포넌트를 그려 `TouchableOpacity` 대신 `Profile` 을 넣고,<br>
`imageUrl`에 `profileUrl`을 넣어 받는다.
