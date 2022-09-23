> **1.Object.is** 

- 语法：Object.is(value1, value2);
- 参数：value1：要比较的第一个值。value2：要比较的第二个值。
- 返回值：一个布尔表达式，指示两个参数是否具有相同的值。
- 说明：解决了
    - 两个NaN相等的问题（实际上任何两个NaN是不等的）
    - +0 和 -0 不相等的问题
```
Object.is(NaN,NaN)  // true
Object.is(+0,-0)    // false
Object.is({},{})    // false
Object.is('12','12')  // true
```

> **2.Object.assign**
- 语法：Object.assign(target, ...sources)
- 参数：target：目标对象。sources：被合并的对象。
- 返回值：修改后的目标对象。 
```
// 用于复制对象（浅拷贝）
let obj = {name:'1'}
let newObj = Object.assign({},obj)
// 合并对象
let obj1 = {name:'2',year:2019}
let assign_obj = Object.assign(obj,obj1) // {name:'2',year:2019}
console.log(obj)   // {name:'2',year:2019}  obj被修改并且如果有相同属性被覆盖
```

> **3.Object.entries** 

ES8的Object.entries是把对象转成键值对数组， [key, value] 对的数组。
- 语法：Object.entries(obj)
- 参数：obj：要返回其自己的可枚举字符串键属性 [key, value] 对的对象。
- 返回值：给定对象自己的可枚举字符串键属性 [key, value] 对的数组。
- Object.fromEntries则相反，是把键值对数组转为对象
```
let obj = {name:'123',age:12}
let newObj = Object.entries(obj)    // [['name','123'],['age',12]]
// Object.fromEntries
let oldObj = Object.fromEntries([['name','12']])   // {'name':'12'}
``` 

> **4.Object.values()** 

 方法返回给定对象自己的可枚举属性值的数组，其顺序与 for...in 循环提供的顺序相同。
- 语法：Object.values(obj)
- 参数：obj：要返回其可枚举自身属性值的对象。
- 返回值：包含给定对象自己的可枚举属性值的数组。
```
Object.values({name:"yym",age:12}) // ["yym",12]
```

> **5.Object.keys()** 

Object.keys() 方法用于返回给定对象自己的可枚举属性名称的数组，以与普通循环相同的顺序迭代。
- 语法：Object.keys(obj)
- 参数：obj：要返回可枚举自身属性的对象。
- 返回值：表示给定对象的所有可枚举属性的字符串数组。
```
Object.values({name:"yym",age:12}) // ["name","age"]
```

> **6.Object.prototype.hasOwnProperty()** 

Object.prototype：说明是Object原型上的方法
指示对象自身属性中是否具有指定属性，也就是判断一个对象的属性定义本身而不是继承自原型链。
- 语法： obj.hasOwnProperty()
- 参数：prop：要测试的属性的字符串名称或符号。
- 返回值：如果对象将指定的属性作为自己的属性，则返回true；否则为false。
```
let obj = {name:'yym',age:23}
obj.hasOwnProperty('name')  // true
```

> **7.Object.prototype.toString** 

继承自object原型的方法

- 语法：toString()
- 返回值：表示对象的字符串。
```
let obj = {name:'yyy'}
obj.toString() // '[object Object]'
```

> **8.Object.freeze()** 

冻结一个对象，这意味着它不能再被更改。冻结对象可防止向其添加新属性，防止删除现有属性，防止更改现有属性的可枚举性、可配置性或可写性，并防止更改现有属性的值。它还可以防止其原型被更改。
- 语法：Object.freeze(obj)
- 参数：obj：要冻结的对象。
- 返回值：传递给函数的对象。

> **9.Object.create()** 

创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。
- 语法：const me = Object.create(person);
- 参数：

    - proto：新创建对象的原型对象。
    - propertiesObject可选。需要传入一个对象，该对象的属性类型参照Object.defineProperties()的第二个参数。如果该参数被指定且不为 undefined，该传入对象的自有可枚举属性(即其自身定义的属性，而不是其原型链上的枚举属性)将为新创建的对象添加指定的属性值和对应的属性描述符。

- 返回值：一个新对象，带着指定的原型对象和属性。
