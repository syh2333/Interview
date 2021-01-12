## 案例
```
<!DOCTYPE html>
<html>
    <head>
        <script type="text/javascript" src="a.js"></script>
    </head>
    <body>
      <span>body</span>
    </body>
</html>
```
a.js如下
```
function fun1(){
  alert("it works");
}

fun1();
```
或 
```
使用块作用域来申明function防止污染全局变量
(function(){
    function fun1(){
      alert("it works");
    }
    fun1();
})()
```

>运行上面两个例子，alert执行的时候，html的内容是一片空白的，当点击确定后，才出现
```
<span>body</span>
```