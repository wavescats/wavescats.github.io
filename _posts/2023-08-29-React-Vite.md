---
layout: post
title: "[React] React 프로젝트에 Vite 번들러를 사용하여 HMR 테스트해보기 ⚡️"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

## 개요 🌱

리액트를 사용하여 프로젝트를 `init` 한 적은 많지만,<br>
성능 개선을 위한 생각은 해 본적이 없는 것 같다.<br>

`Vite` 는 지난번 참여했던 일본 언디파인드 해커톤에서 같은 `Fill-up` 팀 으로 함께했던<br>
윤수님이 리드하신 클라이언트에서 처음 접해봤던 경험이 있다 (ㄹㅇ 프론트 굇수,,,)<br>

리액트를 사용하여 제작된 프로젝트의 성능을 개선시키기 위해 어떤 부가적인 요소가 있을까 ?<br>
에서 이번 포스팅을 시작하려한다.

---

### Vite 란 ?

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHNxG0%2FbtssgtvlZaG%2FauCdWjgwsMYBc6BTQADeOK%2Fimg.png)

`Vite` 란,<br>
`Latin for 'fast'`.<br>
프랑스어로 '빠르다' 라는 뜻을 가진 차세대 프론트엔드 개발 도구이다.<br>
**이름처럼 빌드와 개발 서버 구동시간이 매우 빠르고,**<br>
개발 및 빌드 과정을 훨씬 더 빠르게 만들기 위해 설계된 **웹 개발 도구**이다.<br>

주로 `Vue.js` 프레임워크와 함께 사용하도록 만들어졌는데,<br>
**`Vue.js` 프레임워크 이외의 다른 프레임워크나 라이브러리와도 호환이 가능**하다.<br>

> `Webpack`, `Parcel` 등과 비교하면 **10배 이상의 성능**을 자랑하는데,<br>
> 안쓸 이유가 없다..💦

---

#### 특징 ?

`Vite` 의 가장 큰 장점은,<br>
**빌드 속도나 새로운 코드를 적용했을 때의 반영 속도** 같은 Feedback 속도의 엄청난 개선이라고 할 수 있다.<br>

브라우저에서 ES 모듈을 사용할 수 있기 전에는<br>
개발자에게 모듈화된 방식으로 `JavaScript` 를 작성하는 기본 메커니즘이 없었다.<br>
이로 인해 개발자들이 소스 모듈을 브라우저에서 실행할 수 있는 파일로 크롤링하거나<br>
처리 및 연결하는 도구를 사용하는 **'번들링'** 의 개념에 익숙한 이유이다.

- ES 모듈로 빌드

`Vite` 는 개발 중에는 각각의 모듈을 개별적으로 번들링 하지 않고,<br>
ES 모듈 형태로 로딩하여<br>
개발 서버의 라이브 리로딩과 모듈간의 **더욱 빠른 로딩**을 지원한다.

> **ES 모듈이란 ?**<br>
> Go 언어를 기반으로 작성된 `esbuild` 이며,<br>
> JavaScirpt 기반의 번들러보다 **10 ~ 100 배 더 빠른 번들링의 속도**를 낼 수 있다.

- HMR (Hot Module Replace) 지원

HMR 이란,<br>
파일을 편집할 때 전체 번들을 다시 빌드하는 것이 아닌<br>
페이지의 **나머지 부분에 영향을 주지 않고**<br>
**변경된 모듈 자체를 교체**하여 화면에 빠르게 반영되게 하는 것을 말한다.<br>

즉,<br>
HMR 은 코드의 변경사항을 감지하여<br>
**브라우저를 새로고침 하지 않고도 애플리케이션을 업데이트 할 수 있는** 매커니즘을 의미한다.

---

### init 💥

yarn or npm

```
yarn create vite
```

```
npm init vite
```

위 명령어로 `Vite` 를 초기화 해 준 뒤, 생성되길 원하는 [폴더명]을 입력 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHj5Sb%2FbtssxJp2NM0%2FhaomsOpQj1mhq19iexvgh1%2Fimg.png)

어떤 프레임워크와 `Vite` 를 호환할건지 선택하는 창 이므로,<br>
나는 `React` 를 선택 해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbqBLGk%2Fbtssk9XR1It%2FKiXiTIRHC1PnGP8nJWT3LK%2Fimg.png)

이후, 초기화 시 사용될 언어를 선택할 수 있는데, `JavaScript` 를 선택했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdyEs0x%2FbtssBoeyyqu%2FvleCCL3wsQma19v4hI1d71%2Fimg.png)

> SWC (Super-fast, Whole-program Compiler)<br>
> Rust 기반 JavaScript 와 TypeScript 컴파일러로,<br>
> 속도와 효율성을 강조하며 대규모 프로젝트에서도 빠른 컴파일 수행을 목표로 한다.

설치가 모두 되었다면,<br>
해당 경로로 진입하여 `yarn install` 혹은 `npm install` 을 통해 `Dependencies` 를 추가 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FebE25o%2Fbtssvg2RLfi%2FsB7vvpkGg1F7BJ1d6jSN01%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgHA7T%2FbtssCuFs997%2FDalgZfVh0tkxnXiNRLmlE0%2Fimg.jpg)

폴더 구조를 확인하고, `yarn dev` 혹은 `npm run dev` 명령어를 입력하면,<br>
5173 (default Port) 로 앱이 열리게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFkdCc%2FbtssBnfD4DA%2FCABKtsKmIb4nZkz1kmswo1%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdXzIC%2Fbtssv24iC52%2FKbts8zz6fcbtYDZCCQwkK1%2Fimg.jpg)

![](https://blog.kakaocdn.net/dn/0xSGc/btssvyii1bG/23QP6weYTh9DNkeumFuVak/img.gif)

---

#### HMR ⚡️

앱 중앙에 보면,<br>
버튼을 클릭하여 `Count` 를 증가시킬 수 있는 `State` 가 존재한다.

![](https://blog.kakaocdn.net/dn/zv5WS/btsswXn8T4K/Fh5UuGkBKWdWxVhhIshJq1/img.gif)

이미지와 같이 `State` 를 변경 하고, 소스코드를 수정 후 저장해도<br>
`State` 가 `initial State` 로 초기화 되지 않고 그대로 남아있음을 볼 수 있다.<br>

즉,<br>
앱 전체를 `reload` 하는 형태가 아닌,<br>
수정된 부분만 업데이트하는 형태를 직접 확인해 볼 수 있었다.

---

## Reference 🌊

> <https://khys.tistory.com/31><br><https://despiteallthat.tistory.com/256><Br><https://jongik.tistory.com/11>
