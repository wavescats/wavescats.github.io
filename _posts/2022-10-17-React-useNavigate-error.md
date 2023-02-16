---
layout: post
title: "[React] 에러는 없는데 페이지 랜더링이 되지 않을 때"
subtitle: #공공데이터 / Pandas
categories: React
tags: [리액트, Error]
---
### 에러 발생
---
npm start 명령어로 리액트 서버를 실행시켰더니,<br>
에러 없이 실행됨을 확인했다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxbePd%2FbtrXJqGIz2r%2Fj7rA9oW2gWxusjxN7VWt01%2Fimg.png)

### 에러 확인
---
하지만, <br>
어째선가 구성한 페이지가 보이지 않아 콘솔창을 확인 해 보니 에러 메세지가 있다.
> Uncaught Error: useNavigate() may be used only in the context of a <'Router'> component.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvVot5%2FbtrXHH3YjbP%2F4YZ1uuQ3cB8EIqiWp4ZTAK%2Fimg.png)

오류 메세지를 확인해보니, <br>
'useNavigate() 함수를 Router 컴포넌트 내에서 사용할 수 없다'<br>
라는 형태의 오류인 것 같다.

### 에러 해결
---
코드를 살펴보자.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkJ3Jp%2FbtrXJsdt5ZF%2F8SwcBrhGoKAzNbmOIVTewk%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRokY6%2FbtrXJsdt5YI%2FUwo048kkpRJa2RovKQEVk0%2Fimg.png)

복.붙 해온 코드에서<br>
정의된 useNavigate 를 담은 변수인 navigate 부분을 주석 처리 해주니 정상적으로 동작함을 볼 수 있었다.

> 현재는 라우팅 기능이 구현되지 않은 단면적인 컴포넌트 이며,<br>
세부적인 DB 연결 및 테이블 생성 작업이 필요할 것 같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcJocBg%2FbtrXHIPoKiz%2FZHrc33Okyktt5LweiiYjh1%2Fimg.png)