# Redux toolkit fixes

**How to reset state of Redux Store when using configureStore from @reduxjs/toolkit?**

worked on this in hefazat web app

```jsx showLineNumbers
import { authReducer } from './auth'
import { combineReducers } from 'redux'
import { Action, actionTypes } from '../interfaces'

const combinedReducer = combineReducers({
  auth: authReducer,
})

export type RootState = ReturnType<typeof combinedReducer>

const rootReducer = (state: RootState, action: Action) => {
  if (action.type === actionTypes.LOGOUT) {
    // check for action type
    // state = undefined
    state = {} as RootState
  }
  return combinedReducer(state, action)
}


export default rootReducer

```

```jsx showLineNumbers title="/src/store/index.tsx"
function HelloCodeTitle(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

https://stackoverflow.com/questions/59061161/how-to-reset-state-of-redux-store-when-using-configurestore-from-reduxjs-toolki
