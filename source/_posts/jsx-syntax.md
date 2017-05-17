---
title: JSX语法深入理解
date: 2017-05-17 14:51:31
tags:
categories: react
---

简介：从根本上来说，JSX语法提供了一种创建[React](http://lib.csdn.net/base/react)元素的语法糖，JSX语句可以编译成： 
React.createElement(component, props, …children)的形式，比如：

```jsx
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```

编译结果：

```jsx
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)
```

## 指定React元素的类型

JSX标签的头部，决定了React元素的类型，大写的标签，意味着JSX的标签与React的组件一一对应，比如

```jsx
<Foo/>标签就对应了Foo组件
```

**（1）必须包裹在一定的范围内**

```jsx
import React from 'react';
import CustomButton from './CustomButton';

function WarningButton() {
  // return React.createElement(CustomButton, {color: 'red'}, null);
  return <CustomButton color="red" />;
}
```

比如这样，引入了2个组件，构成了一个新的组件WarningButton，组件的返回值的元素，必须包含在一定范围内，这里通过函数的’{ ‘, ’ } ‘实现包裹的效果。

**（2）用户定义的组件必须大写**

我们前面已经说过，JSX的标签与组件是一一对应的，当我们使用JSX语法，引用组件的时候，标签必须要大写（同时定义组件的函数名也必须是大写的）。

```jsx
function Hello(){
   return <h2>Hello,World</h2>
}
//定义过程

<Hello/>
//使用过程
```

**（3）不能在运行期间，动态的选择类型** 
我们不能在JSX中，动态的规定组件的类型，举例来说：

```jsx
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  return <components[props.storyType] story={props.story} />;
  //这样写是不对的，我们在返回的组件中，动态定义了组件，这种动态的定义是无效的
}
```

应该改写为：

```jsx
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {

  const SpecificStory = components[props.storyType];
  return < SpecificStory  story={props.story} />;
    //这样就是正确的，我们不要在JSX的标签中使用动态定义
}
```

## JSX中的Props属性

**（1）JS表达式** 
可以通过{}，包裹js的语法来使用。比如：

```jsx
<MyComponent foo={1 + 2 + 3 + 4} />
```

等价于：

```jsx
<MyComponent foo={10} />
```

如果不是js表达式，则不能包裹在{}中使用。

**（2）Props属性的默认值** 
Props上的属性可以有默认值，并且默认值为true，比如：

```jsx
<MyTextBox autocomplete />
<MyTextBox autocomplete={true} />
```

上面这两个式子是等价的，但是不推荐使用默认值，因为在`ES6`的语法中`{foo}`代表的意思是：`{foo:foo}`的意思，并不是`{foo:true}`。

**（3）扩展属性** 
可以通过ES6的…方法，给组件赋属性值，例如：

```jsx
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

上面的这两种方式是等价的。

## JSX中的children

**（1）children中的function**

我们来考虑自定义组件中包含函数的情况：

```jsx
function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```

那么何时调用这个children中的方法呢？

```jsx
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}
```

我们从上述的Repeat组件的定义中可以看出来，children中的方法按此定义会一直执行10次。

**（2）忽略Boolean，Null以及Undefined**

`false`,`null`,`undefined`以及`true`是不能通过render()方法，呈现在页面上的，下面的这些div块的样式 
相同，都是空白块：

```jsx
<div />
<div></div>
<div>{false}</div>
<div>{null}</div>
<div>{true}</div>
```

这种属性，在通过render呈现元素的时候，是十分有用的，比如我们只想在div元素中展现Head组件， 
例子如下：

```jsx
<div>
  {showHeader && <Header />}
  <Content />
</div>
```

这里的逻辑是，只有`showHeader==true`，在会在页面呈现`Header`组件，否则为`null`，即为不显示任何东西，这相当于一个`if`的判断了。

再举一个例子：

```jsx
<div>
  {props.messages.length &&
    <MessageList messages={props.messages} />
  }
</div>
```

在这个`div`中，我们需要知道的是即使元素为0，0是能够呈现在页面中的。也就是说上述代码中，只要 
`props.messages`数组存在，不管长度是否为`0`都是存在的。（这里不同于`js`，`js`中的语法认为`0==false`）

**（3）如何显示Null，Undefined和Boolean**

如果我们一定要再页面上显示`Null`等，可以将其先转化为字符串之后再显示。

```jsx
<div>
  My JavaScript variable is {String(myVariable)}.
</div>
```

通过String的转化后就能在页面上显示了。



## 参考地址

http://blog.csdn.net/liwusen/article/details/53383922