---
layout: post
title: "[Git] 로그인 되어있는 Git Bash 의 계정 변경하기 (& git Checkout Error)"
subtitle: #부제목
categories: Git
tags: [깃허브, TIL]
---

## 개요

협업을 위해선 깃허브의 사용은 가히 필수적 이라고 생각한다.<br>
이번 포스팅에서 다뤄볼 내용으로는<br>
현재 서버컴퓨터에 올라가있는 프로젝트를 관리하기 위해<br>
로컬에서 테스트를 하려고 한다.

---

### 에러 발견

> error: Your local changes to the following files would be overwritten by checkout:
> ...
> Please commit your changes or stash them before you switch branches.
> Aborting

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbN26BR%2FbtsoRe9pN0W%2FBdrDB1ylTPeubL0uKUxtKk%2Fimg.png)

기존의 작업중이었던 dev 브랜치에서<br>
새로 생성한 auth 브랜치로 `checkout` 명령어를 사용하여<br>
브랜치를 이동하려고 할 때 발생한 에러 메세지이다.<br>

---

### 에러 해결

해당 에러는,<br>
다른 브랜치로 이동하기 전<br>
작업하고 있던 브랜치에서 변경사항을 커밋(저장)하지 않아 발생하는 에러라고 한다.

에러 메세지를 살펴보면 솔루션도 같이 제공되어 있다.<br>

> Please commit your change or stash them before you switch branches.

**해당 브랜치를 커밋 하거나 임시로 저장해라**

나는 `stash` 명령어를 통해 임시저장하지않고,<br>
`commit` 을 통해 작업내용을 저장 후 브랜치를 변경하여 에러를 해결하였다.

---

## 업로드

`git push` 명령어를 통해 커밋 한 작업내용을 깃허브에 업로드 하려고 할때,<br>
서버와 git bash 가 연결되어있는 깃허브 계정이<br>
다른사람의 계정으로 되어 있었다.<br>
로그인 되어있는 유저를 확인하기 위해서<Br>
아래 명령을 통해 깃허브 ID 를 확인할 수있다.

```bash
git config user.name
```

사용자를 변경하기 위해서는 위 명령어에 변경할 ID 만 입력 해 주면 된다.

```bash
git config user.name [변경할닉네임]
```

만약 이 상태에서 깃허브 저장소에 접근하려한다면 당연히 **실패** 할 것이다.
해당 명령어를 통해 email 까지 변경 해 주면<br>
새 창으로 IDE 인 VSCode 와 깃허브와 연결하고자 하는 창이 열린다.<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbebAZq%2FbtsoYV774oB%2Fn5Ek2QZ49tRKHHUvl20i9K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmP7Fm%2FbtsoSnJ1yrq%2FqKHmAiXP4yJOJHo2i3cNBK%2Fimg.png)

깃허브 로그인을 진행 해 주면<br>
연결에 성공함을 알려주는 리다이렉트 페이지가 보여지고 작업을 이어갈 수 있다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9RJby%2FbtsoRfsaKCg%2FDBzig7NMuZSZKk9k5xiv1K%2Fimg.png)

이후부터 git 명령어를 로컬 프로젝트 내에서<br>
자유롭게 구사 가능한 형태로 세팅이 완료되었다.<br>
`git add`, `git commit`, `git push`

---

## Reference 🌊

> <https://hoohaha.tistory.com/31><br><https://kgw7401.tistory.com/65><br>
