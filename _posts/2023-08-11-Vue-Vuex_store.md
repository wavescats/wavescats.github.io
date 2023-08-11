---
layout: post
title: "[Vue.js] Vuex 를 통한 상태관리 (feat. Store, Mutations)"
subtitle: #부제목
categories: [Vue.js]
tags: [뷰js, TIL]
---

## 개요

`Vue.js` 에서도 `React.js` 와 같이 상태들을 관리해야할 필요가 있는데,<br>
이번 포스팅에서는 `Vuex` 라이브러리를 사용하여 상태를 관리하는 방법에 대해 기록하려한다.

---

### Store

`Store` 는, `Vuex` 에서 제공하는 객체로<br>
애플리케이션의 상태(State) 를 담고있으며, 반응적으로 작동한다는 특징이 있다.

#### 주요 속성 및 메서드

**1. state**<br>
애플리케이션의 상태를 저장하는 객체로<br>
데이터 구조를 보유하고있으며 반응적으로 작동한다.

**2. getters**<br>
`state`에 저장된 값에 기반하여 계산된 값을 반환하는 메서드이다.<br>
이는 `Vue` 컴포넌트 내의 `Computed` 속성과 유사하게 작동한다.

**3. mutations**<br>
`state` 를 변경하는 메서드이다.<br>
이는 동기적으로 작동하며, 상태 변경의 추적을 용이하게 만들 수 있다.

**4. actions**<br>
비동기 연산을 수행하거나<br>
여러 `mutations` 를 연속적으로 `commit` 하는 메서드이다.

**5. modules**<br>
큰 애플리케이션에서는 `store` 를 모듈로 분리하여 관리할 수 있는데,<br>
각 모듈은 자체적으로 `state`, `mutations`, `actions`, `getters` 를 가질 수 있다.

> `Vuex` 의 `store` 는 반응적으로 동작하므로,<br> > `Vue` 컴포넌트에서 `store` 의 상태를 읽으면 상태가 변경될 때 컴포넌트도 자동으로 업데이트 된다.

---

### 예시 (코드)

> 아래 코드는 `Vue 3` 의 `Composition API` 와<br> > `<script lang="ts" setup>` 문법을 사용하여 작성된 예시 코드이다.

- Vue 컴포넌트에서 store 에 접근하기

```javascript
<script lang="ts" setup>
  import {(ref, computed)} from 'vue';
  {/* // Vuex 4 에서 제공하는 useStore Hook 을 가져옴  */}
  import {useStore} from 'vuex';
  {/* // store 인스턴스를 가져옴 */}
  const store = useStore();
  {/* // state에 직접 접근하여 Vuex 의 state 에 있는 count 값을 컴퓨티드로 감싸 반응형으로 만듬 */}
  {/* // count 에 담긴 값이 변경될때마다 자동으로 컴포넌트도 업데이트됨 */}
  const count = computed(() => store.state.count);
</script>
```

<br>
- 뮤테이션을 커밋하여 상태 변경하기

```javascript
<script lang="ts" setup>
import { useStore } from 'vuex';

const store = useStore();

const incrementCounter = () => {
  // incrementCounter 함수가 호출될때마다 increment 뮤테이션을 커밋함.
  store.commit('increment');
};
</script>

<template>
    {/* 버튼 클릭 시 정의된 함수를 호출하여 뮤테이션을 트리거함 */}
  <button @click="incrementCounter">Increase Count</button>
</template>
```

<br>
- 액션 디스패치하기

```javascript
<script lang="ts" setup>
import { useStore } from 'vuex';

const store = useStore();

// 비동기
const someAction = async () => {
  // someActionName 라는 이름의 액션을 디스패치하며 필요한경우 payload 를 전달
  await store.dispatch('someActionName', payload);
};
</script>

<template>
  <button @click="someAction">Trigger Action</button>
</template>
```

<br>
