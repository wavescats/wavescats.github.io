---
layout: post
title: "[Git] Commit & add 의 Staging 상태 취소하기 🙌"
subtitle: #부제목
categories: Git
tags: [Github, TIL]
---

## 개요 🚩

수정 한 소스코드를 Github 에 올려야 할 상태이다.<br>
먼저 `Branch` 를 확인 하고,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAW9uM%2FbtsrxmiJW4a%2FiZnfXVtmdUO94RYN1AugO1%2Fimg.png)

생성된 `Branch` 가 없기에 내 전용 브랜치를 아래 명령어로 생성 해 주었다.

```bash
git checkout -b sw
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUv5XV%2FbtsrwinzP09%2FUKod0n3j2TbM2exetWeds0%2Fimg.png)

이후,<br>
`git add .` 으로 수정된 파일을 Staging 상태로 올리고,<br>
`git commit -m [커밋메세지]` 로 커밋을 작성하고,<br>
`git push origin sw` 로 생성한 내 브랜치로 push 하려던 순간,<br><Br>

`git config user.name` 으로 현재 레포지토리에 적용된 사용자를 확인 해 보니 내 계정이 아닌것이다..

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrvQyo%2FbtsrCoGA4sQ%2F0iNyy6fN9ls3nPlf5sQGik%2Fimg.png)

`push` 를 하기 전에 알아서 다행인데,

> `git add` 와 `git commit` 을 취소 해야하는데 어떻게 해야할까 ?

에서 이번 포스팅을 출발하려한다.

---

### Commit 취소하기 🐋

먼저 `git log` 명령으로 현재 staging 영역에 있는 커밋 기록을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsvGkn%2FbtsrBPdEvzd%2FkKcyEdbCoq0lH3sJfgEOQK%2Fimg.png)

기록을 확인 해 보면<br>
직전에 `social for kakao` 라는 커밋 메세지로<br>
`staging` 영역에 올라간 커밋 기록을 확인할 수 있다.

- git reset HEAD^ (단계로 commit 취소)
  - 커밋 기록 자체를 말소
  - ^ 수 만큼 이전으로 돌아가게 하는 명령어
  - ^ (직전, 한 단계 앞)
  - ^^ (두 단계 앞)
  - ~숫자 로도 가능

```
# [방법 1️⃣]
# commit을 취소하고 해당 파일들은 staged 상태로 워킹 디렉터리에 보존
$ git reset --soft HEAD^


# [방법 2️⃣]
# commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에 보존
$ git reset HEAD^
$ git reset HEAD~1 # 마지막 commit을 취소. 하나를 되돌림

$ git reset HEAD^^
$ git reset HEAD~2 # 마지막 2개의 commit을 취소


# [방법 3️⃣]
# commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에서 삭제
$ git reset --hard HEAD^
```

`git reset --soft HEAD^` 명령어로 직전의 커밋 기록을 제거 한 모습이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNbv49%2FbtsrDCdk3WI%2FwcyN8Yl8uQiwkb1aC7P0aK%2Fimg.png)

---

### add 취소하기 🐇

`Commit` 기록을 위 과정을 통해 unStaging 하였다면,<br>
`add` 또한 유사한 형태로 진행할 수 있다.<br>

`git status` 명령으로 현재 Staging 되어있는 파일들을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FN318w%2FbtsrCpFztPa%2F7r8orCBklRnJQxEcL8xfak%2Fimg.png)

- git add 취소하기 (파일 상태를 Unstage로 변경하기)

```bash
# 특정 파일을 지정하여 Unstage 로 변경
$ git reset HEAD CONTRIBUTING.md

# 전체 범위를 지정하여 취소
$ git reset HEAD
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGAEBB%2FbtsrDfWY88D%2FpknM7b4pQ2MDM7f7gse6a0%2Fimg.png)

해당 명령어를 실행 후 다시 `git status` 명령으로 현재 상태를 확인 해 보면,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcUhnJ9%2FbtsrDIdyYt2%2FJCDTVaXO4cPKAjbjfPah80%2Fimg.png)

Staging 영역에 있던 파일들이 취소됨을 확인할 수 있다.

---

### 계정 변경하기

이제 로그인되어있는 계정과 email 을 변경 해 주고<br>
다시 `add`, `commit`, `push` 과정을 진행 해 주면 된다.

> **깃 계정 변경하기**<br> <https://wavecats.github.io/git/2023/07/24/Git-userChange.html>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbRQcC2%2FbtsrvWymi02%2FFBnTD7GaXxUeXVfyENX0zK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fwzf22%2FbtsrCyigdWE%2FsN0ZZG5a6SUkuC4SJZBOn1%2Fimg.png)

---

## Reference 🌊

> <https://inpa.tistory.com/entry/GIT-%E2%9A%A1%EF%B8%8F-git-add-commit-push-%EC%B7%A8%EC%86%8C%ED%95%98%EA%B8%B0-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-git-reset-restore-clean><br><https://wavecats.github.io/git/2023/07/24/Git-userChange.html>
