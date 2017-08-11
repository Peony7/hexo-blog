---
title: viewports
date: 2017-08-11
tags: viewports
---

原文: http://www.w3cplus.com/css/viewports.html

### 桌面浏览器的特性

#### screen.width/height(屏幕尺寸)

- 含义：用户的屏幕的完整大小。
- 度量：设备的pixels。
- 兼容性问题：IE8里，不管使用IE7模式还是IE8模式，都以CSS的pixels来度量

#### window.innerWidth/Height(浏览器尺寸)

- 含义：包含滚动条尺寸的浏览器完整尺寸
- 度量：CSS的pixels
- 兼容性问题：IE不支持，Opera用设备pixels来度量

#### window.pageX/YOffset(滚动位移)

- 含义：页面的移位
- 度量：CSS的pixels
- 兼容性问题：pageXOffset 和 pageYOffset 在 IE 8 及之前版本的IE不支持, 使用”document.body.scrollLeft” and “document.body.scrollTop” 来取代

#### document. documentElement. clientWidth/Height(viewport的尺寸)

- 含义：viewport的尺寸
- 度量：CSS的pixels
- 兼容性问题：无

为`<html>`元素赋值25%。但document. documentElement. clientWidth/Height的值不变。它虽然貌似从`<html>`元素取值，但实际描述的确是viewport的尺寸。

#### document. documentElement. offsetWidth/Height(`<html>`的尺寸)

- 含义：`<html>`的尺寸
- 度量：CSS的pixels
- 兼容性问题：IE用这个值标示viewport的尺寸而非`<html>`

如果你为`<html>`元素赋值了宽度，offsetWidth会真实的反应出来。



#### pageX/Y, clientX/Y, screenX/Y(事件坐标)

- 含义：见下文
- 度量：见下文
- 兼容性问题：IE不支持pageX/Y,IE使用CSSpixels来度量screanX/Y
- 详细描述:
  - pageX/Y：从`<html>`原点到事件触发点的CSS的 pixels
  - clientX/Y：从viewport原点（浏览器窗口）到事件触发点的CSS的 pixels
  - screenX/Y：从用户显示器窗口原点到事件触发点的设备 的 pixels。


#### mediaqueries(Media查询)

- 含义：见下文
- 度量：见下文
- 兼容性问题：IE不支持.
- 详情描述:
  - device-width/height使用screen.width/height来做为的判定值。该值以设备的pixels来度量
  - width/height使用documentElement.clientWidth/Height即viewport的值。该值以CSS的pixels来度量

在桌面浏览器中使用width而忘记device-width

### 移动设备浏览器的问题

####  两种viewport

因此viewport太窄，不能很好为你的基本CSS布局服务了。最显然的解决方式是让viewport更宽。因此这个需求分为了2个方面：虚拟的visualviewport和布局的layoutviewport。

#### document. documentElement. clientWidth/Height(度量layout viewviewport)

的尺寸

- 含义：layoutviewport尺寸
- 度量：CSS的pixels
- 完整支持：Opera, iPhone, Android, Symbian, Bolt, MicroB, Skyfire, Obigo
- 问题：在Iris上它标示visualvieport
  - 三星的Webkit核心浏览器，仅当在页面上写入`<meta viewport>`标签，才正确表示。否则就代表着
  - FireFox以设备的pixels来度量
  - IE返回1024 x 768 px，而准确的尺寸保存在document.body.clientWidth/Height
  - NetFront仅当100%缩放时候才正确
  - 塞班的Webkit1(在S60v3设备)不支持这些属性
- 不支持：黑莓

很幸运浏览器由于浏览器大战而遗留给我们2个特性对来度量这两种viewport。

旋转只关系到高度，而不是宽度。

#### window.innerWidth/Height(度量visual viewport)

- 含义：visualviewport尺寸
- 度量：CSS的pixels
- 完整支持：iPhone, Symbian, BlackBerry
- 问题：
  - FireFox和Opera以设备的pixels返回该数值
  - Android, Bolt, MicroB, 和 NetFront 以CSS的pixels返回该数值，且为layoutviewport的值
- 不支持：
  - IE，它使用document. documentElement. offsetWidh/Height来表示
  - 三星的Webkit核心浏览器，仅当在页面上写入`<meta viewport>`标签，才正确表示。否则就代表着`<html>`的尺寸
- 混乱：Iris, Skyfire, Obigo返回的值不知所云

我们使用window.innerWidth/Height来度量visualviewport。显然，随着用户缩放浏览器，这值会改变，更多、更少的CSS pixels放进了屏幕。
很不幸这是一个待完善的部分，许多浏览器依然没有支持对visualviewport的度量。到现在为止，没有浏览器将该度量存储在其他地方，我猜测window.innerWidth/Height会成为标准，albeit是最强力的支持者。

#### screen.width and screen.height(屏幕尺寸)

- 含义：屏幕尺寸
- 度量：设备的pixels
- 完整支持：Opera Mini, Android, Symbian, Iris, Firefox, MicroB, IE, BlackBerry
- 问题：
  - Opera在Windows Mobile下只给出横向尺寸(landscape size)。在S60上工作正确。
  - 三星的Webkit核心浏览器，仅当在页面上写入`<meta viewport>`标签，才正确表示。否则就代表着`<html>`的尺寸
  - iPhone和Obigo仅给出竖直尺寸(portrait sizes)
  - Android, Bolt, MicroB, 和 NetFront 以CSS的pixels返回该数值，且为layoutviewport的值
- 不支持：
  - IE，它使用document. documentElement. offsetWidh/Height来表示 - 三星的Webkit核心浏览器，仅当在页面上写入`<meta viewport>`标签，才正确表示。否则就代表着`<html>`的尺寸
- 混乱：Iris, Skyfire, Obigo返回的值不知所云

和pc浏览器一样，screen.width/height标示了设备屏幕的尺寸，以设备的pixels度量。和pc浏览器一样，作为web开发人员你永远不需要这些信息。你不关心屏幕的物理宽度，而关心当前有多少CSS的pixels能供你使用。

#### window.pageX/YOffset(滚动位移)

- 含义：见描述
- 度量：CSS的pixels
- 完整支持：iPhone, Android, Symbian, Iris, MicroB, Skyfire, Obigo
- 问题：
  - Opera, Bolt, Firefox, and NetFront 总是返回 0.
  - 三星的Webkit核心浏览器，仅当在页面上写入标签，才正确表示。
- 不支持： IE，它使用document. scrollLeft/Top来表示

你同意需要知道当前visualviewport相对于layoutviewport的距离。这就是滚动位移，如同在桌面浏览器一样，使用window.pageX/YOffset存储。

#### document. documentElement. offsetWidth / Height

- 含义：html元素的整体尺寸
- 度量：CSS的pixels
- 完整支持：Opera, iPhone, Android, Symbian, Samsung, Iris, Bolt, Firefox, MicroB, Skyfire, BlackBerry, Obigo
- 问题：
  - NetFront只在100%缩放时返回正确的值.
  - IE，使用这个特性对来表示visualviewport的尺寸。它使用document. body. clientWidth/Height来表示

和在桌面系统一样,document.documentElement.offsetWidth/Height给出了

元素以CSS的pixels度量的尺寸。

#### Mediaqueries(Media查询)

- 含义：以CSS的pixels度量`<html>`元素或以设备 的pixels度量设备
- 完整支持：Opera, iPhone, Android, Symbian, Samsung, Iris, Bolt, Firefox, MicroB.
- 不支持：Skyfire, IE, BlackBerry, NetFront, Obigo
- 备注： 我只测试了浏览器是否从正确的特性对里提取这些值。而特性对里的值是否正确并不在这里进行详细测试。

media查询如同桌面系统一样。width/height使用以CSS的pixels度量的layoutviewport，device-width/height使用以设备的pixels度量的设备屏幕（device screen）。

换句话说，width/height 反映document. documentElement. clientWidth/Height的值, device-width/height 反映screen.width/height. (所有浏览器遵循同样原理，即使取值是错误的)。

media查询在标识网站处于桌面浏览器、pad浏览器或手机浏览器方面很重要，而在区别不同pad和手机设备方面并不有用。

#### Eventcoordinates(事件坐标)
- 含义：见下文
- 度量：见下文
- 完整支持：Symbian, Iris
- 问题：
  - Opera 只有pageX/Y，但滚动页面过远时这个值会出错。
  - 在iPhone, Firefox, 和 BlackBerry 上clientX/Y 和pageX/Y相等
  - 在 Android 和 MicroB screenX/Y和clientX/Y相等，也就是它们以CSS的pixels度量屏幕尺寸
  - 在FireFox里screenX/Y值不正确
  - IE, BlackBerry, 和 Obigo 不支持 pageX/Y.
  - NetFront 所以三个值都是screenX/Y.
  - Obigo clientX/Y是screenX/Y.
  - Samsung WebKit 总是返回pageX/Y.
- 未测试：Opera Mini,Bolt,Skyfire

事件坐标在桌面浏览器上多多少少是支持的。不幸的是，移动设备上在所测试的12个主流浏览器中只有Symbian WebKit 和 Iris完全正确的支持这3个坐标特性。其余浏览器多多少少都存在问题。

pageX/Y,该特性依然是基于页面的CSSpixels度量的值，如图在桌面浏览器一样，它是三个特性里面最有用的。

clientX/Y是基于visualviewport的，以CSSpixels度量的值. 这样做比较靠谱，虽然我不是很确信这样计算的好处。

screenX/Y基于设备屏幕以设备的pixels度量的值。显然，它使用和clientX/Y同样的参考，而设备的pixels没什么用。所以我们不需要在意screenX/Y,同在桌面浏览器一样，每个bit都是没用的。

#### Metaviewport(meta viewport)

- 含义：设置layoutviewport的宽度
- 度量：CSS的pixels
- 完整支持：Opera Mobile, iPhone, Android, Iris, IE, BlackBerry, Obigo
- 不支持：Opera Mini, Symbian, Bolt, Firefox, MicroB, NetFront
- 问题：
  - Skyfire 不能处理我的测试页面。
  - 在三星的wibkit浏览器下，出现会改变一些特性对的值。
  - Opera Mobile, iPhone, Samsung, and BlackBerry 不允许用户在设置viewport后再进行缩小操作（do not allow the user to zoom out.）












