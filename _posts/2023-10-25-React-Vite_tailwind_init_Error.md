---
layout: post
title: "[React] 리액트 + Vite 앱에 TailwindCSS 적용하기 🌈"
subtitle: #부제목
categories: React
tags: [리액트, TIL, Error]
---

## 개요 🗽

**`Tailwind CSS`**는,<br>
많은 웹 개발자 및 디자이너에게 인기 있는 CSS 프레임워크 중 하나로<br>
내가 주로 사용하던 **`Styled-Components`** 와 함께,<br>
**`Tailwind`** 에도 익숙함을 가질 수 있도록 적용하는 중 이다.<br>
두 CSS 프레임워크의 장점은, 컴포넌트를 기반으로 설계하여<Br>
가독성과 유지보수 측면에서 우수하다 판단되어 주로 채택하여 사용하고 있다.<br>
**`Vite`** 로 설치한 **`React`** 앱 에서는 **`Tailwind`** 를 별도로 **`init`** 해 주어야 적용이 되므로,<br>
해당 포스팅 에서는 위 과정을 진행하며 마주친 에러와 함께 정리하려고 한다.

---

## init 📜

```
npm install tailwindcss postcss autoprefixer
```

```
yarn add tailwindcss postcss autoprefixer
```

> <https://tailwindcss.com/docs/guides/vite>

공식 문서를 참조하여 **`Vite`** 용 **`tailwind CSS`** 를 install 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbrz3Da%2Fbtsy9hHyjVy%2Fm5TJMfSXkcailMepPzFjfk%2Fimg.png)

---

설치가 완료 되었다면,<br>
프로젝트 루트 디렉토리에 **`tailwind.config.js`** 파일을 생성하고,<br>
필요한 구성을 다음과 같이 추가 해 준다.

```
npx tailwindcss init -p
```

```
yarn run tailwindcss init -p
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtVZeA%2Fbtsy9MtMQVs%2FEG63LyO6X0jaKjUqJhDRPk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcZTiVa%2FbtszbuGpu45%2FRkw6vUkt1cByT0uvJLwun0%2Fimg.png)

```
/** @type {import('tailwindcss').Config} */
export default {
    content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
    theme: {
        extend: {},
    },
    plugins: [],
};

```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHvzp0%2Fbtsy9RhByig%2FKAAztQTvmrIcyk12EA3Iq1%2Fimg.png)

> **`jsx`** 형식의 컴포넌트를 사용한다면<br>**`"./src/**/\*.jsx"`\*\* 를 추가 해 주면 된다.

---

리액트 앱을 생성할 때 같이 생성된,<br>
루트 디렉토리 **`index.css`** 파일에 포함되어있는 스타일을 모두 지우고,<br>
**`Tailwind CSS`** 를 가져온다.

```
/* index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdb71ZY%2FbtszdpdEiVU%2FHfxcqA0kxtANySrGjCUbM0%2Fimg.png)

---

**`Vite`** 설정 파일인 **`vite.config.js`** 에서 CSS 를 불러오도록 수정 해 준다.

```
// vite.config.js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  css: {
    postcss: {
      plugins: [require('tailwindcss'), require('autoprefixer')],
    },
  },
})
```

이제 모든 설정이 끝났으므로,<br>
실제 **`HTML Elements`** 에 **`ClassName`** 을 추가하여 **`Tailwind CSS`** 를 적용 해 보자.

> 모든 설정이 끝났다면,<br>실행중이던 앱을 종료 후 재 시작 해 주는것이 좋다.

---

### Error 🚫

이 에러는 **`index.css`** 에<br>
**`Tailwind`** 모듈을 import 해 주지 않을 경우 발생하는 에러이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPiUIn%2FbtszbwqKBDR%2F5rBaIemt7eKgPrRP4OUNy1%2Fimg.png)

위에 정의하는 부분을 완료 했다면 해당 에러는 해결 될 것이다.

---

#### vite-plugin-windicss 🚧

모든 설정이 끝나고, 앱을 재 실행 하니 에러가 발생했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcwdm5L%2FbtszcG7gjyf%2Fp91yrfzKgH9vsAKNWALi90%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbzb49i%2Fbtsy7PZnfiT%2FHpYdMtkf7Yc4atc8Hp0IW0%2Fimg.png)

이 두 에러는,<br>
주로 **`Vite`** 앱에서 **`Tailwind CSS`** 를 적용하여 사용할 때 발생하는 에러라고 한다.

**`vite.config.js`** 를 열어 기존의 코드를 아래와 같이 수정 해 준다.

```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import WindiCSS from "vite-plugin-windicss";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react(), WindiCSS()],
});
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbwwj7C%2FbtszbSAkUSc%2FpEux9XNA6sipMxEpT9pYK1%2Fimg.png)

코드를 저장하고 다시 앱을 실행 해 보면, 두 번째 에러가 발생할 것이다.<br>
**`vite-plugin-windicss`** 를 설치 해 주면 된다.

```
yarn add vite-plugin-windicss
```

```
npm install vite-plugin-windicss
```

> **`vite-plugin-windicss`** 는,<br>**`Tailwind CSS`** 와 함께 사용되는 **`Vite`** 용 플러그인이다.

---

## 결과 🌅

아래와 같이 **`<div>`** 태그 안에 **`className`** 옵션을 부여하여<br>
**`Tailwind`** 에서 지정한 스타일 속성을 추가하면 정상적으로 적용 됨을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcddOlX%2Fbtszb24mMb5%2FAVInHiljT1kpy1YzslxkRK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcuI9on%2FbtszcHeEx0Z%2FGKJjJIjMdPhr9dErGf7fEk%2Fimg.png)

---

## Reference 🌊

> <https://tailwindcss.com/docs/guides/vite><br><https://youtu.be/fUXQXafPF1A?si=X45TZ3BN8IDbESdu><br><https://xionwcfm.tistory.com/277><br><https://www.padosum.dev/wiki/Setup-Tailwind-CSS-in-React-with-Vite/>
