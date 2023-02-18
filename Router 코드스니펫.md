
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