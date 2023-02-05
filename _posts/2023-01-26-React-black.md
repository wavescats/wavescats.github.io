---
layout: post
title: "[React] 띄어쓰기의 중요성"
subtitle: #부제목
categories: Error
tags: [리액트]
---

### 에러 확인
---

이미지 갤러리를 클론코딩하던 와중에 발생한 에러이다.
<br>

아래와 같이 사용자가 추가한 이미지가 row 형태로 나열되어야 하는데,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmReuA%2FbtrX4l7g1EZ%2FkR63tegYrWyntNlgnHi5cK%2Fimg.jpg)

내가 작성한 프로젝트에서는 column 형태로 나열되어 출력되고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fx6CQa%2FbtrYdhCnupK%2Fmc7b9ZBetSPQvBInCRtnP1%2Fimg.jpg)

이미지가 추가되는 부분을 개발자도구를 열어 확인해 본다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQIuVw%2FbtrX6g5qhG9%2FFoYlGSitUep5izETYXe7HK%2Fimg.jpg)

해당 코드를 열어 확인해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8IvUF%2FbtrX4lTJZjD%2FFPw12Xxepm82HyKYeK2Jj1%2Fimg.jpg)

이상한 부분이 있다.
이미지가 추가되었을 때 'row' 라는 클래스를 생성해 주었는데,<br>
개발자도구에서 확인해 보니 앞의 클래스와 합쳐보이게되어<br>
'row' 클래스에 부여한 스타일이 적용되지 않는것 같다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnviZO%2FbtrX41N9gdF%2FCnO9O8gxK7rzVTjJkBkJ40%2Fimg.jpg)


### 에러 해결
---

> 개발자도구에서 확인했던 className 에 공백을 추가하여<br>
클래스 간의 구분을 짓고,<br>
이미지가 추가된 경우 생성되는 className 인 'row' 에 스타일을 적용시킴.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAVnIQ%2FbtrX33sgSSs%2FRRS1eL8LnNcsC3UarUPBo1%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdsacT0%2FbtrX2VVDusI%2FMoNUzUbhkmK3Lxiw8kOnzk%2Fimg.jpg)
<br>
<br>

추가한 이미지에 flex-direction 속성이 정상적으로 적용되어 출력된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdNojKS%2FbtrX9FXVcGg%2F8fRk0LE7ID8rhLg2YcRs80%2Fimg.jpg)