---
layout: post
title: "[Blockchain] Klaytn 지갑 생성과 erc20 토큰 발행하기"
subtitle: #부제목
categories: Blockchain
tags: [블록체인, TIL, Klaytn]
---

## 개요

> <https://wallet.klaytn.foundation/>

위 링크로 접속하여 지갑을 생성 해 주려고 한다.<br>

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
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDwzvs%2FbtsdInJh95K%2FHKagKUJAX6paCKsaWMk4JK%2Fimg.png)

> 컴파일 시 드롭박스에서 StandardToken 을 선택하며,<br>
> Deploy 시 에도 동일하게 선택해준다.

> 컴파일 시 에러(붉은색) 표시는 Syntax 문제 혹은 버전의 문제일 수 있으나,<br>
> 경고(노란색) 표시는 무시해도 무관하다.

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.4.21;

interface ERC20 {
   function balanceOf(address who) public view returns (uint256);
   function transfer(address to, uint256 value) public returns (bool);
   function allowance(address owner, address spender) public view returns (uint256);
   function transferFrom(address from, address to, uint256 value) public returns (bool);
   function approve(address spender, uint256 value) public returns (bool);
   event Transfer(address indexed from, address indexed to, uint256 value);
   event Approval(address indexed owner, address indexed spender, uint256 value);
}

library SafeMath {
   function mul(uint256 a, uint256 b) internal pure returns (uint256) {
       if (a == 0) {
           return 0;
       }
       uint256 c = a * b;
       assert(c / a == b);
       return c;
   }

   function div(uint256 a, uint256 b) internal pure returns (uint256) {
       // assert(b > 0); // Solidity automatically throws when dividing by 0
       uint256 c = a / b;
       // assert(a == b * c + a % b); // There is no case in which this doesn't hold
       return c;
   }

   function sub(uint256 a, uint256 b) internal pure returns (uint256) {
       assert(b <= a);
       return a - b;
   }

   function add(uint256 a, uint256 b) internal pure returns (uint256) {
       uint256 c = a + b;
       assert(c >= a);
       return c;
   }
}

contract StandardToken is ERC20 {
   using SafeMath for uint;

   string internal _name;
   string internal _symbol;
   uint8 internal _decimals;
   uint256 internal _totalSupply;

   mapping (address => uint256) internal balances;
   mapping (address => mapping (address => uint256)) internal allowed;

   function StandardToken() public {
       _name = "SimJunko";                   // Set the name for display purposes
       _decimals = 18;                            // Amount of decimals for display purposes
       _symbol = "SSW";                           // Set the symbol for display purposes
       _totalSupply = 100000000000000000000000000;         // Update total supply (100000 for example)
       balances[msg.sender] = 100000000000000000000000000;               // Give the creator all initial tokens (100000 for example)
   }

   function name()
   public
   view
   returns (string) {
       return _name;
   }

   function symbol()
   public
   view
   returns (string) {
       return _symbol;
   }

   function decimals()
   public
   view
   returns (uint8) {
       return _decimals;
   }

   function totalSupply()
   public
   view
   returns (uint256) {
       return _totalSupply;
   }

   function transfer(address _to, uint256 _value) public returns (bool) {
       require(_to != address(0));
       require(_value <= balances[msg.sender]);
       balances[msg.sender] = SafeMath.sub(balances[msg.sender], _value);
       balances[_to] = SafeMath.add(balances[_to], _value);
       Transfer(msg.sender, _to, _value);
       return true;
   }

   function balanceOf(address _owner) public view returns (uint256 balance) {
       return balances[_owner];
   }

   function transferFrom(address _from, address _to, uint256 _value) public returns (bool) {
       require(_to != address(0));
       require(_value <= balances[_from]);
       require(_value <= allowed[_from][msg.sender]);

       balances[_from] = SafeMath.sub(balances[_from], _value);
       balances[_to] = SafeMath.add(balances[_to], _value);
       allowed[_from][msg.sender] = SafeMath.sub(allowed[_from][msg.sender], _value);
       Transfer(_from, _to, _value);
       return true;
   }

   function approve(address _spender, uint256 _value) public returns (bool) {
       allowed[msg.sender][_spender] = _value;
       Approval(msg.sender, _spender, _value);
       return true;
   }

   function allowance(address _owner, address _spender) public view returns (uint256) {
       return allowed[_owner][_spender];
   }

   function increaseApproval(address _spender, uint _addedValue) public returns (bool) {
       allowed[msg.sender][_spender] = SafeMath.add(allowed[msg.sender][_spender], _addedValue);
       Approval(msg.sender, _spender, allowed[msg.sender][_spender]);
       return true;
   }

   function decreaseApproval(address _spender, uint _subtractedValue) public returns (bool) {
       uint oldValue = allowed[msg.sender][_spender];
       if (_subtractedValue > oldValue) {
           allowed[msg.sender][_spender] = 0;
       } else {
           allowed[msg.sender][_spender] = SafeMath.sub(oldValue, _subtractedValue);
       }
       Approval(msg.sender, _spender, allowed[msg.sender][_spender]);
       return true;
   }
}
```

환경(ENVIRONMENT) 을 Baobab(테스트넷) 으로 변경 후,<br>
지갑이 연결되면 컨트랙트 내부에서 발행할 토큰의 Name 과 Symbol 을 지정해준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVGnRC%2FbtsdIoBrklx%2FyrCWw2iEy9ywVGNCkPCC61%2Fimg.png)

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

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzxdOr%2FbtsdM0GN07H%2Fy22pMgxrrSXNEzQoctymzk%2Fimg.png)

Name 과 Symbol 을 작성 후 StandardToken 으로 변경하고 Deploy 하면,<br>
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
