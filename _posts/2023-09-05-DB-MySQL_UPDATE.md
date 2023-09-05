---
layout: post
title: "[DataBase] MySQL 의 쿼리문을 사용하여 DB 업데이트하기 (UPDATE, WHERE) 🐬"
subtitle: #부제목
categories: [DataBase]
tags: [뷰js, TIL, DB, MySQL]
---

## 개요 🙋

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkYd5R%2FbtstaBSrECL%2FWSbBkCVtX9ve9o5GxXe5tK%2Fimg.png)

이번 포스팅에서는 `MySQL` 에서 제공하는 **GUI 프로그램을 사용**하여<br>
DB 를 업데이트하는 과정을 정리 해 보려고 한다.

---

### DB 확인 🌻

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCrans%2Fbtss3Ebtw9Y%2FJeT6TivTlKGtyksZDNz0O1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmjKtL%2Fbtss8kKuXKN%2FiwKcjMQIDrLZLEjmafEiBk%2Fimg.png)

해당 DB 는 `Vue.js` 앱에서<br>
리스트렌더링을 통해 출력된 아이템들의 카테고리를 `idx` 로 구분짓기위해 생성한 테이블이다.

![](https://blog.kakaocdn.net/dn/daRqpJ/btss72J54pW/hvDALrdiSDfskRVjIaJud0/img.gif)

---

### UPDATE 🌵

**콘솔 창에서 CLI 명령어로 쿼리문을 날려 DB 를 수정할 수도 있지만,**<br>
이번 포스팅에서는 **GUI 로 DB 를 업데이트한다.**

```sql
UPDATE [테이블명] SET [필드명]=[변경할 값] WHERE [PK]=[PK 값];
```

나는 위 쿼리문을 통해 DB 의 값을 수정했다.<br>
`PK` 에는 변하지 않는 고유한 값을 지정해 주었고,<br>
해당 테이블에는 `idx` 가 `index` 의 역할을 해 주고 있으므로 지정 해 주었다.<br>

만약,<br>
`users` 테이블에서 `username` 이 `'john_doe'` 인 사용자의 이메일을 변경하려면<br>
아래의 쿼리문을 사용할 수 있다.

```sql
UPDATE users SET email='new_email@example.com' WHERE username='john_doe';
```

실제 내가 사용한 쿼리문은 다음과 같다 🔔

```sql
UPDATE zeroquest_kor.data_mall_categorys SET name='업사이클' WHERE idx=1;
UPDATE zeroquest_kor.data_mall_categorys SET name='다회용기' WHERE idx=2;
UPDATE zeroquest_kor.data_mall_categorys SET name='친환경 ' WHERE idx=3;
```

여러개의 idx 를 변경 해 주어야 하므로 중첩된 코드를 반복해서 사용했다.<br>

> 이 부분에 대해서는 축소할 수 있는 부분이 있을것같다 ❗️ => Refectoring ✔️

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1Syuj%2Fbtss8kjqK21%2FkY06KpYcuIlmcdLwGQBP31%2Fimg.png)

> 쿼리문을 작성 했으면, 항상 ; 세미콜론을 찍어 쿼리문을 끝내주자 ❗️

상단의 번개 ⚡️ 모양을 클릭하면 작성된 쿼리문을 적용시킬 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBJptm%2FbtstayuF3tH%2Fd40LK0MjKzgBvJ2rxIu83K%2Fimg.png)

수정된 사항을 하단의 `Output` 탭에서 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPda6y%2Fbtss8izba24%2FwppK2aWq2rFf9md1z4BcQk%2Fimg.png)

![](https://blog.kakaocdn.net/dn/m55xW/btstfP3itik/NVJbObufT2RguuYgG0Syc1/img.gif)

---

## Reference 🌊

> <https://reallemonjuice.tistory.com/32><br><https://blog.naver.com/15elly/221862179282><br><https://lovelydiary.tistory.com/29><br><https://velog.io/@shinsw627/Mysql-workbench-%EC%97%90%EC%84%9C-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%88%98%EC%A0%95%EC%9D%B4-%EC%95%88%EB%90%A0-%EB%95%8C-%ED%95%B4%EA%B2%B0%EB%B2%95>
