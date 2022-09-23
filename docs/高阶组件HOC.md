1. 什么是高阶组件
将一个组件作为参数传给另一个组件。然后返回一个新的组件。
2. react Hooks的好处
- 代码复用更简单，更容易拆分组件
- 代码看起来更简洁
- 不需要声明周期了
- 不需要this了


https://lvan-zhang.blog.csdn.net/article/details/117399682?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-117399682-blog-120421164.pc_relevant_multi_platform_whitelistv6&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-117399682-blog-120421164.pc_relevant_multi_platform_whitelistv6&utm_relevant_index=1

3. 组件通信
父-子 ： 通过props向子组件传递数据
子-父 ： props + 回调函数
跨级 ： 如果是兄弟组件 可以都将数据传到父组件 再分发
       跨域层级较多 可以使用  context
       可以使用redux进行全局状态管理
4. react-router
- hash
- history
https://www.jianshu.com/p/612345f92897
```
<BrowserRouter>
    <Routes>
      <Route path="/" element={<App />} />
      <Route path="expenses" element={<Expenses />} />
      <Route path="invoices" element={<Invoices />} />
    </Routes>
  </BrowserRouter>
```
