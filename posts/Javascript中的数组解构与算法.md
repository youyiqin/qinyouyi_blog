---
title: 'Javascript中的数组解构与算法'
date: '2020/12/29'
tags:
- JavaScript
- 数据结构与算法
mainImg: 'https://images.unsplash.com/photo-1580706483913-b6ea7db483a0?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8&ixlib=rb-1.2.1&q=80&w=1080'
coverImg: 'https://images.unsplash.com/photo-1580706483913-b6ea7db483a0?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8&ixlib=rb-1.2.1&q=80&w=400'
intro: '几乎所有的编程语言都内置支持了数组类型,数组简单而有效,应用及其广泛.大多数编程语言的数组存储同一类型的值,而 JavaScript 则支持存储不同的值,但建议大家遵守最佳实践,避免这么做.'
---

JavaScript 中数组的基础知识不再多提.但是在此,依然希望再次巩固一次内置的数组静态方法,及其返回值.

想要查看`JavaScript`数组的文档信息,可以看看:[Array - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

# 创建数组

```js
let arr = new Array() // []
arr = new Array(7) // length is 7, [empty * 7]
arr = new Array(1,2,3) // [1,2,3]
arr = [] // 常用
arr = Array.from({length: 3}, (el, index) => index) // [0, 1, 2]
```

# 常用方法

主要分为:

- 添加元素
- 删除元素
- 迭代

`JavaScript`内置的数组方法是我们处理数组逻辑的最佳实践.

首先,添加元素内置从开始和从末尾添加.

```js
const arr = [1,2]
arr.push(3) // arr = [1,2,3], 返回数组添加数据后的长度:3

arr.unshift(0) // arr = [0,1,2,3], 同样返回新长度: 4
```

如果需要组合两个数组,并且将新数组返回可以参考如下代码:

```js
let arr1 = [1]
let arr2 = [2]
let arr3 = arr1.concat(arr2)
// arr3 = [1,2],没有副作用,不会修改原数组
```



其次是删除元素,非常方便:

```js
arr.pop() // arr = [0,1,2], 返回弹出的末尾元素 3
```

如果是需要从指定位置删除指定数量的元素,则可以使用`splice`方法.这个方法返回`被修改的内容`.例如删除了 n 个元素,则以数组的形式返回被删除的元素.如果删除元素为 0,且添加了若干元素,会返回一个`空数组`.

```js
arr.splice(5, 3)
// 删除 index 为 5, 6, 7 的元素,自动修正 length 属性
// 如果需要在指定位置插入新数据,也可以实现
let a = arr.splice(5, 0, 1, 2) 
// 下标为 5 为初始插入点,从参数上看,0 指的是删除 0 个数据,后续的 1 和 2 是新插入的数据,自动修正 length
// a is []
```



最后,为了灵活操作数组,`JavaScript`内置了多种迭代方式.

```js
let arr = [1, 2, 3, 4]
// every 迭代每个元素,直到迭代函数返回 false,立刻停止并且返回 false
arr.every(i => i > 0) // 返回 boolean 值 true

// 同样依次使用函数迭代,直到此函数返回 true,立刻停止并且返回 true,否则返回 false
arr.some(i => i === 1) // 返回 true

// 依次迭代每一个元素执行传入的函数,不会提前停止.
arr.forEach(i => console.log(i))

// 迭代结束后,返回新的数组
arr.filter(i => i % 2) 
=> [1, 3]
arr.map(i => i*i)
=> [1, 4, 9, 16]

// 实现累加
arr.reduce((prev, current) => prev + current, 0)
// 接收的函数还支持继续添加起始 index 和数组array
```

`ES6`继续带来了更多的数组功能,减少了外部库的载入和开发者的开发量.

- @@iterator: 默认与 values() 返回值一致,可以用`for..of..`迭代,返回一个迭代器,主要通过`Symbol.iterator`访问.
- copyWithin: 强悍的修改自身数组的方法,可以指定`target`为复制到自身的位置,`start`和`end`为复制区间,复制过程会动态调整复制内容,但是总体本身的`length`不变,最后修改自身数组并返回.
- entries: 返回包含数组所有键值对的@@iterator,如果使用`for..of`循环,每次`item`是一个数组,下标 0 是 key,1 是 value.
- includes: ES7 新增,支持查询是否包含查询目标,支持查询`NaN`.
- find: 数组查询,接收一个查询函数作为参数,找到则返回第一个值,否则返回`undefined`.
- findIndex:类似`find`,只是返回下标或者`-1`
- fill: 有趣的静态填充方法,指定填充内容,起始位置和结束位置,不包括结束位置,无返回值.
- from: 根据已有数组创建新数组并且返回.注意是浅拷贝的.还支持提供`mapFn`和`thisArg`,指定每个数组的回调函数和`this`对象.可以使用`Array.from({length: 2}, (el, i) => i)`创建数组`[0, 1]`.
- keys: 返回数组所有索引的@@iterator.
- values: 返回数组所有值的@@iterator.
- of: 函子,根据传入的参数创建数组.每个参数都是新数组的一个值.



# 多维数组

如果我们需要存储周一到周五每天上午和下午的天气,则可以使用如下多维数组:

```js
const weather = []
// 周一
weather[0][0] = '晴' //上午
weather[0][1] = '阴' //下午
// 周二
weather[1][0] = '雨'
weather[1][1] = '阴'
```

遍历的时候采用两层 for 循环即可.另外,在浏览器中可以使用`console.table(weather)`提供一个多维表格,更好的显示多维数组.



# 类型数组

`JavaScript`默认数组支持存储多种类型数据,但是也支持类型数组,常用的类型数组比如:

- Int8Array
- Unit8Array
- ...

类型数组在操作`webGL`,处理文件和图像的时候更常用.平时我接触的实在太少,此时便是无话可说.

2020年12月30日21:28:15 那么,再会.