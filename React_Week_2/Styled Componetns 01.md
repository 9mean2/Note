
# #CSS-In-JS

#### 우리는 css 파일을 생성하고 그 안에서 CSS를 사용해서 컴포넌트를 꾸몄었다

#### 컴포넌트를 만들고 컴포넌트를 꾸미기 위해 css 파일을 만들어서 import 하고 HTML  tag 마다 ``className``를 넣고 CSS 코드를 작성하는 것을 반복해야 했었다.

## CSS-in-JS 방식이란

###  단어 그대로 자바스크립트 코드로 CSS 코드를 작성하여 컴포넌트를 꾸미는 방식입니다.

#### 순수한 CSS 코드를 우리가 아니라, ``자바스크립트``를 이용해서 CSS 코드를 만들어 내는 것이죠. ``CSS-in-JS`` 방식을 사용하기 위해 우리는 새로운 패키지를 사용할 것이다

## #styled-components 란 무엇인가?

### ``styled-components``는 우리가 리액트에서 ``CSS-in-JS`` 방식으로 컴포넌트를 꾸밀수 있게 도와주는 패키지 이다

-   **(1) 기본적인 사용법 알아보기**
    SC의 기본적인 원리는 **꾸미고자 하는 컴포넌트를 SC의 방식대로 먼저 만들고, 그 안에 스타일 코드를 작성하는 방식
    으로 진행 이된다.**
    
    ``` JSX
const StBox = styled.div
// 이 안에 스타일 코드를 작성합니다. 스타일 코드는 우리가 알고 있는 css와 동일합니다.`

width: 100px;

height: 100px;

border: 1px solid red;

margin: 20px;
```
    
    그리고 `styled.` **뒤에는 html의 태그**가 옵니다. 아래 처럼 내가 원하는 html 태그를 사용해서 styled-components를 만들 수 있습니다.
    
    div ➡️ `styled.div`

    span ➡️ `styled.span`

    button ➡️ `styled.button`

-   **(2) 조건부 스타일링이란?**
    
    classname을 사용해서 구현하기는 조금 까다로운 조건부 스타일링을 styled-components를 이용하면 간편하게 할 수 있습니다. 만약에 스타일 코드를 작성할 때 `if문을 사용할 수 있다면?` , `switch문을 사용할 수 있다면?` , `삼항연산자를 사용할 수 있다면?` 이라는 생각을 혹시 해보셨나요? **CSS-in-JS 방식의 강점이 바로 스타일 코드를 JS코드 작성하듯이 스타일 코드를 작성할 수 있다는 점 입니다.**

위 코드를 한번 분석해볼까요?

1.  먼저 **styled-component를 생성**합니다.
   
2. 그리고 생성한 **styled-component**를 부모 컴포넌트에서 사용합니다. 여기서 부모컴포넌트는 App.js 이겠군요.
   
3. 그리고 이제 우리가 원하는 값, 즉 borderColor를 **props**로 자식컴포넌트, 여기서는 자식컴포넌트가 **styled-components** 겠죠? **StBox** 에 전달합니다.
   
4. 부모 컴포넌트에서 **props**를 보냈습니다. 자식 컴포넌트에서는 받아야겠죠? 아래와 같은 모양으로 받습니다. 순서대로 어떻게 된건지 알아볼까요?
``` JS
const StBox = styled.div` border: 1px solid ${(props) => props.borderColor}; `;
```

1.  첫째, 먼저 **자바스크립트 코드를 사용하기 위해 `${ }` 를 열어줍니다.**
    
2.  둘째, 비어있는 화살표 함수를 열어 줍니다. `${( )=>{ }}` 이렇게요.
    
3.  셋째, 함수의 인자에서 props를 받아오고, props안에는 부모 컴포넌트에서 보낸 borderColor가 있습니다. 그것을 return 합니다.
    `${(props)⇒{ return props.borderColor }}` 이렇게 리턴하면 `(props)⇒{ return props.borderColor }` 의 값이 `=== 'red'` 가 되고 결국 우리 눈에는 복잡해보이지만, 브라우저는 `border: 1px solid red` 라는 코드로 인식하여 스타일링이 되는 것 입니다.

``` JSX
//1. styled-components를 만들었습니다.
const StBox = styled.div`

width: 100px;

height: 100px;

border: 1px solid ${(props) => props.borderColor};

margin: 20px;

`;

function App() {
return (

<StContainer>

<StBox borderColor="red">빨간박스</StBox>
<StBox borderColor="blue">파란박스</StBox>
<StBox borderColor="green">초록박스</StBox>

</StContainer>
);
}
```

-   **(4) Swtich문과 map을 사용해서 리팩토링 해보기**
    
    위에서 구현한 코드를 자바스크립트의 **map**과 **switch**문을 이용해서 리팩토링 해봤다.
    
    ```JSx
    import React from "react";

import "./App.css";

import styled from "styled-components";

  

const StContainer = styled.div`

display: flex;

`;

  

//1. styled-components를 만들었습니다.

const StBox = styled.div`

width: 100px;

height: 100px;

//4. 부모 컴포넌트에서 보낸 props를 받아 사용합니다.

border: 1px solid ${(props) => props.borderColor};

margin: 20px;

`;

  

// 박스의 색

const boxList = ["red", "blue", "green", "black"];

  

// 색을 넣으면 이름을 반환

const getBoxName = (color) => {

switch (color) {

case "red":

return "빨간박스";

case "green":

return "초록박스";

case "blue":

return "파란박스";

default:

return "검정박스";

}

};

  

function App() {

return (

<StContainer>

{/* <StBox borderColor="red">빨간박스</StBox> */}

{boxList.map((box) => {

return <StBox borderColor={box}>{getBoxName(box)}</StBox>;

})}

</StContainer>

);

}

  

export default App;
```

## 정리

-   **CSS-in-JS**란, 자바스크립트로 CSS코드를 작성하는 방식을 말한다.
-   **props**를 통해서 부모 컴포넌트로부터 값을 전달받고, 조건문을 이용해서 조건부 스타일링을 할 수 있다.