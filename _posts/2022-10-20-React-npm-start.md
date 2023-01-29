---
layout: post
title: "[React] 프로젝트의 npm start 가 실행되지 않을 때"
subtitle: #공공데이터 / Pandas
categories: Error
tags: [리액트]
---

### 에러 확인
---
npm start 명령어 실행 시 에러 문구는 출력되지 않고,<br>
아래와 같이 랜더링이 되지 않고 자동으로 탈출 되는 현상이 있었다.
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/397c7963-3563-48c1-8945-1d558352143a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T172514Z&X-Amz-Expires=86400&X-Amz-Signature=66aad80512d95943e32d27d022c36af8001361aadb8ea5251cf1dea6dacb1df3&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

구글 검색을 해 보니<br>
package.json 의 scripts 부분에 아래와 같은 옵션이 추가되어있었다.
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0993da7b-961a-4bfd-9a2d-544d3500a5f1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T172738Z&X-Amz-Expires=86400&X-Amz-Signature=2068d939ebd2068d76172447e15c705d6b46d8167f9a667ea2042a44491faaac&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)


실행 순서는 (&& 기준) 앞 구문 이 먼저 실행되고,<br>
뒤에 있는 react-scripts start 구문이 실행되는데<br>
먼저 실행되는 앞 구문에서 버전 관련하여 오류가 발생하여<br>
뒤에 있는 구문이 실행이 되지 않았다.
<br>
<br>

### 에러 해결
---
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c32459ea-6f6d-4c70-9ea3-bc877f593779/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230129%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230129T172924Z&X-Amz-Expires=86400&X-Amz-Signature=1b139e306beb4f1c5bc7b07e52139163485085ee63a084ac5d4cdf61b9e526dc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

다음과 같이 오류가 발생하는 앞 구문을 지워주고 실행하니 정상적으로 랜더링이 되었다.