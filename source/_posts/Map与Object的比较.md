---
title: Map与Object的比较
date: 2018-03-20 
tags:
---
![](/images/socket-800-400.png)
# 前言
***
Maps是es6里面新增的对象类型，创建形式如下：
```JavaScript
// Creating new map
let myMap = new Map()
```
<!-- more -->
传递数组参数：
```JavaScript
const myMap = new Map([
  ['name',  'xiaoHong'],
  ['gender', '女'],
  ['age', 23]
])

console.log(myMap)
// Output:
// Map { 'name' => 'xiaoHong', 'gender' => '女', 'age' => 23 }
```
对象转化参数：
```JavaScript
const myObj = {
  subject: 'Math',
  level: '1',
  difficulty: 'Medium'
}

const myMap = new Map(Object.entries(myObj))

console.log(myMap)
// Outputs:
// Map { 'subject' => 'Math', 'level' => '1', 'difficulty' => 'Medium' }

```

# 快速了解maps
我们知道Objects是用来以key-value对的形式存储数据的，Maps跟Objects很相似，当你往maps中存储数据的时候，其实也是key-value对的形式。

跟objects很相似，maps可以添加和删除属性，还可以检索values值，那么它们之间到底有什么区别呢？
下面让我们来做个比较：
# Maps vs Objects
简单总结如下：
1. maps的keys可以是 ``任意数据类型``，甚至包括 ``对象`` 和 ``函数``，objects的keys只能是``字符串`` 或者 [symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol)。
2. maps支持keys的排序并且是按照``添加的顺序``进行排列的, objects从es6开始只在``JavaScript engines``中才支持排序，在es6之前是不支持的。
3. maps的key-value对的数量获取更加容易，通过``size``属性即可，而objects要获取key-value对的数量需要先通过``keys()`` 或者 ``values()`` 方法。
4. maps的遍历更加方便快捷，objects需要通过先获取数组形式的keys或者values集合,maps直接调用 ``forEach()``即可，就像数组一样方便，也可以像objects一样使用 ``for...of`` 循环。
forEach():
```JavaScript
const myMap = new Map()
//添加属性值
myMap.set('name', 'xiaoHong')
myMap.set('gender', '女')
myMap.set('age', '23')

myMap.forEach((value, key) => {
  console.log(`${key}: ${value}`)
})
// Output:
// 'name: xiaoHong'
// 'gender: 女'
// "age: 23"

```
for...of和next():
```JavaScript
const myMap = new Map()
//添加属性值
myMap.set('name', 'xiaoHong')
myMap.set('gender', '女')
myMap.set('age', '23')

// 也可以调用 keys() and values()
const entriesIterator = myMap.entries()

for (let item of entriesIterator) {
  console.log(item)
}
// Output:
// [ 'name', 'xiaoHong' ] // [ 'gender', '女'] // [ 'age', '23' ]

const keysIterator = myMap.keys()

console.log(keysIterator.next().value)
// Output:
// 'name'

console.log(keysIterator.next().value)
// Output:
// 'gender'

const valuesIterator = myMap.values()

console.log(valuesIterator.next().value)
// Output:
// 'xiaoHong'

console.log(valuesIterator.next().value)
// Output:
// '女'


```

5. maps对添加和删除key-value对的操作进行了性能上的优化，Objects则没有，所以使用maps可以帮助你提升代码的性能。

## 表格

| Maps     | 	VS   | Objects   |
| -------- | ------  | --------  | 
| 任意类型     | KEY类型  |  String 或者 [Symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol) | 
| YES     | KEY排序 | NO(ES5) |
| YES    | 属性数量 |   NO  |
| YES   | 遍历     |   NO   |
| YES   | Add和Delete性能优化 |   NO   |

