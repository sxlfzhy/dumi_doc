# 小程序代码构成

参考文档：[https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html)

通过一个hello小程序帮助开发者对小程序的代码有一个基本了解，简单介绍一下json配置、vue文件构成、标签语法、ts文件。

1、介绍project.config.js
2、介绍hello小程序src目录下的代码



## JSON 配置

### 项目配置 project.config.js

### 小程序配置 app.json

### 页面配置 page.json

## TS 逻辑

说明一下小程序的逻辑控制都支持TS代码，帖两个最简单的app.ts和page.ts的描述。
链接到typescript官网--英文网站

## Vue 模板

1、我们vue模板的组成
2、标签体系，后续我们要链接到组件文档那里，说明一下样式体系都是flutter的


### 标签体系

参考：https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html#WXML-%E6%A8%A1%E6%9D%BF

### class样式

重点说明一下我的class样式，大概就是下边这种形式
<script data-is-style>
atom.reusableStylesManager.add([
    [
        'page-container',
        ContainerStyles.c({
            color: Color.fromRGBO(255, 255, 255, 1)
        })
    ]
]);
</script>
