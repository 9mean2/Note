# Redux 생성 순서 코드 스니펫

1. Redux 설치하기

```bash
yarn add redux react-redux
```

2. Src 폴더에 redux 폴더 구성하기

```
📦src  
 ┣ 📂redux  
 ┃ ┣ 📂config  
 ┃ ┃ ┗ 📜configStore.js  
 ┃ ┣ 📂modules
 ┃   ┗ 📜 todoModule.jsx  
 ┃ ┗ 📜.DS_Store 
 ┣ 📂pages  
 ┃ ┗ 📜Home.jsx  
 ┣ 📂shared  
 ┃ ┗ 📜Router.js  
 ┣ 📜.DS_Store  
 ┣ 📜App.css  
 ┣ 📜App.js  
 ┗ 📜index.js
```

3. configStroe.js 연결하기 

`src/redux/config/configStore.js`

```jsx
// 중앙 데이터 관리소(store)를 설정하는 부분
import { createStore } from "redux";
import { combineReducers } from "redux";

const rootReducer = combineReducers({
 //이곳에 Modules 폴더에 넣어놓은 state의 묶음들을 넣을 예정
 //즉, 리듀서
}); 
const store = createStore(rootReducer); 

export default store; 
```

4. index.js에 스토어 뿌려주기 

`./index.js`

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
// Provider import
import { Provider } from 'react-redux'; 
//주의: 반드시 config에서 가져와야 한다. 정확한 경로 필수
//tip: export default로 작성했을때는 import시 { store }로 작성하면 안된다.
import store from './redux/config/configStore';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  //Provider:
  //스토어에서 만들어놓은 중앙데이터 관리소를 App 컴포넌트 하부에서 스토어를 가능하게 해줌
  <Provider store={store}>
    <App />
  </Provider>
);
```

5. 리듀서 모듈 생성하기

`src/redux/modules/리덕스모듈이름.jsx`

```jsx
// 1. Actions
const CREATE = "todo/CREATE";

// 2. Action Creators
//create
export function addTodo(title, desc) {
  return {
    type: CREATE,
    title,
    desc,
  };
}

// 3. 초기 상태값
const initialState = {

};

// 4. Reducer
export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    case CREATE:
      return 
    default:
      return state;
  }
}
```

6. react-router-dom 설치하기

```bash
yarn add react-router-dom 
```

7. Router 파일 생성

`src/shared/Rounter.js`

```jsx
import React from "react";
import { BrowserRouter, Route, Routes } from "react-router-dom";
import 페이지이름 from "페이지 경로";

const Router = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<페이지이름 />} />
      </Routes>
    </BrowserRouter>
  );
};

export default Router;
```

8. App.js에 Router.js import 해주기

`./App.js`

```jsx
import React from "react";
import Router from "./shared/Router";

function App() {
  return <Router />;
}

export default App;
```

9. page내의 .jsx 뼈대 구성

`src/pages/페이지이름.js`

```jsx
import React from 'react'

const Home = () => {
  return (
			<>
    	</>
  )
}

export default Home
```

1. 스타일드 컴포넌트
   
   ``` bash
   yarn add styled-components
```









돔 라우터 연결하기

TodoCard.jsx 에서 Navigate import 하기
``` JSX
import { useNavigate } from "react-router-dom";
```

 navigate를 통해 상세 페이지 접근
``` JSX
const navigate = useNavigate();
```

상세페이지 버튼 생성 
``` JSX
<button onClick={() => { navigate("/페이지"); }}
```

```JSX
<button onClick={() => navigate(`/${item.id}`)}>

상세페이지

</button>
```

Detail 페이지 만들고 라우터에 페이지 연결
``` JSX
<Route path="/:id" element={<Detail />} />
```

디테일 페이지에서 스토어 접근하기 위해 useSelector 사용
``` JSX
const data = useSelector((state) => {

return state.reducer;

});
```

어떤 todolist인지 찾아 보기위해 조건에 맞는(data.id === params.id) 것들만 가져옴
``` JSX
const params = useParams();

const foundData = data.find((item) => {

console.log("item.id -->", String(item.id), "params.id--->", params.id);

return String(item.id) === params.id;

});
```

return한 JSX에 스토어에 있는 값을 Dom에 뿌려줌
``` JSX
return (

<>

<div>

<p>{`id: ${foundData.id}`}</p>

<h1>{foundData.title}</h1>

<h3>{foundData.desc}</h3>

</div>

</>

);
```

Home으로 가기 버튼 생성을 위해 useNavigate 사용
``` JSX
const navigate = useNavigate();
```

``` JSX
<button onClick={() => navigate("/")}>집으로 가자</button>
```

