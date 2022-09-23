>**1.vueRouter实现懒加载**
- 非懒加载
```
import List from '@/components/list.vue'
const router = new VueRouter({
  routes: [
    { path: '/list', component: List }
  ]
})
```
- 使用箭头函数 + import动态添加
```
const List = ()=>import('@/components/list.vue') 
const router = new VueRouter({
  routes: [
    { path: '/list', component: List }
  ]
})
```
- 使用箭头函数 + require添加
```
const router = new VueRouter({
  routes: [
    { 
         path: '/list', 
         component: resolve => require(['@/components/list.vue'],resolve) 
    
    }
  ]
})
```
- 使用webpack的require.ensure技术，也可以实现按需加载。 这种情况下，多个路由指定相同的chunkName，会合并打包成一个js文件。
```
// r就是resolve
const List = r => require.ensure([], () => r(require('@/components/list')), 'list');
// 路由也是正常的写法  这种是官方推荐的写的 按模块划分懒加载 
const router = new Router({
  routes: [
  {
    path: '/list',
    component: List,
    name: 'list'
  }
 ]
}))
```

>**2.路由的hash和history**
- hash 
  
  默认的是hash，hash值只会出现在URL里（带一个#），但是不会出现在HTTP请求中，对后端没有影响。已经成为SPA的标配。
  原理：window.onhashchange

  ```
  window.onhashchange = function(event){
	console.log(event.oldURL, event.newURL);
	let hash = location.hash.slice(1);
  }
  ```
  无需向后端发送请求，并且hash值变化对应的URL都会被浏览器记录下来，浏览器就能实现页面的前进和后退。

- history
  用户在输入一个URL，服务端便收到一个路由，并进行解析。没有#更加美观，但是需要服务端支持。如果没有相应的路由资源，则会404
  history API 
   - 修改历史状态 ： pushState()和replaceState()，虽然修改了url但不会立即向后端发送请求。要做到改变url又不刷新页面可以使用
   - 切换历史状态 ： forward go back
  
  使用history模式 需要配置
  ```
  const router = new VueRouter({
    mode: 'history',
    routes: [...]
    })
  ```