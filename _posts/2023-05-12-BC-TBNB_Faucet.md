---
layout: post
title: "[Blockchain] 바이낸스(BSC) 테스트넷에서 토큰(TBNB Faucet) 받기 💛"
subtitle: #부제목
categories: Blockchain
tags: [블록체인, Binance, Faucet, TIL]
---

### TBNB 란 ❓

**바이낸스 테스트넷 (Binance Testnet)** 은,<br>
실제 바이낸스 메인넷을 **모방한** 테스트 환경이다 ✨<br>

이 환경에서는 실제 자산을 사용하지 않고도 트레이딩, 스마트 컨트랙트 배포, 디버깅 등<bR>
다양한 작업이 가능하다.

#### 특징 👍

**1️⃣ 무료 테스트 토큰**<Br>
사용자는 테스트 토큰을 Faucet 함으로 인해,<br>
실제 비용 없이 트레이딩 전략을 테스트 해볼 수 있다.<br>

**2️⃣ API 지원**<Br>
바이낸스의 실제 거래 API 와 유사하므로, 개발중인 애플리케이션을 테스트하기에 적합하다.<br>

**3️⃣ 스마트 컨트랙트 테스트**<Br>
바이낸스 스마트 체인 (Binance Smart Chain, BSC)과 같은 블록체인 환경에서<bR>
스마트 컨트랙트를 배포하고 테스트 할 수 있다.<Br>

---

### TBNB 테스트넷 메타마스크에 등록 (추가)

#### 자동으로 추가하기 ✅

> <https://chainlist.org/chain/97>

`ChainList` 사이트에 접속하여 `BNB` 를 검색하면 연관된 체인들이 검색된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpYa3t%2FbtsteBknC50%2FKvHmcXTtWd8dwCr7vapEY1%2Fimg.png)

> 테스트넷을 포함하여 검색하기 위해 `Include Testnets` 버튼을 클릭 해 준다.

![](https://blog.kakaocdn.net/dn/piIVv/btss85z1Gpk/c1z8rOxoKJkQqs0mKE0fz1/img.gif)

메타마스크를 확인 해 보면 직전에 추가한 TBNB 체인으로 변경됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdFYTZR%2Fbtss8lbOcr3%2FEAQwV48LvgV6TJs0cOHjkk%2Fimg.png)

---

#### 수동으로 추가하기 ☑️

메타마스크 설정에 들어가 **네트워크 추가를 수동으로** 해 주어야 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtuSdn%2Fbtss85mrJDV%2FJmK2aA86kq3PWUtKqTmtCK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbQkbQr%2FbtstggmrZV4%2FJgkKHUn1Lp2zdizwHY53P0%2Fimg.png)

- 네크워크이름 : Binance Smart Chain Testnet
- 새 RPC URL : <https://endpoints.omniatech.io/v1/bsc/testnet/public>
- 체인 ID : 97
- 통화 기호 : tBNB
- 블록탐색기 URL : <https://testnet.bscscan.com>

---

### Faucet 🚧

> <https://testnet.bnbchain.org/faucet-smart>

TBNB 테스트넷에서 사용할수있는 토큰을 **Faucet 받을 수 있는 사이트** 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FT9VKF%2Fbtstbd5DKGY%2FV5UGwJ8UCH8KOwl23qGcq0%2Fimg.png)

해당 사이트에서는 24 시간 마다 **0.1 TBNB** 를 받을 수 있으며,<br>
**24 시간 이내에 테스트 fee 로 모두 소진했다면**<br>

다른 Faucet 사이트에서도 추가로 받을 수 있다.

<https://faucet.quicknode.com/binance-smart-chain/bnb-testnet><br>
(👆 다른 Faucet 사이트 1)

<https://testnet.help/en/bnbfaucet/testnet><br>
(👆 다른 Faucet 사이트 2)

<https://faucet.triangleplatform.com/bnbsmartchain/testnet><br>
(👆 다른 Faucet 사이트 3)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw9hvW%2Fbtss9hOi4V0%2FaYkkdsVx6v6OhXDXKzXkM0%2Fimg.png)

---

## Reference 🌊

> <https://wavescats.github.io/blockchain/2023/01/20/bc61.html>
