# 逻辑层

参考文档：https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/

依次说明注册小程序、注册页面、小程序生命周期、页面生命周期、页面路由、模块化、和Api等内容。

参考微信的文档。

* 使用`swan.app`，注册小程序App实例
* 支持 `onLaunch`， `onShow`，`onHide`，`onPageNotFound`等钩子函数，监听实例状态。
* 支持使用 `swan.navigateTo`进行页面的跳转
* 支持使用 `swan.logger.error`和`adb logcat`结合进行日志查看和调试等
* 支持使用es6进行模块化导入导出
