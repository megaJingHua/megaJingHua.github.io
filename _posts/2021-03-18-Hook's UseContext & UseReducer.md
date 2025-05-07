---
title: Hook's UseContext & UseReducer
tags: [React]

layout: single
date: 2020-03-04
---

# Hook's UseContext & UseReducer
###### tags: `React`

### 實作範例
[CH4-Hooks useContext-Number+-](https://codesandbox.io/s/ch4-hooks-number--pbio5)
[CH5-Hooks useReducer](https://codesandbox.io/s/ch4-hooks-number--pbio5)

### UseReducer
###### 參考範例：[CH5-Hooks useReducer](https://codesandbox.io/s/ch4-hooks-number--pbio5)
+ 將資料傳入 state，並使用 dispatch 做 reducer 的溝通
``` javascript
import {todoReducer,initState} from './reducer'

const [listName, setListName] = useState(‘’)
const [state, dispatch] = useReducer(todoReducer, initState)

const addTodo = () => {
	dispatch({ type: 'ADD_TODO', payload: { name: listName } })
}

```

### UseContext
###### 參考範例：[CH4-Hooks useContext-Number+-](https://codesandbox.io/s/ch4-hooks-number--pbio5)
+ 在 component 中以 useContext 代替 mapPropsToState 和 Connect
``` javascript
import React, { useReducer } from 'react'
import {reducer, initialState} from './reducer/number'

const CounterContext = React.createContext()
 
function CounterProvider(props) {
	const [state, dispatch] = useReducer(reducer, initialState)
	return (
	<CounterContext.Provider value={{ state, dispatch }}>
		{props.children}
	</CounterContext.Provider>
	)
}

export { CounterContext, CounterProvider }

```
+ useContext 只能接收上層組件 React.creatContext 的 state 與 dispatch
``` javascript
import React, { useContext } from 'react'
import ReactDOM from 'react-dom'
import { CounterProvider, CounterContext } from './Context'
 
function Counter() {
    const { state, dispatch } = useContext(CounterContext)
    return (
        <div>
            <h5>{state.count}</h5>
            <button onClick={() => dispatch({ type: 'increment' })}>+</button>
            <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
        </div>
    )
}

function App() {
    return (
        <div className="App">
            <CounterProvider>
                <Counter />
            </CounterProvider>
        </div>
    )
}

const rootElement = document.getElementById('root')
ReactDOM.render(<App />, rootElement)
```




