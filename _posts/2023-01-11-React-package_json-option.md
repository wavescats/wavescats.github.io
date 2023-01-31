---
layout: post
title: "[React] Webpack 을 활용한 Package.json 의 초기 설정 및 수정 방법"
subtitle: #부제목
categories: TIL
tags: [리액트]
---


## 프로젝트 생성
---

프로젝트 진행을 위해 빈 디렉토리를 생성하고 

`npm init -y` 명령을 통해 package.json 파일을 생성한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fk0PCN%2FbtrXJq0121e%2Fg2HJuwMli8s3CHmXIUrkc1%2Fimg.png)

<br>

## 패키지 설치
---

다음으로 아래 명령어를 통해 webpack 관련 패키지를 설치해준다.
```
npm i -D webpack webpack-cli webpack-dev-server
```
> 명령어에 쓰여진 -D 옵션은<br>
package.json 의 devDependencies 에 추가하겠다는 의미이다.

<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FowtpQ%2FbtrXGTKo4X0%2FTLamDP94ZyVYa7aQz2co70%2Fimg.jpg)



## 패키지 버전 관리
---

`npm` 명령어로 설치한 패키지의 버전과 강의에서 사용한 버전이 일치하지 않는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb4w7ZS%2FbtrXGUWShnI%2FrK4nVZGf9KMF7mLspsWbO1%2Fimg.jpg)
<br>
<br>

이 때,<br>
아래와 같이 package.json 의 버전을 직접 바꿔 준 뒤 저장 하고<br>
npm i 를 실행하면 수정된 버전이 설치된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FchSxOV%2FbtrXIzDY7v6%2FYdei1VfiV3ezOjCqlaELbK%2Fimg.jpg)


## Reference
---
### -y 옵션이 뭐지?
> <https://velog.io/@lsh__97/npm-init-y-%EC%9D%98%EB%AF%B8>

### devDependencies 가 뭐지?
로컬에서 개발이나 테스트에 필요한 패키지로, 배포 시 포함되지 않는 영역을 말한다.
> <https://www.codeit.kr/community/threads/29051>