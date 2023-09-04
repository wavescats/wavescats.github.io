---
layout: post
title: "[Typescript] 타입스크립트에서 메타마스크 연결하기 (Web3.js)"
subtitle: #부제목
categories: Typescript
tags: [리액트, 타입스크립트, 블록체인, Web3.js, TIL]
---

## 개요

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuuONN%2FbtssVNTzSZu%2F4FwMZ3ECgw0URLhYkqjj0K%2Fimg.png)

앞서 초기화하여 생성한 앱인,<br>
**`React` + `TypeScript`** 환경에서 해당 실습을 진행하려한다.<br>
타입스크립트를 사용하여 메타마스크를 연결하고자하는 이유는,<br>
메타마스크 같은 **외부 서비스를 연결할 때 오류의 가능성**을 줄이고,<br>
**코드의 안정성**과 **명확성을 향상**시키는데 목적을 둔다는 점에서 해당 포스팅을 시작하려한다.

---

### 설치

해당 라이브러리를 사용하기 위한 **패키지를 설치**한다.

```
npm install web3
```

or

```
yarn add web3
```

---

### custom Hook

- `useWeb3.ts`

해당 컴포넌트에서는 `MetaMask` 와 연결하는 로직을 담고있다.

```javascript
import { useEffect, useState } from 'react';
import Web3 from 'web3';

export const useWeb3 = () => {
  const [web3, setWeb3] = useState<Web3 | null>(null);
  const [accounts, setAccounts] = useState<string[]>([]);

  useEffect(() => {
    const init = async () => {
      // MetaMask 연결
      if (window.ethereum) {
        const web3Instance = new Web3(window.ethereum);
        try {
          // 계정 접근을 사용자에게 요청
          const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
          setAccounts(accounts);
          setWeb3(web3Instance);
        } catch (error) {
          console.error("User denied account access");
        }
      }
      // Legacy dapp browsers
      else if (window.web3) {
        setWeb3(new Web3(window.web3.currentProvider));
      }
      // Non-dapp browsers
      else {
        console.log('Non-Ethereum browser detected. You should consider trying MetaMask!');
      }
    };

    init();
  }, []);

  return { web3, accounts };
};
```

---

### App.tsx

- `App.tsx`

상위 컴포넌트에서 정의한 `Custom Hook` 을 `App.tsx` 에 import 하여 사용한다.

```javascript
import React from "react";
import { useWeb3 } from "./useWeb3";

const App: React.FC = () => {
  const { web3, accounts } = useWeb3();

  return (
    <div className="App">
      {web3 ? (
        <div>
          <h1>Connected to MetaMask</h1>
          <div>
            <strong>Accounts:</strong>
            {accounts.map((account, i) => (
              <div key={i}>{account}</div>
            ))}
          </div>
        </div>
      ) : (
        <div>
          <h1>Not Connected to MetaMask</h1>
        </div>
      )}
    </div>
  );
};

export default App;
```

---

### Error

`App.tsx` 의 코드를 살펴보면,<br>
`window` 를 사용한 `ethereum` 과 `web3` 객체에서 에러가 발생함을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFXyf4%2FbtssVHEVypi%2FjcZkRdSf4DJQhXolEeyITk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbC6xu7%2FbtssP8RBYMV%2F7MgF1WWiid6es9NUNA8Lk0%2Fimg.png)

#### Window 란 ?

`window` 객체란,<br>
웹 브라우저에서 윈도우를 나타내는 객체이다.<br>
이 객체는 웹 페이지에 대한 정보를 담고 있고, DOM 과도 연관이 있다.<br>
위에서 사용된 `'Window.ethereum'` 은 Ethereum 호환 브라우저에 주로 내장되어있는<br>
`Ethereum Provider` 이다.<br>
주로, 메타마스크와 같은 Web3 지갑이 이와 같은 형태를 제공한다.

> 단, 이 코드는 웹 브라우저 환경에서 실행되어야하며,<br>
> Ethereum 지갑 확장 프로그램(ex/ MetaMask 등) 이 설치되어 있어야 작동한다.

#### 인터페이스 정의 (`react-app-env.d.ts`)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdN05UP%2Fbtstbd39ZNJ%2FsPyfewKfX86EQLoIUvdLh0%2Fimg.png)

```javascript
/// <reference types="react-scripts" />

interface Window {
  ethereum: any;
  web3: any;
}
```

Window 라는 객체에 메타마스크를 설치하면 ethereum: any 라는 오브젝트가 생긴다.<br>
하지만,<br>
리액트에선 이걸 인식하지 못하므로 별도의 파일(환경변수를 관리하는)을 생성하여 지정해준다.

> TypeScript 로 init 할 경우 `react-app-env.d.ts` 파일이 자동 생성됨.

---

### 실행

![](https://blog.kakaocdn.net/dn/bdCTIE/btssVLBqMR4/WUsQ1hAp1306zcpck9lZh0/img.gif)

`useEffect` 훅을 사용하여 페이지가 렌더링 되자마자 `custom Hook` 이 실행되도록 작성했으므로,<br>
페이지를 새로고침 시 `window.ethereum` 객체가 실행된다.<br>

메타마스크를 확인하여 페이지와 연결된 상태의 지갑 주소를 확인 해 보면,<br>
화면에 출력된 주소와 동일함을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIfxiP%2Fbtss8iyn0J7%2FFVnK8CUeSYzrcLHhkk6ya0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F2wmyy%2Fbtss9kvX0EG%2FZkKCfmuIHcrwMkOFsbKKmk%2Fimg.png)

---

### Reference 🌊

> <https://blog.valist.io/how-to-connect-web3-js-to-metamask-in-2020-fee2b2edf58a><br><https://velog.io/@mjlee0326/React%EC%99%80-Web3%EC%9D%98-%EB%A7%8C%EB%82%A8><Br><https://velog.io/@pwh7121/window.ethereum%EC%9D%B4%EB%9E%80><br><https://www.inflearn.com/questions/528387/window-ethereum><Br><https://docs.metamask.io/wallet/how-to/get-started-building/set-up-dev-environment/#basic-considerations><br><https://velog.io/@schk9611/react-app-env.d.ts-%ED%8C%8C%EC%9D%BC%EC%9D%80-%EB%AC%B4%EC%8A%A8-%EC%97%AD%ED%95%A0%EC%9D%84-%ED%95%A0%EA%B9%8C><br><https://stackoverflow.com/questions/70961190/property-ethereum-does-not-exist-on-type-window-typeof-globalthis-error><br><https://wavescats.github.io/typescript/2022/06/06/ts0.html>
