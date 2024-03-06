# promise

## 1. 基本概念

### 1.1 什么是 Promise

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了 Promise 对象。
所谓 Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

### 1.2 Promise 对象

ES6 规定，Promise 对象是一个构造函数，用来生成 Promise 实例。

```
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
})
```

Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

resolve 函数的作用是，将 Promise 对象的状态从“未完成”变为“成功”（即从 Pending 变为 Resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject 函数的作用是，将 Promise 对象的状态从“未完成”变为“失败”（即从 Pending 变为 Rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise 实例生成以后，可以用 then 方法分别指定 Resolved 状态和 Rejected 状态的回调函数。

```
promise.then(function(value) {
  // success

})
.catch(function(error) {
  // failure
})
```

### 1.3 Promise.prototype.then()

Promise 实例的 then 方法，用来注册回调函数。

```
getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
})
```

### 1.4 Promise.prototype.catch()

Promise 实例的 catch 方法，是.then(null, rejection)的别名，用于指定发生错误时的回调函数。

```
getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}).catch(function(error) {
  console.error('出错了', error);
});
```

### 1.5 Promise.prototype.finally()

Promise 实例的 finally 方法，用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。

### 1.6 Promise.all()

Promise.all 方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

```
const p = Promise.all([p1, p2, p3]);
```

上面代码中，Promise.all 方法接受一个数组作为参数，p1、p2、p3 都是 Promise 实例，如果不是，就会先调用下面讲到的 Promise.resolve 方法，将参数转为 Promise 实例，再进一步处理。另外，Promise.all 方法的参数可以不是数组，但是一旦数组成员不是 Promise 实例，就会先调用下面讲到的 Promise.resolve 方法，将参数转为 Promise 实例，再进一步处理。

### 1.7 Promise.race()

Promise.race 方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。

```
const p = Promise.race([p1, p2, p3]);
```

上面代码中，只要 p1、p2、p3 之中有一个实例率先改变状态，p 的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给 p 的回调函数。

### 1.8 Promise.resolve()

有时需要将现有对象转为 Promise 对象，Promise.resolve 方法就起到这个作用。

```
const jsPromise = Promise.resolve($.ajax('/whatever.json'));
```

上面代码将 jQuery 生成的 deferred 对象，转为一个新的 Promise 对象。

### 1.9 Promise.reject()

Promise.reject(reason)方法也会返回一个新的 Promise 实例，该实例的状态为 rejected。

```
const p = Promise.reject('出错了');
// 等同于
const p = new Promise((resolve, reject) => reject('出错了'));
p.then(null, function (s) {
  console.log(s);
});
// 出错了
```

### 1.10 promise 的三个状态

1. pending: 初始状态，既不是成功，也不是失败状态。
2. fulfilled: 意味着操作成功完成。
3. rejected: 意味着操作失败。

### 1.11 promise 的缺点

1. 无法取消 Promise，一旦新建它就会立即执行，无法中途取消。
2. 如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。
3. 当处于 pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

### 1.12 promise 的优点

1. 可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。
2. 可以在对象之间传递和操作 Promise，帮助我们处理队列。
3. 可以在 Promise 执行中加入更多的处理逻辑，比如加入定时器，加入错误处理逻辑等。
4. 链式调用，可以解决回调地狱的问题。
5. 多个操作可以并行执行。
6. 错误处理机制，可以避免层层嵌套的回调函数。
7. 支持 Promise/A+规范。

### 1.13 promise 函数底层原理是根据什么封装的

    根据原生js提供的网络请求XMLHttpRequest封装的

# 2.XMLHttpRequest

### 2.1 基本用法

```
    const p =new Promise((resolve,reject)=>{
        //1.创建对象，创建链接XMLHttpRequest
      const xhr = new XMLHttpRequest()
      //2.初始化，设置请求方法和url
      xhr.open('GET','https://api.apiopen.top/getJoke')
      //3.发送
      xhr.send()
      //4.绑定事件，处理响应结果
      xhr.onreadystatechange = function(){
        //判断 等于4成功建立请求链接
        if(xhr.readyState === 4){
          if(xhr.status >= 200 && xhr.status < 300){
            resolve(xhr.response)
          }else{
            reject(xhr.status)
          }
        }
      }
    })
```
