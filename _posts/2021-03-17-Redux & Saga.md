---
title: Redux & Saga
tags: [React]

layout: single
date: 2020-03-04
toc: true
toc_sticky: true
---


### 文件
- [redux 官方](https://chentsulin.github.io/redux/docs/basics/index.html)
- [redux-saga 中文文件](https://neighborhood999.github.io/redux-saga/docs/introduction/BeginnerTutorial.html)
- [redux-devtools-extension](https://juejin.im/post/5c35cf00e51d45522665134b)

### 實作範例
[CH1-Redux -To do list](https://codesandbox.io/s/ch1-redux-to-do-list-707b9)
[CH2-Redux Thunk API-Movie list](https://codesandbox.io/s/ch2-redux-thunk-api-movie-list-pi1p5)
[CH3-Redux Saga API-Movie list](https://codesandbox.io/s/ch3-redux-saga-api-movie-list-usjtx)

### Redux 生命週期
![](https://i.imgur.com/SPUE2WW.png)
###### 參考範例：[CH1-Redux -To do list](https://codesandbox.io/s/ch1-redux-to-do-list-707b9)
1. **Action**：定義 Reducer 的進入點 ( type )
3. **Reducer**：由 Action 進入，對資料作用並儲存
    - **combineReducers**：可統一管理所有的 Reducer
5. **Store**：綁定 Reducer 創建完整的 Redux，並將資料存於 State
    - Store 只能有一個!
### 使用 Hooks 概念取值與觸發 Reducer
###### 參考範例：[CH1-Redux -To do list](https://codesandbox.io/s/ch1-redux-to-do-list-707b9)
由於使用 Redux 取資料與觸發 Reducer 過程繁雜，因此採用 react-redux 中的 useSelect 與 useDispatch。

+ import { useSelector, useDispatch } from "react-redux"
+ useSelector
+ useDispatch

### Redux Thunk
![](https://i.imgur.com/ddrT2Wt.png)
###### 參考範例：[CH2-Redux Thunk API-Movie list](https://codesandbox.io/s/ch2-redux-thunk-api-movie-list-pi1p5)

+ import thunk from "redux-thunk"
+ Store：createStore(rootReducer, applyMiddleware(thunk))

### Redux Saga
![](https://i.imgur.com/ggO2yrT.png)
###### 參考範例：[CH3-Redux Saga API-Movie list](https://codesandbox.io/s/ch3-redux-saga-api-movie-list-usjtx)
+ 使用指標函式(function*)
+ Store：
    ```javascript
    import { createStore, applyMiddleware, compose } from 'redux';
    import createSagaMiddleware from 'redux-saga';
    import reducer from '../reducer/index';
    import rootSaga from '../saga';
    
    const sagaMiddleware = createSagaMiddleware();
    export default createStore(reducer, applyMiddleware(sagaMiddleware));
    sagaMiddleware.run(rootSaga);

    ```









