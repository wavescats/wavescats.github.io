---
layout: post
title: "[React] Interface 를 통해 Props 관리하기 💨"
subtitle: #부제목
categories: React
tags: [타입스크립트, 리액트, TIL]
---

## Interface 란 ?

`Interface` 는 TypeScript 와 같은 타입을 사용하는 문법요소 중 하나로,<br>
객체의 구조나 함수의 형태를 정의하는데 사용된다.<br>

interface 는,<br>
실행 시에는 존재하지 않고, 컴파일 시에만 타입검사에 사용된다.<br>

이를 사용함으로 인해 타입 안정성을 향상시킬 수 있고,<br>
한 번 정의한 인터페이를 다른 곳에서도 재사용 할 수있어, DRY 원칙을 지키는데 도움을 준다.

> **DRY 원칙이란 ?**<br>
> 'Do not Repeat Yourself' 의 약자로, 반복하지 말라는 의미를 갖고있다.<br>
> 소스코드에서 동일한 코드가 반복될 경우 잦은 에러를 야기하므로,<br>
> 이는 개발습관과 밀접한 관계가 있는 원칙이라 할 수 있다.

---

### App.tsx

```javascript
import styled from "@emotion/styled";
import Card from "./components/Card";
import { useState } from "react";
import Edit from "./components/Edit";

const CardContainer = styled.div`
  display: flex;
  gap: 40px;
  flex-wrap: wrap;
  align-items: center;
`;

const PlusCard = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 48px;
  border: solid 1px #707070;
  width: 80px;
  height: 80px;
  padding-bottom: 8px;
  box-sizing: border-box;
  cursor: pointer;
  margin: 80px;
`;

function App() {
  const [mode, setMode] = (useState < "edit") | ("view" > "view");

  return (
    <>
      {
        // mode 가 view 일 때만 보이게
        mode === "view" && (
          <CardContainer>
            <Card title="asd" />
            <Card title="asd" />
            <Card title="asd" />
            <Card title="asd" />
            <PlusCard onClick={() => setMode("edit")}>+</PlusCard>
          </CardContainer>
        )
      }
      {
        // mode 가 edit 일 때만 보이게
        mode === "edit" && <Edit setMode={setMode} />
      }
    </>
  );
}

export default App;
```

해당 컴포넌트에서는,<br>
`useState` 훅을 사용하여 `mode` 라는 상태를 관리하고있다.<br>
해당 `State` 는 `Edit` 또는 `View` 둘 중 하나의 값만 가질 수 있으며,<br>
'view' 라는 문자열을 매개변수의 초기값으로 받고있다.<br>

`CardContainer` 아래의 컨텐츠들은 State `mode` 가 `view`일 때만 보여주고,<br>
`edit` 일 때는 다른 UI 를 보여줄것이다.<br>

`PlusCard` 에 Click 이벤트를 걸어 해당 버튼을 클릭 할 경우,<br>
State `mode` 를 `edit` 으로 바꿔준다.<br>
즉, 매개변수가 `edit` 이므로 `Edit.tsx` 컴포넌트가 화면에 출력 되는 형태이다.

![](https://blog.kakaocdn.net/dn/bDcfHY/btst6lmRHeQ/Rxz2K4tkQJ0EkBAdQ9uYEk/img.gif)

---

### Edit.tsx

```javascript
import styled from "@emotion/styled";
import Button from "./Button";

const TitleInput = styled.input``;

const ContentInput = styled.textarea`
  height: 360px;
`;

const EditContainer = styled.div`
  display: flex;
  gap: 16px;
  flex-direction: column;
`;
const ButtonContainer = styled.div`
  display: flex;
  gap: 16px;
  cursor: pointer;
`;

// props 를 넘겨주기 위해 선언
interface EditProps {
  setMode: (mode: "edit" | "view") => void;
}

const Edit = ({ setMode }: EditProps) => {
  return (
    <EditContainer>
      <TitleInput />
      <ContentInput />

      <ButtonContainer>
        <Button onClick={() => setMode("view")}>뒤로가기</Button>
        <Button>저장</Button>
      </ButtonContainer>
    </EditContainer>
  );
};

export default Edit;
```

`EditProps` 라는 인터페이스를 통해 `setMode` 함수의 타입을 명시한다.<br>
이 컴포넌트 내부에는 `TitleInput` 과 `ContentInput` 등의 내부 컴포넌트가 존재한다.<br>
`ButtonContainer` 에는 두 개의 버튼을 row 형태로 보여지게 하기 위해 감싸주었고,<br>
첫 번째 버튼에 `onClick` 이벤트를 통해 State `setMode` 를 통해 `view` 를 호출한다.<br>

이 버튼을 클릭하게 되면,<br>
`mode` 가 `view` 로 바뀌게 되고,<br>
`App.tsx` 컴포넌트에서는 `Card` 컴포넌트들이 보여지게 된다.

![](https://blog.kakaocdn.net/dn/bgGF4l/btstX4zSZEY/ePVjaKQorRIacxjkJTruk0/img.gif)

---

### Error

정상적으로 동작하는 로직에서 에러를 강제로 발생시켜보자 !<br>

```javascript
{
  // mode 가 edit 일 때만 보이게
  mode === "edit" && <Edit />;
}
```

해당 부분을 `App.tsx` 컴포넌트에 적용할 경우,<br>
`Edit` 컴포넌트를 사용할 때 `setMode` 함수를 전달하지 않고있다며 에러가 발생한다.

![](https://blog.kakaocdn.net/dn/bmuCrZ/btstX1wl2wP/c4uORqWn3gLDirU1M7jyFk/img.gif)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbX2bBs%2FbtstX4s6s6e%2Fk4KSRYc2LIv8XjGaeZVpi1%2Fimg.png)

따라서,<br>
Typescript 혹은 JSX 가 `Edit` 컴포넌트에 필요한 Props 가 누락되었다고 에러가 발생될 것이다.<br>

이를 수정하기 위해선,<br>
`App` 컴포넌트에서 `Edit` 컴포넌트를 사용할 때<br>
`setMode` 함수를 아래와 같이 전달 해 주어야 지정한 컴포넌트에서의 상태가 공유될 것이다.

```javascript
{
  // mode 가 edit 일 때만 보이게
  mode === "edit" && <Edit setMode={setMode} />;
}
```

---

## Reference 🌊

> <https://medium.com/humanscape-tech/react%EC%97%90%EC%84%9C-%EB%98%91%EB%98%91%ED%95%98%EA%B2%8C-props-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-dbea865f53><br><https://blog.naver.com/PostView.nhn?blogId=pjt3591oo&logNo=222342618084><br><https://velog.io/@kim98111/Component-Props>
