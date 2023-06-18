---
layout: post
title: "[Blockchain] Klaytn 체인에서 Generative Art 방식을 사용하여 NFT 민팅해보기"
subtitle: #부제목
categories: Blockchain
tags: [블록체인, NFT, TIL]
---

### 개요

이번 포스팅에서는 Klaytn 체인 위에서 NFT 를 발행하고 조회하며<br>
이를 분산형 저장소에 업로드하고,<br>
간단한 민팅 페이지를 만들어 보는 실습을 해 보려고 한다.

> <https://github.com/LgcLazyboy/hashlips_art_engine>

먼저,<br>
위 레파지토리에서 해당 소스코드를 Clone 해 로컬로 가져온다.

### 설치 및 실행

```bash
npm install canvas
```

**Canvas** 는 HTML5 요소를<br>
Node.js 환경에서 사용할 수 있도록 해 주는 라이브러리 이다.<br>
해당 라이브러리를 통해<br>
JavaScript 코드에서 그래픽 작업을 수행하고 이미지를 생성 및 수정할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJ6WZf%2FbtsedaVGRGd%2F6yEkOk0LIRppUXVpMNBJRk%2Fimg.png)

```bash
npm install
```

깃허브 레파지토를 로컬로 Clone 해 가져올 경우,<br>
프로젝트 내부에 존재하는 `.gitignore` 파일로 인해<br>
`./nodemodule` 폴더가 포함되지 않은 채 다운로드 된다.<br>
이를 해결하기 위해<br>
Git Clone 을 했다면 `npm i` 명령을 통해<br>
프로젝트에(`./package.json`) 적용되어있는 라이브러리를 먼저 설치 해 주는것이 좋다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtD3ji%2Fbtsd9NGI08K%2FdhbKqlPDfB7PqVvkoNcyT0%2Fimg.png)

```bash
npm run build
```

해당 명령을 통해 프로젝트를 실행한다.<br>
`./package.json` 을 확인 해 보니<br>
`npm run build` 명령을 실행 할 경우<br>
`index.js` 를 실행하는 구조로 지정되어 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeHClMZ%2Fbtsd0vtA5xD%2FrFFH25PUOK3Mck9ApoKKtK%2Fimg.png)

명령을 실행하니<br>
약 100 개의 무언가가 실행되며,<br>
디렉토리 내부에는 build 디렉토리가 새로 생성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdTQ8ro%2Fbtsd0SbuVN7%2FQg2zDdoj2RM6cpOwW0B6ik%2Fimg.png)

디렉토리 내부에는 `images` 와 `json` 디렉토리가 생성되며

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlEWfc%2Fbtsd1iHKyp0%2FAcrhUrsjpdhc6u5iCtQz71%2Fimg.png)

그 안에는,<bR>
각각의 고유한 이미지 파일과 `json` 형태의 데이터가 담긴 파일들이 생성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJpQFY%2Fbtsd4eSbsTk%2F4By231aY4YxFfVn8b1Mro0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXwsh9%2Fbtsd6sW7Rkq%2FKlUg0D2A0R2gg6du80JTS0%2Fimg.png)

### 등장빈도

대게
특성명 #등장빈도율로 파일명을 설정한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fx7Zos%2FbtskhLJo14q%2FgKWBLLIkNwrcQqMin0EUBk%2Fimg.png)

해당 파일 명을 살펴보면<br>
분모를 100 으로 기준하여 설정할 경우 30 의 기준으로 등장하는 비율로 지정이 되어있다. <br>

> 30/100, 1/100, 15/100, 15/100, 15/100, 20/100, 4/100

이 기준은<br>
랜덤 조합 시 레어리티 빈도를 지정하여 등장하는 기준이다.

### IPFS 에 소스파일 업로드하기

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRsj0X%2Fbtsd9MHRXF7%2F4Aot8Toy7f6khpQjNKkpc0%2Fimg.png)

> <https://nft.storage/>

로그인을 위해 이메일을 입력 후 버튼을 클릭하면,<br>
입력한 이메일에 cirnfim 메일이 온다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F2MAA8%2FbtsejKWILBJ%2Fnfh9Q4Kx7m55xut0masVQ0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4iJpP%2Fbtsecvy4jF3%2FrKh3rumLtpb8RNYNE3zHk1%2Fimg.png)

로딩 화면이 끝나게 되면 페이지가 리다이렉션 되며,<br>
로그인 버튼이 로그아웃 버튼으로 바뀌게 되며 로그인 상태로 변환된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FM9WPE%2Fbtsd9exn0fU%2Fa7fwd6UrTKWHMmtvCEAWK0%2Fimg.png)

API Key 탭 에서 새로운 Key 를 생성 해 준다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbf8wlb%2FbtsejK3qNFU%2FmDldnLrNbX27hUxsyaHYZk%2Fimg.png)

이름은 임의로 설정 해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtDBGR%2Fbtseh7YKhcV%2FDRtzImc6fJXDVfGU4CuN81%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblJEqt%2Fbtsd0uVPnLH%2FIrfT1Jf34AK4fAyUNPsPc1%2Fimg.png)

발급받은 API 키를 `store.mjs` 내부에 넣어준다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYQfVL%2Fbtsd1inuXTX%2FOfkOzUJvZRKcsWUY7rUvkK%2Fimg.png)

파일을 저장 후 터미널에서 `node store.mjs` 명령을 실행하면,<br>
다음과 같은 데이터가 담긴 객체가 생성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcj1qGg%2Fbtsd9MgKWOg%2Fwla26FvCkbdewaAkZTQ3Xk%2Fimg.png)

다시 <nft.storage> 에 접근 해 `Files` 탭에 접근 해 보면,<br>
파일이 추가 된 것을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdkex7J%2Fbtsd3fc0Lwe%2FjHGqBfsuucsDKd1We9dm1K%2Fimg.png)

생성된 파일에 CID 에 접근해보면,<bR>
생성된 100 개의 이미지파일을 분산형 스토리지인 IPFS 에 업로드 한 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyA65b%2FbtsejKh7il9%2FhQ0Lx01EpBIzz3WBCKSIr1%2Fimg.png)

해당 이미지 정보를 build/json 내 1.json 을 확인 해 보면<br>
image 가 복사한 IPFS URL 로 변경된것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8zIDu%2Fbtsd6toeyE6%2F8WAdrkMKgTK1DRem2DK93K%2Fimg.png)

다음으로는 이미지에 해당하는 부가정보(메타데이터)를<br>
IPFS 서버에 업로드하려 한다.<br>
<br>

이미지 파일이 담긴 URL 을 복사하여<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIM0bA%2Fbtsd9MulZmO%2FuvnBUXQWRCvfJMTa7fHJUK%2Fimg.png)

`./addr.mjs` 에 붙여넣어준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbQghJh%2Fbtsd5YhjmIv%2FI2HiGioM15H8PwX5eGpwkK%2Fimg.png)

터미널에 `node addr.mjs` 실행 !

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgkVql%2FbtseoYmB6Wa%2F2moBLt6ICpB67SGKB2I9B1%2Fimg.png)

명령을 실행하게 되면<br>
`./build/json/1.json` 의 image 주소가 변경됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8zIDu%2Fbtsd6toeyE6%2F8WAdrkMKgTK1DRem2DK93K%2Fimg.png)

마찬가지로 `storejson.json` 파일 내부에 api 키를 입력 해 준뒤

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fchr7dT%2Fbtseh8QSeAN%2FBJZkDE1A7k9UXLfTs6VHK0%2Fimg.png)

터미널에 `node storejson.mjs` 명령을 실행하면,<br>
IPFS 서버에 파일이 추가로 생성 됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbI75KR%2Fbtsd3eZsvP8%2FNjHpIkHVWG5OOgYyY2R0A1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPzh2T%2Fbtseh7qSyrl%2FLlazKXL7ghmlEsOWPECPL1%2Fimg.png)

생성된 파일의 CID 로 접근 해 보면,<br>
추가로 업로드 한 부가정보(메타데이터) 가<br>
IPFS 서버에 업로드 됨을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcdhUO%2Fbtseh7ErNmm%2FKzov0G9CHe0tCrBo3gnPh0%2Fimg.png)

### Remix

이제 IPFS 에 업로드한 데이터를 기반으로<br>
클레이튼 체인 위에서 스마트컨트랙트를 배포하려한다.

Wallet 은 KaiKas 를 사용하며<br>
Baobab 테스트넷으로 전환하여 사용할 예정이다.

> Faucet 과정 생략.

---

> <https://github.com/LgcLazyboy/KIP17NFTContract>

해당 레파지토리로 접근하여<br>
`KIP17NFTTokenFlatten.sol` 컨트랙트를 Remix 에 불러온다.

불러온 컨트랙트를 컴파일 해 보면 에러가 발생하는데,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fwy7Ma%2Fbtskg8kOGWl%2FkxpiDUo66T2nC0SoCDJR91%2Fimg.png)

이 때<br>
컴파일러의 버전을 0.5.17 로 변경 후 다시 컴파일을 진행

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgwSg7%2FbtskhaCGsI5%2F7LOxqzUpHhaYwZMZuoHNsk%2Fimg.png)

---

하단에 클레이튼 Deploy 탭으로 접근하여<br>
KaiKas 개인키 주소를 입력 해 준다.
<bR>
<br>
그리고 Contract 부분에는 확장 버튼을 눌러,<br>
`KIP17NFTToken` 을 선택한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC8PYS%2FbtskgdfE1VO%2F831tQfvtCgksBLJs9pVC80%2Fimg.png)

Deploy 탭을 확장하여<br>
Name 과 Symbol 을 지정하여 Transact 버튼을 클릭한다.

> Name -> NFT 프로젝트명<br>
> Symbol -> 비트코인 = BTC 등의 축약어 심볼

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fsq1IO%2FbtskhaWYd40%2F0m2hgbR9iBKfkFkOSkzLkk%2Fimg.png)

생성된 트랜잭션을 확인하고,<br>
Deployed Contracts 에서<br>
복사 버튼을 눌러 스마트 컨트랙트의 주소를 획득한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKVAGj%2FbtskgHAZ3Ll%2FVIRHTS3txhPfoi56BbBmM0%2Fimg.png)

확장 버튼을 클릭하여<br>
컨트랙트에 작성된 함수의 기능을 확인할 수 있다.
<br>

우리는 `setBaseURI` 함수를 사용할 것이며,<br>
이곳에 Copy 한 IPFS URL 을 입력하고<br>
주소 마지막에는 '/' 를 삽입한 후 Transact 버튼을 클릭한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOVxML%2FbtskgHgGKgb%2FfgWBxgzfjJRdeYJ3W7yNUK%2Fimg.png)
<br>
민팅된 NFT 의 판매 설정을 초기화 하는 함수인 <br>
`setupSale` 을 다음과 같이 입력 후 Transact 버튼을 클릭한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcBW18R%2Fbtskg7T4Wi5%2FZ2TqL8EfBsDweu4yL6ALTk%2Fimg.png)

`setPublicMintEnabled` 함수를 `true` 로 입력 후 Transact 버튼을 클릭한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtjxRa%2Fbtskgp8pIwu%2FBeATo8AbkWxsVtFpGEauk0%2Fimg.png)

> 이 함수는,<br>
> 퍼블릭 민팅 설정값을 불가능에서 -> 가능으로 변경하는 의미이다.

---

#### 함수

- `newAntibotinterval`
  - 연속 시도 방지 지연시간
  - bot 을 통한 불공정 민팅 방지

- `newMintLimitPerBlock`
  - 한 번의 트랜잭션에 최대로 민팅할 수 있는 개수

- `newMintLimitPerSale`
  - 이번 민팅 기간동안 한 지갑이 최대로 민팅할 수 있는 개수

- `newMintStartBlockNumber`
  - 이번 민팅 기간이 시작되는 블록의 높이

- `newMintIndexForSale`
  - 이번 민팅 기간에 최초로 민팅될 NFT 번호

- `newMaxSaleAmount`
  - 최대 NFT 개수 제한

- `newMintPrice`
  - 민팅 가격 (peb 단위, 10^18 Klay)

---

### 프론트엔드

Deploy 한 컨트랙트를<br>
웹에서 보여주기위한 작업을 한다면 해당 포스팅은 마무리 된다.

> <https://github.com/LgcLazyboy/nft-minting-site>

해당 레파지토리를 Clone 하여<br>
`config.js` 파일 내부에 Deploy 한 컨트랙트의 주소를 넣는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtOaXt%2Fbtskk8jL8lj%2FKAKS7xaXsZgXhNNsY8IdW1%2Fimg.png)

해당 수정사항을 저장하고,<br>
코드가 포함된 폴더를 Netlify 에 업로드 한다

> <https://www.netlify.com/>

해당 과정은 정적인 웹 페이지를 배포하는 과정으로<br>
Netlify 서버에 해당 프로젝트를 배포한 경우<br>
언제 어디서나 URL 을 통해 접근이 가능하다.

> Drag & Drop 방식으로 해당 프로젝트 업로드

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCLcPW%2FbtskifRtJmT%2FTlKwo1K5WVkKvCMo4ZPB11%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbe7h8V%2FbtskgqGx570%2FBYVjIp2HFrkBJUT8Mdjie1%2Fimg.png)

> 배포하지 않은 채 `index.html` 로 접근하여 보니<br>
Wallet 연결이 에러와 함께 되지 않음을 알 수 있었다.

![](https://blog.kakaocdn.net/dn/d0m9L6/btskhaiDVJI/1xUrDTKis5xOSc0yrWNvc1/img.gif)

---

### 민팅

프론트엔드 단 에서 민팅을 시도하면,<br>
트랜잭션을 확인하고 민팅이 완료된다.

이 과정을 opensea testnet 에서 확인 가능하며
지갑 연결을 하고 mycollection 으로 접근하면 서명 메세지가 출력이 된다.
서명을 동의하고 난 후,<br>
내 컬렉션 페이지에서 직전에 민팅한 NFT 를 확인할 수 있다.

![](https://blog.kakaocdn.net/dn/eqL4Uj/btskll4T1zp/VtOfIeADS8aKibvhfrhzNK/img.gif)

해당 NFT 는 등록한 부가정보가 불러와지지 않은 상태이므로,<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmmijy%2Fbtskg7GB20E%2F4OmvZIxPTSfwcJvTaDAJK1%2Fimg.png)

More - Refresh metadata 를 눌러 부가정보를 연동 시킬 수 있다.

그리고,<br>
민팅된 NFT 는 Klaytn 체인 위에서 발행했기 때문에<br>
Klayscope 에서 트랜잭션을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGXDzY%2FbtskrdrInyC%2Fpfq5dESgbDHEccxIigmHxk%2Fimg.png)

### Reference

> <https://github.com/LgcLazyboy/KIP17NFTContract><br><https://github.com/LgcLazyboy/hashlips_art_engine><br><https://github.com/LgcLazyboy/nft-minting-site><br><https://nft.storage/>