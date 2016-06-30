---
title: react-router使用指南
date: 2016-05-20 17:00:39
tags: React
categories: React
---

react-router 作为react的路由插件，整体使用上我觉得比vue-router更为方便（除了变来变去的api），
特别是路由嵌套简洁很多。
原文见[react-router-tutorial](https://github.com/reactjs/react-router-tutorial)

## 一、安装

```bash
npm install react-router --save
```

## 二、显示路由
在入口文件处
- 引入`Router` 、`Route`、`hashHistory`

- render `Router`

```js
import { Router, Route, hashHistory } from 'react-router'
import About from './modules/About'
import Repos from './modules/Repos'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
    <Route path="/repos" component={Repos}/>
    <Route path="/about" component={About}/>
  </Router>
), document.getElementById('app'))
```

使用history api 管理路由时：
```js
// index.js
// ...
import { Router, Route, browserHistory } from 'react-router'

render((
  <Router history={browserHistory}>
    {/* ... */}
  </Router>
), document.getElementById('app'))
```

## 三、嵌套路由
嵌套路由的实现相比vue-router中通过声明子路由的方法简洁直观了很多
路由的嵌套与对应组件的嵌套之间是存在对应关系，通过这种对应关系来实现嵌套路由
```
<App>       {/*  /          */}
  <Repos>   {/*  /repos     */}
    <Repo/> {/*  /repos/123 */}
  </Repos>
</App>
```

```js
// index.js
// ...
render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>
      {/* make them children of `App` */}
      <Route path="/repos" component={Repos}/>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))

```

```js
// modules/App.js
// ...
  render() {
    return (
      <div>
        <h1>Ghettohub Issues</h1>
        <ul role="nav">
          <li><Link to="/about">About</Link></li>
          <li><Link to="/repos">Repos</Link></li>
        </ul>

        {/* add this */}
        {this.props.children}

      </div>
    )
  }
// ...
```

## 四、导航样式
访问各路由时显示对应的激活样式

#### 1. Active Styles
```js
// modules/App.js
<li><Link to="/about" activeStyle={{ color: 'red' }}>About</Link></li>
<li><Link to="/repos" activeStyle={{ color: 'red' }}>Repos</Link></li>
```

#### 2. Active Class Name
```js
// modules/App.js
<li><Link to="/about" activeClassName="active">About</Link></li>
<li><Link to="/repos" activeClassName="active">Repos</Link></li>
```
```css
.active {
  color: green;
}
```

#### 3. 封装成NavLink组件
```js
import React from 'react'
import { Link } from 'react-router'

export default React.createClass({
  render() {
    return <Link {...this.props} activeClassName="active"/>
  }
})
```

```js
// modules/App.js
import NavLink from './NavLink'

// ...

<li><NavLink to="/about">About</NavLink></li>
<li><NavLink to="/repos">Repos</NavLink></li>
```

#### 4. IndexLink
```js
// App.js
import { IndexLink } from 'react-router'

// ...
<li><IndexLink to="/" activeClassName="active">Home</IndexLink></li>
```

#### 5. onlyActiveOnIndex
```js
<li><Link to="/" activeClassName="active" onlyActiveOnIndex={true}>Home</Link></li>
```

```js
<li><NavLink to="/" onlyActiveOnIndex={true}>Home</NavLink></li>
```

## 五、参数传递
用户获取及传递url中附带的参数
有`/repos/:userName/:repoName`这样的路由

```js
// modules/Repo.js
import React from 'react'

export default React.createClass({
  render() {
    return (
      <div>
        <h2>{this.props.params.repoName}</h2>
      </div>
    )
  }
})
```

```js
// ...
// import Repo
import Repo from './modules/Repo'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>
      <Route path="/repos" component={Repos}/>
      {/* 添加新路由 */}
      <Route path="/repos/:userName/:repoName" component={Repo}/>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))
```

```js
// Repos.js
import { Link } from 'react-router'
// ...
export default React.createClass({
  render() {
    return (
      <div>
        <h2>Repos</h2>

        {/* 添加跳转链接 */}
        <ul>
          <li><Link to="/repos/reactjs/react-router">React Router</Link></li>
          <li><Link to="/repos/facebook/react">React</Link></li>
        </ul>

      </div>
    )
  }
})
```

## 六、设置初始路由
```js
// index.js
// 从'react-router' 中添加新的引用： `IndexRoute`
import { Router, Route, hashHistory, IndexRoute } from 'react-router'
// 添加 Home 组件
import Home from './modules/Home'

// ...

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>

      {/* 将Home组件作为 `/`的子路由添加 */}
      <IndexRoute component={Home}/>

      <Route path="/repos" component={Repos}>
        <Route path="/repos/:userName/:repoName" component={Repo}/>
      </Route>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))
```

## 七、触发路由
使用`browserHistory`
```js
// modules/Repos.js
import { browserHistory } from 'react-router'

// ...
  handleSubmit(event) {
    // ...
    const path = `/repos/${userName}/${repo}`
    browserHistory.push(path)
  },
// ...
```

使用`Router`
```js
// ask for `router` from context
  contextTypes: {
    router: React.PropTypes.object
  },

  // ...

  handleSubmit(event) {
    // ...
    this.context.router.push(path)
  },
```