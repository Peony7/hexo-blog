---
title: ES6中的模块介绍
date: 2017-05-17 15:44:45
tags:
categories: es6
---

ES6在语言规格的层面上，实现了模块功能，而且实现得相当简单，完全可以取代现有的CommonJS和AMD规范，成为浏览器和服务器通用的模块解决方案。

ES6模块主要有两个功能：export和import

- export用于对外输出本模块（一个文件可以理解为一个模块）变量的接口
- import用于在一个模块中加载另一个含有export接口的模块。

## 以对象属性形式的export和import

```jsx
//export.js
let var1=1;
let var2=2;
function method1(){}
let method2=function(){}

export {var1,var2,method1,method2}
```

```jsx
//export.js
export let var1=1;
export let var2=2;
export function method1(){}
export let method2=function(){}
```

```jsx
//import.js
import{var1,var2,method1,method2} from "./export.js"
import * as myVar from "./export.js"
console.log(var1,var2,method1,method2,myVar)
//1
//2 
//method1() {} 
//method2() {} 
//Object {var1: 1, var2: 2,  method1:method1(),method2:method2(),default: "aaaa",__esModule: true}
```

## 以模板形式的export和import

```jsx
//export.js
export default let x=1;1212

//import.js
import x from  "./export.js";
console.log(x) //输出的是x
```

可以发现，通过export模板的话，输出的格式不是以对象的形式{x}，而是直接的x。