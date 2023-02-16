---
layout: post
title: "[React] 프로젝트의 npm start 가 실행되지 않을 때"
subtitle: #공공데이터 / Pandas
categories: React
tags: [리액트, Error]
---

### 에러 확인
---
npm start 명령어 실행 시 에러 문구는 출력되지 않고,<br>
아래와 같이 랜더링이 되지 않고 자동으로 탈출 되는 현상이 있었다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnDVP8%2FbtrXGUWQRyq%2FYi1wk8XC5eKPOqRmnK9th0%2Fimg.png)

구글 검색을 해 보니<br>
package.json 의 scripts 부분에 아래와 같은 옵션이 추가되어있었다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FU7aVp%2FbtrXHB3OvAj%2Fk97bTQ7uVizGBesrwGADlK%2Fimg.png)


실행 순서는 (&& 기준) 앞 구문 이 먼저 실행되고,<br>
뒤에 있는 react-scripts start 구문이 실행되는데<br>
먼저 실행되는 앞 구문에서 버전 관련하여 오류가 발생하여<br>
뒤에 있는 구문이 실행이 되지 않았다.
<br>
<br>

### 에러 해결
---
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuyOoz%2FbtrXIoo5VQZ%2FhNq3XiqOQ319mlnt47JDb1%2Fimg.png)

다음과 같이 오류가 발생하는 앞 구문을 지워주고 실행하니 정상적으로 랜더링이 되었다.