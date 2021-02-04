## CMD Common Module Definition 通用模块定义 sea.js
__先执行主模块，碰到依赖执行依赖__
## 使用方法
只有define，没有require
```
// 1.js
define(function(){
    var a = require('2.js')
    var b = require('3.js')
})
// 2.js
define(function(){
    var b = require('3.js')
})
// 3.js
define(function(){
    //xxx
})
```