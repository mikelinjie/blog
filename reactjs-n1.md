# ReactJS 学习笔记

## 前言

入门教程 React中文网站：http://docs.reactjs-china.com/react/docs/getting-started.zh-CN.html

中文网站的例子已经很好了，另找了一个例子作为参考https://github.com/ruanyf/react-demos

简易服务器搭建
```
$ npm install -g http-server
$ cd /your excamples dir
$ http-server -p 8080
```


## CommonJS

### 起源

JavaScript是一个强大面向对象语言，它有很多快速高效的解释器。官方JavaScript标准定义的API是为了构建基于浏览器的应用程序。然而，并没有定于一个用于更广泛的应用程序的标准库。

CommonJS API定义很多普通应用程序（主要指非浏览器的应用）使用的API，从而填补了这个空白。它的终极目标是提供一个类似Python，Ruby和Java标准库。这样的话，开发者可以使用CommonJS API编写应用程序，然后这些应用可以运行在不同的JavaScript解释器和不同的主机环境中。在兼容CommonJS的系统中，你可以实用JavaScript程序开发：

* 服务器端JavaScript应用程序
* 命令行工具
* 图形界面应用程序
* 混合应用程序（如，Titanium或Adobe AIR）

### NodeJS和CommonJS之间的关系

CommonJS是一种规范，NodeJS是这种规范的实现。CommonJS是一个不断发展的规范，计划将要包括如下部分：
* Modules
* Binary strings and buffers
* Charset encodings
* Binary, buffered, and textual input and output (io) streams
* System process arguments, environment, and streams
* File system interface
* Socket streams
* Unit test assertions, running, and reporting
* Web server gateway interface, JSGI
* Local and remote packages and package management

具体每个子规范的定制进度请查看官方网站的说明：http://commonjs.org/specs/

CommonJS有很多实现，其中不乏很多大名鼎鼎的项目，比如 说：Apache的CouchDB和node.js等。但这些项目大 部分只实现了CommonJS的部分规范。具体的项目和实现部分参见官方网站的说明：http://commonjs.org/impl/

## ReactJS简介

### 原理

在Web开发中，我们总需要将变化的数据实时反应到UI上，这时就需要对DOM进行操作。而复杂或频繁的DOM操作通常是性能瓶颈产生的原因（如何进行高性能的复杂DOM操作通常是衡量一个前端开发人员技能的重要指标）。React为此引入了虚拟DOM（Virtual DOM）的机制：在浏览器端用Javascript实现了一套DOM API。基于React进行开发时所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。而且React能够批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，例如你连续的先将节点内容从A变成B，然后又从B变成A，React会认为UI不发生任何变化，而如果通过手动控制，这种逻辑通常是极其复杂的。尽管每一次都需要构造完整的虚拟DOM树，但是因为虚拟DOM是内存数据，性能是极高的，而对实际DOM进行操作的仅仅是Diff部分，因而能达到提高性能的目的。这样，在保证性能的同时，开发者将不再需要关注某个数据的变化如何更新到一个或多个具体的DOM元素，而只需要关心在任意一个数据状态下，整个界面是如何Render的。

### 组件化

虚拟DOM(virtual-dom)不仅带来了简单的UI开发逻辑，同时也带来了组件化开发的思想，所谓组件，即封装起来的具有独立功能的UI部件。React推荐以组件的方式去重新思考UI构成，将UI上每一个功能相对独立的模块定义成组件，然后将小的组件通过组合或者嵌套的方式构成大的组件，最终完成整体UI的构建。

**React的虚拟DOM树，感觉优点像以前MFC中的双重渲染的机制，这种设计方案在很多框架中都有应用。**

### 与AngularJS区别

主要从性能方面来考虑，其他方面感觉没什么必然的优势。

虽然Angular的数据的表达能够非常紧凑, 但是渲染大型数据集依旧被证明是一个痛点. 由于双向数据绑定需要监听每一个可变元素, 数据量变大就会带来显著的性能问题. React, 在另一方面, 使用虚拟DOM来跟踪元素的变化. 当检测到变化时, React会构建一个针对DOM变化的补丁, 然后应用这些补丁. 由于不必在每个元素每次变化时重新渲染整个巨大的table, React相对于其他JavaScript框架有显著的性能提升.

在为你的应用选择JavaScript框架时，要考虑每个框架的优势和劣势，这需要对相关的知识有深入的了解。正如上文所述，如果应用时常要处理大量的动态数据集，并以相对简便和高性能的方式对大型数据表进行显示和变更，React是相当不错的选择。但是React不像AngularJS那样包含完整的功能，举例来说，React没有负责数据展现的控制器（Controller）层。

**但是，从AngularJS2.0的发展趋势来看，未来的AngularJS方向已经有点和ReactJS趋同了。只能说如果一样设计，它确实是好的，那么它就会被推广，被模仿。**


### pubsub、react-route、ajax、flux、webpack
由于ReactJS只是view层的框架，在简洁，轻巧的同时，也会有有一些功能上的不足。这里介绍下几种相应的框架可以和ReactJS很好的结合，完成应用的构建。pubsub框架是一个事件框架，或者说是一种模式。当两个没有联系，不构成父子级关系的组件需要进行数据通信时就可以使用pubsub的方式进行通信，就像以前AngularJS在1.x时代的$emit、$on、$broadcast一样。react-route，路由的功能就不必多说了，想必大家都经常用。


## 一个简单的单页应用
pubsubjs:建议用bower安装js包后，跟着包里的demo或者操作说明来操作，否则新手可能会坑到自己。在此用pubsubjs + react-route + react 搭了一个简单的demo，可以作为参考
https://github.com/mikelinjie/react-demo
