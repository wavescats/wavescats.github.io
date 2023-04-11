---
layout: post
title: "[React] npm i 로 패키지 설치 시 권한 에러"
subtitle: #부제목
categories: React
tags: [리액트, TIL, Error]
---

## 에러 확인

npm i 명령어로 `openzeppelin/contracks` 을 설치하는 과정에 있다.<br>
<br>
여느 때와 같이 에러 없이 설치가 되나 싶었지만..<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbC2F3J%2Fbtr9mTlpxU2%2FtwfmCWtaTXMczW0tvOsD31%2Fimg.png)

에러를 살펴보니

> that you lack permissions to access it.

엑세스에 접근하려했지만,<br>
권한이 없어 접근하지 못한다는 에러 같다.<br>

버전 관련 에러는 많이 봤었지만,<br>
권한 관련에러는 처음 겪어 당황스러웠다.<br>

이를 해결하기 위해<br>
`cmd` 를 관리자 권한으로 실행시켜 명령어를 다시 입력해보아도 별 차이는 없었다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKMJ2e%2Fbtr9qAZrrBr%2FOmwCOxkxc2kTnKgsqzoDSk%2Fimg.png)

GUI 로 관리자 권한으로 접근하여 실행하는 것이 아닌,<br>
`sudo` , `apt` 명령어를 사용해 관리자 권한을 부여하여 npm 명령어를 실행했지만,<br>
해당 명령어를 실행할 수 없다는 메세지만 출력이 되고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbQMzg3%2Fbtr9mSGOvv9%2Fv1vW4qnml1F3QhsPqI56I1%2Fimg.png)

## 에러해결

추측해보건데,<br>
npm 의 버전의 문제가 아닐까 싶다.<br>
<br>
에러와 별개로<br>
이를 해결하기 위해 `npm` 이 아닌 `yarn` 으로 설치를 진행하자 패키지가 정상적으로 설치되었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FW6Vbk%2Fbtr9sjb4TQm%2FQgxizuh5B0gg5R433btZAK%2Fimg.png)

---

혹은,<br>
외부 패키지를 설치하여 실행하는것이 아닌<br>
빈 파일을 생성하여<br>
불러오고자 하는 컨트랙트에 담긴 코드 자체를 가져와<br>
로컬에서 `import` 하는 방식으로도 에러 없이 실행 가능했었다.
<br><br>
이를 테스트하기위해<br>
Remix-ide 에 코드를 가져와 컴파일 해 보았을때 정상적으로 실행이 되었다.

## Reference

> <https://velog.io/@lifefm_j/Node.js-npm-%EC%98%A4%EB%A5%98><br><https://remix-ide.readthedocs.io/en/latest/import.html><br><https://www.openzeppelin.com/contracts><br><https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.2/contracts/token/ERC20/ERC20.sol>
