---
layout: post
title: "[React] 크롤링이란 ? (Feat.SEO ⚡)"
subtitle: #부제목
categories: React
tags: [리액트, 크롤링, SEO, TIL]
---

## 개요 🔔

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdzfdyK%2FbtsC0aDoLlo%2FGzNZxU3yHMuhGWbDGBAKK0%2Fimg.jpg)

정보의 바다라고 불리는 웹 사이트는 지금 이 시간에도 **무수히 많은 정보**가 쏟아져 나오고 있다.<br>
이처럼 방대한 양의 정보(데이터) 를 사용자에게 보다 **쉽게** 전달하기 위해<br>
우리 (프론트엔드 as 개발자) 는 페이지들을 인덱싱 하여 화면에 렌더링 해 준다.

만약,<br>
가공되지 않은 데이터를 누군가가 인덱싱 & 저장 하여 관리하지 않는다면,<br>
사용자는 해당 컨텐츠에 접근할 수 있는 방법이 존재하지 않을 것이다.

그래서 등장한 개념이 **`크롤링`** 이고,<br>
이를 보다 쉽게 사용하기 위해 소프트웨어로 감싼것을 **`크롤러`** 라고 한다.

> 위키 백과 👇<br><https://namu.wiki/w/%ED%81%AC%EB%A1%A4%EB%A7%81>

그럼,<br>
크롤링을 사용해야하는 이유는 뭘까 ?

결론부터 말하자면 **`당신의 시간은 소중하니까`** 라고 할 수 있다.<br>
즉,<br>
필요한 데이터를 **복사 + 붙여넣기**를 통해 번거로운 작업을 하는것이 아닌<br>
크롤링의 자동화를 통해 정보(데이터)를 취득하는 시간을 **효율적으로 관리**한다는 점에 의미를 두고 있다.

> 밈 으로 👉 **`'진정한 개발자는 게을러야 한다'`** 라는 말이 있듯,<br>개발자라면 **반복적인 작업을 지양**해야하며<br>이는 자동화된 프로그램을 만들어 업무 효율을 증가시킨다 라는 의미를 가진다.

---

## Deep inf 👀

위 모든 과정을 가장 잘 다루는 곳은 어딜까 ?<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbs7Y9m%2FbtsCZ613WfE%2FnADwFosIINxukOK7RJazz1%2Fimg.png)

바로, **`Google`** 이다.

**`Google`** 은 앞서 말했듯,<br>
무한히 늘어나는 웹 페이지를 인덱싱함으로 인해 보다 쉽게 정보를 제공하여 사용자 경험을 증가시켜 준다.

해당 분야에서 가장 대표적인 소프트웨어로는,<br>
**`Python`** 의 **`Beautiful Soup`** 이 있고,<br>
**`Java`** 의 **`jsoup`** 이라는 HTML 파싱 라이브러리가 존재한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd29lh0%2FbtsCU0an8aY%2FGCEC8uIdY6zaz4MegHp071%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwEz7c%2FbtsCRg6expe%2FcNTgPDk6ndIP4ApwmFKMxk%2Fimg.png)

실제로 구글에 **`크롤링`** 이라는 키워드로 검색하면,<br>
**`Beautiful Soup`** 를 활용한 예제가 대부분임을 확인할 수 있다..🙄

하지만 **`Beautiful Soup`** 같은 경우는 동적으로 데이터를 추출하는 크롤러가 아닌,<br>
정적으로 이미 그려진 웹 페이지를 **`Seed`** == **`baseURL`** 로 하여<br>
데이터를 추출하는 **`스크래퍼`**, **`스크래핑`** 쪽에 조금 더 가깝다.

스크래퍼를 동적으로 추출하는 크롤링의 개념을 적용하기 위해 등장한 라이브러리가<br>
**`Python`** 의 **`Selenium`** 이다.

**`Selenium`** 은,<br>
다양한 옵션을 제공하는데 크롤링은 방대한 양의 데이터를 추출해야 함으로 **`자동화`** 를 목적으로 두고있기 때문에,<br>
**`WebDriver`**와 **`Headless`** 옵션을 통해 **`CLI`** 창에서 데이터를 추출하고 가공할 수 있다.

추가적으로 우리가 주로 다뤄야하는, 다루는 언어인 **`JavaScript`** 에서도<br>
위와 같은 기능이 구현된 라이브러리가 존재한다.

**`Cheerio`** 와 **`Puppeteer`** 가 있는데,<br>
바로 다음 포스팅에서 두 라이브러리의 차이와 예제를 통해 학습했던 방법을 정리하려고 한다.

---

## Robots.txt 🤖

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFA952%2FbtsCUzKG0Om%2FC8TSI9iHu0VnfHkFC6T7V0%2Fimg.png)

아, 이제 크롤링에 대한 어느정도 이해도 끝났고,<br>
내가 원하는 데이터를 추출하여 멋진 웹 사이트를 만들어 봐야지 ❗❗

라고 한다면 큰 실수일 수도 있다 🚫<br>
보통 웹 사이트에는 크롤링이 가능한 허용범위 ✅ 에 대한 정보가 담긴 문서가 존재한다.<br>
이와 같은 정보는 **`Robots.txt`** 파일에 담겨있는데,<br>
이 파일은 검색엔진최적화(**`SEO`**) 와 밀접한 관계가 있다.

> 크롤링 할 **`baseURL`** 뒤에 **`/robots.txt`** 를 입력 해 주면,<br>해당 사이트에 대한 크롤링 정책을 확인할 수 있다.<br>👉 네이버의 경우 **`.txt`** 파일이 다운로드 된다.

단, **`Params`** 로 지정된 하위 페이지 경로에서 **`robots.txt`** 를 붙이게 되면,<br>
간혹 정책을 확인할 수 없는 경우도 있기에<br>
하위 경로를 모두 제거한 최 상위 (메인 URL) 에서 확인하는게 가장 이상적인 방법이다 💌💨

### SEO ⚡

아래 사진은 구글 URL 에서 **`robots.txt`** 를 추출하여 확인한 이미지 이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FljtdP%2FbtsCOEs7r52%2FON0xFuiLdkt3rD0Ns2Yxe0%2Fimg.png)

> 출처 👇<br><https://developers.google.com/search/docs/crawling-indexing/robots/create-robots-txt?hl=ko>

이 이미지가 의미하는 바는 다음과 같다.<br>

- 이름이 **`Googlebot`** 인 사용자는 **`baseURL`** 에서 **`/nogooglebot`** 으로 시작하는 URL 을 크롤링 할 수 없다.<br>
  👉 **`https://exaple.com/nogooglebot/...`**
  <br><br>
- 그 외 사용자 (**`*`** == **`와일드카드`**) 는 모든 경로 (**`/`**) 에서 크롤링을 할 수 있다.<br>
  👉 해당 부분은 생략 가능
  <br><br>
- **`Sitemap`** 은 크롤링 봇에게 알려주는 **가이드** 정도의 의미를 담고 있으며,<br>
  **`.xml`** 형식의 파일로 작성되어있다.<Br>
  👉 해당 파일은 URL 뒤에 심어주는 형식으로 구성되어 있으며,<br>
  **`Google Docs`** 를 참고하면 해당 파일을 생성하는 **가이드라인**과 **커스텀이 가능한 프리셋**을 제공하고 있다.
  <br>

또한, 이 **`robots.txt`** 파일에 담긴 **`Googlebot`** 을 통해<br>
우리가 만든 사이트를 검색엔진에 잘 노출시킬 수 있도록 최적화 시킬 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft92Nv%2FbtsCP21xOVN%2FB7kULrAtTcq7yX2iRobkE0%2Fimg.png)

검색엔진이 자료를 긁어가는 주기가 정확하진 않지만,<br>
구글을 기준으로 한다면 1일 1회 이상 우리가 만든 **`DDocker`** 라는 사이트를<bR>
**`robots.txt`** 와 **`Sitemap.xml`** 을 기준으로 웹 사이트 안의 모든 정보를 크롤링 하여<br>
구글 검색엔진 DB 에 저장하는 형태로 구현되어 있다.

우리는, 보다 효율적으로 **검색엔진에 내 서비스를 노출**시켜주어야 하는걸 목표로 두고 있기에<br>
**`robots.txt`** 를 검색엔진에 노출이 잘 되게끔 설정 해 주어야 한다.<br>
이 파일은 프로젝트 내부 **`/public`** 경로에 생성하여 빌드하면 자동으로 반영이 된다.

> 설정 후 실제 반영은 24시간 정도 이후부터 된다고 한다.

실제 검색엔진에 잘 노출이 되게끔 하기 위해서는<br>
크롤링 봇 🤖 에게 알려주는 **`robots.txt`** 와 **`Sitemap.xml`** 도 중요하지만<br>
코드 내부에 정의하는 각종 태그에도 영향을 받는다.

검색엔진 최적화를 위해 태그를 수정하는 방법은 아래 링크를 참조하여 적용하면 좋을 것 같다.<br>
<https://yozm.wishket.com/magazine/detail/1540/>

---

## Reference 🌊

> <https://jins-sw.tistory.com/55><br><https://www.fun-coding.org/post/crawl_basic2.html#gsc.tab=0><br><https://brunch.co.kr/@webbible/5><br><https://youtu.be/xGkftwkoJK4?si=IhnTcFQy8qQJzJr4>
