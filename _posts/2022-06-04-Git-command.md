---
layout: post
title: "[Git] Git 명령어"
subtitle: #부제목
categories: Git
tags: [TIL]
---

### `git init`
Clone 한 레포지토리를 관리하기 위해 Git 에게 선언 하는 명령어.

### `git add`
디렉토리의 변경 사항을 추적하기 위해 Git 이 어떤 파일들을 기록할지 지정해주는 명령어.

> 명령어 뒤에는 파일의 경로를 적으면 되며,<br>
현재 디렉토리의 변경 사항을 전부 지정하려면  `.`  혹은 `-A `<br>
모두 지정 할 때는, 주의 해야 할 사항을 점검 해야 한다.

### `git status`
Git 의 현재 상태를 보고 싶을 때 사용되는 명령어.

> **현재 상태** 에 표시되는 정보로는<br>
- 어떤 파일들을 추적하고 있는지
- 파일들이 어떤 상태인지
- 어떤 파일이 변경되었는지
- 어떤 Branch 에서 작업하는지 등

### `git commit`
 git add 를 통해 어떤 파일들을 기록할지 정했다면 Github 에 업로드(Push) 해야 할 차례다.

 ```bash
 $ git commit -m "git commit message"
 ```
 > 따옴표 안에 지정할 문구를 넣어 실행시키면 커밋이 저장된다.

### `git remote`
 현재 Git 과 연결되어 있는, 즉, 원격 레포지토리와 관련된 명령어.

 ```bash
 $ git remote -v
 ```
 위 명령어를 통해 현재 어떤 원격 레포지토리 주소와 연결되어있는지 확인할 수 있다.

#### 💥 원격 레포지토리 주소를 추가하는 방법
```bash
$ git remote add apple https://github.com/codestates/apple.git
```

먼저, **git remote** 를 통해 포문을 열고,<br>
주소를 추가하기 위해 **add** 명령어를 추가 한다.<br>
그 뒤에는 어떤 이름으로 저장할지(apple) 입력하고,<Br>
어느 주소와 연결이 되는지(URL) 지정해주면 된다.

#### 🔥 추가된 원격 레포지토리 주소를 삭제하는 방법
```bash
$ git remote remove apple
```

### `fetch`, `merge`, `pull`
`git pull`명령어는<br>
`git fetch`와 `git merge`라는 두 명령어를 합친 명령어이다.

    `git fetch` 는 특정 주소에서 변경된 사항을 가지고 오는 명령어이다.

#### 💫 예시
```bash
$ git fetch apple main
```

`'apple'`이라는 원격 주소 이름의 `'main'` Branch가 Github 에서 업데이트 되었고,<br>
변경된 내용을 로컬로 가지고 오고 싶다면 위 명령어를 실행 시키면 된다.

예시를 통해 가져온 변경 사항은 저장되지 않은 임시 Branch 로 가져와 진다.<br>
이 임시 브랜치를 현재 작업하고 있는 브랜치와 합치기 위해 `git merge` 를 사용한다.

```bash
$ git merge 브랜치_이름
```

적용하고 싶은 Branch 에서 실행하고 명령어 뒤에는 불러올 Branch 이름을 입력하면 된다.

`git pull` 명령어는 위의 과정을 알아서 해결 해 준다.<br>
즉,<br>
변경 사항을 원격 주소에서 가지고 온 뒤 merge 를 해준다.

### 💡 브랜치 변경을 위한 명령어
```bash
$ git checkout '브랜치명'
```

#### 🌟 새로운 브랜치 생성 및 변경을 위한 명령어
```bash
$ git checkout -b '브랜치명'
```

### 자주 사용하는 Git 명령어
#### 🙋 Local 에서 작업할 때 주로 사용하는 명령어
- git status
- git log
- git commit
- git add
- git branch
- git checkout

#### 👬 Github 등 온라인으로 Git 을 활용할 때 사용되는 명령어
- git push
- git pull
- git fetch
- git merge
- git remote
