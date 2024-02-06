---
layout: post
title: "[React-Native] Expo 프로젝트에 Tailwind CSS 적용하기 🎫"
subtitle: #부제목
categories: React-Native
tags: [리액트 네이티브, expo, TIL, TailwindCSS]
---

## 개요 👂

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fm01YE%2FbtsEy1SylqE%2FgyzobxRONhaZSouC56dOC1%2Fimg.png)

해당 포스팅에서는,<br>
요즘 유의깊게 살펴보고 있는 **`Vercel`** 팀에서 채택한 **`Tailwind CSS`** 를<br>
**`React-Native`** 환경에서 어떻게 적용하고, 그 이유에 대해 정리 해 보고자 한다.

---

### Why Tailwind ❓

사실 이전 프로젝트에서는 거의 모든 스타일을 `Tailwind CSS` 를 적용하여 작성 했는데,<br>
요즘들어 **`Styled-Components`** 나 **`Panda CSS`** 등을 사용했던 것 같다.

**`Tailwind CSS`** 를 주로 사용하는 이유는 아래와 같다.

> <https://www.nativewind.dev/core-concepts/tailwindcss>

공식 문서에도 있듯,<br>
1️⃣ **유틸리티 클래스를 사용하여 `HTML` 에 직접 요소의 스타일을 지정할 수 있다.**

- 이를 통해 클래스 **이름을 추상화 하기 위해 시멘틱하게 정할 때 소요되는 리소스**가 줄어든다.

<br>
2️⃣ **스타일 재사용을 통해 중복을 관리하고, 재사용 가능한 추상화를 생성한다.**

- **사전에 정의된 모듈을 불러와 사용**함으로 인해 빌드 시 발생하는 리소스 낭비를 줄일 수 있다.<br>
  중복되어 작성된 비 효율적인 속성을 **루프하여 관리**할 수 있다.
  > <https://tailwindcss.com/docs/reusing-styles>

<br>
3️⃣ **커스텀 스타일 적용 가능.**

- 사전에 정의되어있는 스타일을 불러와 사용하지만, 종종 예외의 상황이 발생할 경우가 존재한다.<br>
  이를 해결하기 위해 **`theme`** 섹션에 **커스텀된 속성을 부여하여 사용**할 수 있다.

---

## init 💫

> <https://www.nativewind.dev/quick-starts/expo>

먼저,<br>
**`React-Native`** 환경에서 **`Tailwind CSS`** 를 사용하려면,<br>
**`NativeWind`** 라는 라이브러리가 필요하다.

이는 **`React-Native`** 커뮤니티에 불어온 혁명같은 바람이었으며,<br>
기존에 존재했던 **`Tailwind CSS`** 의 강력한 기능을 앱 개발에 도입함으로 인해<br>
유의미한 영향이 끼쳤다고 본다.

설치 방법은 공식 문서에도 있지만, 매우 간단하다.

```
yarn add nativewind
yarn add --dev tailwindcss
```

> 패키지 매니저로 **`yarn`** 을 사용했지만 **`npm`** 도 무관하다.<br>단, **`pnpm`** 은 **`ios`** 빌드 시 에러가 발생하므로 권장하지 않는다.<br>👉 **`React-Native`** 와 **`pnpm`** 은 아직 호환이 되지 않는 것 같음.

### Error 💥

**`yarn add --dev tailwindcss`** 명령으로 프로젝트에 **`tailwind`** 를 설치 할 경우,<br>
의존성 에러가 발생했다.

이를 해결하기 위해 **`yarn add --dev tailwindcss@3.3.2`** 버전을 명시하여 설치 해 주었고,<br>
발생한 에러를 해결할 수 있었다.

---

## 1️⃣ Setup - tailwind.config

```
npx tailwindcss init
```

해당 명령으로 프로젝트 루트경로에 **`tailwind.config.ts`** 파일이 생성 될 것이다.<br>
**`CSS`** 파일에 대한 구성파일을 설정 해 주어야 한다.

```
/** @type {import('tailwindcss').Config} */
module.exports = {
    content: ["./App.{js,jsx,ts,tsx}", "./<custom directory>/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbittIQ%2FbtsEvxkUZGg%2F2OYwkxN3kRx5LPpOE5nlg1%2Fimg.png)

> **`<custom directory>`** 부분에는 **`tailwind CSS`** 가 적용되기를 원하는 경로를 지정 해 주면 된다.<br>나의 경우 **`./App`** 과 **`./src`** 하위 모든 요소들을 지정 해 주었다.

---

## 2️⃣ Setup - babel.config

**`babel.config`** 를 수정함으로 인해,<br>
소스코드를 컴파일 할 때 **`NativeWind`** 를 사용하여 컴파일 할 수 있다.

> **`NativeWind`** 는,<bR>**`CSS-in-JS`** 방식의 스타일로 관리하기에<br>이를 컴파일 하여 **`JavaScript`** 로 변환해야 한다.

```
module.exports = function(api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['nativewind/babel'],
  };
};
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxY4T3%2FbtsEquWLUe8%2F8Qjn1jXJWKUfurklj7CUq0%2Fimg.png)

> **`babel.config`** 를 수정하면 서버를 재시작 해 주어야 적용이 된다.

---

## 3️⃣ Setup - app.d.ts

간단했지만 모든 설정이 끝났다.<br>
이제 기본 **`React-Native`** 문법에 맞춰 작성하고,<br>
**`className`** 을 부여하여 스타일을 지정하려 하는데 에러가 발생한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FS8F9X%2FbtsEy8YrBxT%2F1O5Msq0TcZ0ctcUqlKKYq1%2Fimg.png)

이 에러는,<br>
**`React-Native`** 환경에서 **`TypeScript`** 를 사용하려 할 때 주로 발생하며<br>
기본적으로 **`View`** 컴포넌트는 **`className`** props 로 인식하지 않는다.

이를 해결하기 위해,<br>
**`app.d.ts`** 파일을 추가하여 **`TypeScript`** 에서 사용자 지정 타입을 선언했다.

```
/// <reference types="nativewind/types" />
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7LEJq%2FbtsExHAykTK%2FpVrWdAlfDOGXYaWHCK5uf1%2Fimg.png)

> **`NativeWind`** 를 사용할 때 **`React-Native`** 에 사용할 수 있는 유형을 확장 해 주어야 하는데,<br>해당 유형을 참조하기 위해 **삼중 슬래시 지시어**를 통해 명시 해 주었다.<br><https://www.nativewind.dev/getting-started/typescript>

---

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtCVdU%2FbtsEvXjmWWm%2FlmJ8tzoQMKYZE5kto2u5bk%2Fimg.png)

## Reference 🌊

> <https://enfp-jake.tistory.com/261><br><https://fe-developers.kakaoent.com/2022/220303-tailwind-tips/?ref=codenary><br><https://www.nativewind.dev/getting-started/typescript><br><https://tailwindcss.com/docs/utility-first><br><https://www.nativewind.dev/quick-starts/expo><br><https://www.codenary.co.kr/techstack/detail/tailwind>
