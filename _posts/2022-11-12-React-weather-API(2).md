---
layout: post
title: "[React] 날씨 기반 API 를 활용한 프로젝트 - 2"
subtitle: #부제목
categories: Project
tags: [프로젝트]
---

## UI 제작
---

***Reference***
![](https://files.cdn.thinkific.com/file_uploads/523761/images/0ac/c3c/3d3/1648395289245.jpg)
**<https://bitna-weather.netlify.app>**

먼저,<br>
각각의 Element 들을 제작하기보다 Bootstrap 을 활용하여 UI 를 제작하려 한다.
```bash
npm install react-bootstrap bootstrap
```

### Bootstrap 과 React-Bootstrap 의 차이
***Bootstrap은 상태값과 클래스를 사용하고,<br>
React-Bootstrap은 function과 hooks를 사용한다.***

> React-bootstrap 은 리액트에 최적화 되어있으며 컴포넌트에 초점을 맞춰 제작되어<br>
가독성이 좋고 다양한 애니메이션 구현시 더 유용하다.

Reference 를 보면,<br>
body 태그 안에 두개의 컴포넌트가 구현되어있음을 예상할 수 있다.


```bash
npm install --save styled-components
```