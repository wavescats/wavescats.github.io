---
layout: post
title: "[React] 에러는 없는데 페이지 랜더링이 되지 않을 때"
subtitle: #공공데이터 / Pandas
categories: Error
tags: [리액트]
---
### 에러 발생
---
npm start 명령어로 리액트 서버를 실행시켰더니,<br>
에러 없이 실행됨을 확인했다.
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d3b4f2f7-2778-4b50-bbf5-0bd75894f757/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T173126Z&X-Amz-Expires=86400&X-Amz-Signature=f7a27c5c59565cc98362352510da2e2a160ac054cd57375063efd5c847fe6c49&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### 에러 확인
---
하지만, <br>
어째선가 구성한 페이지가 보이지 않아 콘솔창을 확인 해 보니 에러 메세지가 있다.
> Uncaught Error: useNavigate() may be used only in the context of a <'Router'> component.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e61d7b9b-ba2b-4cd8-824a-8a2f90f3fa5b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T173310Z&X-Amz-Expires=86400&X-Amz-Signature=a4eca00784524ce3de2736aeb1d4e2ed03b267670ca82a2dc185cb259468d860&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

오류 메세지를 확인해보니, <br>
'useNavigate() 함수를 Router 컴포넌트 내에서 사용할 수 없다'<br>
라는 형태의 오류인 것 같다.

### 에러 해결
---
코드를 살펴보자.
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1187b191-fd40-40b1-b5a3-d59739ec28f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T173605Z&X-Amz-Expires=86400&X-Amz-Signature=61e1778678877795cd1ce70203e936f76f8c22c3e091338b7d6c9bc7f2a2d434&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5313a87f-13c9-44c0-96be-2d90dd8ddeb4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T173623Z&X-Amz-Expires=86400&X-Amz-Signature=dc275b2471d8743af2ab1bf9e188f9c41159d70fadb608b8dcd310e1b66a6cb1&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

복.붙 해온 코드에서<br>
정의된 useNavigate 를 담은 변수인 navigate 부분을 주석 처리 해주니 정상적으로 동작함을 볼 수 있었다.

> 현재는 라우팅 기능이 구현되지 않은 단면적인 컴포넌트 이며,<br>
세부적인 DB 연결 및 테이블 생성 작업이 필요할 것 같다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8ee2eb30-9780-4e71-a863-eee267baac6f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230127%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230127T173744Z&X-Amz-Expires=86400&X-Amz-Signature=366ef6ab67188ef1103d31b2d45278f14dcaf081e4027b5cdc62a4db97aee66f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)