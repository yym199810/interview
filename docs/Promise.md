## 一、问题
 1. Promise如何请求多个

 2.

## 二、知识点
1. 解决回调地狱

首先，我们要知道为什么会有Promise的出现？
就是解决回调地狱问题。那么什么是回调地狱？如下的一堆嵌套
```javaScript
function a(function b(){

     c(function d(){

 })})
```
2. 三种状态
- pending : 等待 也就是初始状态
- fullfilled : 成功
- rejected : 失败

状态会从 pending变为fullfilled或者rejected，一旦改变就不回不去了（要么成功、要么失败）。

3. resolve和reject
- resolve 返回成功内容 -- 状态从pending变为fullfilled
- reject 返回失败内容  -- 状态从pending变为rejected
```
// 创建一个Promise对象 需要一个回调函数
let p1 = new Promise((resolve,reject)=>{
    resolve('成功')
    // 不会执行
    reject('失败')
})
```
这里好要提一下throw（抛出异常），也会相当于reject
```
let p1 = new Promise((resolve,reject)=>{
    throw('异常')
})
```

