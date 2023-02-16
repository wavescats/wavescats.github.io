---
layout: post
title: "[Anaconda] 가상환경 목록을 추출해 .txt 파일에 저장하기"
subtitle: 
categories: Anaconda
tags: [아나콘다, 파이썬]
---

### Conda 란?
Anaconda 에 포함된 도구를 말하며,<br>
패키지 관리 및 가상 환경을 관리해주는 도구를 말한다.

### 가상환경 생성 및 관리

`practice` 라는 이름의 가상 환경을 생성하는 명령어 이며,<br>
파이썬의 버전은 3.8 로 지정 해 주었다.

```bash
$ conda create --name 'practice' python=3.8
```
<br>

`Create` 명령어로 생성된(혹은 존재하고 있던) 가상 환경의 목록을 보여주는 명령어이다.

```bash
$ conda env list
```
<br>

생성된 가상 환경인 `Practice` 에 진입하기 위한(`activate`) 명령어이다.<br>
생성된 가상 환경에서 `pip install` 등 새로운 패키지를 설치하여도<br>
다른 가상환경에 영향을 끼치지 않는다.

```bash
$ conda activate 'practice'
```
<br>
가상 환경에 진입한 상태라면,<br>
아래 명령어로 진입한 가상환경을 종료할 수 있다.

```bash
$ conda deactivate
```
<br>

생성된 가상 환경을 제거하는 명령어이다.
```bash
$ conda env remove --name 'practice'
```

### 가상환경 목록 추출
---

먼저 가상화면 목록들을 확인하기 위해 아래 명령어를 입력한다.
```bash
$ conda env list
```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc9DqBc%2FbtrYRV7W6am%2FHVeSZHDcggZmkEVVKVDIQk%2Fimg.png)


생성된 목록들을 지정 디렉토리 안에 있는 result.txt 파일 안에 저장하고싶다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHGkKy%2FbtrYUSWgNSm%2Fxuaw7Bmyt3sW8bZW4jHT00%2Fimg.png)

쉘 리다이렉션 옵션을 통해 가상환경 목록을 저장한다.

#### Reference
> <https://wikidocs.net/29734>

```bash
$ conda list -n s1n1 > result.txt
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcpLvfK%2FbtrYUSBYevK%2FShfgetTBSnmYyXVrj4o8E1%2Fimg.png)

> **(리뷰 기간을 활용한 블로그 정리 중 이므로, 생성된 가상 환경의 목록이 다를 수 있음)**