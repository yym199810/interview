# Headline

> An awesome project.

1. 包装类
https://www.cnblogs.com/dingdc/p/15213369.html
2. Object.create()
```
function create(obj){
    function F(){}
    F.prototype = obj
    <!-- 实例化 -->
    return new F()
}
```

docsify serve ./docs