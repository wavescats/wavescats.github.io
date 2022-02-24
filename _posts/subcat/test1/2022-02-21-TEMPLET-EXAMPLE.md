---
layout: post
title: Subcat-Test1-post1
image: 
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  Version 9 is the most complete version of Hydejack yet.
  Modernized design, big headlines, and big new features.
sitemap: false
categories:
  - Subcat
  - test1 
---


* toc
{:toc .large-only}

**링크**

 that reason, a [chapter on images](../../docs/basics.md#adding-images) has been added to the documentation.

 [글씨누르면 링크연결하기](https://www.naver.com)
* * *

>🌈 **결과**  *결과*

><details> 세부정보1<br>세부정보2

</details>

☝ 접기/펼치기 버튼

* * *

<blockquote>
블록
</blockquote>

* * *

~~~html
<details>
<blockquote>
@ ~~~ 로 감싸주면 메모장효과 / 태그 무시
</blockquote>
</details>
~~~

* * *

🌈 **접기/펼치기 버튼**

<details>
<blockquote>
숨김숨김
</blockquote>
</details>

* * *

## 이모지

#### 이모티콘

🖐🙏🍀🌍🌈🔥🙌 
**윈도우키 + ; 누르기**

* * *

## 123 리스트

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

* * *

## 표만들기

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

* * *

### 구역 나누는 선

* * *

## Li 리스트

*   Item foo
*   Item bar
*   Item baz
*   Item zip

* * *

## 수학 수식
>🔍**결과**
~~~
>$$x + y = 1$$
~~~
$$x + y = 1$$

$$\alpha$$


* * *

#### 강조체

<kbd> THIS </kbd>

<a> THIS </a>

<code> THIS </code>

<mark> THIS </mark>

<under> THIS </under>

* * *

#### 유튜브 영상

{% include youtubePlayer.html id="dQw9v7bWbPE" %}

### 슬라이드 이미지 (slick)

<div class="main_center">
    <div><img src= "/assets/img/blog/jj-ying.jpg" style="width: auto; height: 500px;"></div>
    <div><img src="/assets/img/blog/louis-hansel.jpg" style="width: auto; height: 500px;"></div>
    <div><img src= "/assets/img/blog/dark-mode-ii.jpg" style="width: auto; height: 500px;"></div>
</div>
<script>
    $(document).ready(function() {
        $('.main_center').slick({
            autoplay : true, /*자동으로 슬라이딩됨*/
            dots : true, /* 하단 점 버튼 */
            speed : 300 /* 이미지가 슬라이딩시 걸리는 시간 */,
            infinite : true,
            autoplaySpeed : 30000 /* 이미지가 다른 이미지로 넘어 갈때의 텀 */,
            arrows : true,
            slidesToShow : 1,
            slidesToScroll : 1,
            touchMove : true, /* 마우스 클릭으로 끌어서 슬라이딩 가능여부 */
            nextArrows : true, /* 넥스트버튼 */
            prevArrows : true,
            arrow : true, /*false면 좌우 버튼 없음, true면 좌우 버튼 보임*/
            fade : false
        });
    });
</script>