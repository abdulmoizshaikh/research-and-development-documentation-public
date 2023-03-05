# Redux Toolkit

## Redux toolkit is recommended by official redux creators

@deprecated
`We recommend using the configureStore method of the @reduxjs/toolkit package, which replaces createStore.`

`Redux Toolkit` is our `recommended` approach for writing Redux logic today, including store setup, reducers, data fetching, and more.

For more details, please read this Redux docs page: https://redux.js.org/introduction/why-rtk-is-redux-today

configureStore from Redux Toolkit is an improved version of createStore that simplifies setup and helps avoid common bugs.

You should not be using the redux core package by itself today, except for learning purposes. The createStore method from the core redux package will not be removed, but we encourage all users to migrate to using Redux Toolkit for all Redux code.

If you want to use createStore without this visual deprecation warning, use the legacy_createStore import instead:

```jsx showLineNumbers
import { legacy_createStore as createStore } from "redux";
```

https://redux.js.org/introduction/why-rtk-is-redux-today

## createSlice vs createReducer

createSlice: A function that accepts an initial state, an object full of reducer functions, and a "slice name", and automatically generates action creators and action types that correspond to the reducers and state. createReducer: A utility that simplifies creating Redux reducer functions.21-Feb-2021

https://stackoverflow.com/questions/66307302/react-redux-createslice-or-createreducer#:~:text=createSlice%3A%20A%20function%20that%20accepts,simplifies%20creating%20Redux%20reducer%20functions.

**createSlice vs createReducer**

I would recommend createSlice() over createReducer() in almost all cases.

I can imagine a few hypothetical scenarios where you want to do some more hands-on definitions of action creators or define a reducer completely separately, but for the most part there's really no point.

The biggest issue atm with createSlice() is that there's not currently a way to write action creators that accept multiple arguments and process them to create the payload - you always have to pass the payload itself directly into the action creator. We've got a potential PR open to try to add payload customization, though.

https://www.reddit.com/r/reactjs/comments/cijpg8/createslice_vs_createreducer/

## redux toolkit with redux saga

https://codesandbox.io/s/mfetp?file=/src/saga.js

## nextjs-redux-example

https://github.dev/officialrajdeepsingh/nextjs-redux-example

## NextJs redux-saga example

https://github.com/vercel/next.js/tree/canary/examples/with-redux-saga
