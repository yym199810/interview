> **1. Object.defineProperty**

有如下三个配置项
- 可枚举 enumerable
- 可修改 writable
- 可删除 configurable
```
let person = {
    name:'yym'
}
Object.defineProperty(person,'age',{value:18})
// 使用defineProperty添加的属性，在遍历person是得不到的。
Object.keys(person)
// 1.enumerable:true 控制枚举
Object.defineProperty(person,'age',{
        value:18,
        enumerable:true 
})
person.age = 19
console.log(person)  // 此时age属性不会被更改 还是 {name:'yym',age:18}
// 2.控制属性是否可以被修改
Object.defineProperty(person,'age',{
        value:18,
        enumerable:true,
        writable:true 
})
delete person.age   // false
// 3.控制属性可以删除
Object.defineProperty(person,'age',{
        value:18,
        enumerable:true,
        configurable:true 
})
```
**get**

当有人读取person的age属性时，get函数（getter）就会被调用，且返回值就是age的值。

getter:属性名为get，属性值是个函数，加到一起我们叫getter
```
// number更改person的age也更改
let number = 18;
let person = {
    name:'yym',   
}
Object.defineProperty(person,'age',{   
 get:function(){
    return number
 }
})
number = 19
console.log(person)   // {name:'yym',age:19}
```
**set**

当有人修改person的age属性时，set函数（setter）就会被调用，且会收到修改的具体值
```
set(value){
    // 修改 age的值 让number变量也改变
    number = value
}
```
**数据代理**

通过一个对象代理对另一个对象中属性的操作（读/写），如下obj2可以读取obj1的x属性。obj2也可修改x属性
```
let obj1 = {x:100}
let obj2 = {y:200}
Object.defineProperty(obj2,'x',{
    get(){
        return obj1.x
    },
    set(value){
        obj1.x = value
    }
})
```
> **2.vue的数据代理**
