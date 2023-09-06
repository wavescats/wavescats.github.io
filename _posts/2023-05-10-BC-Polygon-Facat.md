---
layout: post
title: "[Blockchain] Polygon 테스트넷 '뭄바이(Mumbai)' 에서 폴리곤(Matic faucet) 받기"
subtitle: #부제목
categories: Blockchain
tags: [블록체인, Polygon, Faucet, TIL]
---

## Mumbai Test Network

폴리곤(Polygon) 은 이더리움의 확장성 문제를 해결하고자 나온 프로젝트로,<br>
이더리움의 확장 및 인프라 개발을 위한 만들어진 플랫폼 이다.

> 이더리움의 비싼 가스비로인해 개발에 어려움을 겪는 사용자들을 위해 등장한 '폴리곤' 이다.

---

## Mumbai 테스트넷 메타마스크에 등록 (네트워크 추가)

확장 프로그램으로 설치된 메타마스크를 확인 해 보면,<br>
Polygon 메인넷은 보이지만 테스트넷인 Mumbai 는 보이지 않는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclJnwL%2FbtseGLoIA7b%2FZWSox5rPsPKXiGgGqjsfZK%2Fimg.png)

이 보이지 않는 네트워크를 추가하기 위해 `ChainList` 를 이용하면 해결할 수 있다.

<https://chainlist.org/>

> Chainlist 사이트는 ‘메타마스크’에 안보이는 네트워크를 추가 할 수 있는 사이트다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmsO1P%2FbtseHlJPoHl%2F1qhbTmg1GlSiXiNNCkx5Fk%2Fimg.png)

검색에서 `Mumbai` 를 검색 후 테스트넷 포함(Include Testnets) 체크박스를 선택하면 `Mumbai Testnet` 이 나타난다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FddVOfT%2FbtseGa3nolf%2F9LnPX0wEv0xQRoUP4GQtT1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FccD9EB%2FbtseGXJwKEN%2FmNbHp4dlGyXsDKQwGCWRR1%2Fimg.png)

메타마스크에 추가된 `Mumbai` 확인

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckWxiz%2FbtseHQv25az%2FVbgf348mj63AcT3xnTAa8k%2Fimg.png)

## faucet

Mumbai TestNetwork 에서 사용할수있는 **'테스트용’** 으로 나눠주는 폴리곤 (MATIC) 을 말하며,<br>
Sepolia, goerli 등 의 네트워크에서도 테스트넷 토큰을 채굴 할 수 있다.

> 테스트넷으로 채굴하는 토큰은 **실제 화폐 가치가 없다**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckEZfL%2FbtseGMurKDT%2FiYNOZ1z80b5UGlb9M4T520%2Fimg.png)

<https://mumbaifaucet.com/>

> 24 시간 마다 **'1 Matic'** 씩 받을 수 있다.

해당 faucet 페이지에서 받은 Matic 을 모두 소진하였을 경우,<br>
다른 faucet 페이지에서 추가로 받을 수 있다.

<https://faucet.polygon.technology/>

## Reference

> <https://wavescats.github.io/blockchain/2022/06/04/bc47.html>
