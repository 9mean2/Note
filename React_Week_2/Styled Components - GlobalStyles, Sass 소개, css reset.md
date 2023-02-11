
## 1. GlobalStyles(전역 스타일링)

-   **(1) 전역 스타일링이란?**
    
    styled components는 컴포넌트 내에서만 활용할 수 있었다. 
    하지만 프로젝트에 공통적으로 들어가야 할 스타일을 적용해야 할 필요도 있다. 그럴 경우 **‘전역적으로(globally)’ 스타일을 지정한다.** 
    그럴 때 적용하는 방법이 바로 **전역 스타일링** 이다
    
-   **(2) 컴포넌트 단위 스타일링**
    
     `<h1>`, `<p>`, `<div>` 태그는 각각 `<Title />`, `<Contents />`, `<Wrapper />`에서 새롭게 스타일링 됐다
    
    ```jsx
    import styled from "styled-components";
    
    function TestPage(props) {
      return (
        <Wrapper>
          <Title>{props.title}</Title>
          <Contents>{props.contents}</Contents>
        </Wrapper>
      );
    }
    
    const Title = styled.h1`
      font-family: "Helvetica", "Arial", sans-serif;
      line-height: 1.5;
      font-size: 1.5rem;
      margin: 0;
      margin-bottom: 8px;
    `;
    
    const Contents = styled.p`
      margin: 0;
      font-family: "Helvetica", "Arial", sans-serif;
      line-height: 1.5;
      font-size: 1rem;
    `;
    
    const Wrapper = styled.div`
      border: 1px solid black;
      border-radius: 8px;
      padding: 20px;
      margin: 16px auto;
      max-width: 400px;
    `;
    
    export default TestPage;
    ```
    
    규모가 좀 큰 프로젝트라고 한다면 공통적으로 적용되는 스타일링 부분은 빼줄   필요가 있습니다. 
    우리의 경우는 글꼴(font)와 `line-height`를 공통 요소라 가정하고 **GlobalStyles을** 적용해볼게요.
    
-   **(3) GlobalStyles 적용**
  
	GlobalStyle.jsx
	
	```jsx
	import { createGlobalStyle } from "styled-components";
	
	const GlobalStyle = createGlobalStyle`
	  body {
	    font-family: "Helvetica", "Arial", sans-serif;
	    line-height: 1.5;
	  }
	`;
	
	export default GlobalStyle;
	```
	
	App.jsx
	
	```jsx
	import GlobalStyle from "./GlobalStyle";
	import BlogPost from "./BlogPost";
	
	function App() {
		const title = '전역 스타일링 제목입니다.';
		const contents = '전역 스타일링 내용입니다.';
	  return (
	    <>
	      <GlobalStyle />
	      <BlogPost title={title} contents={contents} />
	    </>
	  );
	}
	
	export default App;
	```
	
	앞으로 공통적으로 적용해야 할 스타일이 생긴다면 GlobalStyles를 적용 해보자


## 2. Sass 소개, Nesting

-   **(1) Sass(Syntactically Awesome Style Sheets)란?**
    
    `CSS`를 전통적인 방법보다 효율적으로 사용하기 위해 만들어진 언어이다. `CSS`는 웹 프로젝트 규모가 커지면 커질수록 코드가 복잡해지고 유지보수도 불편해지며 계속해서 동일한 코드를 복사하고 붙여넣는 과정을 반복해야 하기 때문이다 `Human Error`를 줄이려는 노력은 중요하다
    
    그래서 코드의 재사용성을 높이고, 가독성 또한 향상시켜줄 수 있는 방법이 바로 `Sass` 이다
    
-   **(2) Sass 특징 및 예시 소개**
  
    -   변수를 사용할 수 있다
        
        ```scss
        $color: #4287f5;
        $borderRadius: 10rem;
        
        div {
        	background: $color;
        	border-radius: $borderRadius;
        }
        ```
        
    -   중첩할 수 있다(Nesting)
        
        ```scss
        label {
              padding: 3% 0px;
              width: 100%;
              cursor: pointer;
              color: $colorPoint;
        
              &:hover {
                color: white;
                background-color: $color;
              }
        }
        ```
        
    -   다른 style 파일을 import 할 수 있다
        
        -   common.scss
            
            ```scss
            // colors
            $color1: #ed5b46;
            $color2: #f26671;
            $color3: #f28585;
            $color4: #feac97;
            ```
            
        -   style.scss
          
          ``` SCSS
          //style.scss 
          @import "common.scss"; .box { background-color: $color3; }
```

## 3. css reset

-   **(1) css reset이란?**
    
    브라우저는 기본적으로 `default style`을 제공한다. 
    예를 들면 **margin**이나 **글자의 크기** 같은 경우이다.
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        Default Style을 테스트 해 봅니다.
      </body>
    </html>
    ```
    

    다양한 웹브라우저들은 저마다 조금씩은 다른 `default style`을 제공하고 있기 때문에 이를 초기화하고 우리가 정하는대로만 표현되는 것이 중요하다
    
-   (2) CSS 초기화하기
    
    reset.css
    
    ```css
    html, body, div, span, applet, object, iframe,
    h1, h2, h3, h4, h5, h6, p, blockquote, pre,
    a, abbr, acronym, address, big, cite, code,
    del, dfn, em, img, ins, kbd, q, s, samp,
    small, strike, strong, sub, sup, tt, var,
    b, u, i, center,
    dl, dt, dd, ol, ul, li,
    fieldset, form, label, legend,
    table, caption, tbody, tfoot, thead, tr, th, td,
    article, aside, canvas, details, embed, 
    figure, figcaption, footer, header, hgroup, 
    menu, nav, output, ruby, section, summary,
    time, mark, audio, video {
    	margin: 0;
    	padding: 0;
    	border: 0;
    	font-size: 100%;
    	font: inherit;
    	vertical-align: baseline;
    }
    /* HTML5 display-role reset for older browsers */
    article, aside, details, figcaption, figure, 
    footer, header, hgroup, menu, nav, section {
    	display: block;
    }
    body {
    	line-height: 1;
    }
    ol, ul {
    	list-style: none;
    }
    blockquote, q {
    	quotes: none;
    }
    blockquote:before, blockquote:after,
    q:before, q:after {
    	content: '';
    	content: none;
    }
    table {
    	border-collapse: collapse;
    	border-spacing: 0;
    }
    ```
    
    index.html
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <link rel="stylesheet" href="./reset.css" />
      </head>
      <body>
        <span>Default Style을 테스트 해 봅니다.</span>
        <h1>이건 h1 태그에요</h1>
        <p>이건 p 태그에요</p>
      </body>
    </html>
    ```
    