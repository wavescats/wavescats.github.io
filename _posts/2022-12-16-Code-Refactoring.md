---
layout: post
title: "[React] Code Refactoring 을 통한 리소스 줄이기"
subtitle: #부제목
categories: React
tags: [리액트, TIL]
---

### 프로젝트 MBTI

MBTI 를 구현할때 선택한 버튼에 해당하여 누적된 Score 를 계산해주는 로직이다.
<br>
다음과 같이 버튼 A 와 B 를 눌렀을 때 점수를 계산해주는 내용이 정의된 함수가 있다.

```JS
const handleClickButtonA = (no, type) => {
    if (type === "EI") {
      // 기존 스코어에 더할 값을 계산 (기존의 값 + 배점)
      const addScore = totalScore[0].score + no
      // 새로운 객체
      const newObject = { id : 'EI', score : addScore}
      // splice 를 통해 새로운 객체를 해당 객체 자리에 넣어줌
      totalScore.splice(0, 1, newObject)
    } else if (type === "SN") {
      const addScore = totalScore[1].score + no
      const newObject = { id : 'SN', score : addScore}
      totalScore.splice(1, 1, newObject)
    } else if (type === "TF") {
      const addScore = totalScore[2].score + no
      const newObject = { id : 'TF', score : addScore}
      totalScore.splice(2, 1, newObject)
    } else if (type === "JP") {
      const addScore = totalScore[3].score + no
      const newObject = { id : 'JP', score : addScore}
      totalScore.splice(3, 1, newObject)
    }
	
		// 다음 문제 출력
    setQuestionNo(questionNo + 1)
  }
  ```
  ```JS
  const handleClickButtonB = (no, type) => {
    if (type === "EI") {
      // 기존 스코어에 더할 값을 계산 (기존의 값 + 배점)
      const addScore = totalScore[0].score + no
      // 새로운 객체
      const newObject = { id : 'EI', score : addScore}
      // splice 를 통해 새로운 객체를 해당 객체 자리에 넣어줌
      totalScore.splice(0, 1, newObject)
    } else if (type === "SN") {
      const addScore = totalScore[1].score + no
      const newObject = { id : 'SN', score : addScore}
      totalScore.splice(1, 1, newObject)
    } else if (type === "TF") {
      const addScore = totalScore[2].score + no
      const newObject = { id : 'TF', score : addScore}
      totalScore.splice(2, 1, newObject)
    } else if (type === "JP") {
      const addScore = totalScore[3].score + no
      const newObject = { id : 'JP', score : addScore}
      totalScore.splice(3, 1, newObject)
    }

		// 다음 문제 출력
    setQuestionNo(questionNo + 1)
  }
  ```

가만 보니 정의된 두 함수 내부의 코드가 똑같다.<br>
이는 코드가 너무 길고, 중복된 부분이 많아 가독성이 떨어지게된다.

#### 초기 값
**console.log**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIsY8A%2FbtrX9E7fSvs%2FsagXNxvWKqZ6t6BHDUPKG1%2Fimg.png)

**'EI' 에 해당하는 질문에 '예' 를 눌렀을 때**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbH1amN%2FbtrYkE5cVjn%2FnyUjUUz9kGNB86uZjJtPv0%2Fimg.png)

두 함수를 A 와 B 로 구분짓지 않고 합쳐줌. (함수 내부의 코드가 같으므로)<br>
→ 예(1), 아니오(0) 으로 카운트

```JS
const handleClickButton = (no, type) => {
    // 새로운 변수 선언 == newScore
    const newScore = totalScore.map((s) => // 기존의 totalScore 를 인자로 받아 map 함수 실행 
    // 요소 s 의 id 가 type 과 같다면 { } 안의 내용 실행, 그게 아니라면 : s 실행
    s.id === type ? { id : s.id, score : s.score + no } : s)

    // 기존의 배열을 newScore 로 변경
    setTotalScore(newScore)
    
    // 다음 문제로 넘어가기
    // DB 에 저장된 문제는 12개 이므로 13 번째를 호출 시 에러 발생
    // QuestionData 의 전체 개수에서 questionNo 의 인덱스 번호가 11 번째인것까지는 +1 을 해주고
    if (QuestionData.length !== questionNo + 1) { 
      setQuestionNo(questionNo + 1)
    } else {
      // 12번째 문제부터는 페이지 이동 => 결과페이지로 이동
      navigate('/result')
    }
```


### 프로젝트 SNS

Message List 를 불러올 때,<br>
데이터가 없는 상태에서 더미 데이터를 만들어 확인하기 위한 로직이다.

다음과 같이 두 개의 userID 를 받아 랜덤한 메세지를 출력하는 로직을 작성하려한다.

```JS
const UserIds = ['roy', 'jay']
const getRandomUserId = () => UserIds[Math.round(Math.random())]

const msgs = [
    {
        id: 1,
        userId: getRandomId(),
        timestamp: 12345678901,
        text: '1 mock text'
    },
    {
        id: 2,
        userId: getRandomId(),
        timestamp: 12345678902,
        text: '2 mock text'
    },
    {
        id: 3,
        userId: getRandomId(),
        timestamp: 12345678903,
        text: '3 mock text'
    },
]

const MsgList = () => <ul className = "messages">{
    msgs.map(x => <MsgItem { ...x} />)
}</ul>
```
```JS
const msgs = Array(50).fill(0).map(( ,i) => ({
    id: i + 1,
    userId: getRandomUserId(),
    timestamp: 12345678901 + i * 1000 * 60 // ms 단위를 s 단위로 변경 후 m 단위로
    text: `${i + 1} mock text`
}))

const MsgList = () => <ul className = "messages">{
    msgs.map(x => <MsgItem key={x.id} { ...x} />)
}</ul>

```
> mapping 을 위해 fill 에 빈 값을 추가하였고,<br>
fill 이 없는 경우 배열에 대해서 map 함수가 실행하지 않음

위 코드와 같이 더미 데이터를 복.붙 하여 사용할수도 있지만,<br>
한번에 일괄적으로 처리하는게 효율이나 가독성에도 좋을것같다.
<br>
<br>
이와같이 매우 긴 코드를 간략하게 줄일 수 있는 방법을 통해<br>
발생하는 리소스도 줄이고 가독성도 올라가게 되니 위와 같은 방법을 사용하지 않을 수 없다.