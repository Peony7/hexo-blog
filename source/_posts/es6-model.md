---
title: ES6中的模块介绍
date: 2017-05-17 15:44:45
tags:
categories: es6
---



简要介绍：ES6在语言规格的层面上，实现了模块功能，而且实现得相当简单，完全可以取代现有的

CommonJS和AMD规范，成为浏览器和服务器通用的模块解决方案。

ES6模块主要有两个功能：export和import

export用于对外输出本模块（一个文件可以理解为一个模块）变量的接口

import用于在一个模块中加载另一个含有export接口的模块。

1.以对象属性形式的export和import

（1）一般的形式

```
//export.js

export let x=1;

export let y=2;1234512345
```

```
import{x,y} from "./export.js"

console.log(x,y)//输出x=1,y=2123123
```

（2）函数名的形式

```
//export.js
export function x(){

}12341234
```

```
import {x} from "./export.js";
console.log(x)//输出的为x函数1212
```

也就是说：

```
export function x(){

}
等价于==
export let x=function(){

}12345671234567
```

（3）import as

```
//export.js
export let x=1;
export let y=2;

//import.js
import * as myVar from "./export.js"
console.log(myVar.x)//输出为1
console.log(myVar.y)//输出为21234567812345678
```

2.以模板形式的export和import

```
//export.js
export default let x=1;1212
import x from  "./export.js";
console.log(x) //输出的是x1212
```

可以发现，通过export模板的话，输出的格式不是以对象的形式{x}，而是直接的x。