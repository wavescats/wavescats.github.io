---
layout: post
title: "[AWS] AWS EC2 인스턴스 CPU 사용량 100 % 에러 해결 방법 (Feat. EIP) 👀"
subtitle: #부제목
categories: AWS
tags: [Node.js, AWS, EC2, TIL, Error, 프로젝트]
---

## 개요 🔔

해당 포스팅의 시작은 **`AWS`** 에서 생성한 **`EC2 인스턴스`** 를<br>
**VSCode** 의 **SSH Extension** 으로 실행했을 때 발생한 에러를 기록하고자 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1XSeI%2FbtsC33eSR7c%2FUGGNNT66lgP2aT3PNAf5w1%2Fimg.png)

위 사진은 **`VSCode`** 에서 **SSH** 로 원격 서버를 실행했을 때 발생한 **무한 부팅 (?)** 에러이다.

```linux
[22:17:58.478] Log Level: 2
[22:17:58.495] VS Code version: 1.85.1
[22:17:58.495] Remote-SSH version: remote-ssh@0.107.1
[22:17:58.496] win32 x64
[22:17:58.499] SSH Resolver called for "ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d", attempt 1
[22:17:58.500] "remote.SSH.useLocalServer": false
[22:17:58.500] "remote.SSH.useExecServer": false
[22:17:58.500] "remote.SSH.showLoginTerminal": false
[22:17:58.500] "remote.SSH.remotePlatform": {"LocalServer":"linux","DDocker_LocalServer":"linux"}
[22:17:58.501] "remote.SSH.path": undefined
[22:17:58.501] "remote.SSH.configFile": undefined
[22:17:58.501] "remote.SSH.useFlock": true
[22:17:58.501] "remote.SSH.lockfilesInTmp": false
[22:17:58.501] "remote.SSH.localServerDownload": auto
[22:17:58.504] "remote.SSH.remoteServerListenOnSocket": false
[22:17:58.504] "remote.SSH.showLoginTerminal": false
[22:17:58.504] "remote.SSH.defaultExtensions": []
[22:17:58.504] "remote.SSH.loglevel": 2
[22:17:58.504] "remote.SSH.enableDynamicForwarding": true
[22:17:58.505] "remote.SSH.enableRemoteCommand": false
[22:17:58.505] "remote.SSH.serverPickPortsFromRange": {}
[22:17:58.505] "remote.SSH.serverInstallPath": {}
[22:17:58.515] SSH Resolver called for host: DDocker_LocalServer
[22:17:58.515] Setting up SSH remote "DDocker_LocalServer"
[22:17:58.520] Using commit id "0ee08df0cf4527e40edc9aa28f4b5bd38bbff2b2" and quality "stable" for server
[22:17:58.526] Install and start server if needed
[22:17:58.533] Checking ssh with "C:\Program Files\Eclipse Adoptium\jdk-11.0.19.7-hotspot\bin\ssh.exe -V"
[22:17:58.538] Got error from ssh: spawn C:\Program Files\Eclipse Adoptium\jdk-11.0.19.7-hotspot\bin\ssh.exe ENOENT
[22:17:58.538] Checking ssh with "C:\Ruby32-x64\bin\ssh.exe -V"
[22:17:58.540] Got error from ssh: spawn C:\Ruby32-x64\bin\ssh.exe ENOENT
[22:17:58.540] Checking ssh with "C:\Windows\system32\ssh.exe -V"
[22:17:58.542] Got error from ssh: spawn C:\Windows\system32\ssh.exe ENOENT
[22:17:58.542] Checking ssh with "C:\Windows\ssh.exe -V"
[22:17:58.544] Got error from ssh: spawn C:\Windows\ssh.exe ENOENT
[22:17:58.544] Checking ssh with "C:\Windows\System32\Wbem\ssh.exe -V"
[22:17:58.546] Got error from ssh: spawn C:\Windows\System32\Wbem\ssh.exe ENOENT
[22:17:58.546] Checking ssh with "C:\Windows\System32\WindowsPowerShell\v1.0\ssh.exe -V"
[22:17:58.550] Got error from ssh: spawn C:\Windows\System32\WindowsPowerShell\v1.0\ssh.exe ENOENT
[22:17:58.550] Checking ssh with "C:\Windows\System32\OpenSSH\ssh.exe -V"
[22:17:58.640] > OpenSSH_for_Windows_8.1p1, Lib
[22:17:58.640] > reSSL 3.0.2

[22:17:58.645] Running script with connection command: "C:\Windows\System32\OpenSSH\ssh.exe" -T -D 53233 "DDocker_LocalServer" bash
[22:17:58.650] Terminal shell path: C:\Windows\System32\cmd.exe
[22:17:58.965] > ]0;C:\Windows\System32\cmd.exe
[22:17:58.965] Got some output, clearing connection timeout
[22:18:20.019] > ssh: connect to host DDocker_LocalServer port 22: Connection timed out
[22:18:20.033] > 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:18:21.322] "install" terminal command done
[22:18:21.322] Install terminal quit with output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:18:21.323] Received install output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[22:18:21.324] Failed to parse remote port from server output
[22:18:21.326] Resolver error: Error:
	at g.Create (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:642703)
	at t.handleInstallOutput (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:640069)
	at t.tryInstall (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:761983)
	at async c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:722522
	at async t.withShowDetailsEvent (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:725828)
	at async I (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:719493)
	at async t.resolve (c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:723199)
	at async c:\Users\user\.vscode\extensions\ms-vscode-remote.remote-ssh-0.107.1\out\extension.js:2:907003
[22:18:21.340] ------

[22:18:23.868] Opening exec server for ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d
[22:18:23.899] Initizing new exec server for ssh-remote+7b22686f73744e616d65223a2244446f636b65725f4c6f63616c536572766572227d
[22:18:23.906] Using commit id "0ee08df0cf4527e40edc9aa28f4b5bd38bbff2b2" and quality "stable" for server
[22:18:23.911] Install and start server if needed
[22:18:23.933] Running script with connection command: "C:\Windows\System32\OpenSSH\ssh.exe" -T -D 53263 "DDocker_LocalServer" bash
[22:18:23.935] Terminal shell path: C:\Windows\System32\cmd.exe
[22:18:24.276] > ]0;C:\Windows\System32\cmd.exe
[22:18:24.277] Got some output, clearing connection timeout
```

터미널도 열리지 않고,<BR>
아무런 키가 작동을 하지 않아 여러 방면으로 검색 등을 활용 해 봤지만<br>
필요한 정보는 얻을 수 없었다.

어제까지만 해도 잘 열리던 서버인데 먼가 이상하다..🙄

그런 중 **EC2 인스턴스 관리 페이지**에서 아래와 같은 정보를 확인할 수 있었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcPESoi%2FbtsC6p9y5GG%2FJIqDFHkRnWuCmwUNb5xYK1%2Fimg.png)

**`CPU`** 의 사용량이 **비 정상적인 수치**로 확인되고있다.

---

## 에러 확인 💥

확인 해 본 결과,<br>
위 에러는 비 정상적으로 치솟은 **`CPU`** 사용량에 의해<br>
연결되어있는 **`SSH 서버`** 가 모두 끊기는 (터지는) 현상이었다.

**원인없는 결과는 존재할수없듯,**<br>
내가 시도했던 방법을 추적해본 결과

**무언가를 설치하는 명령어** 를 실행할때마다 CPU 사용량이 기하급수적으로 치솟았다.

즉,<br>
리눅스 쉘에서 **외부와 통신하는 명령어**를 실행 할 때<br>
이를 수행할 **메모리에 부하**가 기준치보다 높게 측정되어 발생하는게 원인이었다.

프리티어로 생성한 **`EC2 인스턴스`** 의 경우 보통 **`t2.micro`** 를 사용하게 될 텐데,<bR>
지원되는 **메모리의 크기가 작고,**<br>
**네트워크의 성능이 비교적 낮음**을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxCCe0%2FbtsC6TwwAlm%2FSjYcwedGsWTZDqPiqzR9h0%2Fimg.png)

이 경우 인스턴스 유형을 업그레이드 하여<br>
보다 좋은 성능을 가진 인스턴스를 사용하면 문제가 가볍게 해결될테지만,<br>
그에 따른 **과금**되는 요금또한 만만치 않으며

미니 프로젝트를 위한 인스턴스로는 **`t2.micro`** 로도 감사하다..🙏

아..❗<br>
언제 문득 **`EC2 인스턴스`** 를 **도커 (Docker)** 로 가져와 이미지를 띄운다는 얘기를 들었던것 같은데<br>
혹시 이와 같은 문제를 해결하기 위해서..❔ 일까..❔

알면 알수록 궁금해지는게 많은 백엔드(서버) 인 것 같다 👶

---

## 에러 해결 ✅

### 인스턴스 재부팅 💫

내가 마주친 에러와 같은 경우,<br>
인스턴스를 **재 부팅** 해 주면 거의 왠만하면 해결이 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPB29i%2FbtsC6VulJKx%2FO5RK9sDOerTR6YP5u8Mtv1%2Fimg.png)

> 재부팅으로도 해결이 되지 않는다면,<br>**`인스턴스 중지`** 후 다시 **`인스턴스 시작`** 을 해 준다.

하지만,<br>
인스턴스를 재부팅을 할 경우<br>
**`퍼블릭 IPv4 주소`** 와 **`퍼블릭 IPv4 DNS`** 가 바뀌어 새로 할당되는데,<br>
이 경우 연결되어있는 **`SSH`** 가 해제되며 다시 연결 해 주어야 하는 상황이 발생한다.

---

### 탄력적 IP (EIP) 🌐

해당 파트는,<br>
인스턴스를 재 부팅하거나 중지 후 재 시작을 할 경우<br>
**`퍼블릭 IPv4 주소`** 와 **`퍼블릭 IPv4 DNS`** 가 재 할당되는데,

생성한 EC2 는 낮은 버전의 메모리를 사용하는 환경이므로 **잦은 재부팅**을 해야할지도 모르는 상황이기에<br>
한 번 발급받은 **`IP`** 주소를 고정시킬 수 없을까 ? 에서 시작하려한다.

이미 나와 같은 생각을 한 사람이 수 없이 많이 존재했고,<bR>
비교적 쉽게 정보를 얻을 수 있었다.

바로 **`탄력적 IP`** 인데,<br>
이는 특정 주소를 할당받아 동적으로 **`IP 주소`** 가 변경되지 않게하는 **`AWS`** 의 서비스 이다 👉 **`EIP`**

해당 서비스를 이용하기 전,<br>
유의사항으로는 과금이 발생할 수도 있다는 것이다.

단,<br>
아래 사항에 해당하는 경우에만 말이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbT7Zvf%2FbtsC6y6UWc3%2FYZVTDhN4Jy4kbCk6E9C311%2Fimg.png)

> 사이드 프로젝트를 통해 **AWS** 의 서비스를 이용하는데,<br>문서를 다시금 확인하여 **불필요한 사항**에서 과금이 발생하지 않게 유의하자 ❗❗<br>참조 링크 👉 <https://repost.aws/ko/knowledge-center/elastic-ip-charges>

먼저,<br>
왼쪽의 사이드 바 에서 **`탄력적 IP`** 를 선택하여 해당 탭으로 이동한다.

**[탄력적 IP 주소 할당]** 버튼을 통해 생성 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FW1h6c%2FbtsDfVzf0m6%2FDroka0lKSJjuFrXdN7SoR1%2Fimg.png)

네트워크 그룹을 사용자의 현재 위치에 맞게끔 지정하고,<br>
**[할당]** 버튼을 통해 **`탄력적 IP`** 를 생성 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlniC7%2FbtsC6zY6uE0%2FjGLPz7lK1oBsOUWdT3iag1%2Fimg.png)

비교적 간단하게 생성할 수 있으며, 이를 기존의 인스턴스와 연결 만 해 주면 끝이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAXJ71%2FbtsC50iif8l%2Fx1IQbu0NwmsZmCYleu6bEk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPtbZd%2FbtsC8XrA9em%2F1p9WjkXImd6uUSk9qHZGA1%2Fimg.png)

생성된 **`탄력적 IP`** 주소를 확인하고,<br>
**[인스턴스]** 를 선택 후 연결할 인스턴스와 프라이빗 IP 주소를 입력한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbUrqmg%2FbtsDfiasSE2%2FJi108UDLkT7z0IiN04azKk%2Fimg.png)

---

위 과정을 통해,<br>
발급받은 **`탄력적 IP`** 주소와 인스턴스를 연결 완료하였고,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbqVZlZ%2FbtsC4u43RS1%2Fi8ny5DyZUoZQFskmjt2F31%2Fimg.png)

인스턴스에 올바르게 적용 되었는지 확인하면 끝이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdZ7jIX%2FbtsDdGiiliw%2F0b4CV4DsVohSbShGA9apgK%2Fimg.png)

---

## Reference 🌊

> <https://velog.io/@yesparrot/EC2-%ED%83%84%EB%A0%A5%EC%A0%81-IP-%EC%A0%81%EC%9A%A9-AWS-EIP><br><https://repost.aws/ko/knowledge-center/elastic-ip-charges><br><https://assaeunji.github.io/aws/2020-03-30-elastic-ip/><br><https://hjjooace.tistory.com/42><br><https://velog.io/@kkj53051000/AWS-EC2-CPU-%EC%82%AC%EC%9A%A9%EB%A5%A0-100-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0-%EA%B3%BC%EC%A0%95><br><https://vlog.tion.co.kr/aws-ec2-cpu-%EC%82%AC%EC%9A%A9%EB%9F%89-100-%EC%84%9C%EB%B2%84%EB%B6%80%ED%95%98-%EC%9B%90%EC%9D%B8/>
