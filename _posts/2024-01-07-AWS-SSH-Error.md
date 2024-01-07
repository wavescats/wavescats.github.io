---
layout: post
title: "[AWS] VSCode 에서 SSH 로 실행한 원격 서버 연결 실패시 해결방법 🙋‍♂️"
subtitle: #부제목
categories: AWS
tags: [Node.js, AWS, EC2, TIL, Error, 프로젝트]
---

## 개요 🔔

**`AWS`** 에서 생성한 **`EC2 인스턴스`** 에 `MySQL` 설치 명령을 실행하니,<br>
아래와 같이 원격 서버에 접속이 되지 않는 상황이다.

실행한 명령은 다음과 같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Folecl%2FbtsC2zL2yeP%2F5E4KUOhuC8E2smTsuHivaK%2Fimg.png)

**`Permission denied`** 에러가 발생하여 권한(**`sudo`**)을 추가 해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbXYB8O%2FbtsC4C2sx24%2FLgLOY7sz5sKnVuXdCEGUvK%2Fimg.png)

이후 설치가 멈추더니, **`VSCode`** 에디터가 종료되었고<br>
아래와 같이 원격 서버를 실행하기 위한 로딩 화면이 무한 반복되고있다 😭😭

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwCMWo%2FbtsC7p2pLvq%2Fy0GYfrt2qaBtBqedBDQK2K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn6lGf%2FbtsC2y7dVfF%2FqYzzrrqlb9uORq6Z34Dg8K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdi2mPU%2FbtsC36Qfb8A%2F64SnoYRvck0x48WS5bWHQk%2Fimg.png)

```linux
[22:50:29.446] Log Level: 2
[22:50:29.480] SSH Resolver called for "ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d", attempt 1
[22:50:29.481] "remote.SSH.useLocalServer": false
[22:50:29.482] "remote.SSH.useExecServer": false
[22:50:29.482] "remote.SSH.showLoginTerminal": false
[22:50:29.482] "remote.SSH.remotePlatform": {"LocalServer":"linux","DDocker_LocalServer":"linux"}
[22:50:29.482] "remote.SSH.path": undefined
[22:50:29.482] "remote.SSH.configFile": undefined
[22:50:29.483] "remote.SSH.useFlock": true
[22:50:29.483] "remote.SSH.lockfilesInTmp": false
[22:50:29.484] "remote.SSH.localServerDownload": auto
[22:50:29.484] "remote.SSH.remoteServerListenOnSocket": false
[22:50:29.484] "remote.SSH.showLoginTerminal": false
[22:50:29.484] "remote.SSH.defaultExtensions": []
[22:50:29.485] "remote.SSH.loglevel": 2
[22:50:29.486] "remote.SSH.enableDynamicForwarding": true
[22:50:29.486] "remote.SSH.enableRemoteCommand": false
[22:50:29.486] "remote.SSH.serverPickPortsFromRange": {}
[22:50:29.486] "remote.SSH.serverInstallPath": {}
[22:50:29.488] VS Code version: 1.85.1
[22:50:29.488] Remote-SSH version: remote-ssh@0.107.1
[22:50:29.488] win32 x64
[22:50:29.490] SSH Resolver called for host: DDocker_LocalServer
[22:50:29.490] Setting up SSH remote "DDocker_LocalServer"
[22:50:29.495] Using commit id "0ee08df0cf4527e40edc9aa28f4b5bd38bbff2b2" and quality "stable" for server
[22:50:29.500] Install and start server if needed
[22:50:29.506] Checking ssh with "C:\Program Files\Eclipse Adoptium\jdk-11.0.19.7-hotspot\bin\ssh.exe -V"
[22:50:29.509] Got error from ssh: spawn C:\Program Files\Eclipse Adoptium\jdk-11.0.19.7-hotspot\bin\ssh.exe ENOENT
[22:50:29.510] Checking ssh with "C:\Ruby32-x64\bin\ssh.exe -V"
[22:50:29.511] Got error from ssh: spawn C:\Ruby32-x64\bin\ssh.exe ENOENT
[22:50:29.511] Checking ssh with "C:\Windows\system32\ssh.exe -V"
[22:50:29.513] Got error from ssh: spawn C:\Windows\system32\ssh.exe ENOENT
[22:50:29.514] Checking ssh with "C:\Windows\ssh.exe -V"
[22:50:29.516] Got error from ssh: spawn C:\Windows\ssh.exe ENOENT
[22:50:29.517] Checking ssh with "C:\Windows\System32\Wbem\ssh.exe -V"
[22:50:29.518] Got error from ssh: spawn C:\Windows\System32\Wbem\ssh.exe ENOENT
[22:50:29.518] Checking ssh with "C:\Windows\System32\WindowsPowerShell\v1.0\ssh.exe -V"
[22:50:29.520] Got error from ssh: spawn C:\Windows\System32\WindowsPowerShell\v1.0\ssh.exe ENOENT
[22:50:29.520] Checking ssh with "C:\Windows\System32\OpenSSH\ssh.exe -V"
[22:50:29.748] > OpenSSH_for_Windows_8.1p1, LibreSSL 3.
[22:50:29.749] > 0.2

[22:50:29.755] Running script with connection command: "C:\Windows\System32\OpenSSH\ssh.exe" -T -D 52752 "DDocker_LocalServer" bash
[22:50:29.758] Terminal shell path: C:\Windows\System32\cmd.exe
[22:50:30.135] > ]0;C:\Windows\System32\cmd.exe
[22:50:30.136] Got some output, clearing connection timeout
[22:50:51.200] > ssh: connect to host DDocker_LocalServer port 22: Connection timed out
[22:50:51.254] > 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:50:52.528] "install" terminal command done
[22:50:52.528] Install terminal quit with output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:50:52.528] Received install output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:50:52.529] Failed to parse remote port from server output
[22:50:52.532] Resolver error: Error:
	at g.Create (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:642703)
	at t.handleInstallOutput (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:640069)
	at t.tryInstall (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:761983)
	at async c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:722522
	at async t.withShowDetailsEvent (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:725828)
	at async I (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:719493)
	at async t.resolve (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:723199)
	at async c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:907003
[22:50:52.552] ------




[22:50:54.951] Opening exec server for ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d
[22:50:55.037] Initizing new exec server for ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d
[22:50:55.102] Using commit id "0ee08df0cf4527e40edc9aa28f4b5bd38bbff2b2" and quality "stable" for server
[22:50:55.106] Install and start server if needed
[22:50:55.129] Running script with connection command: "C:\Windows\System32\OpenSSH\ssh.exe" -T -D 52780 "DDocker_LocalServer" bash
[22:50:55.131] Terminal shell path: C:\Windows\System32\cmd.exe
[22:50:55.469] > ]0;C:\Windows\System32\cmd.exe
[22:50:55.470] Got some output, clearing connection timeout
[22:51:16.497] > ssh: connect to host DDocker_LocalServer port 22: Connection timed out
[22:51:16.521] > 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:51:17.785] "install" terminal command done
[22:51:17.786] Install terminal quit with output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:51:17.786] Received install output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:51:17.787] Failed to parse remote port from server output
[22:51:17.788] Exec server for ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d failed: Error
[22:51:17.788] Error opening exec server for ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d: Error
```

---

## 에러 확인 ❌

로그를 보면,<br>
**`SSH`** 호스트에 연결하려고 시도하고 있지만, 시간 ⏱ 이 초과되는 문제가 발생하고있다 ✅

```linux
ssh: connect to host DDocker_LocalServer port 22: Connection timed out
```

**`SSH`** 클라이언트를 실행 하는 중 문제 ❌ 가 발생했다.

```linux
프로세스에서 없는 파이프에 쓰려고 했습니다.
```

이는 **`SSH`** 클라이언트 실행 중에 다른 문제가 발생한 것으로,<br>
**명령이 중단되거나 비 정상적으로 종료되었다는 것을 의미**한다.

---

## 해결 방법 💨

### known_hosts 🙄

앞서 **`EC2`** 인스턴스를 생성할 때 발급받은 **`.pem`** 키를 저장한 디렉토리로 가 보면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOu3ie%2FbtsC8YKgjOa%2FXes9NPBcG4R90763y4K97K%2Fimg.png)

**`known_hosts`** 파일이 생성되어 있을텐데,<br>
이 파일을 열어보면 **`서버 IP ssh - ras 키`** 순으로 여러 줄이 작성되어 있을것이다.

여기서 접속이 되지 않는 IP 주소 **`(Remote)`** 를 찾아<br>
그 줄을 제거 후 다시 **`SSH`** 접속을 하면 대부분 해결이 된다.

해당 에러는 **이전 호스트들과 충돌**하여 발생하는 문제 때문에 발생하는 에러이다.

하지만, 내가 마주친 에러는 이 해결방법으로 해결이 되지 않아 **다른 방법**을 시도해야할것같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdi2mPU%2FbtsC36Qfb8A%2F64SnoYRvck0x48WS5bWHQk%2Fimg.png)

### Uninstall VSCode Server 💥

1️⃣ **`VSCode`** 에서 명령 팔레트를 열고,<br>
**`Remote-SSH: Kill VS Code Server on Host...`** 를 선택하고<br>
종료 할 **Remote 서버를 선택하여 종료** 후 재 시도한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuM9hu%2FbtsC5YjWjTR%2FetBCUR1WmYTCFzvz28Xo2K%2Fimg.png)

2️⃣ 1️⃣ 번으로 해결이 되지 않을 경우,<br>
**`Remote-SSH: Uninstall VS Code Server from Host...`** 를 선택후<br>
**Remote 서버를 삭제 후 재 설치** 하여 다시 시도해본다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGlABC%2FbtsC52s8EXa%2FLkO2nDxCHIX1mJVm2Ik5rk%2Fimg.png)

---

### SSH Key Permission 🔑

위 두가지의 방법으로도 해결이 되지 않아 이 방법까지 왔을텐데,<br>
**나는 실제 이 방법으로 해결이 되었다.**

먼저, **`EC2`** 를 생성하며 발급받은 **`.pem`** 키가 있는 디렉토리에서,<br>
파일의 속성을 클릭한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdSsm1t%2FbtsC9A3pAOH%2FNMQ8E5vGPWL53CpJkLrxLK%2Fimg.png)

**[보안]** 탭에서 **[고급]** 으로 접근한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FznXn4%2FbtsC7mxSSuQ%2FAsRuwKbI91laa2jqDLQYf1%2Fimg.png)

이미 존재하는 사용 권한 항목들을 아래 **[상속 사용 안 함]** 버튼을 클릭하여 모두 제거 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbiNYy0%2FbtsC2w9zY9z%2FYg84a4e8tSqHvjKtDKrEVk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcTWiDb%2FbtsC4GcJQND%2FNSaH1e3Tpn98ln7vLM8ek1%2Fimg.png)

빈 값이 확인되면, **[보안 주체 선택]** 을 클릭하여 사용자를 추가 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEVU5Q%2FbtsC2yzxPXU%2FNK5OIxomVgdhqBl2GRvOl0%2Fimg.png)

위 과정을 모두 마치면,<br>
**`VSCode`** 의 **`Remote`** 서버에 정상적으로 접근이 가능해 진다.

---

## Reference 🌊

> <https://lovflag.tistory.com/17><br><https://bonita-sy.tistory.com/entry/VSCode-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%97%90%EC%84%9C-%EC%97%86%EB%8A%94-%ED%8C%8C%EC%9D%B4%ED%94%84%EC%97%90-%EC%93%B0%EB%A0%A4%EA%B3%A0-%ED%96%88%EC%8A%B5%EB%8B%88%EB%8B%A4-The-process-tried-to-write-to-a-nonexistent-pi>
