---
layout: post
title: "[Next.js] Prisma 를 사용하여 HTTP 요청 시 마이그레이션 에러 💫"
subtitle: #부제목
categories: [Next.js]
tags: [넥스트, TIL, Error]
---

## 개요 💥

**`Prisma`** 를 사용하여 `CRUD` 를 구현하는 중 `Delete` 과정에서 마주친 에러이다.<br>

---

### API Handler ✋

- delete.ts

```javascript
import type { NextApiRequest, NextApiResponse } from 'next'
import { prisma } from '../../../utils/prisma'

export default async function handle(req: NextApiRequest, res: NextApiResponse) {
  const { id } = req.query

  if(req.method === 'DELETE') {
    try {
      await prisma.notice.delete({
        where: { id: Number(id) },
      })
      console.log('Delete successful'); // 삭제 성공 로그
      res.status(200).json({ success: true, message: 'Notice deleted successfully' });
    } catch (error: any) {
        console.error('Error deleting notice:', error.message); // 에러 메시지 확인
      res.status(500).json({ error: "Unable to delete notice" })
    }
  } else {
    console.log('Invalid method:', req.method); // 유효하지 않은 메서드 로그
    res.status(405).end() // Method Not Allowed
  }
}
```

해당 코드는 `/pages/api` 경로에 생성된 HTTP 요청을 처리하기 위한 핸들러이다.<br>

웹 브라우저나 다른 클라이언트에서 `HTTP DELETE` 요청이 들어오면,<br>
`notice` 레코드를 제거하고,<br>
`Prisma Client` 를 사용하여 데이터베이스에 접근이 가능한 로직이다.<br>

첫 줄에서 `prisma` 객체를 선언하여 이미 초기화된 `Prisma Client` 인스턴스를 불러와 사용한다.<br>

`handle` 함수는 Next.js 의 `API 라우트 핸들러` 이며,<br>
비동기적으로 HTTP 요청과 응답 객체를 인자로 받아 `req.query` 를 통해 URL 의 쿼리 파라미터를 추출한다.<bR>

요청 메서드가 `DELETE` 일 경우 아래 로직을 실행하며,<br>
제거하는 요청이 성공 할 경우 200 번대의 상태코드를 반환하고,<bR>
실패할경우 500 번대의 상태코드를 반환한다.<br>

이 외에 `DELETE` 요청이 아닐경우 유효한 메서드로 간주하지 않고,<bR>
405 상태코드를 반환한다.

---

### Hooks 👊

- useDelete.ts

```javascript
import { useCallback } from 'react';
import { useRouter } from 'next/router';
import axios from 'axios';

function useDelete() {
  const router = useRouter();

  const deleteNotice = useCallback(async (id: number) => {
    try {
        console.log('Sending delete request for id:', id); // id 값 확인
      const res = await axios.delete(`/api/notice`, { params: { id } })

      console.log('delete successfully: ', res.data);

      router.push('/list'); // 또는 다른 경로로 리다이렉트
    } catch (error: any) {
      console.error(error.message);
    }
  }, [router]);

  return { deleteNotice };
}

export default useDelete;
```

해당 로직은,<br>
코드의 중복을 줄이고 컴포넌트의 재사용을 통해 유지보수에 용이할 수 있도록 사용한<br>
`커스텀 훅(Custom Hooks)` 이다.<br>

Next.js 에서 제공하는 `router` 를 가져와 페이지 내부에서 라우팅 처리를 위해 선언하고,<br>
`Delete` 요청이 성공할 경우 `router.push` 함수를 통해 지정된 경로로 리다이렉트된다.<br>

위에서 정의한 핸들러의 엔드포인트로 `(`/api/notice`,{ params: { id } }))`<br>
특정 id 를 찾아 제거하는 `axios` 요청을 보내 비동기적으로 수행한다.<br>

만약,<br>
이 요청이 실패할 경우 에러 메세지를 출력하고,<br>
의존성 배열에 router 를 넣어줌으로 인해<br>
`router` 객체가 변경될 때만 `deleteNotice` 함수가 재생성된다.<br>

`useDelete` Hooks 은,<br>
`deleteNotice` 함수를 return 하므로 이 Hooks 를 사용하는 컴포넌트에서 사용가능하다.

---

### Components 🔮

- /pages/read/[id].tsx

해당 경로에 생성한 컴포넌트는,<br>
`http://localhost:3000/read/{id}` 의 값을 가지는 URL 을 생성한다.<Br>

`useDelete` 훅 에서 return 값으로 보낸 `deleteNotice` 를 불러와 사용한다.

```javascript
const { deleteNotice } = useDelete();
```

목록 리스트에서 특정 게시물을 선택하면 `{id}` 값을 가져와<br>
`Detail` 컴포넌트로 라우팅 처리되어 리다이렉트로 페이지가 이동된다.<br>

`Detail` 페이지에는 3 개의 버튼을 구성했는데,<br>
그 중 구현한 삭제 버튼에 `onClick` 이벤트를 추가하여 `Delete` 훅을 실행한다.

```javascript
// delete event
const handleDelete = () => {
  if (window.confirm("정말 삭제하시겠습니까?")) {
    console.log(`Deleting notice with id: ${id}`);
    deleteNotice(id);
  }
};
```

```javascript
<div
  className="w-13 pl-3 pr-3 pt-2 pb-2 bg-red-600 rounded-md flex justify-center items-center space-x-2 cursor-pointer"
  onClick={handleDelete}
>
  <div className="text-center text-white text-lg font-medium leading-4 break-words font-pretendard">
    삭제
  </div>
</div>
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmQDiL%2FbtsvXV1og0H%2FIS5YkjdGnNPjUjWh98AzQK%2Fimg.png)

---

### Error ❌

- 404 Error

위에서 구현한 컴포넌트에서 구현한 `삭제` 버튼을 클릭 시 404 에러가 발생했다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FndZ8a%2FbtsvXWMLrWn%2FD84Ml9mqWcyh3NshM4y9o0%2Fimg.png)

해당 프로젝트를 진행하며 주로 발생했던 404 에러는,<br>
HTTP 요청을 보내는 엔드포인트를 잘못 지정했을 때 발생했다.<br>

`useDelete` 훅을 보면,<br>

```
const res = await axios.delete(`/api/notice`, { params: { id } })
```

위 경로로 `Delete` 요청을 보내는데,<br>
이를 살펴보면<br>
`pages/api/` 에 있는 디렉토리를 불러올 뿐 API 핸들러를 요청하는 엔드포인트가 아니었다.<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNbkNU%2FbtsvMSytrvU%2FFFCDcI1eiwSS4CVhCzSyi1%2Fimg.png)

즉, 엔드포인트가 다르게 지정되어 404 에러가 출력되고 있는것이다.

```javascript
const res = await axios.delete(`/api/notice/delete`, { params: { id } });
```

요청하는 엔드포인트에 `/delete` 를 추가하여 정상적으로 API 핸들러에 요청을 보낼 수 있었다.<br><Br>

---

- Migration Error

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fen2wRK%2FbtsvXh48WiG%2Fn4FjsnoZPMqVtwpKRGiZp0%2Fimg.png)

위에서 구현한 컴포넌트에서 구현한 `삭제` 버튼을 클릭 시 다음과 같은 에러가 발생했다.<br>

메세지를 살펴보면,<br>
`prisma.notice.delete()` 를 요청했는데,<br>
next_mariaDB 의 Notice 테이블에 createAt 컬럼이 없어서 해당 명령을 수행할 수 없다는것같다.

`schema.prisma` 에 정의되어있는 Notice 모델을 확인 해 보니,<bR>
실제 `createAt` 컬럼이 존재하지 않아 아래와 같이 추가 해 주었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbakiMu%2Fbtsv8hvKdqR%2FinPgDgY30PkKhc0XghNfIk%2Fimg.png)

`schema.prisma` 파일을 수정 한 후에는 수정사항을 적용하기 위해 아래 명령을 실행해줘야한다.

```
npx prisma migrate dev
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8GXzn%2Fbtsv7xloFvP%2FBTbpVXk2ieftXfdK1XwjhK%2Fimg.png)

마이그레이션을 통해 해당 스키마를 적용하고,<br>
다시 컴포넌트에 구현된 `삭제` 버튼을 눌렀지만, 아직도 같은 에러가 발생한다.<br>

schema 를 업데이트 하고난 후에는,<br>
이를 기반으로 `prisma.client` 를 생성 해 주어야 한다고 한다.

> <https://www.prisma.io/docs/concepts/components/prisma-client>

```
npx prisma generate
```

> $ npx prisma generate
> Environment variables loaded from .env
> Prisma schema loaded from prisma\schema.prisma
> Error:
> EPERM: operation not permitted, unlink 'D:\next_pagesup\node_modules\.prisma\client\query_engine-windows.dll.node'

`generate` 명령을 실행하니 위 에러가 발생했다.<br>
에러를 검색 해 보니,<br>
파일시스템의 권한과 관련된 부분에서 해당 경로에 있는 `.node` 파일을 제거할 수 없다고 한다.<br>

터미널을 관리자 권한으로 실행하여 명령어를 다시 입력해 보았지만 계속해서 에러가 발생한다.<br>

나는 이 에러를 해결하기 위해<br>
`/node_modules` 와 `yanr.lock` 을 GUI 로 지우고<br>
다시 `yarn install` 을 통해 패키지 설치 후 `prisma client`를 생성 해 주었다.<br>

`geneate` 에러가 계속해서 발생한 이유로는,<br>
에러가 발생했던 `createAt` 필드가 마이그레이션을 해도<br>
이전에 존재했던 마이그레이션 또는 다른 곳에서 이 필드를 참조하고 있기 때문에 발생할 수 있다고 한다.<br>

위와 같은 방법으로 `/node_modules` 을 지우고,<br>
다시 `yarn install` 후 아래 명령어를 실행하니 권한 에러가 해결되고,<br>
`prisma Client` 가 생성됨을 확인할 수 있었다.

```
npx prisma generate
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmKmVu%2Fbtsv9INAxUW%2F49Lo0x9LHg2LNCMkc3Kik1%2Fimg.png)

---

## Reference 🌊

> <https://www.prisma.io/docs/concepts/components/prisma-client><bR><https://blog.outsider.ne.kr/1617><br><https://defineall.tistory.com/872><br><https://github.com/prisma/prisma/issues/9184><Br><https://lightrun.com/answers/prisma-prisma-generator-output-is-relative-to-prisma><br><https://codingapple.com/forums/topic/api-handler-should-not-return-a-value-received-object-%EC%A7%88%EB%AC%B8/>
