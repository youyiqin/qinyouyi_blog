---
title: 'Javascript,I promise - 异步编程'
date: '2021/4/9'
tags:
- JavaScript
mainImg: 'https://images.unsplash.com/photo-1611923973164-e0e5f7f69872?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MTc5NzU1MTI&ixlib=rb-1.2.1&q=80&w=1080'
coverImg: 'https://images.unsplash.com/photo-1611923973164-e0e5f7f69872?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MTc5NzU1MTI&ixlib=rb-1.2.1&q=80&w=400'
intro: 'Promise, JavaScript 世界中的异步处理对象.我阅读了 Dr.Axel 前辈的电子书,充满感激.'
---

虽然此前我已经接触过一些异步编程的概念,并且有过一定的实际运用.但是自我感觉,我对`JavaScript`异步编程的了解依然十分浅显,因此我打算再次对`JavaScript`中的异步编程进行学习和总结,然后分享出来.

# 1. 前文

在对`Promise`知识进行总结之前,我将回顾一部分`JavaScript`与异步编程相关的知识.

## 1.1 浅述 JavaScript 调用栈

当函数之间发生内嵌调用,将产生`函数调用栈`.

> `函数调用栈`是解释器追踪函数执行流的一种机制,函数入栈的同事也保存了其上下文环境.

```js
function h(z) {
  console.log(new Error().stack)
}
function g(y) {
  h(y + 1)
}
function f(x) {
  g(x + 1)
}
f(1)
```

如上述,随着调用函数`f(1)`,调用栈内开始存储函数`f(1)`,内部调用了`g(2)`也被存入调用栈,最后将`h(3)`存入调用栈,当前函数执行结束即将之从调用栈定移除,接着执行可能存在的剩余代码,最终调用栈被清空,执行流程回到全局作用域,最终打印如下:

```js
Error
    at h (REPL3:2:15)
    at g (REPL6:2:3)
    at f (REPL9:2:3)
    at REPL10:1:1
    at Script.runInThisContext (node:vm:133:18)
    at REPLServer.defaultEval (node:repl:474:29)
    at bound (node:domain:416:15)
    at REPLServer.runBound [as eval] (node:domain:427:12)
    at REPLServer.onLine (node:repl:793:10)
    at REPLServer.emit (node:events:388:22)
```

栈是有限度的,不同环境的栈空间大小不等,分配的栈空间被占满之后,将会引发栈溢出错误.



## 1.2 浅述浏览器事件循环

`JavaScript`具有一个基于`事件循环(event loop)`的并发模型.

我们可以简单的认为每个浏览器`tab`运行于一个简单的`事件循环`进程来实现`非阻塞`,浏览器中的诸多单一任务,例如:

- 解析 HTML
- 执行脚本中的 JavaScript 代码
- 响应用户交互
- 异步网络请求
- 等等

这些任务形成了独立于主线程的`任务队列(task queue)`,所有任务只能逐一通知主线程进行处理.由于`JavaScript`的单线程限制,即使`Web Worker标准`允许`JavaScript`脚本创建多个线程,但是子线程由主线程控制,且不可操作`DOM`,可以说`JavaScript`的本质依然是`单线程`.

如下是`Philip Roberts`演讲的时候使用的示意图:

![](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014100802.png)

当主线程执行栈上的同步任务执行完毕之后,就去读取`task queue`,按队列先进先出的属性,依次获取任务进行处理,然后重复检查主线程执行栈,通常我们为异步事件编写的`回调函数`,就进入了任务队列.

如果再细分任务队列中的任务,依然可以分为:

- 微任务(micro task)
- 宏任务(macro task)

像`setTimeout`和`setInterval`则是宏任务.

> **当前执行栈执行完毕时会立刻先处理所有微任务队列中的事件，然后再去宏任务队列中取出一个事件。同一次事件循环中，微任务永远在宏任务之前执行**。

## 1.3 定时器简析

`setTimeout(callback, ms)`函数创建了一个定时器等待若干毫秒, 然后将`callback`放入`task queue`,并且在等待计时器的其间脱离了主线程,这也就意味着如果主线程执行了耗时的同步任务,则任务队列被读取的时间就将被延迟了,因此可能不会在`ms`毫秒后执行`callback`回调函数.

实际延时还有其他的影响因素.

- 不同浏览器具有自己的`DOM_MIN_TIMEOUT_VALUE`,最小延时值.
- 为了优化后台 tab 的加载损耗(以及降低耗电量),在未被激活的 tab 中定时器的最小延时限制为`1S`.
- 追踪型脚本延时在后台 tabs 中,这个最小延时限制是 `10S`,这个限制会在文档第一次加载后的`30s`后生效.



## 1.4 显示 DOM 变化

对于大多数`DOM`元素的变化来说,它们的改动数据并不是实时更新的,`DOM`和`布局`的改动也与`事件循环`机制有关.如果需要频繁更新`DOM`,可以考虑`requestAnimationFrame()`函数.

> **`window.requestAnimationFrame()`** 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行

## 1.5 event loop 阻塞和消除

来看看一个阻塞事件循环的例子🌰 From `Dr. Axel Rauschmayer`:

```js
<p>
  <a id="block" href="">Block for 5 seconds</a>
<p>
    <button id="btn">This is a button</button>
<div id="statusMessage"></div>
<script>
document.getElementById('block').addEventListener('click', onClick);
document.getElementById('btn').addEventListener('click', onClickBtn);

function onClickBtn() {
  console.log("click the btn")
}

function onClick(event) {
  event.preventDefault();

  setStatusMessage('Blocking...');

  // Call setTimeout(), so that browser has time to display
  // status message
  setTimeout(function () {
    sleep(5000);
    setStatusMessage('Done');
  }, 0);
}
function setStatusMessage(msg) {
  document.getElementById('statusMessage').textContent = msg;
}
function sleep(milliseconds) {
  var start = Date.now();
  while ((Date.now() - start) < milliseconds);
}
</script>
```

我给`button`加了点击监听,如上所示,当你点击链接触发监听函数的时候再点击`button`,事件循环被阻塞5秒.这个期间点击`button`的监听函数无法如`"预期"`马上执行其逻辑,阻塞状态结束之后,点击函数的监听效果才会出现.

我们有两种方法消除事件循环的阻塞,其一便是将耗时的任务转移到`Worker API`中去,让另一个线程去处理.其二便是不使用同步的长时间等待逻辑,而是选择使用异步的方式去改写耗时的同步代码.例如上述的`sleep`函数便可以使用`setTimeout`来让我们达到异步的效果.

## 1.6 异步接收结果

首先,让我们来看看如何通过`事件处理机制`来异步获取结果,来看看一个`XMLHttpRequest`的例子:

```js
const req = new XMLHttpRequest();
req.open('GET', url);
// req.send();
req.onload = () => {
  if(req.status === 200) {
    // balabala
  } else {
  	console.log(`Error: ${req.statusText}`) 
  } 
}

req.onerror = () => {
  console.log('Error...')
}

req.send();
```

`req.send()`执行的时候只是将之添加到`任务队列`中,而非立刻执行此请求.因此,我们也可以将之写在设置`onload`和`onerror`事件的代码之前.

类似`Vue`和`Angular`中我们有时候会看到如下代码:

```js
// Vue
<button v-on:click="fb">
  Add 1
</button>
// Angular
<button (click)="fb()">
  some thing
</button>
```

上述代码`并不是行内属性`,我们可以很灵活的利用`JavaScript`和框架的特性灵活编写代码,为`DOM`添加事件监听.

> 上述示例代码风格只能给相应的属性设置一个值,后续的`onload`值将会覆盖前者.

在`IE9`之后,更常见的事件处理机制的使用方案也许是`addEventListener`(IE8 则可以使用`attachEvent`进行 hack),这种方案能够更大限度的设置事件监听的范围,例如设置多个同类型的事件处理函数,删除某个监听函数等等.

接着,我们来看看通过`callback`回调函数获取异步结果的示例:

```js
// Node.js
fs.readFile('file.txt', { encoding: 'utf8'}, (error, text) => {
  if(error) {
    // balabala
  }
  // 无错误
  // balabala
})
```

如上所示,如果读取文件内容顺利,将会执行回调函数.回调函数约定接收两个参数,一个是`错误`对象,另一个便是`预期数据`,如果我们不按约定编写回调函数,也不会报错.

如上这种异步编程风格被称为`continuation-passing style(CPS)`,开发者总是使用一个回调函数作为参数去调用,显示的将`控制流`作为参数进行传递,开发者可以看到程序内部隐式的控制流跳转.

`CPS`挺有趣的,我们来看一个简单例子.

```js
// 省略部分代码
const a = foo(x)
const b = someFunction(a)
```

如果我们按`CPS`风格来写:

```js
const b = foo(x, someFunction)
```

由此可见,我们可以在例如`惰性求值/异步/流程控制`等场景下编写上述风格的代码,`"也许"`是一种更好的选择(仁者见仁智者见智).

来看另一个例子:

```js
function foo(input, callback) {
	setTimeout(() => {
    callback(input)
  }, 0)
}
console.log('a')
foo('b', function step2(param) {
	console.log(param)
  foo('c', function step3(param) {
  	console.log(param)
  })
 	console.log('d')
})
console.log('e')
```

输出结果:` a e b d c`.

回调和控制流相互嵌套,常常让我们写出`"回调地狱"`代码.

在`Promise`出现之前,开发者们编写着各种回调函数,为了避免隐式`BUG`而孜孜不倦地检查异常处理逻辑,重复地为每一个回调函数编写冗长的`if error`错误监听.

# 2. Promise 异步

`TC39`依据`Promise/A+`制定了`ES6 Promise`规范,自此`JavaScript`异步编程向前迈进了一大步,开发者们可以更好的编写异步代码以应对复杂的场景和需求.

## 2.1 promise 实例和状态转换

`Promise`实例具有三种状态:

- `pending`: 初始化
- `fulfilled`: 成功
- `rejected`: 失败

> fulfilled 和 rejected 统称`settled`.

通过`Promise`构造器实例化一个`promise`的时候,其状态为`pending`.在实例化的时候传入一个函数`(execotor)`去处理状态转换逻辑.

> 本文不会对`promise`做面面俱到的介绍,推荐阅读官方文档.

首先,我们来创建一个`promise`实例:

```js
let promise = new Promise((resolve, reject) => {
  // balabala
  if(...) {
    resolve(value) // success
  } else {
  	reject(reason) // failure
  }
})
promise
  .then(function(value) {
		// balabala
  })
	.then(function(value) {
		// balabala
  })
	.catch(reason => {
  	// balabala
  })
```

传入的函数内部,可以显示按逻辑指定下一个状态.下图是`MDN`提供的`Promise`状态转移图.

![](https://mdn.mozillademos.org/files/8633/promises.png)

> `then`函数可以接收不同形参的函数以实现不同的状态处理逻辑,但是我们推荐使用单参数和使用 catch 处理错误的代码风格.

需要注意的是,`promise`实例的状态转换是单向的,一旦`settled`则不可逆转.

`promise`支持链式调用,每个`then`函数内部最后将返回一个新的`promise`实例,默认返回一个值为`undefined`,状态为`fulfilled`的`promise`实例.

**`Promise`出现之前,编写可以一次性监听所有回调函数的错误处理逻辑是困难的,`Promise实例`的实例方法`catch`能应对链式调用之前所有的`then`函数错误和显示的`reject`行为**.

我们可以显示地使用`return value`指定返回的`promise`对象的值.举个例子:

```js
asyncFunc()
	.then(function(v1) {
  	return 1
  	// return Promise.resolve(1)  	
})
	.then(function(v2) {
  	console.log(v2); // 1
})
```

除了`return`一个显示的值,在一些`Promise`相关的库源码中我们可能还会看到某些场景下返回一个`thenable`对象.

> `thenable对象`: 任意具有`then`方法的对象.

返回`thenable对象`的时候将执行其`then`方法,`Promise`实例对象也是`thenable对象`,因此在某些嵌套`Promise`的场景下,可以返回一个`异步函数调用`,就像这样:

```js
asyncFunc1()
	.then(v1 => {
  	asyncFunc2()
  		.then(v2 => {
      	//balabala
    })
})

// 扁平化
asyncFunc1()
	.then(v1 => asyncFunc2())
	.then(v2 => {
  	// balabala
})
```

## 2.2 Promise 静态方法

`Promise`类具有两个能创建一个新的实例的静态方法:

- Promise.resolve(param)
- Promise.reject(param)

二者区别在于返回的`promise`实例的状态,前者为`fulfilled`,后者为`rejected`.

此外,`Promise`类还有如下几个静态方法:

- `Promise.all(iterable)`
- `Promise.race(iterable)`
- `Promise.any(iterable)`
- `Promise.allSettled(iterable)`

这几个静态方法各有其应用场景.

### 2.2.1 all

首先,`Promise.all(iterable)`方法接收一个`iterable`对象作为参数,最终返回一个`promise 实例`.

首先,如果`iterable`对象是空的,则返回的结果是空数组.

```js

```



# 参考

- [JavaScript 运行机制详解：再谈Event Loop - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2014/10/event-loop.html)
- [JavaScript进阶01：异步1-事件监听和回调函数 | forkai's Notes](https://notes.forkai.com/2017/11/06/javascript%E8%BF%9B%E9%98%B601%EF%BC%9A%E5%BC%82%E6%AD%A51-%E4%BA%8B%E4%BB%B6%E7%9B%91%E5%90%AC%E5%92%8C%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0/)
- [architecture - Difference between event handlers and callbacks - Stack Overflow](https://stackoverflow.com/questions/2069763/difference-between-event-handlers-and-callbacks)
- [javascript - addEventListener vs onclick - Stack Overflow](https://stackoverflow.com/questions/6348494/addeventlistener-vs-onclick)
- 