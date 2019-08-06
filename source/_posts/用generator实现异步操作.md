---
title: 用generator实现异步操作
date: 2017-04-16 18:28:23
tags: Javascript
categories: 编程
---

实现一个co函数，接收一个generator，实现自动执行

示例代码
```js
function* generator() {
  console.log('generator start')
  yield new Promise((resolve, reject) => {
    resolve(1)
  })
  console.log('generator 1')
  yield new Promise((resolve, reject) => {
    console.log('generator 2')
    resolve(2)
  })
}

function co(gen) {
  const iterator = gen();

  function autoRun(iteration) {
    if (iteration.done) {
      return iteration.value;
    }
    const anotherPromise = iteration.value;
    anotherPromise.then(x => {
      return autoRun(iterator.next(x));
    })
  }

  return autoRun(iterator.next());
}

co(generator)
// generator start
// generator 1
// generator 2
```

co函数的流程如下:
- co传入一个genetor并运行，获得一个iterator(generator())
- 调用next()方法，获取到iteration,iteration的value是异步流程的结果，也即一个Promise。
- yield返回出的任务，由外部执行和处理，结束后在返回,于是使用then方法。
- 处理后的结果为x，调用iterator.next(x)把x返回的同时，拿到了下一个yield的抛出的任务。
- 处理任务，得到result，并通过next(result)返回给genetor。
