---
layout: post
title: "[React] 프로젝트 생성 시 발생한 에러 'npx create-react-app'"
subtitle: #부제목
categories: Error
tags: [리액트]
---

### 에러 확인
---

새로운 프로젝트를 위해 npx 명령어를 입력하던와중 에러가 발생했다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d0e13855-3655-49ef-8fad-c01986ec3da8/%EB%A9%8B%EC%82%AC%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%83%9D%EC%84%B1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T070121Z&X-Amz-Expires=86400&X-Amz-Signature=ef1ffa2bb5a50d741ded857a157521d420f534680047f3d56a07a027f4ca587d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22%25EB%25A9%258B%25EC%2582%25AC%25ED%2594%2584%25EB%25A1%259C%25EC%25A0%259D%25ED%258A%25B8-%25EB%25A6%25AC%25EC%2595%25A1%25ED%258A%25B8%25EC%2583%259D%25EC%2584%25B1.JPG.jpg%22&x-id=GetObject) 

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ba23ba63-6744-42a7-9c61-0f9e37eeb85a/%EB%A9%8B%EC%82%AC%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%83%9D%EC%84%B1-%EC%98%A4%EB%A5%98.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T070223Z&X-Amz-Expires=86400&X-Amz-Signature=06ee7f0569c272d59274231261b0c60c67eda03f35f23ffb0e76b1976103e420&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22%25EB%25A9%258B%25EC%2582%25AC%25ED%2594%2584%25EB%25A1%259C%25EC%25A0%259D%25ED%258A%25B8-%25EB%25A6%25AC%25EC%2595%25A1%25ED%258A%25B8%25EC%2583%259D%25EC%2584%25B1-%25EC%2598%25A4%25EB%25A5%2598.JPG.jpg%22&x-id=GetObject)


에러를 살펴보면,<br>

> *name can no longer contain capital letters

npm이 사용하는 명령어의 일부이거나 프로젝트명에<br>
대 소문자 또는 특수기호를 입력하지 말라는 뜻 이다.
<br>

아마, 프로젝트를 생성하기 전<br>
프로젝트를 위한 빈 디렉토리를 생성하고 명령어를 입력해서 발생했던 실수인것같다.
<br>

> 생성하는 리액트 프로젝트명에는 대문자나 특수기호가 포함되어있는지 꼭 확인하자.

<br>
<br>

### 에러 해결
---

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d0ece129-5f2f-4fc4-bb83-ac153b4e7f79/%EB%A9%8B%EC%82%AC%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%83%9D%EC%84%B1-%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T070718Z&X-Amz-Expires=86400&X-Amz-Signature=f87c68966363641839d843cd8888be9c8ff71f773125ba3df2233110d97e140b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22%25EB%25A9%258B%25EC%2582%25AC%25ED%2594%2584%25EB%25A1%259C%25EC%25A0%259D%25ED%258A%25B8-%25EB%25A6%25AC%25EC%2595%25A1%25ED%258A%25B8%25EC%2583%259D%25EC%2584%25B1-%25EC%2598%25A4%25EB%25A5%2598%25ED%2595%25B4%25EA%25B2%25B0.JPG.jpg%22&x-id=GetObject)

프로젝트명을 소문자로 변경하니 정상적으로 실행됨을 알 수 있다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/77cf99b5-dae5-4345-b58b-0a4ad6e06c71/%EB%A9%8B%EC%82%AC%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%83%9D%EC%84%B1-%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0-%EC%83%9D%EC%84%B11.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T070818Z&X-Amz-Expires=86400&X-Amz-Signature=e96d9bcb237004b942750a4f3b56cdc2a41bb132c7f2e1fd78b5998c4c11e1b4&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22%25EB%25A9%258B%25EC%2582%25AC%25ED%2594%2584%25EB%25A1%259C%25EC%25A0%259D%25ED%258A%25B8-%25EB%25A6%25AC%25EC%2595%25A1%25ED%258A%25B8%25EC%2583%259D%25EC%2584%25B1-%25EC%2598%25A4%25EB%25A5%2598%25ED%2595%25B4%25EA%25B2%25B0-%25EC%2583%259D%25EC%2584%25B11.JPG.jpg%22&x-id=GetObject)

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a74f622f-c0d1-43a8-88ad-be696cc2b742/%EB%A9%8B%EC%82%AC%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%83%9D%EC%84%B1-%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0-%EC%83%9D%EC%84%B12.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230130T070833Z&X-Amz-Expires=86400&X-Amz-Signature=6aced9d6662f945df6e133e4085c27e3210eb78b79ac2c44f4ccffe92452a3a4&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22%25EB%25A9%258B%25EC%2582%25AC%25ED%2594%2584%25EB%25A1%259C%25EC%25A0%259D%25ED%258A%25B8-%25EB%25A6%25AC%25EC%2595%25A1%25ED%258A%25B8%25EC%2583%259D%25EC%2584%25B1-%25EC%2598%25A4%25EB%25A5%2598%25ED%2595%25B4%25EA%25B2%25B0-%25EC%2583%259D%25EC%2584%25B12.JPG.jpg%22&x-id=GetObject)