---
layout: post
title: "[React] Webpack 을 활용한 Package.json 의 초기 설정 및 수정 방법"
subtitle: #부제목
categories: TIL
tags: [리액트]
---


## 프로젝트 생성
---

프로젝트 진행을 위해 빈 디렉토리를 생성하고 

`npm init -y` 명령을 통해 package.json 파일을 생성한다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/89d121e8-9a1b-4ac5-859f-7ae056ba1570/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T094631Z&X-Amz-Expires=86400&X-Amz-Signature=8ea491972c8a42b317aee20fbf7debf0846a759d7c447cc62a05c2cc75ac534d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br>

## 패키지 설치
---

다음으로 아래 명령어를 통해 webpack 관련 패키지를 설치해준다.
```
npm i -D webpack webpack-cli webpack-dev-server
```
> 명령어에 쓰여진 -D 옵션은<br>
package.json 의 devDependencies 에 추가하겠다는 의미이다.

<br>

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bed606cd-8fa5-48de-864d-c9b7860c6748/Untitled.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T094724Z&X-Amz-Expires=86400&X-Amz-Signature=8190b2e9ad46110586ab9e76221751cab1821f1aba47f9e2f625eaacf5a6a388&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.jpeg%22&x-id=GetObject)



## 패키지 버전 관리
---

`npm` 명령어로 설치한 패키지의 버전과 강의에서 사용한 버전이 일치하지 않는다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c0225433-dd24-4555-acad-7d855060350b/Untitled.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T095410Z&X-Amz-Expires=86400&X-Amz-Signature=032eae38eb7507def58d485b5d1e6c35a97163bab2d71b98f4c66194e7b04685&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.jpeg%22&x-id=GetObject)
<br>
<br>

이 때,<br>
아래와 같이 package.json 의 버전을 직접 바꿔 준 뒤 저장 하고<br>
npm i 를 실행하면 수정된 버전이 설치된다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3ce92000-a61d-44ad-b562-bcc2647c691a/Untitled.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T095627Z&X-Amz-Expires=86400&X-Amz-Signature=805facad01b9cde3923a2ff181b9b95f378fa17da9c25de7c77691abd860da5c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.jpeg%22&x-id=GetObject)


## Reference
---
### -y 옵션이 뭐지?
> <https://velog.io/@lsh__97/npm-init-y-%EC%9D%98%EB%AF%B8>

### devDependencies 가 뭐지?
로컬에서 개발이나 테스트에 필요한 패키지로, 배포 시 포함되지 않는 영역을 말한다.
> <https://www.codeit.kr/community/threads/29051>