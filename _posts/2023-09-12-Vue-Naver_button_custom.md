---
layout: post
title: "[Vue.js] 네이버 소셜로그인 버튼 커스텀하기 (feat.Naver SDK) 🌿"
subtitle: #부제목
categories: [Vue.js]
tags: [뷰js, Error, TIL]
---

## 개요 🔥

소셜 로그인을 구현하는 웹 페이지에서<br>
`구글`, `카카오`, `네이버` 를 각 플랫폼에서 제공하는 **`SDK`** 를<br>
**`index.html`** 에 `import` 하여 화면에 불러온 상태이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F52osH%2Fbtstyjx28Lq%2FGpqq8ARias9lotzj6KJGJ1%2Fimg.png)

> <https://developers.naver.com>

다음과 같이 예제 코드에 작성된 코드를 사용해보면 알 수 있듯,<br>
이미지 파일을 import 하지 않았음에도 불구하고,<br>
**`SDK`** 안에 내장되어있는 이미지 경로를 불러온다.

문제는,<br>
해당 버튼의 위치 및 크기를 조절하려 스타일을 적용이 되지 않는다는 점 이다 😱<br>

이번 포스팅에서는<bR>
꽤나 다루기 까다로운 네이버 녀석의 소스코드를 분석하며 로그인버튼을 커스텀하는 방법을 작성하려한다.

---

### SDK 💌

> <view-source:https://static.nid.naver.com/oauth/sample/javascript_sample.html>

네이버 측 에서 제공하는 **`Login With NaverID Javascript SDK`** 이 적용되어있는 sample 💬 소스코드이다.<br>
코드를 살펴보면,<bR>
**`div`** 태그에 `naverIdLogin` 라는 id 값을 가진 요소가 있으며,<br>
이 요소 하위에는<br>
SDK 에 내장되어있는 버튼의 URL 이 담긴 `a` 태그가 존재한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdEGnsj%2FbtstSA5yXj3%2FktA6ckCHkVc5SWK5EWviY1%2Fimg.png)

이 `a` 태그에는 **이미지 경로를 지정 해 주지 않아도 자동으로 지정되어 화면에 출력되는 버튼이 있다.**<br>

이 버튼을 수정하기 위해 다시 개발자문서를 살펴본다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdoolzX%2FbtstRK8JBLc%2FU7YKkWu1WesUBYuBBM5EKk%2Fimg.png)

해당 버튼 디자인을 다운로드하여 import 하면 변경된 버튼으로 손쉽게 변경 할 수있는것같다.

---

### 버튼 커스텀 💫

공식 문서를 참조하여 버튼을 커스텀 할 수 있다고 하여<br>
sdk 에 내장된 버튼이 아닌,<br>
다운로드 받은 버튼 이미지를 화면에 적용하려한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKL4DL%2FbtstRQWbUkx%2F3kj4bYEsXYCeK6R3DcCsQ1%2Fimg.png)

버튼이 담겨있는 컴포넌트에<br>
변경할 이미지와, 사이즈를 임의로 조정했지만 정상적으로 반영이 되지 않더라.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F52osH%2Fbtstyjx28Lq%2FGpqq8ARias9lotzj6KJGJ1%2Fimg.png)

분명, Docs 에는 디자인을 변경할 수 있다고 했지만<br>
SDK 에 버튼을 심어버림으로 변경을 못하게끔 막아버린 네이버...😡

**이 문제를 해결하기 위해** 아래의 방법을 사용했다.<br>

**`div`** 태그에 지정되어있는 naverLogin 라는 `id` 값을 가진 태그에<br>
**`style="display: none"`** 를 추가하고,<br>
별도의 `div` 로 `a` 태그를 감싸준 뒤,<br>
해당 요소를 핸들링할 수 있는 이벤트를 클래스에 연결해준다.

```javascript
<template>
  <div>
    <div id="naverIdLogin" style="display: none"></div>
    <div>
      <a href="#" @click="customNaverLogin" class="btn sns-naver">
        <img class="h-20 w-46 rounded-xl" src="@/assets/images/naver_btnG.png" alt="네이버 로그인" />
      </a>
    </div>
  </div>
</template>

<script lang="ts" setup>
let naverLogin: any = null;

// 사용자 정의 버튼 클릭 시 실행될 함수
const customNaverLogin = () => {
  const btnNaverLogin = document.getElementById("naverIdLogin")?.firstChild as HTMLElement;
  btnNaverLogin?.click();
};
<script>
```

옵셔널체이닝(`?.`) 방식을 사용하여<br>
해당 요소가 존재 할 경우 `firstChild` 를 가져오고,<br>
존재하지 않을 경우 `undefined` 를 반환한다.

`as HTMLElement` 를 사용하여<br>
해당 요소를 `HTML` 요소로 처리할 수 있도록 형 변환을 해 주었으며,
`btnNaverLigin?.click()` 은,<br>
선택한 첫 번째 자식요소(버튼) 에 `click` 이벤트를 걸어주는 형태로 작동된다.<br>

만약 옵셔널체이닝 방식 (`?.`) 을 사용하지 않는다면,<br>
아래의 방법으로 동일한 작업을 조건문을 통해 구현할 수 있다.

```javascript
const customNaverLogin = () => {
  const naverIdLoginElement = document.getElementById("naverIdLogin");
  if (naverIdLoginElement) {
    const btnNaverLogin = naverIdLoginElement.firstChild as HTMLElement;
    if (btnNaverLogin) {
      btnNaverLogin.click();
    }
  }
};
```

조건문을 사용하는 방법을 사용한다면,<br>
`naverIdLogin` 이 `null` 인지 아닌지 확인하고,<br>
그 후에 `firstChild` 가 `null` 인지 아닌지 확인하게된다.<br>

해당 조건을 통해<br>
각 단계에서 유효한 값이 있는 경우에만 다음 단계로 넘어가는 형태로 구현했다.<br>

> 해당 이벤트를 통해<br>`naverIdLogin` 이라는 `id` 값을 가진 버튼을<br>
> 직접 클릭하지 않아도 해당 로직을 통해 원래의 이벤트와 동일한 동작이 수행된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdJsJQP%2FbtstQTlnm1R%2Fde8i4KMZle1NUNXwVgPoJ1%2Fimg.png)

## Reference 🌊

> <https://minggu92.tistory.com/37><br><https://velog.io/@wiostz98kr/%EB%84%A4%EC%95%84%EB%A1%9C%EB%84%A4%EC%9D%B4%EB%B2%84-%EC%95%84%EC%9D%B4%EB%94%94%EB%A1%9C-%EB%A1%9C%EA%B7%B8%EC%9D%B8%ED%95%98%EA%B8%B0-%EB%B2%84%ED%8A%BC-%EC%BB%A4%EC%8A%A4%ED%85%80%ED%95%98%EA%B8%B0><br><https://velog.io/@rxxdo/%EB%84%A4%EC%9D%B4%EB%B2%84-%EB%A1%9C%EA%B7%B8%EC%9D%B8-API-%EB%84%A4%EC%95%84%EB%A1%9C-%EC%9D%98-%EB%AA%A8%EB%93%A0-%EA%B2%83-%EB%B2%84%ED%8A%BC-%EC%BB%A4%EC%8A%A4%ED%85%80-feat.-useRef>
