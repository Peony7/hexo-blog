---
title: react-scu
date: 2017-05-17 15:20:09
tags:
categories: react 
---



简介：ShouldCompleteUpdate，下文简称SCU，就是指明什么时候component（组件）需要进行更新。

1.常见的SCU的用法：

（1）比如在下面的例子中，组件中只有2个值，props.color和state.count可以发生改变，我们可以这样

使用SCU。

```
class CounterButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }

  shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
      return true;
    }
    if (this.state.count !== nextState.count) {
      return true;
    }
    return false;
  }

  render() {
    <button
      color={this.props.color}
      onClick={() => this.setState(state => ({count: state.count + 1}))}>
      Count: {this.state.count}
    </button>
  }
}123456789101112131415161718192021222324123456789101112131415161718192021222324
```

在上述代码中，组件仅仅会校验prop.color和state.count,如果这些值都不会改变，那么组件就不会有更新。

（2）如果组件更加复杂，拥有的状态变量更多

当组件复杂化，拥有状态变多时，我们需要设计一种模式，对所有的props变量和state变量，做一个“shallow comparison(浅比较）”，这样会使得SCU函数冗杂化，为了解决该问题，[React](http://lib.csdn.net/base/react)给了我们提供了另一个继承方法——React.PureComponent：

```
class CounterButton extends React.PureComponent {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }

  render() {
    <button
      color={this.props.color}
      onClick={() => this.setState(state => ({count: state.count + 1}))}>
      Count: {this.state.count}
    </button>
  }
}12345678910111213141234567891011121314
```

在大多数的情况下，”shallow comparison（浅比较）”是有意义的，因此在大部门情况下我们可以用React.PureComponent来代替SCU，但是当props和state中的变量发生突变的情况下，“shallow comparison”会失效，因此在props和state的变量发生突变的情况下，不能通过React.PureComponent来更新组件。

1. shallow comparison失效的情况

shallow comparion在js中：

```
var x=[1,2];
var y=x;
x.push(3);
console.log(x==y)//输出true12341234
```

```
var x={a:1};
var y=x;
x.b=2;
console.log(x==y)//输出true12341234
```

从上面我们可以看出，shallow comparison不能进行深层比较的原因是，js中数组和对象的本质都是Object，一旦赋值y=x后，无论x如何变化，x,y都会只想的是同一个对象。

3.如何解决shallow comparison失效的问题

（1）

失效状态1：

```
 handleClick() {
    // This section is bad style and causes a bug
    const words = this.state.words;
    words.push('marklar');
    this.setState({words: words});
  }123456123456
```

解决方法：

```
handleClick() {
  this.setState(prevState => ({
    words: prevState.words.concat(['marklar'])
  }));
}1234512345
```

失效状态2：

```
function updateColorMap(colormap) {
  colormap.right = 'blue';
}123123
```

解决方法：

```
function updateColorMap(colormap) {
  return Object.assign({}, colormap, {right: 'blue'});
}123
123
```

本质:解决方法的本质是生成了一个新的对象，新对象与原对象比较一定返回的是false。

（2）另一种方法是通过插件Immutable.js解决，不详细描述。

## 参考地址

 [React高级教程（es6）——（4）ShouldComponentUpdate的用法](http://blog.csdn.net/liwusen/article/details/53908266)