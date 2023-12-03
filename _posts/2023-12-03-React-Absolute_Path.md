---
layout: post
title: "[Typescript] React + Typescript + Vite 환경에서 절대경로 설정하기 (Feat. pNpM) 🤞"
subtitle: #부제목
categories: [Typescript]
tags: [리액트, 타입스크립트, TIL]
---

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FldhvU%2FbtsBjBp0HSJ%2F9HBpoSCB9I7tXmbyfyOGs0%2Fimg.png)

## 개요 🔔

프로젝트를 진행하다 보면,<br>
아래와 같이 경로가 점점 깊어지는 현상을 겪었던 적이 있을 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbf5GwX%2FbtsBh4UlnAj%2FsjvtxWsKFzTkhhUHgNpfM1%2Fimg.png)

현재는 단 두 **`deps`** 만의 경로를 불러오고 있지만,<br>
만약 뎁스가 깊어지고, 디렉토리가 다양해진다면 **`../../../../../........`** 의 형태와 같이<br>
복잡하고 가독성이 떨어지는 형태로 구현이 될 것이다.<br>

이를 해결하기 위해 아래와 같이 절대경로(**`@`**) 를 설정하는 방법을 이번 포스팅에 정리하고자 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdU8SC%2FbtsBgwDmMKS%2FyKLckwRkukvsSxEKk9Pal1%2Fimg.png)

---

## vite.config.ts ⚡

만약, 자바스크립트 환경으로 **`vite`** 앱을 생성했다면,<br>
**`vite.config.js`** 파일에만 옵션을 설정 해 주면 간단히 절대경로를 설정할 수 있다.

```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import path from "path";

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: [
      { find: "@", replacement: path.resolve(__dirname, "src") },
      {
        find: "@components",
        replacement: path.resolve(__dirname, "src/components"),
      },
    ],
  },
});
```

**`resolve`** 하위에 **`alias`** 라는 배열안에 객체의 형태로<br>
**`find`** 에는 **절대 경로**의 별칭을,<br>
**`replacement`** 에는 **해당 절대 경로**를 입력하면 된다.

---

### Error 🚫

**`path`** 를 지정하기 위해 **`path`** 를 **`import`** 하고,<br>
**`__dirname`** 을 사용했는데 아래 에러가 발생했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fp3hGb%2FbtsBjrgKJ4g%2FmxxOTZCHLftsU6mBbvDaC1%2Fimg.png)

이 에러는 먼저 에러 메세지를 살펴보면,<br>
**`path`** 를 사용하기 위해 작성한 **`require`** 문에서 발생한 에러이다.

> 타입스크립트는 에러와 함께 필요한 종속성들을 안내 해 준다.. 😆🙏

해당 패키지를 설치 해 주어 에러를 해결할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbe23t8%2FbtsBjpJYvhC%2FmytuTolUXNeBRdIbxBwIBK%2Fimg.png)

> Require statement not part of import statement.eslint@typescript-eslint/no-var-requires

그리고 위 에러는,<br>
**`import`** 형식이 아닌 **`require`** 문을 사용하여 **`path`** 를 불러오고 있는데,
이는, **`ESLint`** 의 **`Typescript`** 플러그인이 **`CommonJS`** 형식의 **`require`** 문을 허용하지 않기 때문에 발생한 문제이다.

**`ESLint`** 의 타입스크립트 규칙은 일반적으로 **`ES 모듈`** 형식을 지향하기에,<br>
**`require`** 문의 사용 보다는 **`import`** 문을 사용하는 것을 권장한다.

하지만..🤦‍♂️<br>
개발자라면 발생한 에러나 경고를 모름지기 해쳐나가는 것을 즐겨야 하지 않는가..😎

> /_ eslint-disable @typescript-eslint/no-var-requires _/

위 주석을 **`vite.config.ts`** 최 상단에 넣어주면,<br>
해당 파일에서만 **`no-var-requires`** 규칙이 비활성화되어 경고가 발생하지 않고 무시할 수 있다.<br>
즉, **`import`** 방식이 아닌 **`require`** 문을 사용할 수 있다는 것이다.

---

### \_\_dirname ❔

**`__dirname`** 이란,<br>
자바스크립트에서 정의된 변수에 붙여 사용할 수 있는<br>
**`diretory`** 와 **`name`** 의 합성어 이다.

현재 파일이 위치한 폴더 (**`directory`**) 의 절대경로(**`absolute path`**) 를 알려준다.

> **`process.cwd()`** 는 👉 항상 프로젝트 폴더(**`directory`**) 를 반환한다.<br>**`__dirname`**은 👉 현재 파일명을 알려준다.

---

## tsconfig.ts 🔮

하지만, 이번에 진행하는 프로젝트는 **`Typescript`** 환경이므로,<br>
**`tsconfig.json`**, **`vite.config.ts`** 두 파일에 옵션을 추가 해 주어야 한다.

- **tsconfig.json**

```javascript
{
  "compilerOptions": {
    ...
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
      "@components/*": ["src/components/*"],
      "@pages/*": ["src/pages/*"],
    }
    ...
  },
  "include": ["src", "**/*.ts", "**/*.tsx"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

> **`paths`** 속성을 타입스크립트에서 사용하기 위해서는,<br>**`@types/node`** 패키지를 설치 해 주어야 한다.

**`baseUrl`** 속성에는 기본(**`default`**) 경로를 설정하고,<br>
**`paths`** 속성에는 절대경로를 지정하고 싶은 경로들을 **`"별칭": "경로"`** 순으로 지정 해 주면 된다.

**`baseUrl`** 을 어떻게 설정하냐에 따라 **`path`** 속성의 경로를 적용할 수 있다.

```javascript
"baseUrl": "src",
"paths": {
  "@/*": ["*"],
  "@pages/*": ["pages/*"],
  "@components/*":["components/*"]
}
```

> 👉 **`baseUrl`** 을 **`scr`** 로 지정 해 주었을 때의 **`paths`** 경로

---

### 절대경로와 상대경로 🆚

```javascript
// 절대 경로
import ExampleComponent from "@/src/ExampleComponent";

// 상대 경로
import ExampleComponent from "./src/ExampleComponent";
```

---

## What is pNpM ❓

<https://bit.ly/4a713Xo>

---

## Reference 🌊

> <https://nodejs.org/api/path.html><br><https://stackoverflow.com/questions/41553291/can-you-import-nodes-path-module-using-import-path-from-path><br><https://www.daleseo.com/js-node-path/><br><https://gigibean.tistory.com/72><br><https://shape-coding.tistory.com/entry/Vite-TypeScript-Vite-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-%EC%A0%88%EB%8C%80-%EA%B2%BD%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0><br><https://engineering.ab180.co/stories/yarn-to-pnpm>
