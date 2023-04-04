---
layout: post
title: "[Docker] Windows 에서 install 시 발생한 'Docker Desktop requires a newer WSL kernel version.' 에러"
subtitle: #부제목
categories: Docker
tags: [도커, TIL, Error]
---

## Install

- Docker 공식 홈페이지
  > <https://www.docker.com/get-started>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCSdlt%2Fbtr7HhIkADT%2FcaqraWx9iC2tygx1tg2fCk%2Fimg.png)

다운받은 installer 를 실행시키면, <br>
아래와 같이 추가적으로 설치할 수 있는 창이 실행된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdu0a31%2Fbtr7R23331z%2F2riosWX3X77z5tOFxyUKK1%2Fimg.png)

> WSL 은,<br>
> 리눅스용 윈도우 하위 시스템 (Windows Subsystem for Linux) 을 말한다.

둘 다 체크 후 설치를 진행하게 되면 데스크탑에 정상적으로 설치가 완료된다.<bR>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FswgSE%2Fbtr7OLPzS51%2FrtADmCLiXRnfYhOVuil4mK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoT36C%2Fbtr7StAo1Wp%2FSNCnYz7zO1Xk3Ik7S8Yhm1%2Fimg.png)

## 에러

설치가 종료 되면,<br>
설치된 Docker Desktop 이 자동으로 실행된다.

하지만,<br>
다음과 같은 모달 창이 등장하며 Docker Desktop 이 종료된다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkWy5P%2Fbtr7MVdTBQ3%2FwTSdkcHweSqyiLmg44yJLK%2Fimg.png)

에러 메세지를 자세히 읽어보면,<br>
`wsl --update` 명령어를 입력하여 WSL 커널을 업데이트 하거나,<bR>
공식 문서를 참조하여 에러를 해결하라고 한다.

### 에러 해결

Windows Powershell 을 실행하여 명령어를 입력 해 준다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmoYsL%2Fbtr7Ooz66ts%2Fah3O5MnCpnjy4X0I9isMAK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FObnIX%2Fbtr7R234gwT%2FK3UD22PWwQw5TGwS91MRzK%2Fimg.png)

Docker 가 잘 설치 되었는지 확인하기 위해서는,<br>
Bash 나 터미널에 Docker 를 입력 해 보면 명령어를 보여준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdt4yw9%2Fbtr7PpL3PLc%2FoV1abP6K22u59yFfKCLJ01%2Fimg.png)

## Reference

> <https://learn.microsoft.com/ko-kr/windows/wsl/install-manual><br><https://engineeringcode.tistory.com/662>
