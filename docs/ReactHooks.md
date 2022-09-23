
>  **1.ReactHooks 对 React Hook 的理解，它的实现原理是什么**
   组件有两种形式
   - Class组件
     Class组件继承自React.Component，因此可以有很多方法供我们调用，如生命周期。
     编写繁琐，加大了理解成本。组件内部的逻辑难以拆分复用。
   - 函数式组件
     又称为无状态组件，无法定义和维护state。相反其轻量、易于维护、学习成本低。
   
   对比：
      - 类组件需要继承class
      - 类组件可以定义和维护state

> **2. 组件通信**
- 父->子：props
- 子->父：回调函数+props
- 跨域层级较多 ：在中间层组件层层传递 或者 使用 redux 、 Context
```
const BatteryContext = createContext();
 <BatteryContext.Provider value={color}>
        <Child></Child>
</BatteryContext.Provider>
<BatteryContext.Consumer>
 {
     color => <h1 style={{"color":color}}>我是红色的:{color}</h1>
 }
</BatteryContext.Consumer>
```
- 非层级关系：redux 、自定义发布订阅事件（使用pubsub.js ）











> 1. useEffect代替生命周期

[请参考此文]('https://blog.csdn.net/Android062005/article/details/125200236')
- 第二个参数为  [] 空数组 相当于componentDidMount（组件已经挂载）
- 第二个参数中 [a] 有参数 相当于componentDidUpdate （组件已经更新）
- 第二个参数不传 并且第一个参数 返回函数一个函数 代替 componentWillUnmount（组件卸载）
```
function Example() {
  // 当我们不指定第二个参数的同时并在第一个参数中返回一个函数就可以代替我们类组件中的componentWillUnmount
  useEffect(() => {
  	return () => {
	  console.log('will unmount');  
	}
  });  
  return <div></div>;
}
```
![](https://img-blog.csdnimg.cn/9034519e1d5643ceb2d488cdc7ae4c32.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5pip5pme,size_20,color_FFFFFF,t_70,g_se,x_16)


https://www.cnblogs.com/hymenhan/archive/2021/04/28/14711516.html