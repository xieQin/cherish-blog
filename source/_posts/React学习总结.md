---
title: React学习总结
date: 2015-11-15 15:01:07
tags: React
categories: React
---

[文档](http://reactjs.cn/react/docs/getting-started.html)
[个人学习demo](https://github.com/xieQin/react-learning/tree/master/tutorial)

React 主要概念：
- 组件
- JSX
- Virtual DOM
- Data Flow

```js
import React, { Component } from 'react';
import { render } from 'react-dom';

class HelloMessage extends Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

// 加载组件到 DOM 元素 mountNode
render(<HelloMessage name="John" />, mountNode);
```

# 组件生命周期

- `componentWillMount`
- `componentDidMount`
- `componentWillReceiveProps`
- `shouldComponentUpdate`
- `componentWillUpdate`
- `componentDidUpdate`
- `componentWillUnmount`

一个简单例子：
```js
import React, { Component } from 'react';
import { render } from 'react-dom';

class LikeButton extends Component {
  constructor(props) {
    super(props);
    this.state = { liked: false };
  }

  handleClick(e) {
    this.setState({ liked: !this.state.liked });
  }

  render() {
    const text = this.state.liked ? 'like' : 'haven\'t liked';
    return (
      <p onClick={this.handleClick.bind(this)}>
          You {text} this. Click to toggle.
      </p>
    );
  }
}

render(
    <LikeButton />,
    document.getElementById('example')
);
```