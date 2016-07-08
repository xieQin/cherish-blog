---
title: Redux学习总结
date: 2016-06-15 15:01:17
tags: Redux
categories: React
---

![Redux流程图](https://camo.githubusercontent.com/76224d874f32535aa62c0cd01750fb71fb02cf53/687474703a2f2f70362e7168696d672e636f6d2f642f696e6e2f39613331326463632f7265647578466c6f772e706e67)

从Redux的流程图来看，redux的整体思想还是不难理解的
只是当遇到各种为了同构而设计得较为繁琐的API、为了相对高效率地获得状态树的局部状态而引入的第三方库时，
难免有些地方迷糊
因此总结一下学习中的要点，备查

[推荐教程](https://github.com/happypoulp/redux-tutorial)
[文档](http://redux.js.org/)

# 1. Redux

Redux主要特点：
- state以单一对象存储在store对象中
- state只读，state变化时应返回新的state而不是更新原state
- 使用纯函数reducer执行state更新

>state 为单一对象，使得 Redux 只需要维护一棵状态树，服务端很容易初始化状态，易于服务器渲染。state 只能通过 dispatch(action) 来触发更新，更新逻辑由 reducer 来执行

## 1.1 Action

action 可以理解为应用向 store 传递的数据信息（一般为用户交互信息）

```js
function addTodo(text) {
  return {
    type: ADD_TODO,
    text,
  }
}
store.dispatch(addTodo(text))
```
如果要处理异步 action，需要使用一些中间件。 
redux-thunks 和 redux-promise 分别是使用异步回调和 Promise 来解决异步 action 的问题

## 1.2 Reducer
更新state的纯函数，用来执行根据指定 action 来更新 state 的逻辑
`(previousState, action) => newState`
`combineReducers(reducers)` 可以把多个 reducer 合并成一个 root reducer

## 1.3 Store

store 是一个单一对象：

- 管理应用的 state
- 获取 state `store.getState()`
- 触发 state 更新 `store.dispatch(action)`
- 注册 state 变化监听器 `store.subscribe(listener)`
- 创建store `createStore(reducer, [initialState])`

# 2. Middlewares
dispatch(action) 是一个同步的过程：执行 reducer 更新 state -> 调用 store 的监听处理函数。
如果需要在 dispatch 时执行一些异步操作（fetch action data），此时就需要引入 Middleware 解决。

```js
export default function thunkMiddleware({ dispatch, getState }) {
  return next => action =>
    typeof action === 'function' ? action(dispatch, getState) : next(action)
}
```
`newDispatch = middleware1(middleware2(...(dispatch)...))`

# 3. react-redux
[react-redux 文档](http://cn.redux.js.org/docs/react-redux/index.html)

API:

- `<Provider store>`
- `connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])`

# 4. 总结

- action是纯声明式的数据结构，提供事件的所有要素
- reducer是一个匹配函数, 所有的reducer都可以捕捉到action并匹配与自己相关与否，相关就拿走action中的要素进行逻辑处理，修改store中的状态，不相关就不对state做处理原样返回
- store负责存储状态并可以被react api回调，发布action
- react-redux, 提供一个Provider和connect
- Provider是一个普通组件，可以作为顶层app的分发点，传入store属性后，它会将state分发给所有被connect的组件
- connect是一个科里化函数，先接收两个参数（数据绑定mapStateToProps和事件绑定mapDispatchToProps），再接受一个参数（将要绑定的组件本身）
- mapStateToProps：构建好Redux系统的时候，它会被自动初始化，但是你的React组件并不知道它的存在，因此你需要分拣出你需要的Redux状态，所以你需要绑定一个函数，它的参数是state，简单返回你关心的几个值。
- mapDispatchToProps：声明好的action作为回调，也可以被注入到组件里，就是通过这个函数，它的参数是dispatch，通过redux的辅助方法bindActionCreator绑定所有action以及参数的dispatch，就可以作为属性在组件里面作为函数简单使用了，不需要手动dispatch。这个mapDispatchToProps是可选的，如果不传这个参数redux会简单把dispatch作为属性注入给组件，可以手动当做store.dispatch使用。