---
layout: post
title: "[React] 띄어쓰기의 중요성"
subtitle: #부제목
categories: Error
tags: [리액트]
---

### 에러 확인
---

이미지 갤러리를 클론코딩하던 와중에 발생한 에러이다.
<br>

아래와 같이 사용자가 추가한 이미지가 row 형태로 나열되어야 하는데,

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/14a1dd94-1fa6-45b9-ac0e-ce0d171f7ba8/imagebox5.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T072315Z&X-Amz-Expires=86400&X-Amz-Signature=2a4268f9c20001eef2481984c6c9fc1efa978f1bbbfc578ff1c2002ab2842639&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox5.JPG.jpg%22&x-id=GetObject)

내가 작성한 프로젝트에서는 colums 형태로 나열되어 출력되고 있다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1ec01dc5-c3c9-4d7d-ab9a-99ace8d4365d/imagebox1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T072616Z&X-Amz-Expires=86400&X-Amz-Signature=f214c2976738493de79929d0c6b0a458d2ab3b2d737888a8cf137e522b16ae11&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox1.JPG.jpg%22&x-id=GetObject)

이미지가 추가되는 부분을 개발자도구를 열어 확인해 본다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4e20c8a1-a56c-42f5-a386-6c550ab59d00/imagebox2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T072711Z&X-Amz-Expires=86400&X-Amz-Signature=0ff1053c3adcf3a6a1005bad34bf1f446d10bfa216da1f1a252d88645b1796fd&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox2.JPG.jpg%22&x-id=GetObject)

해당 코드를 열어 확인해보자.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/89ea91f2-39f7-4b42-803a-c5cda9367927/imagebox3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T072815Z&X-Amz-Expires=86400&X-Amz-Signature=91adc5c2cee9cb1e5ee9d7b9ac78337065a5e383ec2c37559b67a52bb8656015&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox3.JPG.jpg%22&x-id=GetObject)

이상한 부분이 있다.
이미지가 추가되었을 때 'row' 라는 클래스를 생성해 주었는데,<br>
개발자도구에서 확인해 보니 앞의 클래스와 합쳐보이게되어<br>
'row' 클래스에 부여한 스타일이 적용되지 않는것 같다. 

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b578daf7-a79b-42af-a48b-f218b15dc3ca/imagebox4.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T093300Z&X-Amz-Expires=86400&X-Amz-Signature=940731ea5fb05298de95b17e3de8772b343264bd033f106e6ac275c297545d0e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox4.JPG.jpg%22&x-id=GetObject)


### 에러 해결
---

> 개발자도구에서 확인했던 className 에 공백을 추가하여<br>
클래스 간의 구분을 짓고,<br>
이미지가 추가된 경우 생성되는 className 인 'row' 에 스타일을 적용시킴.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2795eeb4-6464-4b84-ae85-45c1cd74d8d6/imagebox6.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T093425Z&X-Amz-Expires=86400&X-Amz-Signature=aebfce354dbe91ab941434fde0a0768c1e3bb1f17ec1774d883aa73f0471255a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox6.JPG.jpg%22&x-id=GetObject)

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/008a5c2a-f1cc-43ad-9f80-c1245899f557/imagebox7.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T093623Z&X-Amz-Expires=86400&X-Amz-Signature=45052236c3c75293f8e644538e7648139b8a970505ebcd2f8dce24724603b83c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox7.JPG.jpg%22&x-id=GetObject)
<br>
<br>

추가한 이미지에 flex-direction 속성이 정상적으로 적용되어 출력된다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/de6d44d0-e291-434d-af4c-7cc6bb3e8996/imagebox8.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T093636Z&X-Amz-Expires=86400&X-Amz-Signature=36aa80fe5bde999b592300499f6b3ac6b839c3a94ada0cb7a4ad18bb51b1f4b2&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox8.JPG.jpg%22&x-id=GetObject)