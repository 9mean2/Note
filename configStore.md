
``` jsx
import { createStore } from "redux";

import { combineReducers } from "redux";

  

const rootReducer = combineReducers({

//이곳에 Modules 폴더에 넣어놓은 state의 묶음들을 넣을 예정

//즉, 리듀서

});

const store = createStore(rootReducer);

  

export default store;
```