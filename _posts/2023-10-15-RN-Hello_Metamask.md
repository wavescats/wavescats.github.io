---
layout: post
title: "[React-Native] Expo 앱에서 MetaMask 연결 구현하기 🐺"
subtitle: #부제목
categories: [React-Native]
tags: [리액트 네이티브, 블록체인, MetaMask, TIL]
---

## 개요 ☁️

블록체인을 공부하며 얻은 정보로는,<br>
웹 브라우저 (리액트 등) 에서는 Web3 에 대한 자료가 **비교적 풍부**하다.<br>
하지만,<br>
모바일 환경 (RN, Native 등) 에서는 **상대적으로 적은 편** 이라는 것 이다. <br>
해당 포스팅 에서는 내가 생각하는 Dapp 의 기초인 **Wallet Connect** 를 구현하는 과정을 적어보려한다.

---

### init 🔥

해당 과정을 따라가기에 앞서 **React-Native expo** 앱을 생성 해 준다.

```
npx create-expo-app -t expo-template-blank-typescript
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmH34Y%2Fbtsyy9Wpwhu%2FnN3mw9x5xVSvsMsMhT1H70%2Fimg.png)

생성한 앱의 경로로 이동하여 `ls` 명령어로 파일구조를 확인 해 보면,<br>
`./node_modules` 가 존재하지 않기 때문에<br>
`npm install` 명령으로 필요 패키지들을 설치 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctcLVz%2FbtsywiMUVEz%2FzkVyT83RSrKanacUulgxo1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Feuluma%2FbtsyteSeyGC%2FAkxw3soK015sO6iWeIl250%2Fimg.png)

> **Expo 앱을 사용하여 구현하는 이유는,**<br>
> 개발환경은 Window 이지만 디바이스는 ios 를 사용하고 있기 때문이다.<br>
> 물론, 애뮬레이터를 사용하여 Android 로 빌드 할 수도 있겠지만<bR>
> 개발환경의 성능 이슈로 인해 Expo 앱으로 채택하여 진행한다.

설치가 모두 끝났다면,<br>
`npm start` 명령으로 생성한 Expo 앱을 실행 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcxV93q%2FbtsywvFq8Ji%2Fwo8B5SWhTLbW4GJnS3FwpK%2Fimg.png)

디바이스의 카메라로 해당 QR 코드를 인식하여 Expo 앱을 개발환경과 연동 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwAFtE%2Fbtsytd0oW4F%2Ft6O6K0Li6UTgX4mcUTaK11%2Fimg.png)

---

### Wellet Connect 🌷

> <https://walletconnect.com/>

해당 사이트에 접속하여 대시보드를 누르면 메타마스크 연결을 통해 로그인 할 수 있다.<bR>

대시보드에 접근하여 새로운 프로젝트를 생성 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckRdR3%2Fbtsyt9W9RxV%2FmdXbbkpPFtzRwyTbZl8Y8k%2Fimg.png)

생성한 프로젝트를 보면,<br>
Project ID 가 있는데 이 키는 React-Native 앱과 지갑 연결을 구현할 때 필요하므로 저장 해 놓는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FojQVt%2FbtsyucGmVB3%2FAStbNksgzJcSG0Stu8Oh0k%2Fimg.png)

> <https://docs.metamask.io/wallet/how-to/connect/set-up-sdk/javascript/react-native/>

실제 메타마스크 공식문서를 살펴보면,<br>
React-Native 앱에서 메타마스크 SDK 를 사용할 수 있는 패키지가 출시 전 이라 위와 같은 과정으로 진행한다.

---

### install 🔮

이벤트를 실행시킬 때 Wallet Connect 모달 창을 표시하기 위해 해당 라이브러리를 설치 해 준다.

```
npx expo install @walletconnect/modal-react-native
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbA9LuB%2FbtsytRCwjRD%2Fu1PhUKfwkDvFOGh6c7xRHk%2Fimg.png)

해당 라이브러리를 통해 화면에 보여지는 모달 창은,<br>
구현된 코드에서 사용자에게 지갑 연결 및 연결 해제를 위한 UI 를 그려준다.<br>
옵션으로<br>
`explorerRecommendedWalletIds`, <br>
`explorerExcludedWalletIds`, <Br>
`projectId`, <br>
`providerMetadata` 를 받는다.<br>

- `explorerRecommendedWalletIds` : 추천하는 지갑 식별자 배열로 사용자에게 모달을 통해 표현된다.<br>
- `explorerExcludedWalletIds` : 모달에서 표시되지 않는 지갑의 식별자를 지정한다.<br>
  `ALL` 로 지정 시 모든 지갑이 표시되지 않는다.<br>
- `projectId` : Wallet Connect 프로젝트 식별자<br>
- `providerMetadata` : 지갑에 대한 정보를 포함하는 객체로 이름, 설명, URL 및 아이콘 정보를 담을 수 있다.

---

다음은 React-Native 환경에서 Wallet Connect 를 구현하기 위해 필요한 부가적인 라이브러리들이다.

```
npx expo install
@react-native-async-storage/async-storage
react-native-get-random-values
react-native-modal
react-native-svg
```

각 라이브러리들은,<br>

- 비동기 스토리지와 데이터를 처리하기 위한 라이브러리로, 앱 데이터를 로컬 스토리지에 저장할 때 사용한다.<br>
- 보안을 위하여 암호화된 난수를 생성하는 라이브러리이다.<br>
- 모달 창을 통해 팝업, 경고창 등을 화면에 출력하기 위한 라이브러리다.<br>
- SVG 이미지를 React-Native 앱에서 렌더링 할 때 사용되는 라이브러리이다.<br>

> SVG 형식의 이미지는 화면 크기에 맞게 확대 및 축소에 용이하여 다양한 해상도와 크기에 적합하다.

---

### 코드 구현 💻

> <https://walletconnect.com/>

앞서 복사 해 둔 Project ID 를 변수에 담아 불러온다.

```javascript
const projectId = "[Project ID]";
```

WalletConnect 라이브러리를 초기화할 때 사용되는 데이터를 포함하는 객체로,<br>
아래 정의된 객체는 템플릿 데이터이다.

```javascript
const providerMetadata = {
  name: "YOUR_PROJECT_NAME",
  description: "YOUR_PROJECT_DESCRIPTION",
  url: "https://your-project-website.com/",
  icons: ["https://your-project-logo.com/"],
  redirect: {
    native: "YOUR_APP_SCHEME://",
    universal: "YOUR_APP_UNIVERSAL_LINK.com",
  },
};
```

---

`useWalletConnectModal` 훅에서 현재 Wallet Connect 와 관련된 정보를 가져온다.<br>

```javascript
const { open, isConnected, address, provider } = useWalletConnectModal();
```

`onClick` 이벤트를 실행할 함수를 생성한다.<br>
이 함수는 비동기적으로 버튼이 눌렸을 경우 실행되며,<br>
Wallet 에 연결하려고 할 때 호출된다.<br>
이미 연결되어 있는 경우 `provider?.disconnect()` 를 호출하여 현재 연결을 끊는다.<br>

그렇지 않은 경우, (false) <br>
`open()` 함수를 호출하여 Wallet Connect 모달을 실행한다.

```javascript
const handleButtonPress = async () => {
  if (isConnected) {
    return provider?.disconnect();
  }
  return open();
};
```

화면에 보여지는 부분을 간단하게 나타내보도록 하자.<br>

`{isConnected ? address : "No Wallet Connected"}`<br>
지갑 연결 상태에 따른 텍스트를 출력하는 부분으로,<br>
`isConnected` 가 true 일 경우 연결된 지갑의 주소를 출력하고,<br>
그렇지 않을 경우 No Wallet Connected 를 출력한다.

```javascript
return (
  <View style={styles.container}>
    <Text style={styles.heading}>WalletConnect</Text>
    <Text>{isConnected ? address : "No Wallet Connected"}</Text>
    <Pressable onPress={handleButtonPress} style={styles.pressableMargin}>
      <Text>{isConnected ? "Disconnect" : "Connect"}</Text>
    </Pressable>
    <WalletConnectModal
      explorerRecommendedWalletIds={[
        "c57ca95b47569778a828d19178114f4db188b89b763c899ba0be274e97267d96",
      ]}
      explorerExcludedWalletIds={"ALL"}
      projectId={projectId}
      providerMetadata={providerMetadata}
    />
  </View>
);
```

## 전체 코드 🔐

```javascript
import { StyleSheet, Text, View, Pressable } from "react-native";
import {
  WalletConnectModal,
  useWalletConnectModal,
} from "@walletconnect/modal-react-native";

const projectId = "[Project ID]";

const providerMetadata = {
  name: "",
  description: "",
  url: "",
  icons: [""],
  redirect: {
    native: "",
    universal: "",
  },
};

export default function App() {
  const { open, isConnected, address, provider } = useWalletConnectModal();

  const handleButtonPress = async () => {
    if (isConnected) {
      return provider?.disconnect();
    }
    return open();
  };

  return (
    <View style={styles.container}>
      <Text style={styles.heading}>WalletConnect</Text>
      <Text>{isConnected ? address : "No Wallet Connected"}</Text>
      <Pressable onPress={handleButtonPress} style={styles.pressableMargin}>
        <Text>{isConnected ? "Disconnect" : "Connect"}</Text>
      </Pressable>
      <WalletConnectModal
        explorerRecommendedWalletIds={[
          "c57ca95b47569778a828d19178114f4db188b89b763c899ba0be274e97267d96",
        ]}
        explorerExcludedWalletIds={"ALL"}
        projectId={projectId}
        providerMetadata={providerMetadata}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
  heading: {
    fontSize: 18,
    fontWeight: "bold",
    marginBottom: 16,
  },
  pressableMargin: {
    marginTop: 16,
  },
});
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaSRw4%2FbtsytcAutvb%2FRQzWoZVrtIxSsWmMwktzWK%2Fimg.png)

![](https://blog.kakaocdn.net/dn/ouoOl/btsyHpZ4MG0/IWzDrxKk8P0kKAKvPd1wb1/img.gif)

---

### Error ❌

만약,<br>
모든 코드를 작성하고 앱을 실행시킨 경우 아래 에러가 발생한다면,<br>
추가적으로 해당 라이브러리를 설치 해 주면 에러가 없이 정상적으로 실행이 될 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FciHl3w%2Fbtsytgo1lKS%2FULqPZ1pbl33BqCYO7S00l1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FddQx2s%2Fbtsys6mGVzm%2FiW81VKvAVaDpn2C3HoT6Tk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fx1E6D%2FbtsyssDsMLH%2FKGc9nnsIcAeMmA1T1A17TK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcV3cst%2Fbtsywjryl7z%2Fz3NhXczgzwjAL5kyVLsk00%2Fimg.png)

---

## Reference 🌊

> <https://cloud.walletconnect.com/><br><https://docs.metamask.io/wallet/how-to/connect/set-up-sdk/javascript/react-native/><br>
