---
layout: post
title: "[React] npx 로 하드햇(hardht) 설치 시 발생한 에러 (An unexpected error occurred Error)"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

## 에러 확인

리액트와 메타마스크를 연동하기 위해<br>
`npx hardhat` 명령어로 로컬 환경에 hardhat 을 설치 해 주는 과정에서 발생한 에러이다.<br>

---

먼저,<br>
프로젝트를 위해 빈 디렉토리를 생성 후<br>
그 안에 `npm init` 을 통해 package.json 을 생성 해 준다.<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbS2UOH%2Fbtr8OVP4GIV%2FKBguBwTSwIe6uKAHQbVhG1%2Fimg.png)

```bash
npx hardhat
```

> yarn == npm 혼용 가능.

명령어를 실행하면,<br>
원하는 언어로 프로젝트를 생성할 수 있다.<br>
첫 번째 `JavaScript` 로 생성 해 주고,<br>
경로 및 `.gitignore` 는 defalut 값 으로 지정하여 설치 해 주면된다.<br>
<br>
파란색의 텍스트를 확인하고,<br>
다시 `npx hardhat` 명령어를 입력 하면<br>
**hardhat 명령어들이 담긴** **npx hardhat help [task]** 매뉴얼이 등장해야 하지만,<br>
<br>
본인은 에러 메세지가 출력되고 있었다.<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJ98jy%2Fbtr8JprOc0d%2FaiosnhfEQ39VpolcYezq5k%2Fimg.png)

> An unexpected error occurred:<br>
> Error: Cannot find module '@nomicfoundation/hardhat-toolbox'

에러를 번역하면,<br>
예상치 못한 에러가 발생했고,<br>
`@nomicfoundation/hardhat-toolbox` 모듈을 찾을 수 없다고 한다.<br>

## 에러 해결

검색을 해 보니,<br>
패키지 문제가 아닌 캐시 오류로 인해<br>
모듈을 찾을 수 없는 경우도 있다 하여 해당 명령으롤 통해 캐시를 지워주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVU2FO%2Fbtr8OW2HYP8%2FfKC0Ofl9smo82w4YgjilZ1%2Fimg.png)

캐시 제거 후에도 `npx hardhat` 명령어가 실행되지 않아<br>
에러메세지에 출력된 패키지를 따로 설치 해 주었다.

```bash
npm install @nomicfoundation/hardhat-toolbox
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUXqhr%2Fbtr8LNFrwDp%2F77LwNJKYqdd7KRHIFC8S61%2Fimg.png)

패키지를 별도로 설치하자 `package.json`에 새로운 dependencies 가 추가 되었고,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHL19D%2Fbtr8LNZKLD0%2FLZccIBt8dKoDyAipZDYan1%2Fimg.png)

`npx hardhat` 명령어가 정상적으로 실행되었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcV6KQc%2Fbtr8MqXq5pN%2F9kjneMI0xmS2zmHKbMckZ0%2Fimg.png)

## Reference

> <https://stackoverflow.com/questions/73431182/cannot-find-module-nomicfoundation-hardhat-toolbox><br><https://github.com/NomicFoundation/hardhat/issues/1890>
