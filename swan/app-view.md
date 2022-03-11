# 视图层

参考文档：https://developers.weixin.qq.com/miniprogram/dev/framework/view/

1. 说明我们的小程序渲染部分是基于flutter的
2. 视图层的开发形式是vue template的形式，介绍我们的组件，简单介绍即可，参考微信中如何介绍wxml的
3. 样式系统
4. 事件系统介绍

* 小度小程序基于flutter渲染引擎渲染，在标签语法上使用atom-flutter提供的标签语法，样式使用flutter内置的class和style样式

* 整个视图层逻辑使用vue模板语法，组件中包含template模板、样式脚本以及js逻辑部分。详见[小程序代码构成](./code.md)

* 样式支持class和style两种形式，书写形式上与web应用有所区别。详见[小程序代码构成](./code.md)

* 事件绑定系统，atom-flutter提供了强大的手势绑定系统，支持tap，tapDown，tapUp等手势。详见[手势](http://10.24.7.83:8080/docs/doc/gesture/gestureDetector/)
