---
title: flexbox伸缩盒布局
date: 2014-11-21 09:37:20
tags: CSS
categories: 前端
---
Flex元素可以让你的布局根据浏览器的大小变化进行自动伸缩
原文[guide-to-flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

Flex元素分为flex containers 和 flex items

## 1. Flex container

![container](https://css-tricks.com/wp-content/uploads/2014/05/flex-container.svg)

#### 1.1 display
用于定义一个flex container 元素
```css
.container {
  display: flex; /* or inline-flex */
}
```

#### 1.2 flex-direction
用于设置主轴
![flex-direction](https://css-tricks.com/wp-content/uploads/2014/05/flex-direction1.svg)
```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

#### 1.3 flex-wrap
![flex-wrap](https://css-tricks.com/wp-content/uploads/2014/05/flex-wrap.svg)
```css
.container{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

#### 1.4 flex-flow
`flex-direction` 与 `flex-wrap` 的合并写法
默认属性为 `row nowrap`

```css
flex-flow: <'flex-direction'> || <'flex-wrap'>
```

#### 1.5 justify-content
用于flex items在设置主轴上的对齐方式
![justify-content](https://css-tricks.com/wp-content/uploads/2013/04/justify-content.svg)

```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

#### 1.6 align-items
用于flex items在设置侧轴(cross-axis)上的对齐方式

![align-items](https://css-tricks.com/wp-content/uploads/2014/05/align-items.svg)

```css
.container {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

#### 1.7 align-content

![align-content](https://css-tricks.com/wp-content/uploads/2013/04/align-content.svg)
```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

## 2. Flex items

#### 2.1 order

![order](https://css-tricks.com/wp-content/uploads/2013/04/order-2.svg)
```css
.item {
  order: <integer>;
}
```

#### 2.2 flex-grow

![flex-grow](https://css-tricks.com/wp-content/uploads/2014/05/flex-grow.svg)
```css
.item {
  flex-grow: <number>; /* default 0 */
}
```

#### 2.3 flex-shrink

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

#### 2.4 flex-basis

```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

#### 2.5 flex

`flex-grow`, `flex-shrink` 与 `flex-basis`的合并写法
```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

#### 2.6 align-self

![align-self](https://css-tricks.com/wp-content/uploads/2014/05/align-self.svg)
```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```