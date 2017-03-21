[TOC]

### 🎃JavaScript垃圾回收与内存泄漏

- 计数法：如果一个对象A，没有被别的对象引用（显式或隐式），那么A的引用计数就为0，会被回收器回收。**不能解决循环引用** 。
- 标记-清除法：从根节点开始遍历所有对象的引用情况。那些不能被获得的对象（不可达），会被垃圾回收。
- 内存泄漏：
  - 意外的全局变量。
  - 老版本的IE无法处理循环引用，所以那些DOM上的监听事件会造成内存泄漏。
  - 闭包在老版本的IE上，容易出现循环引用，造成内存泄漏。现在无须担心。



### 🎃函数式编程

- 只是用表达式，不使用语句。表达式有返回值，语句没有返回值。
- 函数式编程的开发动机：处理运算，不考虑系统的读写（I/O）。语句属于对系统的读写操作。
- 没有副作用：函数要保持独立，所有功能就是返回一个新的值，不得修改外部变量的值。
- 不修改状态，使用参数保存状态。
- 引用透明：参数相同则运行结果相同。
- 优势：
  - 代码简洁，易懂
  - 便于管理
  - 易于“并发编程”，由于不修改变量，所以不存在死锁。可以放心的并发处理。






### 🎃设计模式

- React/Redux合在一起：**中介者模式** 。**适配器模式** 。**MVVM**。（M = state，VM = redux，V = react）

  > 如果一个系统的各个组件之间看起来有很多的直接联系，这时候需要一个**中心控制点**，对组件之间的通信进行**统一**管理。

  - 中心控制点就是store。
  - 组件通过connect与store进行联系。
  - `mapStateToProps()`有一点适配器模式的意思。

- Redux中用到的设计模式：

  - 发布/订阅模式：store有个`subscribe`方法，state发生变化是，会执行所有的监听器。
  - 装饰者模式：middleware

- React中用到的设计模式：

  - HOC：装饰者？代理者？Container-Component？
  - 受控组件：React的input组件。（value值是通过onChange事件来改的）
  - 非控制组件：通过`ref`获取value，需要一个`defaultValue`
  - 混合控制组件。

- 代理者模式：为对象提供一个代理者，来控制对这个对象的访问。隐藏这个对象的内部细节。

- 门面模式：定义一个高层接口，为子系统的一组接口提供一个一致的界面。

  - 门面模式与代理这模式的区别：
    - 外观模式是代理模式的宏观版本。
    - 代理模式在对象级别代理真实对象，解耦client和真实对象。
    - 而门面模式是在系统级别代理子系统，解耦client和子系统，这里的子系统可能还会包括若干子系统。




### 🎃浏览器输入url之后发生了什么

- 输入：优先考虑搜索历史和书签等内容给出建议，Chrome浏览器甚至会提前建立TCP链接

- 按下回车：开始解析url，分析输入的是url还是搜索关键字。

- 如果是url，判断使用了哪种协议，检查HSTS列表，判断该请求是否只能用HTTPS协议。

- 进行DNS查询，先查浏览器缓存，再查host文件，最后查DNS服务器。

- 有了IP地址之后，通过Socket API发送数据，选择采用TCP或UDP协议。先到传输层，封装成TCP Segment，再到网络层，封装成TCP packet（加入ip地址），最后到链路层，加入MAC地址

- 被封装的TCP请求通过wifi或以太网或蜂窝数据网络发出。

- 服务器“处理”请求，服务器接收到获取请求，然后处理并返回一个响应。

- 服务器发回一个HTML响应

- 浏览器开始渲染HTML，并请求外部资源。

- 渲染过程：解析html构建dom树 -> 解析CSS构建CSSOM树 -> 构建render树（只有可见元素） -> 布局render树 -> 绘制render树

- HTML/**SVG**/XHTML，解析这三种文件会产生一个DOM树

- js的下载和执行会阻塞Dom树的构建，脚本标记为**async**或**defer**之后可以滞后执行。

- 样式表必须**在脚本之前**加载和解析，因为脚本可能会在解析的过程中请求样式信息。


  > 1. 处理 HTML 标记并构建 DOM 树。
  > 2. 处理 CSS 标记并构建 CSSOM 树。
  > 3. 将 DOM 与 CSSOM 合并成一个渲染树。
  > 4. 根据渲染树来布局，以计算每个节点的几何信息。
  > 5. 将各个节点绘制到屏幕上。



### 🎃HTML5

- HTML标准的最新版本，加入了新的元素、属性和行为。
- 应用缓存：在html元素上添加manifest特性。生成一个manifest file，当应用需要离线时，浏览器读取这一文件，下载相应的文件，并将其缓存到本地。
- DOM存储：sessionStorage、localStorage
- `<audio>`和`<video>`标签支持新的多媒体内容的操作。
- Web Worker：在后台线程运行脚本。线程可以执行任务而不干扰用户界面。生成操作系统级别的线程，且无法访问非线程安全的组件和DOM。
- 新标签：`<section>`,`<figure>`,`<output>`




### 🎃HTML语义化

- 使页面内容结构化，便于浏览器和搜索引擎的解析。
- 便于阅读维护和理解。
- 盲人使用读屏器可以更好地阅读。



### 🎃响应式设计

- 媒体查询
- 在网页头部加上viewport标签
- 不使用绝对宽度，使用栅格布局或rem（移动端）
- 字体大小使用em或rem
- 自适应与响应式：
  - 自适应：自动适应不同尺寸的屏幕，布局一般不变。
  - 响应式：根据不同尺寸的屏幕，调整布局






### 🎃CSS相关问题

- 清除浮动
  - 添加空的div，css设为`clear: both`
  - 在父元素上使用`overflow: hidden`或`overflow: auto`，可以把父元素撑开。
  - 使用`:after`伪元素，给父元素加个`:after`，然后这个`:after`里面设置`clear: both`
  - 在IE下，为了触发hasLayout，要加上`zoom: 1`。
- box-sizing: `content-box` & `border-box`。前者为默认值，后者的`width`和`height`是包含border和padding的。
- absolute：相对上一个设置了position属性的元素进行定位（absolute，relative，fixed）
- css3新特性
  - word-wrap，设置`word-wrap: break-word`的话，在单词换行的情况下，可保持单词的完整性。
  - font-face：可加载服务器端的字体。使网页可以显示用户本地不存在的字体。至少需要`.woff`和`.eot`两种格式的字体。
  - transition, transform, animation





### 🎃Javascript 单线程、异步请求、异步编程

-   异步机制：js的**执行线程**发送异步请求，这时浏览器会开一条新的HTTP请求线程（不进入主线程、进入**任务队列**）来执行请求。js线程继续执行线程队列中剩下的其他任务。然后在未来的某一时刻事件触发线程监视到之前之前的HTTP请求已完成，就会把完成事件插入到js执行队列的尾部等待js处理。
-   异步编程的四种办法：
  - 回调函数：简单，容易理解和部署。但不利于代码的维护，各个部分高度耦合。
  - 事件监听：有利于实现模块化。但整个程序都要变成事件驱动型，运行流程会变得很不清晰。
  - 发布/订阅（观察者模式）：f1向”信号中心“发布信号，f2订阅”信号中心“的该信号。
  - Promise对象：回调函数变成了链式写法，且有一整套的配套方案，功能强大（then,fail,all,race）
-   setTimeout()将事件插入"任务队列"，必须等到当前代码（执行栈）执行完，主线程才会去执行它指定的回调函数。要是当前代码耗时很长，有可能要等很久，所以并没有办法保证，回调函数一定会在setTimeout()指定的时间执行。




### 🎃跨域问题

- 设置document.domain，使得主域名但不同子域名下的页面可以相互操作。

  - 只能通过iframe进行页面嵌套才能实现页面互操作。
  - 只能从子域设置到主域。

- 有src的标签

  - 所有具有src属性的HTML标签都是可以跨域的，包括img，script
  - 只能用于GET方法

- JSONP

  - `<script>`是可以跨域的，且可以在跨域脚本中直接回调当前脚本的函数。
  - 需要创建一个DOM对象并且添加到DOM树，且只能用于GET方法

- navigation对象

  - iframe之间是共享navigator对象的，用它来传递信息
  - IE6/7

- 跨域资源共享CORS

  - 服务器设置`Access-Control-Allow-Origin`HTTP响应头之后，浏览器将会允许跨域请求
  - 浏览器需要支持HTML5。可以支持POST，PUT等方法。

- window.postMessage

  - HTML5允许窗口之间发送消息
  - 浏览器需要支持HTML5，获取窗口句柄后才能相互通信。

  ```javascript
  // URL: http://a.com/foo
  var win = window.open('http://b.com/bar');
  win.postMessage('hello, bar.', 'http://b.com')

  // URL: http://b.com/bar
  window.addEventListener('message', function(event){
    console.log(event.data)
  })
  ```

  ​

### 🎃XMLHttpRequest新老版本的对比

- 老版本：只能传递纯文本数据，没有进度信息，同域限制

- 新版本：可通过FormData管理表单数据、传递二进制文件，有进度信息，可跨域。

- 写一个XMLHttpRequest：

  ```javascript
  if(window.XMLHttpRequest) {
    var request = new XMLHttpRequest()
  } else if (window.ActiveXObject("Microsoft.XMLHTTP")) {
    var request = new ActiveXObject("Microsoft.XMLHTTP")
  }

  request.open("GET", url, true)

  request.onreadystatechange = function() {
    if (request.readyState == 4) {
      if (request.status == 200 || request.status == 302) {
        console.log(request.responseText)
      }
    }
  }

  request.send()

  // readyState的5种状态：
  // 0 - UNSENT : open()尚未调用
  // 1 - OPENED : open()已调用
  // 2 - HEADERS_RECEIVED : send()已调用，收到response的header
  // 3 - LOADING : 正在接收response的body
  // 4 - DONE : 响应完成
  ```

  ​


### 🎃事件绑定的兼容性问题

- 事件在传播过程中的三个阶段：`捕捉阶段`，`目标阶段`，`起泡阶段`。
- 并不是所有事件事件类型都有起泡阶段，例如，表单提交事件就只能够在当前元素身上响应，它不会身上起泡，传播给上级元素。
- 冒泡型事件流的具体约定：
  - IE6.0及其以上：p —> body —> html —> document
  - Mozilla1.0及其以上：p —> body —> html —> document —> window
- 事件绑定
  - `addEventListener()` 和 `removeEventListener()`
  - addEventListener，3个参数，第一个`type`，第二个`listener`，第三个`useCapture`。`userCapture`为true表示在捕获阶段触发响应。`listener`尽量不要用匿名函数，因为FireFox会把结构相同的匿名函数看成不同的函数。
  - IE中：`attachEvent()`和`detachEvent()`。
  - `event = event || window.event`。（后者用于IE中获取事件对象）
  - IE中没有`stopPropagation()`，使用`window.event.cancelBubble = true `来取消冒泡。



### 🎃事件代理

- 父节点代理子节点的事件，通过事件冒泡机制实现。
- 当事件被抛到更上层的父节点时候，通过检查事件的目标对象（target）来判断并获取事件源。
- 事件捕获：顶层对象发出一个事件流，随着DOM树的节点向目标元素流去，过程中事件的相应监听函数不会被触发，直到捕获到目标之后，才会触发对应的监听函数。


```javascript
// 获取父节点，并为它添加一个click事件
document.getElementById("parent-list").addEventListener("click",function(e) {
  // 检查事件源e.targe是否为Li
  if(e.target && e.target.nodeName.toUpperCase == "LI") {
    // 真正的处理过程在这里
    console.log("List item ",e.target.id.replace("post-")," was clicked!");
  }
});
```



### 🎃Target与CurrentTarget

- event.target总是指向触发事件的元素，一直指向目标阶段的那个元素。
- event.currentTarget指向事件绑定的元素，会在捕获和冒泡阶段触发。
- 当处于目标阶段时，target与currentTarget是相等的。



### 🎃META标签（不仅仅是charset=“uft-8”）

- 定义html页面的 **说明** ， **关键字** ， **最后修改日期** ， 和其他的 **元数据** 。这些数据服务于浏览器（如何布局或重载页面），搜索引擎和其他网络服务。

- `name`用于指定`content`的类型

  ```html
  <meta name="keywords" content="Lxxyx,博客，文科生，前端">

  <meta name="description" content="文科生，热爱前端与编程。目前大二，这是我的前端博客">

  <!-- robots用于指定爬虫的索引方式 -->
  <meta name="robots" content="none">

  <!-- viewport用于指定移动端默认窗口大小等属性 -->
  <meta name="viewport" content="width=device-width, initial-scale=1">
  ```

- http-equiv属性

  ```html
  <meta charset="utf-8"> //HTML5设定网页字符集的方式，推荐使用UTF-8

  <!-- 指定IE和Chrome使用最新版本渲染当前页面 -->
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/> 

  <!-- 指定cache-control策略 -->
  <meta http-equiv="cache-control" content="no-cache">

  <!-- 指定缓存到期时间 -->
  <meta http-equiv="expires" content="Sunday 26 October 2016 01:00 GMT" />
  ```

  ​



### 🎃HTTPS与HTTP

- HTTP直接和TCP通信。HTTPS先与 **SSL** 通信，再由SSL和TCP通信。

- SSL采用一种叫做 **公开密钥加密** 的加密方式。

  > 发送密文的一方使用 **对方的公开密钥** 进行加密处理, 对方收到被加密的信息后, 在使用 **自己的私有密钥** 进行解密。

- HTTPS采用混合加密机制。

- HTTP默认使用80端口，HTTPS默认使用443。




### 🎃HTTP缓存

##### ETag

- 服务器返回响应式，在HTTP头部塞入ETag字段。（通常是文件内容的Hash值或某个其他指纹）
- ETag可实现高效的资源更新检查：资源未发生变化时不会传送任何数据。
- 客户端在下一次请求时将ETag发送给服务器，如果指纹仍然相同，则表示资源没有发生变化，可以跳过下载

##### Cache-Control

- 定义浏览器如何缓存以及缓存多久。

- Cache-Control是在HTTP/1.1中定义的，取代了之前的Expires等。

- no-cache：先与服务器确认ETag是否一致，如果一致则利用缓存，反之重新获取。

- no-store：不使用缓存。（个人隐私数据或银行业务数据）

- max-age：缓存时间。

- public&private：public不是必须的，private表示只有浏览器可以缓存，中间件（CDN）不能对该资源进行缓存。（CDN：内容分发网络，采用缓存机制，将缓存服务器分布到用户访问相对集中的地区或网络中，使用户就近取得资源）

- 废弃和更新缓存中的资源：

  > 对整个网站采用no-cache机制，然后，在css和js文件的url中，加入文件的fingerprint信息，这样，文件内容发生变化之后，url也会发生变化，浏览器就知道要去重新向服务器请求资源了。文件内容不发生变化时，max-age可以设置一个很长的时间，然后对一些涉及安全内容的js文件，Cache-Control设为private。
  >
  > 即：组合使用ETag，Cache-Control和唯一网址来实现一举多得：较长的过期时间、控制可以缓存的位置、随需更新。


##### Expires

在expires规定的时间内，直接读取缓存。如果与Cache-Control同时设置的话，**优先级低于** Cache-Control



##### 强缓存与协商缓存

- 强缓存：如果命中强缓存，直接读取资源，不发送http请求
- 协商缓存：当强缓存没命中时，会发送请求给服务器，通过http header内的信息验证是否命中协商缓存，如果命中，则从浏览器读取，如果没有命中，则服务器返回资源。
- 强缓存的实现方法：Expires和Cache-Control的max-age
- 协商缓存的实现方法：【Last-Modified, If-Modified-Since】和【ETag, If-None-Match】。以ETag为例，response的header里，会塞入ETag，浏览器下次请求的时候，request的header里把上一次response的ETag值塞到If-None-Match字段，然后服务器会进行比对。



##### CDN缓存

一种服务器端缓存，也叫网关缓存、反向代理缓存。浏览器先向CDN网关发起WEB请求，网关服务器后面对应着一台或多台负载均衡源服务器，会根据它们的负载请求，动态地请求转发到合适的源服务器上。



##### 基于依赖关系表的静态资源管理系统与模块化框架设计

- 将静态资源按模块进行分类，生成一张map（资源表），map中是资源名称与资源url的映射。

- 实现按需加载资源的接口，一个负责收集静态资源，一个负责加载功能组件，一个负责加载脚本。

- 资源表上新增了一个字段，取名为 `pkg`，就是资源合并生成的新资源。记录打包后的文件所包含的独立资源。

  > 在查表的时候，如果一个静态资源有pkg字段，那么就去加载pkg字段所指向的打包文件，否则加载资源本身。

```json
{
    "res" : {
        "widget/a/a.css" : "/widget/a/a_1688c82.css",
        "widget/a/a.js"  : "/widget/a/a_ac3123s.js",
        "widget/b/b.css" : "/widget/b/b_52923ed.css",
        "widget/b/b.js"  : "/widget/b/b_a5cd123.js",
        "widget/c/c.css" : "/widget/c/c_03cab13.css",
        "widget/c/c.js"  : "/widget/c/c_bf0ae3f.js",
        "jquery.js"      : "/jquery_9151577.js",
        "bootstrap.css"  : "/bootstrap_f5ba12d.css",
        "bootstrap.js"   : "/bootstrap_a0b3ef9.js"
    },
    "pkg" : {
        "p0" : {
            "url" : "/pkg/lib_cef213d.js",
            "has" : [ "jquery.js", "bootstrap.js" ]
        },
        "p1" : {
            "url" : "/pkg/lib_afec33f.css",
            "has" : [ "bootstrap.css" ]
        },
        "p2" : {
            "url" : "/pkg/widgets_22feac1.js",
            "has" : [
                "widget/a/a.js",
                "widget/b/b.js",
                "widget/c/c.js"
            ]
        },
        "p3" : {
            "url" : "/pkg/widgets_af23ce5.css",
            "has" : [
                "widget/a/a.css",
                "widget/b/b.css",
                "widget/c/c.css"
            ]
        }
    }
}
```




### 🎃性能优化

- 制定合理的缓存策略
  - 服务器在返回的头部提供ETag。
  - 组合使用ETag，Cache-Control、唯一网址。
  - 对于更新频繁的资源文件，将其独立开来。保证可以从缓存中读取的资源最大化。

- 防止CSS阻塞渲染

  - 默认情况下CSS是阻塞渲染的，可以通过媒体类型和媒体查询将CSS资源标记为不阻塞的

  - 浏览器会下载所有的CSS资源，无论阻塞还是不阻塞，不阻塞的下载优先级比较低。（所以性能优化在此处仅跟渲染引擎有关）

  - Flash of Unstyled Content (FOUC) : 内容样式短暂失效。指不阻塞CSS的情况下渲染出来的页面。

  - 媒体查询解决阻塞渲染：

    ```css
    <link href="style.css" rel="stylesheet">
    <link href="print.css" rel="stylesheet" media="print">
    <link href="other.css" rel="stylesheet" media="(min-width: 40em)">
    ```

    第一个阻塞，第二个只在打印内容时阻塞，第三个只在符合条件后才阻塞。

- `script`标签添加`async`属性（下载完就执行）或`defer`属性（渲染完再执行），将脚本标记为异步，则不会阻塞DOM构建。

- img**不会**阻塞页面的首次渲染。关键渲染路径，通常是指HTML，CSS和JavaScript

- 关键渲染路径的优化：

  - 首选异步加载JavaScript资源
  - 延迟解析对首次渲染无关紧要的JavaScript脚本
  - 将CSS置于head标签内，以便浏览器尽早发出css请求。
  - 避免css import，这回增加关键路径的往返次数：只有在解析到`@import a.css`时才会去请求a.css。
  - 内敛阻塞渲染的css，这样会减少一次css请求。

- 优化JavaScript的执行

  - 动画效果使用requestAnimationFrame，避免使用setTimeout和setInterval
  - 将长时间运行的JavaScript从主线程移到Web Worker

- HTTP/2

  - 支持header字段压缩
  - 支持为请求设置优先级
  - 使用二进制消息分帧。
  - 三个概念：数据流、消息、帧。

  > - 所有通信都在一个TCP连接上完成，此连接可以承载多个双向数据流。
  > - 每个数据流都有一个唯一的标识符和可选的优先级信息。
  > - 每条消息都是一条HTTP请求或HTTP响应，包含一个或多个帧。
  > - 帧是最小的通信单位，里面装的可能是HTTP标头，也可能是payload。
  > - 来自不同数据流的帧可以交错发送。




### 🎃图片懒加载

- img标签中，使用`data-src`存储图片的真实url，src存放一个占位用的图片。
- 当图片滚动到可是窗口区域以内时，再开始加载。
- 可视区域高度：clientHeight
- 页面卷上去的高度：scrollTop
- 图片相对于body，距离顶端的距离：offsetTop的总和
- offsetTop - clientHeight - scrollTop >=0 ? 加载 : 不加载



### 🎃按需加载

- `import()`：一种类似`require`的运行时加载。
- webpack + react-router
  - Route标签中，getComponent替换component，用于异步加载。
  - 将资源分类打包，分成不同的chunk。
  - 使用`require.ensure`，在运行时按需加载需要的资源。







### 🎃计算机网络与网络安全

##### HTTP协议

- Transfer-Encoding: chunked
  - 表明request或response的content-length是未知的，消息体由数量为定的块组成。
  - 以最后一个大小为0的块作为传输结束的标志。
  - 启用Keep-live模式后，两种判断传输完成的方法：1. 传输长度满足Content-Length（静态页面或图片）2. chunked模式（动态页面）

- 会话跟踪：session的实现依赖于Cookie，sessionID放到cookie中传给client。

  ​

##### 网络安全

- 内容安全性政策（CSP）

  - 使用白名单告诉客户端允许加载和不允许加载的内容。

    > 1. 浏览器只允许执行或渲染来自白名单的资源
    >
    >    Content-Security-Policy: script-src 'self' https://apis.google.com

  - 内敛代码和`eval()`被视为是有害的

    > 1. 使用内联函数（而不是字符串）重写您当前正在进行的任何 `setTimeout` 或 `setInterval` 调用。
    > 2. 通过内置 `JSON.parse` 解析 JSON，而不是依靠 `eval` 来解析。
    > 3. 在运行时避免使用内联模板：为在运行时加快模板生成的速度， 许多模板库大量使用 `new Function()`。

  - 可用的一些指令及作用：

    | 指令                | 作用                                       | 例子                                       |
    | :---------------- | :--------------------------------------- | :--------------------------------------- |
    | child-src         | 控制嵌入的帧内容和工作线程的来源                         | child-src https://youtube.com            |
    | script-src        | 控制脚本来源                                   | script-src 'self' https://apis.google.com |
    | connect-src       | 限制可连接的来源                                 | 连接类型：XHR、WebSockets                      |
    | font-src          | 限制网页字体来源                                 | font-src https://themes.google           |
    | frame-ancestors   | 指定可嵌入当前页面的来源                             | 适用于`<frame>`、`<iframe>`、`embed`、`applet` |
    | img-src/media-src | 定义可从中加载图像/视频和音频的来源                       |                                          |
    | object-src        | 控制Flash和其他插件                             |                                          |
    | plugin-src        | 限制页面可以调用的插件种类                            |                                          |
    | default-src       | 设置默认行为，适用于以-src结尾的任意指令。                  |                                          |
    | sandbox           | 将此页面视为使用 `sandbox` 属性在 `<iframe>` 的内部加载的。这可能会对该页面产生广泛的影响：强制该页面进入一个唯一的来源，同时阻止表单提交等其他操作。 |                                          |

- 如何防范跨站攻击（CSRF）

  - 关键操作只接受POST请求
  - 验证码
  - 检测Referer
  - Token：足够随机，一次性，保密性。

- 如何防范跨站脚本攻击（XSS）：

  - 过滤用户输入。
  - 使用外部js文件替代内敛js代码的方法。不仅可以防范xss，还有利于静态资源缓存。



##### TCP协议

- 建立连接时：3次握手

  1. Client发送连接请求报文`(SYN=1, seq=client_isn)`

  2. Server接收连接请求，回复ACK报文，然后为连接分配资源。

     `(SYN=1, seq=server_isn) （ack=client_isn+1）`

  3. Client接收ACK报文，也向Server发送ACK报文，然后为连接分配资源。

     `(SYN=0, seq=client_isn+1) (ack=server_isn+1)`

- 断开连接时：4次握手（下面假设是client发起连接中断）

  1. Client发起中断请求，发送FIN报文。
  2. Server收到FIN报文后，回复ACK报文。（可能数据还没传完，所以先ACK。Client进入FIN_WAIT状态）
  3. Server传完数据后，回复FIN报文。
  4. Client收到Server的FIN报文后，向Server发送ACK报文，然后进入TIME_WAIT状态。经过2MSL时间后，Client进入CLOSED状态。（MSL：最大报文生存时间）



##### Socket编程

- Socket是一种**门面模式**，它把复杂的TCP/IP协议隐藏在Socket接口后面，用来和应用层通信。
- 是网络间不同计算机上的**进程通信**的一种方法。








### 🍪React性能优化

- shouldComponentUpdate

- 使用Production Build

  ```javascript
  new webpack.DefinePlugin({
    'process.env': {
      NODE_ENV: JSON.stringify('production')
    }
  }),
  new webpack.optimize.UglifyJsPlugin()
  ```

- React.PureComponent：会对state和props进行一个`shallow comparison`来判断是否需要update，但是如果数据结构比较复杂的话，shallow comparison是没作用的。

- 使用Immutable Data解决上述浅拷贝的问题。






### 🍪React与Vue的对比

- 相同点

  - 都是用的Virtual Dom
  - 都提供了响应式和组件化的视图组件
  - 都有配套的路由和负责处理全局状态管理的库。

- Vue

  - global event bus：$emit和$on事件，和angular 1里面的通信机制很像
  - vuex：vue的全局状态管理。以mutations替代reducer，无需switch。且Vue有自动重新渲染的特性，所以vuex里面的数据变化后，没有subscribe的过程。
  - vue-router：vue的路由管理
  - 似乎只能运行在IE9以上的浏览器？

- Vue的响应式系统：

  > Vue实例中，data的所有属性都会使用`Object.defineProperty`转为getter和setter。然后每个组件的实例，都有一个watcher，一旦data中的某个setter被触发，watcher通知component进行re-render。

  所以，如果要往某个实例的data中，动态添加**根级响应属性**或**丰富**某个已有属性，需要使用`Vue.set(vm.somOjbect, 'b', 2）`以及`_.extend()`等方法。

- Vue异步执行DOM更新。与react在setState的时候类似。



### 🍪Vue和React的服务端渲染

- 为什么要SSR：
  - 利于SEO，爬虫对于异步加载的内容是无能为力的。(Google例外)
  - 降低网络延迟，通过减少页面请求数量，保证用户在低网速下也能看到基本的内容。
  - 如果只是来改善一个少数的营销页面，用 **预渲染** 替换。
- Vue支持流式渲染：Vue.renderTostream()
- React服务端渲染过程：服务端渲染一遍，客户端也渲染一遍（实际上不会渲染两边，只是在客户端对服务端的component进行实例化），两边是 **同构** 的，服务端第一次渲染完成后，后面客户端掌握对组件的控制权。
  1. Express.js搭建服务端框架
  2. 使用webpack构建供前端使用的js文件
  3. 使用babel-register解决服务端的jsx语法和es6语法。



### 🍪React-Redux

##### Provider
- 在原应用组件上包裹一层，使原来整个应用成为Provider的子组件
- 接受Redux的store作为props，**通过context** 传递给子组件。（Context相当于一个独立的空间，父组件通过getChildContext()向该空间写值。子组件通过this.context.xxx读取）

##### Connect
- 返回一个wrapContent的function，内部对store上的state、action、原组件上的props进行**merge**，传递给原组件。
- **监听** store tree的变化。通过store.subscribe(listener)注册一个监听器。在Connect组件didMount时注册，willUnmount时注销。
- Connect组件中维护了一个**this.state.storeState**，store发生变化时，Connect更新自己的state，内部的子组件得到重新render。
- mapStateToPros, mapDispatchToProps的返回值都是需要merge进props的state和action （出现同名，后者优先）



### 🍪Redux

##### store的概念

通过createStore(reducer)创建。（闭包思想）
```javascript
export default function createStore(reducer, initialState) {
  // 这些都是闭包变量
  var currentReducer = reducer
  var currentState = initialState
  var listeners = []
  var isDispatching = false;

  // 返回当前的state
  function getState() {
    return currentState
  }

  // 注册listener，同时返回一个取消事件注册的方法
  function subscribe(listener) {
    listeners.push(listener)
    var isSubscribed = true

    return function unsubscribe() {
      if (!isSubscribed) {
	     return
      }
      isSubscribed = false
      var index = listeners.indexOf(listener)
      listeners.splice(index, 1)
    }
  }

  ...

  return {
    dispatch,
    subscribe, // store更新后的回调函数
    getState,
    replaceReducer
  }
}
```

subscribe的方法的返回值是一个**unsubscribe**方法。redux采用 **观察者模式** ，当store tree更新后，**依次执行** subscribe里面的所有listener。

##### bindActionCreator

对dispatch进行一层封装，函数式编程思想，将多参数模式，转化为单参数模式。

```javascript
function bindActionCreator(actionCreator, dispatch) {
  return (...args) => dispatch(actionCreator(...args))
}

export default function bindActionCreators(actionCreators, dispatch) {
  if (typeof actionCreators === 'function') {
    return bindActionCreator(actionCreators, dispatch)
  }
  return mapValues(actionCreators, actionCreator =>
    bindAQctionCreator(actionCreator, dispatch)
  )
}
```

##### Middleware
像 redux-thunk 或 redux-promise 这样支持异步的 middleware 都包装了 store 的 dispatch() 方法，以此来让你 dispatch 一些除了 action 以外的其他内容，例如：函数或者 Promise。你所使用的任何 middleware 都可以以自己的方式解析你 dispatch 的任何内容，并继续传递 actions 给下一个 middleware。

当 middleware 链中的最后一个 middleware 开始 dispatch action 时，这个 action 必须是一个普通对象。这是 同步式的 Redux 数据流 开始的地方（译注：这里应该是指，你可以使用任意多异步的 middleware 去做你想做的事情，但是需要使用普通对象作为最后一个被 dispatch 的 action ，来将处理流程带回同步方式）。

##### Redux设计思想

沿用Flux单向数据流的思想。**Store** 负责接收 **Views** 传来的 **Action** , **Reducer** 根据 **Action** 的 **Type** 和 **Payload** 对 **Store** 里的state进行修改。最后，Store通知Views数据更新了，Views取到最新的state之后，进行重新render。

Redux在Flux的基础上，加入了 **Reducer** 和 **Middleware** 的概念。



### 🍪ImmutableJS

解决JavaScript引用赋值带来的问题，deepCopy会浪费CPU和内存，ImmutableJS采用 **Structural Sharing** 的概念，即如果对象树种一个节点发生变化，只修改这个节点和受它影响的父节点，其他节点进行共享。

- 结构共享可以节省内存。
- 提供了数据的Undo/Redo。
- 函数式编程。





### 🍪Webpack

- 与Gulp对比：内存处理方面，webpack共享一个流，gulp每一个任务用一个流。

- Webpack做CSS模块化的目的：避免CSS泄露到全局环境中。（style-loader和css-loader只是提供了解读和加载`<style>`标签到html的头部中。）

  - `css?modules&localIdentName=[name]__[local]-[hash:base64:5]`。对CSS模块化处理，`localIdentName`生成全局唯一的css样式名称。使得每个被引入js模块的`styles`都带上了全局唯一的prefix和suffix，从而实现了 **模块化**。

  - ```scss
    /* config.scss */
    $primary-color: #f40;

    :export {
      primaryColor: $primary-color;
    }

    /* app.js */
    import style from 'config.scss';

    // 会输出 #F40
    console.log(style.primaryColor);

    // 实现了css，js的变量共享。
    ```

- 配置文件的主要参数：

  - entry：js入口源文件
  - output：生成文件
  - module：字符串的处理，文件的编译优化
  - resolve：解决文件路径的指向
  - plugins：插件

- 常用loaders：

  - 处理样式：less-loader, sass-loader
  - 处理图片：url-loader, file-loader
  - 处理js：babel-loader, babel-preset-es2015

- 常用Plugins：

  - 代码热替换：HotModuleReplacementPlugin
  - 将css生成文件，而不是内敛：ExtractTextPlugin
  - 代码丑化：UglifyJsPlugin
  - 多个html共用一个js文件(chunk)：CommonsChunkPlugin

- 使用优化

  - 区分开发环境和生产环境：通过node的环境变量设置
  - 善用alias：对于一些经常要被引用的库，通过resolve参数直接配置路径的位置
  - `devtool: "eval"`可以提高build的速度。`only maps to compiled source code per module`

- webpack-dev-server的作用：

  监控js文件的变化，如果js文件发生变化，webpack会重新打包bundle.js，然后webpack-dev-server将更新后的bundle.js发给浏览器。加上—hot之后，可以热替换。

- 热加载原理：

  > 在构建的时候，webpack添加了一个小型HRM运行环境给bundle文件。这个运行环境跑在了你的app中。当构建结束Webpack并没有推出而是保持激活状态，监听资源文件的改动。如果Webpeck检测到资源文件的改动他将重新build这个改动的模块。
  >
  > 接下来，将根据预先的配置要么让Webpack向HRM发起通知，要么让HRM自动检测webpack的变化。任何一种方式都是将改动后的模块高速HRM运行环境来调起热更新：
  >
  > 首先HRM将检查是否更新的模块能自我接纳，如果不能，他将检查那些`require`过该更新模块的模块如果这些也不能接受，那就将他冒泡到其他层级，继续查找，`require`了这些`require`了变动模块的模块们直到这个更新被接受，如果到了入口点还没有，就说明热更新失败。
  >
  > ​
  >
  > 文件修改会触发 webpack 重新构建，服务器通过向浏览器发送更新消息，浏览器通过 jsonp 拉取更新的模块文件，jsonp 回调触发模块热替换逻辑。

- Webpack中真正对jsx代码进行编译的是`babel-loader`，webpack的存在使得这些js文件都模块化。




### 6️⃣Class

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

- 类的所有方法都定义在类的prototype上

  ```javascript
  Point.toString === Point.prototype.toString

  Point === Point.prototype.constructor
  // prototype对象的constructor属性，直接指向类本身
  ```

- 类的属性名，可以采用表达式

  ```javascript
  let methodName = "getArea";
  class Square{
    constructor(length) {
      // ...
    }

    [methodName]() {
      // ...
    }
  }
  ```

- 可以通过类的实例的`__proto__`属性，为Class添加方法

  ```javascript
  var p1 = new Point(2,3);
  var p2 = new Point(3,2);

  p1.__proto__.printName = function () { return 'Oops' };

  p1.printName() // "Oops"
  p2.printName() // "Oops"

  var p3 = new Point(4,2);
  p3.printName() // "Oops"
  ```

- 使用Symbol可以实现类的**私有方法**

  ```javascript
  const bar = Symbol('bar');
  const snaf = Symbol('snaf');

  export default class myClass{

    // 公有方法
    foo(baz) {
      this[bar](baz);
    }

    // 私有方法
    [bar](baz) {
      return this[snaf] = baz;
    }

    // ...
  };

  // export暴露的只有myClass，Symbol是取不到的。
  ```

- 类中的this问题：

  ```javascript
  class Logger {
    printName(name = 'there') {
      this.print(`Hello ${name}`);
    }

    print(text) {
      console.log(text);
    }
  }

  const logger = new Logger();
  const { printName } = logger;
  printName(); // 会报错，因为单独使用时，this指向运行时所在的环境。

  //解决办法：
  // 1. 在constructor里面bind
  class Logger {
    constructor() {
      this.printName = this.printName.bind(this);
    }

    // ...
  }

  // 2. 箭头函数
  class Logger {
    constructor() {
      this.printName = (name = 'there') => {
        this.print(`Hello ${name}`)
      }
    }
  }

  // 3. Proxy
  // 申明一个修改原Class的get行为的Proxy，在这个Proxy种，对target进行this的绑定。
  ```

- Class的继承：`super`用来调用父类的方法。子类必须在constructor内部调用`super()`。因为子类没有this对象，而是继承父类的this对象。如果不调用，子类得不到this对象。

- Class的static方法，不会被实例继承，只能通过调用类来使用。

  ```javascript
  class Foo {
    static classMethod() {
      return 'hello';
    }
  }

  Foo.classMethod() // 'hello'

  var foo = new Foo();
  foo.classMethod()
  // TypeError: foo.classMethod is not a function
  ```

- ES6中，Class没有静态属性这种说法。





### 6️⃣Module

- CommonJS：运行时加载。

  ```javascript
  // CommonJS模块
  let { stat, exists, readFile } = require('fs');

  // 等同于
  let _fs = require('fs');
  let stat = _fs.stat;
  let exists = _fs.exists;
  let readfile = _fs.readfile;

  // 会加载fs的所有方法。无法做静态优化。
  ```

- `import`：

  - **编译时加载**。在编译阶段执行import语句。
  - 按需加载。只import大括号内需要的东西。
  - 具有**提升效果**。
  - 是**Singleton**模式。对同一个模块多次import，只会执行一次。
  - 整体加载：`import * as circle from './circle'` 

- `export`：输出一个function或变量时，要加`{}`

  ```javascript
  export function f() {};
  // or
  function f() {}
  export {f}

  //如果直接export f 会报错。
  ```

  - 本质上，`export default`就是输出一个叫做`default`的变量或方法，然后系统允许你为它取任意名字。
  - 模块的继承：如果要继承`circle模块`，通过`export * from 'circle'`，再export自己的东西。

- ES6的模块加载与CommonJS的区别：

  - CommonJS输出的是值的**拷贝**，模块内部的变化不会影响这个值。且CommonJS会对输出的值做**缓存**。

  - ES6输出的是值的**引用**，相当于UNIX的**符号链接**。不做缓存，是动态引用。

  - Node加载ES6模块的路径问题：

    ```javascript
    import './foo';
    // 依次寻找
    //   ./foo.js
    //   ./foo/package.json
    //   ./foo/index.js

    import 'baz';
    // 依次寻找
    //   ./node_modules/baz.js
    //   ./node_modules/baz/package.json
    //   ./node_modules/baz/index.js
    // 寻找上一级目录
    //   ../node_modules/baz.js
    //   ../node_modules/baz/package.json
    //   ../node_modules/baz/index.js
    // 再上一级目录
    ```

- CommonJS模块加载原理：

  - CommonJS中，一个模块就是一个脚本文件。

  - `require`命令第一次加载该脚本，会在内存中生成一个对象：

    ```json
    {
      id: '...',
      exports: { ... },   // 模块输出的各个接口
      loaded: true,       // 脚本是否执行完毕
      ...
    }
    ```

  - 后面无论加载多少次，都是从系统缓存里读取。

- 采用`require`命令加载 ES6 模块时，ES6 模块的所有输出接口，会成为输入对象的属性。

  ```javascript
  // es.js
  let foo = {bar:'my-default'};
  export default foo;
  foo = null;

  // cjs.js
  const es_namespace = require('./es');
  console.log(es_namespace.default);
  // {bar:'my-default'}
  ```

- AMD依赖前置，CMD依赖延迟。前者用户体验好，后者性能好。

### 6️⃣Generator

- 状态机的概念，内部封装多个状态。
- 执行Generator函数会返回一个遍历器对象，遍历器可以依次遍历Generator函数内部的各个状态。（指向内部状态的指针对象）
- Generator可以没有yield语句，这时就变成了一个单纯的暂缓执行函数。
- Generator作为遍历器生成函数，可以直接复制给`[Symbol.iterator]`。
- yield语句后面的表达式，只有当调用`next()`方法时才会执行，是一种 **惰性求值** 。
- `g.return()`可以终结Generator的遍历。如果有`try...finally...`代码块的存在，会等到`finally`部分的代码执行完后再终止。


##### 使用Generator实现协程

- 异步任务的封装

  ```javascript
  var fetch = require('node-fetch');

  function* gen(){
    var url = 'https://api.github.com/users/github';
    var result = yield fetch(url);
    console.log(result.bio);
  }

  // 执行：

  var g = gen();
  var result = g.next();

  result.value.then(function(data){
    return data.json();
  }).then(function(data){
    g.next(data);
  });
  ```

  上面代码中，首先执行 Generator 函数，**获取遍历器对象**，然后使用`next`方法（第二行），执行异步任务的**第一阶段**。由于`Fetch`模块返回的是一个**Promise对象**，因此要用`then`方法调用下一个`next`方法。



### 6️⃣Thunk函数

- 一种“传名调用”的实现策略。

  - 传名调用：参数在被使用的时候才会计算。
  - 传值调用：参数传入的时候，就会被计算。

  ```javascript
  // 正常版本的readFile（多参数版本）
  fs.readFile(fileName, callback);

  // Thunk版本的readFile（单参数版本）
  var Thunk = function (fileName) {
    return function (callback) {
      return fs.readFile(fileName, callback);
    };
  };

  var readFileThunk = Thunk(fileName);
  readFileThunk(callback);
  ```

  `fs`模块的`readFile`方法是一个多参数函数，两个参数分别为文件名和回调函数。经过转换器处理，它变成了一个**单参数函数**，只接受回调函数作为参数。这个单参数版本，就叫做**Thunk函数**。



### 6️⃣async函数

- 用async替代*，用await替代yield，其他和Generator一样

- 是Generator的语法糖，不用手动执行next()，和普通函数一样执行。

- 返回值是一个promise。

  ```javascript
  async function f() {
    return 'hello world';
  }

  f().then(v => console.log(v))
  // "hello world"
  ```


  // 例子2：

```javascript
async function getTitle(url) {
  let response = await fetch(url);
  let html = await response.text();
  return html.match(/<title>([\s\S]+)<\/title>/i)[1];
}

getTitle('https://tc39.github.io/ecma262/').then(console.log)

// "ECMAScript 2017 Language Specification"
```

- await命令后面是一个Promise对象。如果不是，会被转成一个立即resolve的Promise对象。

- async函数的实现原理：Generator函数和自动执行器。

  ```javascript
  function spawn(genF) {
  return new Promise(function(resolve, reject) {
    var gen = genF();
    function step(nextF) {
      try {
        var next = nextF();
      } catch(e) {
        return reject(e);
      }
      if(next.done) {
        return resolve(next.value);
      }
      Promise.resolve(next.value).then(function(v) {
        step(function() { return gen.next(v); });
      }, function(e) {
        step(function() { return gen.throw(e); });
      });
    }
    step(function() { return gen.next(undefined); });
  });
  }
  ```

  ​




### 6️⃣Iterator

- 三类数据结构原生具备Iterator接口：数组、某些类似数组的对象、Set和Map结构。
- [Symbol.iterator]，是一个预定义好的、类型为Symbol的特殊值，所以放在方括号内。数据结构只要带有这个属性，就是可遍历的。这个属性本质上是一个function，执行后得到遍历器。

```javascript
let arr = ['a', 'b', 'c']
let iter = arr[Symbol.iterator]()

iter.next() // { value: 'a', done: false}
iter.next() // { value: 'b', done: false}
iter.next() // { value: 'c', done: false}
iter.next() // { value: undefined, done: true}
```

- 用Iterator实现指针结构。

```javascript
function Obj (value) {
  this.value = value;
  this.next = null;
}

Obj.prototype[Symbol.iterator] = function() {
  let iterator = {
    next: next
  }

  let current = this

  function next() {
    if(current){
      let value = current.value
      current = current.next
      return {value, done: false}
    }else{
      return {done: true}
    }
  }

  return iterator
}

let one = new Obj(1)
let two = new Obj(2)
let three = new Obj(3)

one.next = two
two.next = three

for (let i of one){
  console.log(i)
}
```

- 解构赋值，扩展运算符，会默认调用对象的Iterator接口。所以，任何可遍历的对象，都可以变成数组。

```javascript
let arr = [...iterable]
```





### 6️⃣for…of...

- 和for...in一样简洁，但for...in主要为遍历对象而设计，不适用于遍历数组
- 可以break，continue和return，forEach做不到。
- 通用于数组，set，map

### 6️⃣Promise

- Promise新建后就会立即执行
- then方法接受两个回调函数作为参数，第一个resolve时使用，第二个reject时使用，第二个可以省略。
- catch方法等于then(null,func)
- Promise.all([p1,p2,p3,...])，全部resolve的话，所有结果组成数组传递给then，其中一个rejected，就跳出了。
- Promise.race([p1,p2,p3,...])，p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的Promise实例的返回值，就传递给p的回调函数。
- Promise.resolve()，将现有对象变为Promise对象。且状态为resolved。



### 6️⃣Reflect

- 将Object对象的一些明显**属于语言内部的方法**，放到Reflect对象上。
- 修改某些Object方法的返回结果，让其变得**更合理**（原来会报错的方法，现在会返回false，就不需要try catch了）
- 让object的操作都变成**函数行为**。比如name in obj和delete obj[name]，让他们变成函数行为Reflect.deleteProperty(obj,name)
- 不管Proxy怎么修改默认行为，你总可以在Reflect上**获取默认行为**。




### 6️⃣Set & Map

- WeakSet的成员只能是对象。弱引用对象，无法遍历。WeakMap只接受对象作为key，同样弱引用，当键被回收后，键值对自动移除。**有助于防止内存泄露**
- Map，一种更完善的hash结构。任何类型都可以成为key或value。
- Map中，key直接和内存地址绑定，内存地址不一样，key就不一样。可以解决同名属性碰撞问题。
- Map可以遍历，keys(), values(), entries(), forEach()


```javascript
for ( let [key, value] of map.entries()) {
  ...
}
// 等同于
for ( let [key, value] of map) {
  ...
}
```



### 6️⃣Proxy

一种JavaScript的函数重载。
```javascript
var proxy = new Proxy({}, {
  get: function(target, property) {
    return 35;
  }
});

proxy.time // 35
proxy.name // 35
proxy.title // 35
```
Proxy代理的情况下，this指向Proxy代理。



### 🔨\_\_proto\_\_ & prototype

`__proto__`: 一种属性，每个对象都有这个属性，指向该对象的原型对象

`prototype`: 只有function才有。用来存储要被继承的属性和方法。是function的一个属性，里面包含一个对象。`DOG.prototype = {species: '犬科'}`

`Object.prototype.__proto__ === null`: Object.prototype是原型链的顶端

`Function.prototype === Function.__proto__`: 都指向Function.prototype(JS标准的内置对象)

`Function.prototype.__proto__ = Object.prototype`: JS标准的内置对象的原型是Object.prototype

- prototype实现JavaScript的继承

  ```javascript
  // 父类
  function Animal(){
    this.species = "动物";
  }

  // 子类
  Cat.prototype = new Animal();
  Cat.prototype.constructor = Cat;
  var cat1 = new Cat("大毛","黄色");
  alert(cat1.species); // 动物
  ```

  - 子类的`prototype`指向父类的`实例`。

  - 子类的实例的`__proto__`指向父类的`prototype`

  - 子类需要手动修正prototype的constructor函数，否则constructor会指向Animal。

  - 通过组合式继承，解决给父类传参的问题

    ```javascript
    // 父类
    function Animal(name){
      this.species = "动物";
      this.name = name
    }

    function Cat(name){
      Animal.call(this,name)
    }

    // 子类
    Cat.prototype = new Animal();
    Cat.prototype.constructor = Cat;
    var cat1 = new Cat("大毛");

    alert(cat1.species); // 动物
    alert(cat1.name); // 大毛
    ```

    ​






### 🔨单例模式

- 闭包

  ```javascript
  const getInstance = function(){
    let instance;
    return function(){
      if(!instance){
        instance = new Instance()
      }
      return instance;
    }
  }
  ```

- 构造函数的静态属性缓存实例

  ```javascript
  function Person(){
    if(typeof Person.instance === 'object') {
      return Person.instance
    }
    this.createTime = new Date();
    Person.instance = this;
    return this;
  }
  ```

  ​



### 🔨正则表达式

- `*`：0次或多次

- `+`：1次或多次

- `?`：0次或1次，如果紧跟在任何量词`*`、`+`、`?`、`{}`的后面，将会使量词变为非贪婪的，匹配尽量少的字符。

  ```javascript
  regx1 = /\d+/
  regx1.exec("123abc") = [ '123', index: 0, input: '123abc' ]

  regx2 = /\d+?/
  regx2.exec("123abc") = [ '1', index: 0, input: '123abc' ]
  ```

- `.`：匹配除换行符之外的任何单个字符。

- `(x)`：匹配x并记住x，括号被称为捕获括号。

  ```javascript
  'bar,foo'.replace(/(...),(...)/,'$2,$1') = 'foo,bar'
  ```

- `(?:foo)`：匹配foo但不记住foo，单纯的将foo括起来，作为一个整体

- `Jack(?=Sprat)`：匹配Jack当且仅当Jack后面跟着Sprat。（正向肯定查找）

- `[]`：字符集和，匹配方括号中的任意字符，包括转义序列，即`.`和`*`等在方括号中不用转义。





### 🔨 this关键字

- 原则：this指向调用者的那个对象。

- 通过bind，apply，call来绑定this。

- 闭包的内嵌函数中，要const that = this

- 当把含有this的方法赋值给 **一个变量** 时，要通过bind维持this的值

  ```javascript
  var data = [
    {name: "Samantha", age: 12},
    {name: "Alexis", age: 14}
  ];

  var user = {
    data: [
    	{name: "T. Woods", age: 37},
      {name: "P. Mickelson", age: 43}
    ],
    showData: function(event) {
    	var randomNum = ((Math.random() * 2 | 0) + 1) - 1; // 0 和 1 之间的随机数
      console.log(this.data[randomNum].name + " " + this.data[randomNum].age);
    }
  }

  var showUserData = user.showData.bind(user)

  showUserData()
  // bind之后，输出的就是user的data而不是全局的data
  ```



### 🔨var,let,const的一点小细节

- `for…of`循环中，`const`和`let`每次循环都会生成一个新的绑定，`var`只生成一个。

- 普通for循环中，`const`不能用来申明循环的下标。

- 暂时性死区：只要块级作用域内存在`let`命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

  ```javascript
  var tmp = 123;

  if (true) {
    tmp = 'abc'; // ReferenceError
    let tmp;
  }

  // 存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错。
  ```





### 🔨在string上使用Array.map

```javascript
var map = Array.prototype.map;
var a = map.call('Hello World', function(x) {
  return x.charCodeAt(0);
});
```





### 🔨querySelectorAll与getElementBy

- querySelectorAll，参数是**css selector**，多个selector之间用**逗号**隔开。返回的是non-live NodeList，是元素快照，不会受DOM的变化而变化。

- querySelectorAll无法查询伪元素

- getElementBy返回的是live NodeList

  ```javascript
  var ul = document.getElementsByTagName('ul')[0],
      lis = ul.getElementsByTagName("li");
  for(var i = 0; i < lis.length ; i++){
      ul.appendChild(document.createElement("li"));
  }
  // 会造成无限循环，每次调用live NodeList都会重新去查询一遍DOM
  ```

  ​
### 🔨debounce、throttle、requestAnimationFrame

- debounce：把触发非常频繁的事件（比如按键）合并成一次执行。

  - 典型例子：autocomplete，等用户停止输入之后再发送请求。

  - 实现：

    ```javascript
    function debounce(fn, delta) {
      var timeoutID = null;

      return function() {
        clearTimeout(timeoutID);

        // 保存函数调用时的上下文和参数
        var context = this；
        var args = arguments;

        timeoutID = setTimeout(function() {
          fn.apply(context, args);
        }, delta);
      };
    }
    ```

    ​

- throttle：保证每 X 毫秒恒定的执行次数。

  - 典型列子：页面底部的载入更多。

  - 与debounce的区别：`_.throttle(func,300)` 300ms内，func至少执行一次。

  - 实现：

    ```javascript
    function throttle(fn,threshhold){
      var last  		//记录上次运行时间
      var timeoutID  	//定时器

      threshhold || (threshhold = 250)

      return function(){

        var context = this
        var args = arguments

        var now = Date.now()

        if(last && now < last + threshhold){
          clearTimeout(timeoutId)

          timeoutId = setTimeout(function(){
            last = now
            fn.apply(context,args)
          },threshhold)
        }else{
          last = now
          fn.apply(context,args)
        }
      }
    }
    ```

    ​

- requestAnimationFrame：可替代 throttle ，函数需要重新计算和渲染屏幕上的元素时，想保证动画或变化的平滑性，可以用它。但需要手动控制动画的开始和结束。



### 🔨解决setTimeout的this问题

```javascript
myArray = ['zero', 'one', 'two'];
myArray.myMethod = function (sProperty) {
    alert(arguments.length > 0 ? this[sProperty] : this);
};

myArray.myMethod(); // prints "zero,one,two"
myArray.myMethod(1); // prints "one"


setTimeout(myArray.myMethod, 1000); // prints "[object Window]" after 1 second
setTimeout(myArray.myMethod, 1500, '1'); // prints "undefined" after 1.5 seconds
```

在不使用bind的情况下，setTimeout里面的这个function，this默认指向window。

解决办法：

```javascript
setTimeout(function(){myArray.myMethod()}, 2000); // prints "zero,one,two" after 2 seconds
setTimeout(function(){myArray.myMethod('1')}, 2500); // prints "one" after 2.5 seconds

// or use arrow function

setTimeout(() => {myArray.myMethod()}, 2000); // prints "zero,one,two" after 2 seconds
setTimeout(() => {myArray.myMethod('1')}, 2500); // prints "one" after 2.5 seconds

// 或者使用Proxy重写window的setTimeout函数
var __nativeST__ = window.setTimeout,

window.setTimeout = function (vCallback, nDelay /*, argumentToPass1, argumentToPass2, etc. */) {
  var oThis = this,
      aArgs = Array.prototype.slice.call(arguments, 2);
  return __nativeST__(vCallback instanceof Function ? function () {
    vCallback.apply(oThis, aArgs);
  } : vCallback, nDelay);
};
```

#### 其他的this问题：

- 非strict模式下，this只跟**调用者**有关。是谁在调用，就指向谁。

- 箭头函数中，this只跟**定义时**的上下文有关，跟被谁调用无关。

  - 特殊情况：

    ```javascript
    var obj = {
      bar: function(){
        var x = () => this
        return x
      }
    }

    var fn = obj.bar()

    console.log(fn() === obj) // true

    var fn2 = obj.bar

    console.log(fu2()() === window) // true
    ```

- function作为一个object的方法（属性）时，this**指向这个object**。且如果这个function被多个object引用时，this指向**最后一个**。

- 原型链上的this：

  ```javascript
  var o = {f: function() { return this.a + this.b; }};
  var p = Object.create(o);
  p.a = 1;
  p.b = 4;

  console.log(p.f());
  // 5
  // 虽然f方法在原型o上，但this依旧指向p
  ```

### 🔨`typeof`和`Object.prototype.toString.call()`的对比

- 实例：

  ```javascript
  typeof Math  // object
  Object.prototype.toString.call(Math)  // [Object Math]

  typeof [] // object
  Object.prototype.toString.call([])  // [Object Array]
  ```

- Object.prototype.toString.call()的运行原理

  1. 获取this对象的`[[Class]]`属性的值
  2. return "[Object " + [[Class]] + " ]"

  > [[Class]] 是一个内部属性，原生对象和内置对象都有。
  >
  > [[Class]] 属性的值，可以用来判断一个原生对象属于哪种内置类型，这就是为什么这个方法可以获取最真实的类型的原因。

- 七种基本类型：Number, String, Boolean, Object, Null, Undefined, Symbol

- Object衍生出来的对象：Array, Function, Date, RegExp

- `undefined`和`null`的区别：前者是一个unexpected no-value，后者是一个expected no-value。就是说，本该有一个value，但却没有value的时候，就是undefined。手动控制没有value 的时候，就是null。

- 原生对象与宿主对象

  - 原生对象是由ECMAScript定义的那些对象，独立于宿主环境。是那些具有内部`[[Class]]`属性的对象。
  - 宿主对象是在js环境中，一开始便生成的那些对象
  - built-in object: object specified and supplied by an ECMAScript implementation

  ```
  Native Objects:
  Object, Function, Array, String, Boolean, Date, Math, RegExp

  Host Objects:
  window, document, location, history
  ```

  ​



JavaScript模块引用

组件化，模块化

canvas

按需加载

深拷贝

排序算法

webpack

设计模式

javascript 继承

子类的原型为什么指向父类的实例而不是父类的原型。

https和http