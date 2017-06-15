---
title: 路由的配置项
date: 2017-05-17 15:35:12
tags:
categories: react 
---

## 路由的基本使用方法

```jsx
import React from 'react'
import { render } from 'react-dom'
import { Router, Route, Link } from 'react-router'

const App = React.createClass({
  render() {
    return (
      <div>
        <h1>App</h1>
        <ul>
          <li><Link to="/about">About</Link></li>
          <li><Link to="/inbox">Inbox</Link></li>
        </ul>
        {this.props.children}
      </div>
    )
  }
})

const About = React.createClass({
  render() {
    return <h3>About</h3>
  }
})

const Inbox = React.createClass({
  render() {
    return (
      <div>
        <h2>Inbox</h2>
        {this.props.children || "Welcome to your Inbox"}
      </div>
    )
  }
})

const Message = React.createClass({
  render() {
    return <h3>Message {this.props.params.id}</h3>
  }
})

render((
  <Router>
    <Route path="/" component={App}>
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

如果路由按这种配置，我们就可以得到路由与URL的映射表： 

| URL                 | Components              |
| ------------------- | ----------------------- |
| /                   | App                     |
| /about              | App -> About            |
| /inbox              | App -> Inbox            |
| /inbox/messages/:id | App -> Inbox -> Message |



## Router的基础配置

**（1）路由默认首页（`IndexRoute`）** 

当URL为`/`的时候，我们需要增加一个默认的初始显示子组件。我们可以通过`IndexRoute`来设置默认页。

```jsx
import { IndexRoute } from 'react-router'

const Dashboard = React.createClass({
  render() {
    return <div>Welcome to the app!</div>
  }
})

render((
  <Router>
    <Route path="/" component={App}>
      {/* Show the dashboard at / */}
      <IndexRoute component={Dashboard} />
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

通过这样的设置，现在我们就有了默认元素了，这种方式类似于`apache`的直接根目录（`directorIndex`）或

者是`nginx`的`index`.是对直接根路径匹配路由，下面我们来看现在这种方式下的路由与URL的关系：

| URL                 | Components              |
| ------------------- | ----------------------- |
| /                   | App -> Dashboard        |
| /about              | App -> About            |
| /inbox              | App -> Inbox            |
| /inbox/messages/:id | App -> Inbox -> Message |

我们发现与上面相比，这里多了默认的首页路由：url为：`/`，路由的组件为`App ->Dashboard`

**（2）从`URL`中解耦`UI`**

如果我们能从URL为`/inbox/messages/:id` 的路由中，移除`/inbox`使得路由的真正页面为：`/message/:id`

同时保留了`JSX`的页面结构，[React](http://lib.csdn.net/base/react)-router允许我们使用这种缺省路径的方法。我们来看如下代码：

```jsx
render((
  <Router>
    <Route path="/" component={App}>
      <IndexRoute component={Dashboard} />
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox} />

      {/* Use /messages/:id instead of /inbox/messages/:id */}
      <Route component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

注意：这里的`message`所在的父路由，缺省了`path`，这样实际上我们就将路由从`/inbox/message/:id`转化

成为了`/message/:id`，但是整体的`JSX`结构并没有发生变化，只是缺省了`path`而已。这种缺省的方式，

使得我们能够避免非常复杂的层层`url`的书写方式，这样使得我们整个路由的控制显得简单名了。这种方式

的访问结果如下：

| URl           | Components              |
| ------------- | ----------------------- |
| /             | App -> Dashboard        |
| /about        | App -> About            |
| /inbox        | App -> Inbox            |
| /messages/:id | App -> Inbox -> Message |

上图中，值得注意的是我们只要通过`url: /message/:id `就可以访问到组件：`App -> Inbox -> Message`，大大的简化了`url`，但是访问结果却与`inbox/message/:id`完全相同。

**（3）重定向路由（`Redirect`）**

通过`Redirect`，我们可以重新定向路由。我们来看下面的例子：

```jsx
import { Redirect } from 'react-router'

render((
  <Router>
    <Route path="/" component={App}>
      <IndexRoute component={Dashboard} />
      <Route path="about" component={About} />

      <Route path="inbox" component={Inbox}>
        {/* Redirect /inbox/messages/:id to /messages/:id */}
        <Redirect from="messages/:id" to="/messages/:id" />
      </Route>

      <Route component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

现在，当我们访问`/inbox/message/:id`的时候，路由会自动跳转到新的`url：/message/:id`，这样我们就实现了路由的重定向。

**（4）路由的leave和enter,路由的进入和移除的过程**

路由定义了进入和移除时的`hook`，也就是路由的移入或者移除的时候会触发一定的事件，这些`hooks`是非常

有用的，比如路由移入（进入访问）的时候需要做一个**权限认证**，或者说路由移除（移除访问）的时候需要

**保存一些参数**等，我们来看什么时候会触发`leave hook`，什么时候会触发`enter hook`。

举一个例子：当我们从`url：/messages/5`，跳转到新的`url：/about`的过程。

（a）首先触发`/messages/:id` 路由的`leave hook`

（b）再次触发`/inbox `路由的`leave hook`

（c）最后触发`/about `路由的`enter hook`

**（5）利用插件的方法来配置路由，并且同时根据leave和enter hook，在JS中实现Redirect**

```jsx
const routes = {
  path: '/',
  component: App,
  indexRoute: { component: Dashboard },
  childRoutes: [
    { path: 'about', component: About },
    {
      path: 'inbox',
      component: Inbox,
      childRoutes: [{
        path: 'messages/:id',
        onEnter: ({ params }, replace) => replace(`/messages/${params.id}`)
      }]
    },
    {
      component: Inbox,
      childRoutes: [{
        path: 'messages/:id', component: Message
      }]
    }
  ]
}

render(<Router routes={routes} />, document.body)
```

这里通过`onEnter`中的方法来触发重定向，从而实现`Redirect`.

## 参考地址

 [Reacter-router（config）基础配置项](http://blog.csdn.net/liwusen/article/details/53282245)