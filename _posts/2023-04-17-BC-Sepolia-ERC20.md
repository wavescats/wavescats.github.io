---
layout: post
title: "[Blockchain] 세폴리아 (Sepolia) 네트워크 환경에서 erc20 토큰 발행하기"
subtitle: #부제목
categories: Blockchain
tags: [블록체인, TIL, Sepolia, ERC20]
---

## Sepolia ?

Sepolia 는 이더리움 메인넷과 동일한 환경을 갖춘 테스트넷이다.<br>
이더리움 테스트넷으로는 Goerli 네트워크도 존재하는데,<br>
이는,<br>
**Sepolia 는 테스트넷에서 분기되어 만들어졌으며,**<br>
**Goerli 은 이더리움 클래식 테스트넷에서 만들어진 네트워크** 정도로 말할 수 있다.<br>
하지만, 두 네트워크 모두<br>
스마트컨트랙트를 체인 위에 올리기 전 테스트를 위한 목적으로는 동일한 환경을 제공하며,<br>
이더리움 기반의 개발을 위해 안정적인 테스트넷으로 활용할 수 있다.

> Sepolia = > Rinkeby 와 호환,<br>
> Goerli => Ethereum Classic 과 호환<br><br>
> Sepolia, Goerli => PoA (Proof of Authority) consensus algorithm 사용

### Faucet

<https://sepolia-faucet.pk910.de/><br>

- 위 페이지는 Sepolia 테스트넷에서 ‘테스트용’으로 나눠주는 이더리움을 받을 수 있는 페이지이다.<br>

- 1시간마다 **0.05 Sepolia ETH** 를 받을 수 있다 (Faucet)

- Goerli 테스트넷의 수수료가 비싸져서 Sepolia 테스트넷으로 이동하는 추세이다

## Sepolia 네트워크 환경에서 erc20 토큰 발행하기

> <https://github.com/tommykim/cau/blob/main/MPC.sol>

강사님이 해당 깃헙에 소스코드를 공개하여 <bR>
`MPC.sol` 파일을 Remix 에 가져와 ERC20 을 생성하려한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrpQY9%2Fbtsa8BBFcDx%2FWR69xqjXOLJSrw86SpKx91%2Fimg.png)

컨트랙트버전을 맞춰주어야 Remix IDE 에서 컴파일 시 에러가 발생하지 않는다.<br>

---

### 토큰 발행

토큰 발행을 위해 `name` 과 `Symbol` 을 수정 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbed88U%2Fbtsa7tDTWfe%2FT61ZEGYxYkS5QItZzuFcR0%2Fimg.png)

> `_decimals` 은 보낼 토큰의 양 뒤에 붙는 0 의 개수를 의미하며,<br>
> 보통 10 의 18 승으로 지정하는 이유는 이더리움의 단위 때문이다.

> `_totalSupply` 는 발행된(할) 전체 토큰의 개수를 의미한다.

---

#### Deploy

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIphfA%2Fbtsa6CHWJ8x%2FVu2lZw6ftatJ22MKliJ72k%2Fimg.png)

Remix 의 **ENVIRONMENT** 를 Injected Provider - MetaMask 를 선택하면,<br>
메타마스크가 실행되며<br>
이 때 Sepolia 테스트 네트워크를 선택하면 해당 컨트랙트와 지갑이 연결된다.
<br>
<br>
Contract 는 **StandardToken** 선택한다.

> StandardToken 은, <br>
> 스마트 계약인 ERC20 및 BasicToken 기능이 있는 토큰을 만드는 데 사용된다.

Deploy 버튼을 누르게 되면 배포 되었다는 아이콘과 함께<br>
`View on etherscan` 을 누르면 새 창으로 트랜잭션을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FItbQg%2Fbtsa9zRb9MO%2FvEGZj9NAmq0Tg6TuggBGa1%2Fimg.png)

- Status 가 Success 로 바뀌게 되면 토큰이 발행 되었다는 의미로 알 수 있다.

---

### 토큰 가져오기

토큰을 발행한 지갑을 확인하면 발행된 토큰이 보이지 않을것이다.<br>
<br>
**자산** 탭에 하단에서 토큰 가져오기를 통해 발행한 토큰을 가져올 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FurvWh%2FbtsaViRmNwB%2FFJmxWSmTCI25OsR2GIGQmk%2Fimg.png)

토큰 계약 주소 칸 에는 방금 배포한 컨트랙트 주소를 넣어주면,<br>
Symbol 명과 발행한 토큰의 개수를 확인할 수 있고,<br>
발행한 토큰을 지갑에 가져올 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fddif3Q%2Fbtsa44ERDZn%2FeOMiiDD6dyh4oIUEUvcgO0%2Fimg.png)

---

### 토큰 거래하기

생성한 토큰은 실제 다른 사용자와도 주고받을 수 있다.<br>
<br>
주고 받을 계정을 새로 생성하고,<br>
기존의 지갑에서 **보내기**를 통해 토큰을 전송할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fblgu2N%2Fbtsa8BIsQqt%2FK5O874RCoOKVdlvskIso10%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcEuoDw%2Fbtsa8AvZX6t%2FCGHqzne5TAgB2B6xT2yTCK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fu9w2E%2FbtsaVhrgz5W%2Fbnx8GV354OlSeo4kRWvNv0%2Fimg.png)

전송되는 과정은 **활동** 탭에서 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKsS4J%2FbtsaTgfehy1%2FTdb3jf2AMX9XXgOku2oTZk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FupjhR%2Fbtsa8hcbl5K%2F6rCZVhRcKxscXSKynAI8dk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlmuGz%2FbtsaTePgR7d%2F99pitNW48kO4IAIW2tKkx1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7eR8f%2Fbtsa9LEwQh7%2FpktMKJOLgVhNeGRZNoyUOk%2Fimg.png)
