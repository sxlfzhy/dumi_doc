# 小程序配置

参考文档：[https://developers.weixin.qq.com/miniprogram/dev/framework/config.html](https://developers.weixin.qq.com/miniprogram/dev/framework/config.html)

用文档说明小程序app.json配置内容和page.json中的配置内容。

## 全局配置

小程序根目录下的 app.json 文件用来对微信小程序进行全局配置，具体配置shi

```json
{
    "entryPagePath": "pages/home/home",
    "pages": [
        "pages/home/home",
    ],
    "window": {
        "backgroundColor": "#000000",
        "navigationBarTextStyle": "black"
    },
    "debug": true,
    "networkTimeout": {
        "request": 10000
    }
}
```

参数介绍：

| 属性 | 类型 | 必填 | 描述 |
| :---: | :-----: | :----: | :--------------------: |
| `entryPagePath` | string | 否 | 小程序默认启动首页入口|
| `pages` | string[] | 是 | 页面路径列表|
| `window` | Object | 否 | 全局默认窗口表现配置|
| `debug` | boolean | 否 | 是否开启debug模式，默认为false|
| `networkTimeout` | Object | 否 | 网络超时时间|

## 页面配置

每一个小程序页面也可以使用同名 .json 文件来对本页面的窗口表现进行配置，页面中配置项会覆盖 app.json 的 window 中相同的配置项。详细配置如下：

```json
{
    "backgroundColor": "#000000",
    "navigationBarTitleText": "标题示例"
}
```

参数介绍:

| 属性 | 类型 | 默认值 | 描述 |
| :---: | :-----: | :----: | :-------: |
| `backgroundColor` | string | #ffffff | 窗口的背景色|
| `navigationBarTitleText` | string[] | - | 导航栏标题文字内容 |
