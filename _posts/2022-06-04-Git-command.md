---
layout: post
title: "[Git] Git 명령어"
subtitle: #부제목
categories: TIL
tags: [Github]
---

- `git init`<br><br>
클론 한 레포지토리를 관리하기 위해 Git 에게 선언 하는 명령어.

- `git add`<br><br>
디렉토리의 변경 사항을 추적하기 위해 Git 이 어떤 파일들을 기록할지 지정해주는 명령어.

> 명령어 뒤에는 파일의 경로를 적으면 되며,<br>
현재 디렉토리의 변경 사항을 전부 지정하려면  `.`  혹은 `-A `<br>
모두 지정 할 때는, 주의 해야 할 사항을 점검 해야 한다.

- `git status`<br><br>
Git 의 현재 상태를 보고 싶을 때 사용되는 명령어.

> **현재 상태** 에 표시되는 정보로는<br>
- 어떤 파일들을 추적하고 있는지
- 파일들이 어떤 상태인지
- 어떤 파일이 변경되었는지
- 어떤 Branch 에서 작업하는지 등

- `git commit`<br><br>
 git add 를 통해 어떤 파일들을 기록할지 정했다면 Github 에 업로드(Push) 해야 할 차례다.

 ```bash
 $ git commit -m "git commit message"
 ```
 > 따옴표 안에 지정할 문구를 넣어 실행시키면 커밋이 저장된다.

 - `git remote`<br><br>
 현재 Git 과 연결되어 있는, 즉, 원격 레포지토리와 관련된 명령어.

 ```bash
 $ git remote -v
 ```
 위 명령어를 통해 현재 어떤 원격 레포지토리 주소와 연결되어있는지 확인할 수 있다.

- 원격 레포지토리 주소를 추가하는 방법<br>
(예시)<br>
```bash
$ git remote add apple https://github.com/codestates/apple.git
```

먼저, **git remote** 를 통해 포문을 열고,<br>
주소를 추가하기 위해 **add** 명령어를 추가 한다.<br>
그 뒤에는 어떤 이름으로 저장할지(apple) 입력하고,<Br>
어느 주소와 연결이 되는지(URL) 지정해주면 된다.

- 추가된 원격 레포지토리 주소를 삭제<br><br>
```bash
$ git remote remove apple
```

- `git fetch`, `git merge`, `git pull`<br><br>
`git pull`명령어는<br>
`git fetch`와 `git merge`라는 두 명령어를 합친 명령어이다.

    `git fetch` 는 특정 주소에서 변경된 사항을 가지고 오는 명령어이다.