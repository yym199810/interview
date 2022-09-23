> **1.对虚拟 DOM 的理解？虚拟 DOM 主要做了什么？虚拟 DOM 本身是什么？**
- 本质上，是一个javascript对象，描述DOM结构。因为是javaScript对象所以可以实现跨平台
- 通过事务处理机制，将多次更改结果一次渲染到页面，减少页面的重绘和重排，提高性能
- 对于react或者vue，在代码渲染到页面之前，会创建一个javascript对象，也就是（虚拟DOM）。更新前，会将javascript对象进行缓存，更新时新创建的虚拟DOM和缓存的虚拟DOM进行对比。



优点：
- 保证性能：减少重绘重排
   - 真实DOM：HTML字符串 + 重建所有DOM
   - 虚拟DOM：vNode + DOM diff + 必要的DOM更新 
- 跨平台

> **2.React diff 算法的原理是什么？**

