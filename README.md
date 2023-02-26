<div align="center">

# **☑️원티드 프리온보딩 프론트엔드 챌린지 TODO 사이트☑️**

<img width="1000" src="https://user-images.githubusercontent.com/87015026/221516277-f1d797f2-4744-4807-9375-57c528392d6b.png"/>

</div>

</br>

# **1. 개발 환경💻**

### **[Front-End]**

- React, TypeScript
- React-router
- Context API, useContext, useReducer
- useState, useEffect, useNavigate, useCallback
- CSS module, classnames 라이브러리

```
 "@types/react": "^18.0.28",
 "@types/react-dom": "^18.0.10",
 "@types/react-router-dom": "^5.3.3",
 "classnames": "^2.3.2"
```

### **[Back-End]**

- 제공된 API 사용
- https://github.com/starkoora/wanted-pre-onboarding-challenge-fe-1-api

```
> yarn
> yarn start # http://localhost:8080
```

### **[버전 관리 및 트러블슈팅]**

- GitHub
- GitHub-Wiki

### **[테스트용 계정]**

- 🧑🏻‍💻 id: `test100@naver.com`
- 🔐 password: `12345678`

</br>

# **2. 폴더 트리 구조🌳**

```
📦
├─ tsconfig.json
├─ package-lock.json
├─ package.json
svg
├─ public
│  └─ index.html
└─ src
   ├─ global.d.ts
   ├─ App.tsx
index.tsx
context
   │  └─ TodoDataCotnext.tsx
   ├─ components
   │  ├─ auth
   │  │  ├─ AuthInput.tsx
   │  │  ├─ Button.tsx
   │  │  └─ FormWrap.tsx
   │  └─ todo
   │     ├─ TodoDetails.tsx
   │     ├─ TodoDetailsWrap.tsx
   │     ├─ TodoList.tsx
   │     └─ TodoListWrap.tsx
   ├─ page
   │  ├─ HomePage.tsx
   │  ├─ JoinPage.tsx
   │  └─ LoginPage.tsx
   └─ style
      ├─ authStyle
      │  ├─ AuthInput.module.css
      │  ├─ Button.module.css
      │  └─ FormWrap.module.css
      ├─ commonStyle
      │  ├─ reset.css
      │  └─ utils.css
      ├─ pageStyle
      │  ├─ HomePage.module.css
      │  ├─ JoinPage.module.css
      │  └─ LoginPage.module.css
      └─ todoStyle
         ├─ TodoDetails.module.css
         ├─ TodoDetailsWrap.module.css
         ├─ TodoList.module.css
         └─ TodoListWrap.module.css
```

©generated by [Project Tree Generator](https://woochanleee.github.io/project-tree-generator)

</br>

# **3. 구현 기능🔗**

## **회원가입 및 로그인** ✅

</br>

|                                                          로그인 성공                                                           |                                                         회원가입 성공                                                          |                                                            로그아웃                                                            |
| :----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------: |
| <img width="300" src="https://user-images.githubusercontent.com/87015026/223122331-d611a1d2-60d6-4df5-b356-7d55053a008b.gif"/> | <img width="300" src="https://user-images.githubusercontent.com/87015026/223122989-e63629f3-9d05-47ad-a781-800d795313de.gif"/> | <img width="300" src="https://user-images.githubusercontent.com/87015026/223123479-57a2024f-975d-4cb3-81a3-e970829082b8.gif"/> |
|                                               token 있을 시 HomePage로 navigate                                                |                                                  이메일, 비밀번호 유효성 확인                                                  |                                                  token 삭제로 간단히 로그아웃                                                  |

</br>

## **TODO 리스트 ✅**

- TODO list API 호출하여 투두리스트 CRUD 기능 구현

- 한 화면 내에서 TODO list와 TODO 상세 내용 확인

- 한 페이지 내에서 새로고침 없이 데이터가 정합성을 갖추도록 구현

</br>

|                                                           TODO 체크                                                            |                                                         TODO 창 조작법                                                         |                                                    이전,다음 todo 상세보기                                                     |
| :----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------: |
| <img width="300" src="https://user-images.githubusercontent.com/87015026/223118670-c899bb26-a175-4aa2-afee-32c5c19ed0fd.gif"/> | <img width="300" src="https://user-images.githubusercontent.com/87015026/223121625-45f691c2-3193-4fdf-bf62-ace818128196.gif"/> | <img width="300" src="https://user-images.githubusercontent.com/87015026/223119152-1472c16a-5d19-495b-8fdc-2ad885cea4f6.gif"/> |
|                                                          끝낸 일 체크                                                          |                                           리스트 클릭으로 열고 'X' 아이콘으로 닫는다                                           |                                           맨 앞과 맨 뒤의 상세에서는 표기되지 않는다                                           |

|                                                           TODO 추가                                                            |                                                           TODO 수정                                                            |                                                           TODO 삭제                                                            |
| :----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------: |
| <img width="300" src="https://user-images.githubusercontent.com/87015026/223116607-0a7105ab-ec38-4fad-a603-babdfe24e62c.gif"/> | <img width="300" src="https://user-images.githubusercontent.com/87015026/223117373-070af603-4d7f-4022-91d3-ecd67ba933ad.gif"/> | <img width="300" src="https://user-images.githubusercontent.com/87015026/223118155-87e0dec4-978a-48e1-a7d5-40ab7800a5b9.gif"/> |
|                                                        새로 할 일 추가                                                         |                                                        기존 할 일 수정                                                         |                                                        기존 할 일 삭제                                                         |

</br>

# **4. 핵심코드📑**

## **TodoDataContext.tsx**

</br>

### **1. 리듀서 함수 정의**

```
const reducer = (state: State, action: ActionType) => {
	switch (action.type) {
		case "SET_TODODATAS":
			return {
				...state,
				todoDatas: action.payload,
			};
		case "SET_PATH":
			return {
				...state,
				path: action.payload,
			};
		default:
			return state;
	}
};
```

- 여러 state들이 한 컴포넌트`(TodoDetailsWrap.tsx)`에 밀집해 있어서 업데이트 로직을 리듀서 함수에 모았다.
- 전체 TODO 리스트 반환하는 `"SET_TODODATAS"` action
- path (= 개별 todo의 고유 id와 동일) 반환하는 `"SET_PATH"` action

</br>

### **2. TodoDataContextProvider 정의**

```
const TodoDataContextProvider: React.FC<{ children?: React.ReactNode }> = ({
	children,
}) => {
	const [state, dispatch] = useReducer(reducer, initialState);

	const handlePath = (clickedId: string | undefined) => {
		dispatch({ type: "SET_PATH", payload: clickedId });
	};

	const handleGetTodoList = async (): Promise<void> => {
		const url: string = "http://localhost:8080/todos";
		try {
			const response = await fetch(url, {
				method: "GET",
				headers: {
					Authorization: localStorage.getItem("userInfo") || "",
				},
			});
			const result = await response.json();

			if ("data" in result) {
				const todoList: TodoData[] = result.data;
				dispatch({ type: "SET_TODODATAS", payload: todoList });
				return;
			}
		} catch (error) {
			console.log("error", error);
		}
	};

	return (
		<TodoDataContext.Provider
			value={{
				getTodoList: handleGetTodoList,
				todoDatas: state.todoDatas,
				getPath: handlePath,
				path: state.path,
			}}
		>
			{children}
		</TodoDataContext.Provider>
	);
};

export default TodoDataContextProvider;
```

- `useReducer` 사용하여 `handlePath` 함수와 `handleGetTOdoList` 함수에서 액션 디스패치
- `TodoDataContext.Provider`에서 state 업데이트 감지하도록 작성
