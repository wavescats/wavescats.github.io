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

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/14a1dd94-1fa6-45b9-ac0e-ce0d171f7ba8/imagebox5.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T103848Z&X-Amz-Expires=86400&X-Amz-Signature=6d10bafbc5ff4f191c0c13245e5de606467ff78252477c82efe87594ea7c97c7&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox5.JPG.jpg%22&x-id=GetObject)

내가 작성한 프로젝트에서는 colums 형태로 나열되어 출력되고 있다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1ec01dc5-c3c9-4d7d-ab9a-99ace8d4365d/imagebox1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T103821Z&X-Amz-Expires=86400&X-Amz-Signature=7e767e2019a50f7d70bc1f72acfc8ac2f5729c031035049a4fbb30984745ba77&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox1.JPG.jpg%22&x-id=GetObject)

이미지가 추가되는 부분을 개발자도구를 열어 확인해 본다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4e20c8a1-a56c-42f5-a386-6c550ab59d00/imagebox2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T103906Z&X-Amz-Expires=86400&X-Amz-Signature=8205ad0527115e6328a0477877a639a4bbef18b22e6c47c560a8f62ad9da93cf&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox2.JPG.jpg%22&x-id=GetObject)

해당 코드를 열어 확인해보자.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/89ea91f2-39f7-4b42-803a-c5cda9367927/imagebox3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T103925Z&X-Amz-Expires=86400&X-Amz-Signature=48b4d0befa3ca0c06e5f60ba923c7d45718f16f33a5e35edf4b67c3fb325ae72&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox3.JPG.jpg%22&x-id=GetObject)

이상한 부분이 있다.
이미지가 추가되었을 때 'row' 라는 클래스를 생성해 주었는데,<br>
개발자도구에서 확인해 보니 앞의 클래스와 합쳐보이게되어<br>
'row' 클래스에 부여한 스타일이 적용되지 않는것 같다. 

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b578daf7-a79b-42af-a48b-f218b15dc3ca/imagebox4.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T103942Z&X-Amz-Expires=86400&X-Amz-Signature=faf6d20ee4f5ae75f0e96cea1a71861e7ff41535ea51b661b891b1c83c64f24b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox4.JPG.jpg%22&x-id=GetObject)


### 에러 해결
---

> 개발자도구에서 확인했던 className 에 공백을 추가하여<br>
클래스 간의 구분을 짓고,<br>
이미지가 추가된 경우 생성되는 className 인 'row' 에 스타일을 적용시킴.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2795eeb4-6464-4b84-ae85-45c1cd74d8d6/imagebox6.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T104005Z&X-Amz-Expires=86400&X-Amz-Signature=9f0e7e283983baf91af7d367838593dd8a886bdfbb50869a756f934064c15a47&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox6.JPG.jpg%22&x-id=GetObject)

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/008a5c2a-f1cc-43ad-9f80-c1245899f557/imagebox7.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T104016Z&X-Amz-Expires=86400&X-Amz-Signature=08afb911edcd0a977dce4c23fca8906c451181530c5e4a8065dc358bb4cf5bd1&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox7.JPG.jpg%22&x-id=GetObject)
<br>
<br>

추가한 이미지에 flex-direction 속성이 정상적으로 적용되어 출력된다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/de6d44d0-e291-434d-af4c-7cc6bb3e8996/imagebox8.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230131T104030Z&X-Amz-Expires=86400&X-Amz-Signature=8a14c2644996722d890815858815d79c79ec11e821b44327782ced2f9a0ba2ce&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22imagebox8.JPG.jpg%22&x-id=GetObject)