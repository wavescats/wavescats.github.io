---
layout: post
title: "[Blockchain] Klaytn 지갑 생성과 erc20 토큰 발행하기"
subtitle: #부제목
categories: Blockchain
tags: [블록체인, TIL, Klaytn]
---

## 개요

> <https://wallet.klaytn.foundation/>

위 링크로 접속하여 지갑을 생성 해 주려고 한다.<br

---

### 지갑 생성

상단에 버튼을 이용해 Baobob Testnet 으로 바꾸어주고,<br>
`Create Account` 로 지갑을 생성 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb7gius%2Fbtr9OyHIIcm%2Fr0qFpmNSurSWHQPY5zJjH0%2Fimg.png)

개인키를 저장하는 지갑의 비밀번호를 설정한다.
![](https://blog.kakaocdn.net/dn/cLB2EB/btr9SOiGatD/4WsAOyUuivorA4jGKX9kbK/img.png)
(번역)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZ1SV9%2Fbtr91yF3oCs%2FZEY23BwhbqMrQHKwF54cpK%2Fimg.png)

다음단계를 누르게 되면 키가 자동으로 다운로드 된다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjxE8t%2Fbtr9PeP3fSB%2FWWUfQykNK5CAqPNRkTE66K%2Fimg.png)

다음단계로 이동하면 개인키와 지갑키가 암호화 되어 부여되며,<br>
키는 따로 보관하는게 좋다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdjOyPZ%2Fbtr91UWoaBI%2FKm0Mhnlga5rMUQtEcIwkz0%2Fimg.png)

#### Faucet

지갑을 생성했다면 무료로 지급되는 Klay 를 받을 수 있다.

> Klay 의 오남용을 방지하여 24시간의 제한을 두고있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc5hx5b%2Fbtsafqvyndn%2FSSSeyKafaBYwp6f9fdSS50%2Fimg.png)

---

### erc20 token

`Faucet` 탭 밑에 `More` 를 클릭하면,<br>
이더리움 가상환경인 Remix IDE 를 새 창으로 열 수 있다.<br>

클레이튼 지갑에서 IDE 를 실행하면,<br>
제일 밑에 Klaytn 버튼이 생긴다.<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdbCEDl%2Fbtr94jJlLHh%2FOhdRXnRzWSLViUPNkVUBx1%2Fimg.png)

아래 컨트랙트를 컴파일 하고<br>
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fyec89%2Fbtr92qbe1UB%2FgvRkuFkM5DXk2TSDZineJ0%2Fimg.png)

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor(string memory name, string memory symbol) ERC20(name, symbol) {
        // Mint 100 tokens to msg.sender
        // Similar to how
        // 1 dollar = 100 cents
        // 1 token = 1 * (10 ** decimals)
        _mint(msg.sender, 100 * 10**uint(decimals()));
    }
}
```

환경(ENVIRONMENT) 을 Baobab(테스트넷) 으로 변경 후,<br>
지갑이 연결되면 DEPLOY 에서 발행할 토큰의 Name 과 Symbol 을 지정해준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFWlf9%2FbtscYp9eOVr%2FUR0GpZ3Ykv8zvzcuMnwLAK%2Fimg.png)

> Symbol 은 코인의 특성을 나타내는 간략한 단어를 의미하며,<br>
> Name 은 코인의 전체 이름을 의미한다.

#### 지갑 가져오기

컴파일을 마치고 Klaytn 의 Deploy 탭에서<br>
ACCOUNT 에 넣어줄 지갑의 주소는<br>
클레이튼 지갑에서 사용자가 지정한 닉네임을 클릭하고,<br>
지갑 키를 내보내기 하면 Private 키를 얻을 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSesKt%2Fbtsabe8lBOb%2FarkE2kQS2cjS9gkVwts6N1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8NwxM%2Fbtr90TL1SrP%2FXCnXHMcBUOHpd1m5k8aftK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnEf6G%2FbtsabeAuJi0%2Fngs4JI39XkF8CCbaKKAAa0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FY7v3b%2Fbtr94k2AD0F%2FFjiZAxnsI4AVpG3fIeCwEk%2Fimg.png)

#### 토큰 생성하기

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8AO4u%2Fbtr90UKWnI8%2FcfKLDmBhib7Fz2cXnFz7l1%2Fimg.png)

Name 과 Symbol 을 지정 후 트랜잭션을 날리면,<br>
해당 컨트랙트가 Deploy 되며 컨트랙트 주소가 출력된다.

> 생성된 토큰을 확인하기 위해서는<br>
> 터미널 창에 출력된 `view on etherscan` 을 누르면<br>
> 새 페이지가 열리며 방금 실행한 컨트랙트의 트랜잭션을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdhuMLb%2FbtsdHOttdcU%2FlRbKgI3x7qcDhckanjFNB0%2Fimg.png)

**해당 트랜잭션은 참고용임을 명시함**

생성된 SSW 토큰은 메인넷이 아닌 Baobab 테스트넷에서 발행되었기때문에,<br>
실제 화폐로써의 가치는 없는 토큰이다.<br>
<br>
만약, 테스트넷이 아닌 메인넷에서 Fee 를 소모하여 발행하였다면,<br>
발행한 토큰을 아래 링크에서 확인할 수 있다.

> <https://etherscan.io/tokens>

## Reference

> <https://velog.io/@fltxld3/ERC20-%EB%82%98%EB%A7%8C%EC%9D%98-%ED%86%A0%ED%81%B0-%EB%A7%8C%EB%93%A4%EA%B8%B0>
