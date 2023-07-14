---
layout: post
title: "[React] 서버사이드렌더링 이란 ? (SSR & CSR)"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

## 개요

리액트를 공부하던 중 Next.js 에 대해 알고만 있었지,<br>
직접 사용해 볼 엄두가 나지 않던 찰나<br>
같은 수강생들과 팀플을 진행하게 됬는데<br>
이 때 새로운 프레임워크로 Next.js 를 사용해 보자 ! 라고 결정을 하게 되었다.<br>
<br>
Next.js 의 강력한 장점으로 SSR 과 SEO 가 있는데,<br>
해당 포스팅으로 두 장점에 대한 내용을 정리하고자 한다.

---

### SSR ?

서버사이드렌더링은<br>
Next.js 를 사용하는 가장 큰 이유라고 생각하는 중요한 기능이라고 생각된다.

SSR 은<br>
서버에서 페이지를 그려 클라이언트(브라우저) 로 보내<br>
화면에 출력하는 렌더링 기법이다.

---

#### CSR 과 차이 ?

SSR 과 CSR 의 차이는<br>
화면에 보일 페이지의 내용을 어디서 그리느냐의 차이이다.<br>
<br>
CSR 은 페이지의 내용을 브라우저에서 그리고,<br>
SSR 은 페이지의 내용을 서버에서 그린 뒤 브라우저에 출력한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcNEQXh%2FbtsnwYSZoBf%2FAEXtVcSaq1kusk3SleXEI0%2Fimg.png)

---

### 특징

<br>
- CSR (Client-Side Rendering)

1. 초기 로딩속도가 빠르며, 로딩 이후에는 API 연동을 통해<br>
   데이터를 가져와 동적으로 렌더링을 한다
   <br>
2. 사용자가 상호작용할 때<br>
   서버로부터 데이터를 받아오는 비동기 요청을 수행한다
   <br>
3. 서버 부하가 상대적으로 적지만,<br>
   클라이언트 자원 (CPU, 메모리 등) 을 비교적 많이 사용한다.
   <Br>
4. 검색 엔진 최적화 (SEO) 기능을 사용하려면 추가 작업이 필요하다.
   <br>
   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmzmTX%2Fbtsnyglvcmt%2FvCKw8osyaNosIy6svzSX5K%2Fimg.png)

- SSR (Server-Side Rendering)

1. 초기 로딩 시 서버에서 모든 컨텐츠가 렌더링 되어 전달되어<br>
   사용자에게 빠른 첫 페이지 로딩을 제공한다
   <br>
2. 동적인 컨텐츠가 변경되는 경우에도<br>
   서버에서 즉시 렌더링하여 새로운 컨텐츠를 빠르게 제공한다
   <Br>
3. 서버 부하가 상대적으로 높아질 수 있으며,<br>
   클라이언트 자원의 사용량은 상대적으로 적다
   <Br>
4. 검색 엔진 최적화에 유리하다

## ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbc3Jci%2FbtsnvJvUzJI%2Fu5wUkZ0UUTRcEKjKVSJpx1%2Fimg.png)

#### SEO ?

검색 엔진 최적화 (SEO, Search Engine Optiomization)<br>
SSR 을 사용하는 큰 목적은 `SEO` 와 `빠른 페이지 렌더링` 이다.<br>
SEO 는,<br>
사용자가 구글, 네이버와 같은 검색 사이트에서 검색을 시도했을 때<br>
결과가 사용자에게 많이 노출될 수 있도록 최적화 하는 기법이다.<br>
특히, SNS 에서 링크를 공유했을 때<br>
해당 웹 사이트의 정보를 이미지와 설명으로 표시해주는<br>
OG (Open Graph) Tag 를 페이지 별로 적용하기 위해서는<br>
`SSR` 이 보다 효율적이다

---

### 단점

그럼 위 내용을 토대로 본다면<br>
사용자에게 제공되는 장점이 많은 SSR 을 사용하는게 좋겠지만,<br>
**서버 사이드 렌더링**
즉, 서버쪽의 환경구성과 실행방법, 빌드 등의 전반적인 이해를 필요로한다.<br>
이에 프론트엔드 개발자로써는 SSR 의 진입장벽이 꽤 높은편 이다.
<br>
동적인 페이지 전환이 있을 경우<br>
HTML 파일 자체를 서버에서 받아오기 때문에 화면 깜빡임 현상이 발생할 수 있다.<Br>
부분적으로 업데이트하는 CSR 과는 다른 차이가 있다.<br><br>
그래서 초기 로딩은 CSR 보다 SSR 이 빠르지만,<br>
페이지 이동 및 렌더링 부분에서는 비교적 느린 편에 속하기도 한다.

---

### Reference 🌊

> <https://joshua1988.github.io/vue-camp/nuxt/ssr.html#%E1%84%89%E1%85%A5%E1%84%87%E1%85%A5-%E1%84%89%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3-%E1%84%85%E1%85%A6%E1%86%AB%E1%84%83%E1%85%A5%E1%84%85%E1%85%B5%E1%86%BC%E1%84%80%E1%85%AA-%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%89%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3-%E1%84%85%E1%85%A6%E1%86%AB%E1%84%83%E1%85%A5%E1%84%85%E1%85%B5%E1%86%BC-%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%A5%E1%86%B7><br><https://developers.google.com/search/docs/fundamentals/seo-starter-guide?hl=ko><br><https://ko.wix.com/blog/post/what-is-seo><br><https://hahahoho5915.tistory.com/52>
