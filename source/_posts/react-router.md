---
title: react-router
date: 2017-05-17 15:35:12
tags:
categories: react 
---





简介：路由的配置项，是为了说明路由是如何根据url来匹配的，并且决定何时根据某一段url执行某一个函

结合官方文档来介绍一些路由的基础配置项。

1.我们在介绍Reacter-router的基础时，介绍了路由的基本使用方法：

```
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
), document.body)1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515212345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152
```

如果路由按这种配置，我们就可以得到路由与URL的映射表： 
![这里写图片描述](http://img.blog.csdn.net/20161122093049071)

2.Router的基础配置

（1）路由默认首页（IndexRoute）: 当URL为“/”的时候，我们需要增加一个默认的初始显示子组件。

我们可以通过IndexRoute来设置默认页。

```
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
), document.body)12345678910111213141516171819201234567891011121314151617181920
```

通过这样的设置，现在我们就有了默认元素了，这种方式类似于apache的直接根目录（directorIndex）或

者是nginx的index.是对直接根路径匹配路由，下面我们来看现在这种方式下的路由与URL的关系：

![这里写图片描述](http://img.blog.csdn.net/20161122104830050)

我们发现与1.相比，这里多了默认的首页路由：url为：‘/’，路由的组件为App——>Dashboard

（2）从URL中解耦UI

如果我们能从URL为/inbox/messages/:id 的路由中，移除/inbox使得路由的真正页面为：/message/:id

同时保留了JSX的页面结构，[React](http://lib.csdn.net/base/react)-router允许我们使用这种缺省路径的方法。我们来看如下代码：

```
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
), document.body)12345678910111213141234567891011121314
```

注意：这里的message所在的父路由，缺省了path，这样实际上我们就将路由从/inbox/message/:id转化

成为了/message/:id，但是整体的JSX结构并没有发生变化，只是缺省了path而已。这种缺省的方式，

使得我们能够避免非常复杂的层层url的书写方式，这样使得我们整个路由的控制显得简单名了。这种方式

的访问结果如下：

![这里写图片描述](http://img.blog.csdn.net/20161122110027878)

上图中，值得注意的是我们只要通过url: /message/:id 就可以访问到组件：App——>Inbox——

> Message，大大的简化了url，但是访问结果却与inbox/message/:id完全相同。

（3）重定向路由（Redirect）

通过Redirect，我们可以重新定向路由。我们来看下面的例子：

```
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
), document.body)1234567891011121314151617181912345678910111213141516171819
```

现在，当我们访问/inbox/message/:id的时候，路由会自动跳转到新的url——>/message/:id

这样我们就实现了路由的重定向。

（4）路由的leave和enter,路由的进入和移除的过程

路由定义了进入和移除时的hook，也就是路由的移入或者移除的时候会触发一定的事件，这些hooks是非常

有用的，比如路由移入（进入访问）的时候需要做一个权限认证，或者说路由移除（移除访问）的时候需要

保存一些参数等，我们来看什么时候会触发leave hook，什么时候会触发enter hook。

举一个例子：当我们从url：/messages/5，跳转到新的url：/about的过程。

（a）首先触发/messages/:id route的leave hook

（b）再次触发/inbox route的leave hook

（c）最后触发/about的enter hook

（5）利用插件的方法来配置路由，并且同时根据leave和enter hook，在JS中实现Redirect

```
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

render(<Router routes={routes} />, document.body)123456789101112131415161718192021222324123456789101112131415161718192021222324
```

这里通过onEnter中的方法来触发重定向，从而实现Redirect.

## 参考地址

 [Reacter-router（config）基础配置项](http://blog.csdn.net/liwusen/article/details/53282245)