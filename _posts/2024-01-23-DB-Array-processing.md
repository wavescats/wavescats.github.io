---
layout: post
title: "[DataBase] DB 에 적재할 데이터 가공하기 (Feat.Python) 🦏"
subtitle: #부제목
categories: [DataBase]
tags: [TIL, DB, MySQL, colap]
---

## 개요 🙋

> <https://www.eaten.co.kr/>

위 사이트에서 커피와 관련된 **브랜드별 영양 정보** 를 크롤링하여<br>
필요한 정보만을 가공하여 사용하려고 한다.

크롤링한 데이터는 아래와 같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbR0z7N%2FbtsDKPAz1Xt%2FsUHRBA3yM9hEzK6g8Ekvv0%2Fimg.png)

이 데이터에서 필요한 정보는 **`브랜드`**, **`메뉴`**, **`카페인`** 이다.

먼저,<br>
번거롭지만 수기로 1 차 가공을 통해 아래와 같은 정보를 얻은 상태이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuyWWD%2FbtsDUhaUvn9%2FPRIYGslcfE8x7LoYV40Lg1%2Fimg.png)

이 정보를 바탕으로,<br>
**`MySQL`** 에 쿼리문을 사용하여 데이터를 적재하려고 하는데,<br>
쿼리문으로 사용하기엔 다소 형식이 맞지 않다고 판단되어,<br>
이를 **`{brand, name, caffeine}`** 형식으로 가공하여 적재하고자 한다.

---

### 생성 & 삽입 쿼리 🔮

```SQL
CREATE TABLE IF NOT EXISTS brand (
    id INT AUTO_INCREMENT PRIMARY KEY,
    brand_name VARCHAR(255),
    name VARCHAR(255),
    caffeine INT,
    url VARCHAR(255)
);
```

위 쿼리문을 해석 해 보면,<br>
먼저 고유한 `id` 값을 가지며 1씩 증가하는 옵션이 추가되어있다. 👉 **`AUTO_INCREMENT`**<br>
다음으로는 문자열인 커피 브랜드, 메뉴 정보가 있고,<br>
커피 메뉴에 따른 카페인 함량에 대한 정보가 정수형태로 저장될 테이블을 생성 해 준다.

다음으로는 생성한 테이블에 데이터를 삽입하기 위해 쿼리문을 날려주어야 하는데,<br>
아래와 같이 작성 해 주면 될 것이다.

```SQL
INSERT INTO brand (brand_name, name, caffeine) VALUES
('엔제리너스', '돌체라떼', 317),
('엔제리너스', '카페 연유다', 176),
('엔제리너스', '아메리치노 라떼', 317);
```

문제는 삽입할 데이터의 양이 너무 많다는것이다 🤦‍♂️

> 이를 일일히 수기로 작성하는것은 소위 **`미련한`** 짓이다.

때문에,<br>
아래의 방법을 사용하여 쿼리문에 사용할 수 있도록 적절하게 가공하고자 한다.

---

### Python 으로 추출하기 🤓

> <https://colab.research.google.com/>

위 사이트는 **`Python`** 을 활용한 코드를 실행시킬 수 있는 **`IDE`** 환경이다.

먼저,<br>
**1 차 가공** 을 마친 객체 형태의 데이터를 변수에 담아 할당 해 준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoVwfV%2FbtsDUI7fI84%2FRxY0KLkGMQJOv2cVTMK5ik%2Fimg.png)

그리고 이를 파싱하여 튜플로 변환하고,<br>
주어진 형식으로 튜플을 출력하고자 한다.

```Python
formatted_data = []

for brand, items in coffeeData.items():
    for item in items:
        formatted_data.append((item['brand'], item['name'], item['caffeine']))

# 튜플 형식으로 출력
output = ',\n'.join([str(item) for item in formatted_data])

print(output)
```

튜플 형태의 데이터를 저장할 **`formatted_data`** 변수에 빈 리스트를 할당하고,<br>
이중 반복문을 통해 **`coffeeData`** 의 각 브랜드와 아이템에 접근한다.

> **외부 루프 (`for brand, items in coffeeData.items(): )**<br>👉 브랜드와 그에 해당하는 아이템을 가져온다.

> **내부 루프 (`for item in items: `)**<br>👉 각 브랜드의 아이템을 하나씩 가져와 처리한다.

**내부 루프** 에서는,<br>
아이템의 정보를 추출하여 **`formatted_data`** 리스트에 튜플 형식으로 저장한다.<br>
이 때,<br>
각 튜플은 **`브랜드, 아이템 이름, 카페인`** 형식으로 구성된다.

다음으로는 **리스트 컴프리헨션** 문법을 사용하여<br>
**`formatted_data`** 리스트의 각 튜플을 문자열로 반환 한 후,<br>
**`',\n'`** 을 구분자로 사용하여 하나의 문자열로 결합(**`join`**) 한다.

위 코드를 실행하면 아래와 같이 가공된 데이터를 얻을 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdHUpqd%2FbtsDNqULKGS%2FzCYwTbQn9TM76j0qWEgnu1%2Fimg.png)

---

### JavaScript 로 추출하기 ⚡

크롤링이 아무리 **`Python`** 이 쉽다 한들,<br>
이를 **`JavaScript`** 에서도 구현 가능해야 옳잖은가 ?

로직은 **`Python`** 과 매우 유사하다.<br>
단,<br>
**`for`** 문을 사용하지 않고 **자바스크립트 내장함수** 인 **`map`** 을 사용하여 반복할 것이다..

```JavaScript
const formattedData =
    Object.values(coffeeData).flatMap(items =>
        items.map(item => [item['brand'], item['name'], item['price']])
);

const output =
    formattedData.map(item =>
        `(${item.map(i => JSON.stringify(i)).join(', ')})`).join(',\n');

console.log(output);
```

주어진 커피 데이터 👉 **1 차 가공된 데이터** 를 준비하고,<br>
이를 **`Object.valuse`** 를 사용하여 객체 형태의 값을 배열로 변환 해 준다.

**`flatMap`** 함수를 사용하여 각 브랜드의 아이템들을 하나의 배열로 평탄화(?) 해 준다.

**`map`** 함수를 사용하여 각 아이템들을 튜플 형식으로 변환하고<br>
**`join`** 메서드를 사용하여 전체 배열을 문자열로 합친다.

> **평탄화** 란 ❔❗<br>아래와 같이 두개의 동일한 예제가 있을 때<br>**`map`** 함수 사용 시 **2 차원 배열** 이 생성되는 반면,<br>**`flatMap`** 함수를 사용하면 이를 **1 차원 배열** 로 **`return`** 한다.<br>즉, **중첩된 이중 구조를 가진 데이터를 단일 수준으로 펼친다** 라는 의미를 갖고있다.

```JavaScript
const arr = [1, 2, 3];

const mapArr = arr.map((num) => [num, num * 2]);
console.log(mapArr); // [[1, 2], [2, 4], [3, 6]]

const flatMapArr = arr.flatMap((num) => [num, num * 2]);
console.log(flatMapArr); // [1, 2, 2, 4, 3, 6]
```

---

### 데이터 삽입 및 DB 확인 👀

위에 있던 데이터 삽입 쿼리를 **`Workbench`** 에서 가공한 데이터를 삽입하고 확인하려 한다.

```SQL
INSERT INTO brand (brand_name, name, caffeine) VALUES
('엔제리너스', '돌체라떼', 317),
('엔제리너스', '카페 연유다', 176),
('엔제리너스', '아메리치노 라떼', 317);
```

> 가공된 데이터를 출력하여 이를 복 붙 하여 가져왔다..<br>좀 더 단순화 하는 방법이 있을텐데 현재로써는 이게 최선이었다 😭

쿼리문을 실행한 후 생성된 테이블을 조회하면 아래와 같은 레코드를 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlSPIm%2FbtsDQeUm0MW%2FaYwh1WQkzOTDoQ3cSobIx1%2Fimg.jpg)

---

## Reference 🌊

> <https://jerryjerryjerry.tistory.com/159><br><https://dang-dang12.tistory.com/18><br><https://inpa.tistory.com/entry/MYSQL-%F0%9F%93%9A-%EA%B8%B0%EB%B3%B8-SQL%EB%AC%B8-%EC%A0%95%EB%A6%AC-%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%A1%B0%ED%9A%8C-%EC%83%9D%EC%84%B1-%EC%88%98%EC%A0%95-%EC%82%AD%EC%A0%9C><br><https://121202.tistory.com/25>
