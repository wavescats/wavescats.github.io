---
layout: post
title: "[Data Analysis & EDA] 데이터 로드 중 인코딩 에러"
subtitle: 공공데이터 / Pandas
categories: DA
tags: [Data Analysis & EDA]
---

### 에러 발생

- 공공데이터를 불러오는 과정에서 아래와 같은 오류가 발생했다.

> ParserError: Error tokenlzing data. C error: Expected 14 fields in line 1273, saw 15

![](https://blog.kakaocdn.net/dn/qJ6M5/btrw7Sxs0J5/mi4IxwtvRNZx4s2ZAhX3Jk/img.jpg)

---

### 에러 확인

구글링을 해 보니 몇몇의 행과 열에서 오류가 발생한 듯 했다.<br>
데이터가 그리 크지 않아 직접 실행하여 눈(GUI)으로 확인해봐야겠다.

![](https://blog.kakaocdn.net/dn/LWaFc/btrw8NWYaXB/5KrMPVOOju1cj9rbHQNlkk/img.jpg)


직접 확인 해 보니 한글이 깨져서 오류가 발생한듯 했다.

> 한글이 깨졌을 경우 파일을 유니코드(UTF-8) 로 다시 저장하여 인코딩을 해 주면 된다고 한다.

> <https://m.blog.naver.com/PostView.nhn?blogId=rbamtori&logNo=220744768992&proxyReferer=https:%2F%2Fwww.google.com%2F> 

---

### 에러 해결 시도

파일을 재 인코딩 한 후에 다시 read_csv 를 통해 파일을 불러오니 새로운 에러가 날 반긴다.

> UnicodeDecodeError: 'cp949' codec can't decode byte 0x80 in position 99392: illegal multibyte sequence

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbc7laO%2FbtrxaPmu6fl%2F3v5YVZSKbgWwKCqN2Qu9uK%2Fimg.jpg)

혹시, cp949 가 아니라 utf-8 로 인코딩 했으니 저것도 바꿔줘야되나? 싶었지만..

> UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc0 in position 1: invalid start byte

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZicHT%2FbtrxcMbdRLR%2Fv1N0A0TtzfXmQzXAWrmWXK%2Fimg.jpg)

아니었다.. :cry: <br>

에러를 해결하기 위해 여러 방법을 시도 해 봤지만,<br>
해결하지 못한 채 결국 맨 처음으로 다시 돌아갔다... :weary::weary::weary:

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcREKwL%2FbtrxaOA9YwN%2FCK6ORPOxnKII9UM2NvHPU1%2Fimg.jpg)

---

### 에러 해결 (미완)

마침 강의에서 사용되는 데이터가 1월~6월 의 데이터였는데,<br>
업데이트가 되어 21년 전체의 정보가 담겨있던 데이터라<br>
깔끔하게 한글이 깨지는 부분을 지워버렸다 ^^ (정신건강에 해로울뻔했다)

> 데이터의 양이 많아 일일이 드래그를 하기엔 7 개월 정도 걸릴것같아 단축키를 사용했다.

> 지우고싶은 시작부분에 커서를 놓고 Shift + Ctrl + End 키를 눌러 한번에 드래그

<br>다시 판다스로 돌아와 파일을 불러왔다.

> cvs 파일 이름이 다른 이유는 위 과정을 거친 후 이기 때문.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblfcYx%2FbtrxaiCp3Pp%2FE1B6vnX9H7bbKHZWwrYVFk%2Fimg.jpg)

처음보는 오류가 또 나를 반긴다.<br>
이것저것 하느라 시간이 오래지나 다시 처음부터 해야됬다.<br>
다시금 초심으로 돌아가 기본세팅이라 불리는 명령어들을 실행해줬다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcscOyz%2FbtrxcaKqvBx%2F8bvTHVoDRu3NzDADYdlMck%2Fimg.jpg)

정상적으로 파일도 불러와지고 df 를 통해 담긴 데이터를 확인했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb0iQ1r%2FbtrxeKcToAo%2FwCAw599AN9pUfaG2EnRPr1%2Fimg.jpg)

휴우 편----안.. :dash:<br>
실습을 마저 진행하러 간다.