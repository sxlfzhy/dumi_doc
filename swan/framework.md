# 小程序框架

参考文档：[https://developers.weixin.qq.com/miniprogram/dev/framework/MINA.html](https://developers.weixin.qq.com/miniprogram/dev/framework/MINA.html)

对小程序的框架进行简单介绍。比如我们的渲染层用的flutter、代码层主要是vue文件的组合等。视图层是怎么搞的，逻辑层是怎么搞的。

小程序开发框架的目标是通过尽可能简单、高效的方式让开发者可以在微信中开发具有原生 APP 体验的服务。

整个小程序框架系统分为两部分：逻辑层（App Service）和 视图层（View）。小程序提供了自己的视图层 Vue 模板，以及基于 JavaScript 的逻辑层框架，并在视图层与逻辑层间提供了数据传输和事件系统，让开发者能够专注于数据与逻辑。

* 逻辑层

    小程序开发框架的逻辑层使用 JavaScript 引擎为小程序提供开发者 JavaScript 代码的运行环境以及小度小程序的特有功能。逻辑层将数据进行处理后发送给视图层，同时接受视图层的事件反馈。在 JavaScript 的基础上，我们增加了一些功能，以方便小程序的开发。

* 视图层

    小度小程序使用flutter渲染，只支持使用flutter的模板标签和样式
