## AMD asynchronous module definition 异步模块定义 require.js
__模块以及模块的依赖都加载完了再执行，主模块最后执行__
***
AMD 诞生原因是因为 CommonJS 不支持异步加载，不适合浏览器环境。RequireJS 实现了 AMD API
***
AMD 规范加载模块是异步的，并允许函数回调，不必等到所有模块都加载完成，后续操作可以正常执行
***
AMD 中，使用<kbd>require</kbd>获取依赖模块，使用<kbd>exports</kbd>导出 API
***
## 使用方法

> 在 index.html 中使用 script 标签加载 RequireJS，通过 data-main 属性指定主文件，没有 data-main 的话，默认是包含 index.html 的目录

```
    <!DOCTYPE html>
    <html>
        <head>
            <title>My Sample Project</title>
            <!-- data-main attribute tells require.js to load scripts/main.js after require.js loads. -->
            <script data-main="scripts/main" src="scripts/require.js"></script>
        </head>
        <body>
            <h1>My Sample Project</h1>
        </body>
    </html>

// main.js
require(['2.js'],function(A){
    //A得到的是2.js模块的返回值
})
// 2.js
define(['3.js','xxx.js'],function(A,B){
    //aaa 是2.js模块的返回值
    return aaa
})
// 3.js
define([],function(){
    //{} 是3.js模块的返回值
    return {}
})

```

**定义两个全局变量函数 require define (入口用require其他用define)**

>requirejs/require: 用来配置 requirejs 及载入入口模块。如果其中一个命名被其它库使用了，我们可以用另一个
> ![alt require](https://user-gold-cdn.xitu.io/2019/1/9/16831c0bd8dcf330?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
>define: 定义一个模块
> ![alt define](https://user-gold-cdn.xitu.io/2019/1/9/16831c4414e9cc5e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

```
es6
import A from 'a.js';
import B from 'b.js';

require.js
define(['a.js','b.js'],function(A,B){})
```

## 优点

> 防止 js 加载阻塞页面渲染
> 使用程序调用的方式加载 js，防止出现如下丑陋的场景

```
<script type="text/javascript" src="a.js"></script>
<script type="text/javascript" src="b.js"></script>
<script type="text/javascript" src="c.js"></script>
<script type="text/javascript" src="d.js"></script>
<script type="text/javascript" src="e.js"></script>
...
```

## 原理

> 插入 script 节点，并加载运行其 js 文件，
> 采用 <kbd>appendChild<kbd> 方法插入 script 节点，会立即<kbd>下载并运行 js <kbd>文件
> 利用 <kbd>onload</kbd>事件不断递归嵌套处理依赖文件
```
3.js 依赖 1.js

var node = document.createElement('script')
node.type = 'text/javascript'
node.src = '3.js'

// 3.js加载完成后触发onload事件
node.addEventListener('load',function(evt){
    var node1 = document.createElement('script')
    node.type='text/javascript'
    node.src='1.js'
    document.body.appendChlid(node2)
})
document.body.appendChild(node)
```
