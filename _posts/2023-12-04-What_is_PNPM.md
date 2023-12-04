---
layout: post
title: "[Node.js] pNpM 으로 패키지 관리하기 (Feat. npm & yarn)"
subtitle: #부제목
categories: Node.js
tags: [npm, yarn, pnpm, TIL]
---

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc17duW%2FbtsBqIvorWe%2FWs2jJ6nkcZwkE2m0t5z051%2Fimg.png)

## 개요 🔔

프로젝트를 진행하다보면,<br>
종속성(Package) 을 설치 해야하는 경우가 다반수 이다.<br>

그리고 **`npm install`** 을 통해<br>
기존에 의존하고 있는 패키지들이 **`./node_modules`** 안에 담기는 것을 확인할 수 있다.

만약 로컬 환경에서 개발 중,<br>
설치한 의존성들이 충돌하여 캐시를 제거하고<br>
**`.lock`** 파일과 **`./node_modules`** 폴더를 제거한 기억이 있지 않은가 ❔<br>
그리고,<br>
이를 제거할 때 시간이 다소 오래 소요되진 않았던가 ❔<br>
위와같은 문제를 해결하기 위해 **패키지 매니저** 들은 점차 보완이 되고 있으며,<br>
**`pnpm`** 까지 등장한 것 이다 ❗<br>
**라는 포문으로 해당 포스팅을 시작하려 한다.**

---

패키지 매니저란,<br>
개발에 필요한 패키지를 설치하고 수정 및 업데이트 등의 작업을 편리하게 도와주는 도구 라고 할 수 있다.<br>
**`JS`** 로 프로젝트를 진행하다 보면,<br>
필요한 다양한 패키지들을 설치하고 관리해야 하는 경우가 있는데<br>
이 패키지들을 의존성 있게 관리 해 주는 것이 **패키지 매니저** 이다.

> 즉, **패키지 매니저**는 👉 프로젝트에 사용되는 패키지를 쉽게 관리하고 설치 해 주는 하나의 도구 ❗

---

## Package Manager

가장 많이 사용되는 **패키지 매니저**로는,<br>
**`npm`**, **`yarn`**, **`pnpm`** 이 있는데,<br>
이 **패키지 매니저**들에 대해 간단한 특징과 어떤 장점이 있어 상황에 맞게 고를 수 있게 정리 해 보고자 한다.

### 1️⃣ npm

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbRrnME%2FbtsBq1uM8m4%2FuV1dgLdnReOQ3TKk5UNefk%2Fimg.png)

**`npm`** 은,<br>
패키지 매니저의 시초이며 프로젝트의 의존성을 수동을 설치해야하는 번거로움을 해결하기 위해 등장했다.<br>
**`node.js`** 에 내장되어 있어 추가적인 설치가 필요하지 않다.<br>

> 즉, 별도의 설치가 필요가 없다는 것이 **`npm`** 의 가장 큰 장점이기도 하다.

또한,<br>
가장 오래된 시초 인 만큼<br>
직접 개발한 모듈뿐만 아니라 **다른 사용자들이 불편함을 개선하고자 만들어 놓은** 다양한 패키지들이 있어<br>
비교적 **생태계에서 얻을 수 있는 정보가 풍부**하다는 장점이 있다.

하지만,<bR>
**`npm`** 의 경우 패키지들이 서로 의존하는 상관관계를 맺고 있기 때문에<br>
하나의 **패키지에서 문제가 발생**한다면,<br>
**다른 패키지에서도 문제가 발생**할 수 있다는 단점 😥 을 가지고 있다.

> 이를 관리하기 위해 **`package.json`** 파일이 필요하다.

```
npm init
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvNH9L%2FbtsBjQ9n0xv%2FXf6nEeNs2ShhqoK9IQH3Wk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnMpLI%2FbtsBj6ElhUe%2FeoohNA0MglVAV5mtO5f1cK%2Fimg.png)

---

### 2️⃣ yarn

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FesRrIj%2FbtsBjPCELgi%2FiFGzeGbjASLiKQ8oja3x0k%2Fimg.png)

**`yarn`** 의 경우,<br>
기존의 **`npm`** 의 문제점 및 단점을 보완하여 등장한 **패키지 매니저**로<br>
페이스북과 구글 개발자들이 협업하여 탄생한 **패키지 매니저** 이다.

사실 두 **패키지 매니저**는 큰 차이가 없고, 프로세스도 거의 유사하지만<br>
가장 큰 차이는 **보안** 이다.

**`npm`** 의 가장 큰 단점은 **보안** 이었는데,<br>
이를 보완하여 탄생한 **`yarn`** 이며,<br>
**`npm`** 의 취약점을 공략하여 보다 안정성을 보장한다는 장점이 있다.

1️⃣ Integrity 체크 👉 다운로드 한 패키지의 무결성을 체크 ✔<br>
2️⃣ Lock 파일의 정확성 👉 **`yarn.lock`** 파일을 통해 보다 정확한 의존성 해결<br>
3️⃣ 프록시 서버 지원 👉 패키지 다운로드 시 **프록시 서버** 를 통해 다운로드 하므로 외부 사용자의 공격에 보안 ⬆<br>
4️⃣ 공통 의존성 최적화 👉 다수의 프로젝트에서 동일한 패키지를 공유함으로 인한 의존성 효율 최적화<br>
5️⃣ 더 빠른 의존성 해결 👉 최적화된 알고리즘을 통해 속도 ⬆<br>
6️⃣ 개발 환경에서 Offline 모드 👉 한번에 모든 패키지를 설치하고, 이후 저장된 캐시를 통해 오프라인 설치 지원 ✔

추가로,<br>
**`yarn`** 의 매력적인 장점 요소로는 **속도** 이다.<br>
여러 개의 패키지를 **순차적으로 설치**하는 것이 아닌,<bR>
**병렬적으로 설치**함으로 인해 속도 측면에서 **`npm`** 보다 우위의 장점을 보여주고 있다.

이러한 이유로 최근에는 **`npm`** 보다 **`yarn`** 을 더 많이 선호하는 추세이며,<br>
**`yarn berry`** 라는 **`yarn`** 의 상위 버전을 통해 다양한 개발과 개선점이 보완되고 있는데,<br>
아직까지는 **`yarn berry`** 보다는 **`yarn`** 을 더 많이 사용하고 있는 것 같다.

```
npm install -g yarn
```

```
yarn init
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb0u2TJ%2FbtsBoixfGQj%2FR7yU7p5LCb6pRagokMlkZk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcdQLzK%2FbtsBqJHPRVO%2FMzaVKHW4k4QpURxytIr4uk%2Fimg.png)

> **`yarn`** 의 경우 **`npm`** 에 의존하기 때문에, **`npm`** 을 통해 먼저 설치 해 주어야 하며,<br>로컬 전역에서 사용 가능하도록 **`-g`** 옵션을 주어 **`global`** 설치를 해 준다.

---

### 3️⃣ pnpm

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc17duW%2FbtsBqIvorWe%2FWs2jJ6nkcZwkE2m0t5z051%2Fimg.png)

**`pnpm`** 은,<br>
2017 년에 개발된 **패키지 매니저**로,<br>
**`Performant npm`**(**`Performent Node Package Manager`**) 의 약자이다.<br>
즉, 효율적인 **`npm`** 이라는 의미로<br>
**`npm`** 이 가진 장점에 효율성을 추가로 더해 등장한 **패키지 매니저** 이다.

**`pnpm`** 의 경우,<bR>
프로젝트 별로 생성되는 **`./node_modules`** 에 매번 패키지를 설치했던 것과는 달리<br>
**`global`** 저장소에 패키지를 한 번만 저장함으로 인해 저장 공간을 절약할 수 있다는 **아주 큰** 장점을 가지고 있다.

> 즉, 똑같은 라이브러리를 매번 중복하여 설치할 필요가 없다는 의미이다.<br>다만, 특정 패키지를 한 번만 설치하기 때문에<br>프로젝트별로 연결을 해 놓으면 호환 에러가 발생할 가능성이 존재한다.<br>👉 **버전관리 필수** ❗

이를 통해 빠르고, 효율적인 디스크 관리를 할 수 있기 때문에<br>
최근 **`pnpm`** 은 2021 년 다운로드 수의 5배 이상을 넘긴것을 확인할 수 있다.

```
npm install -g pnpm
```

```
pnpm init
```

> **`yarn`** 과 동일하게 **`pnpm`** 을 전역(global) 에서 사용할 수 있도록 먼저 설치 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdrOjGp%2FbtsBmTEubqB%2FeAO3AXfhkNKCHlQGDvrvKk%2Fimg.png)

---

#### 모노 레포 🚝

모노 레포란,<br>
여러 프로젝트 혹은 패키지를 단일 저장소에서 관리하는 방식을 의미한다.<br>

**`npm`**, **`yarn`** 과 비교했을 때<br>
**`pnpm`** 로 추가한 패키지는 **`./node_modules`** 폴더에 중복으로 저장되지 않는다.

예를들어 `sample_1`, `sample_2`, `sample_n` 이라는 프로젝트가 존재하고,<br>
각 프로젝트는 **`./node_modules`** 하위에 **`pkg_1`** 이라는 같은 파일을 모두 가지고 있다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqQn9P%2FbtsBkkWFu5L%2FH2Irv9zUfuux7UsHFncVs0%2Fimg.png)

> 이는 중복된 메모리를 사용하여 불필요한 리소스가 발생함을 의미할 수 있다.

반면에 **`pnpm`** 의 경우,<br>
별도의 저장소(**`.pnpm_store`**) 를 가지고 있고,<br>
각 프로젝트에 존재하는 **`pkg_1`** 파일의 복사본(**`Symbolic link`**)을 만들어<br>
이를 별도의 저장소에서 중앙으로 관리한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQ2Egf%2FbtsBr54HC6H%2Fn641nIygVDJBKFqsQS7uP1%2Fimg.png)

> 이를 통해<br>**중복된 6MB (2MB \* 3)** 이라는 메모리로부터 중복된 저장공간을 효율화 시킬 수 있다.<br>👉 프로젝트가 많을수록 이 효과는 더욱 커지게 된다.

(공식 github 참조 👇)<br>
<https://github.com/pnpm/pnpm><br>

---

### 속도 비교 💨

**`pnpm`** 의 공식 **`github`** 레포에 따르면,<br>
**`pnpm`** 은, 다른 **패키지 매니저** 보다 최대 2배 이상 빠르다고 나와 있다.<br>

(공식 github 참조 👇)<br>
<https://github.com/pnpm/pnpm><br>

아래는 공식 레포에 게시된 각 패키지 매니저들이<br>
명령어를 처리하는 속도에 대한 그래프를 시각적으로 나타낸 표 이며,<br>
가로축은 **실행 시간**을 의미한다.

![](https://camo.githubusercontent.com/83b108abddef5c40f6afc985fa8214edc92b6f2226a83d577074a720907463c8/68747470733a2f2f706e706d2e696f2f696d672f62656e63686d61726b732f616c6f7474612d66696c65732e737667)

그래프를 확인 해 보면,<br>
비 정상적으로 속도적인 부분에서 우위를 다루는 것을 확인할 수 있는데,<br>
이는 의존성을 설치하는 명령어가 기존의 **직렬** 방식이 아닌 **병렬** 방식으로 수행되기 때문이다.

---

사실,<br>
각 **패키지 매니저** 들은 현재 사용해도 전혀 손색이 없을 정도로 안정적인 상태이고,<br>
계속해서 보완과 유지보수를 통해 업데이트를 하고 있다.<br>
따라서<br>
각 **패키지 매니저** 들을 직접 사용 해 보고,<br>
본인 상황에 맞는 **패키지 매니저** 를 선택하여 프로젝트를 시작하는 것이 가장 현명한 방법일것 같다.

---

## Reference 🌊

> <https://github.com/pnpm/pnpm><br><https://engineering.ab180.co/stories/yarn-to-pnpm><br><https://devscb.tistory.com/135><br><https://velog.io/@sebinn/%ED%8C%A8%ED%82%A4%EC%A7%80-%EB%A7%A4%EB%8B%88%EC%A0%80-%EB%B9%84%EA%B5%90-npm-yarn-pnpm><br>
