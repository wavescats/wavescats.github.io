---
layout: post
title: "[Docker] Docker CLI 를 통해 image 당겨오기"
subtitle: #부제목
categories: Docker
tags: [도커, TIL]
---

## Preview

- docker/whalesay
  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjpUWq%2Fbtr8nR9fm7E%2F8ZcxnOKXtQ8tUyXBHcK7Uk%2Fimg.png)

- danielkraic/asciiquarium
  ![](https://blog.kakaocdn.net/dn/7K4hb/btr8lPqmvDr/DLbPPnpRSnbDeTSWtCzsUk/img.gif)

## 개요

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3LZbA%2Fbtr8kecMtuG%2FZRKUpf7kc6n288yNcdbch0%2Fimg.png)

도커란 컨테이너 기술을 이용한 오픈소스 **가상화 플랫폼**이다.<br>
도커를 사용하면,<br>
응용 프로그램을 컨테이너로 패키지화하여<br>
어디에서나 운영 체제나 하드웨어 등에 상관없이 실행할 수 있도록 만들 수 있으며<br>
이를 통해 프로그램의 이식성이나 확장성의 효율을 극대화 시킬 수 있는 장점을 가지고 있다.

**도커 이미지를 실행하면 컨테이너가 된다.**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5LM66%2Fbtr8vxaSQ9j%2FP7klXq15a8xPaSYU27ksr0%2Fimg.png)

## 도커 이미지란 ?

도커 이미지란,<br>
도커 **컨테이너를 생성하는데 필요한 파일 값이나 설정 값 등을<br> 포함하고있는 응용프로그램 환경을 패키징화 해 놓은 형태**를 말한다.
<br><br>
도커 이미지는 불변성과 계층적인 구조를 갖고 있다.<br>
한 번 생성된 이미지는 수정되지 않으며,<br>
수정하고자한다면 새로운 이미지를 생성해야한다.<br>
<br>
이전 이미지를 기반으로 새로운 이미지를 만들기 때문에,<br>
이전 이미지를 재사용함으로써 이미지의 크기를 줄일 수 있고 이를 통해 빠른 배포와 실행이 가능하다는 장점이 있다.<br>
<br>
이러한 이미지들은 도커 허브 등의 저장소에 업로드 하고,<br>
필요한 시점에 다운로드하여 컨테이너를 생성하고 실행할 수 있다.

## 이미지 가져오기

도커 Hub 에서는 도커 이미지를 찾거나 사용 방법에 대해 확인할 수 있다.

> Docker Hub : <https://hub.docker.com/>

### docker/whalesay

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckRr9i%2Fbtr8xPvBquH%2FLbica4EjKzX9rkm8FOxAWk%2Fimg.png)

- pull
  - 레지스트리에서 이미지 혹은 레포지토리를 가져온다.

```bash
$ docker image pull docker/whalesay:latest
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbblDAa%2Fbtr8xPbiNcH%2FpLacM8YD0Knt4L7PUT7Ku1%2Fimg.png)

- ls
  - 설치된 혹은 이미 갖고있던 이미지의 목록을 보여준다.

```bash
$ docker image ls
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdjsm5F%2Fbtr8tDXyRvl%2FeSpr0L9jXvkZRLYkU5tc6K%2Fimg.png)

- run
  - 받아온 이미지를 실행시킨다. (이미지 -> 컨테이너)

```bash
$ docker container run --name myName docker/whalesay:latest cowsay boo
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlV7WC%2Fbtr8vJbBqjQ%2Fdlggr81RV9mBjd9KkbLjSK%2Fimg.png)

- ps -a
  - 컨테이너의 목록을 보여준다.
  - -a 옵션을 통해 존재하는 모든 컨테이너를 보여준다.

```bash
$ docker container ps -a
```

- rm
  - 생성한 컨테이너를 삭제한다.

```bash
$ docker container rm myName
```

생성한 docker/whalesay 이미지 지우기

```bash
$ docker image rm docker/whalesay
```

### danielkraic/asciiquarium

이번엔 아쿠아리움 이미지가 담긴 레포지토리를 당겨오려고 한다.<br>

- pull

```bash
$ docker image pull danielkraic/asciiquarium
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbPiLu%2Fbtr8usPfLeY%2F9aCY6VIR7D2k1RIq9vWuhK%2Fimg.png)

- run

```bash
$ docker container run -it --rm danielkraic/asciiquarium:latest
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7McJn%2Fbtr8tvrZ5N3%2FUWKhomh0cXimgYLkdReu70%2Fimg.png)

이전에 당겨왔던 이미지들과 다르게 에러 메세지가 출력된다.<br>

> the input device is not a TTY.<br>
> If you are usin mintty. try prefixing the command with 'winpty'

해당 에러로 검색을 해 보니,<br>
window os 에서 `git bash` 를 Mintty 로 사용할때는 지원을 하지 않는다고 한다.<br>

docker 명령어 앞에 Mintty 를 붙여 다시 실행 해 보니 정상적으로 실행이 되었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8wq7e%2Fbtr8kdyGaEQ%2FjSC7PgdEs9upsEjgFW6U7k%2Fimg.png)

![](https://blog.kakaocdn.net/dn/7K4hb/btr8lPqmvDr/DLbPPnpRSnbDeTSWtCzsUk/img.gif)<br

## Reference

> Docker for Windows: Interactive Sessions in MinTTY Git Bash:<br><http://willi.am/blog/2016/08/08/docker-for-windows-interactive-sessions-in-mintty-git-bash/><br><https://forgiveall.tistory.com/471>
