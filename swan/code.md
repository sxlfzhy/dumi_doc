# 小程序代码构成

参考文档：[https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html)

通过一个hello小程序帮助开发者对小程序的代码有一个基本了解，简单介绍一下json配置、vue文件构成、标签语法、ts文件。

1、介绍project.config.js
2、介绍hello小程序src目录下的代码

## JSON 配置

### 项目配置 project.config.js

#### 1、 小程序运行时项目配置

```js
module.exports = {
    botId: '{{botId}}',
    sk: '{{sk}}',
    cuid: '{{cuid}}',
    phone: '{{phone}}',
    entryPagePath: ''
};
```

#### 2、必要参数

* (必要) `botId`： 小程序技能id
* (必要) `sk`： 密钥（签名Key），技能开放平台创建技能时生成的访问密钥，符合36位UUID规范。见：技能基础信息中的签名Key
* (必要) `cuid`： 设备id（序列号），设备唯一标识，即设备底部sn，为大写子母和数字组合
* (必要) `phone`： 小度app登录的百度账号所绑定的手机号码
* (可选) `entryPagePath`： 小程序打开的页面路径，默认：小程序首页

### 小程序配置 app.json

app.json 是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、权限、网络超时等。app.json 配置内容如下：

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


### 页面配置 page.json

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

## TS 逻辑

小程序代码逻辑原生支持`TypeScript`编写，例子如下：

* app.ts:

```ts
import {ref} from '@atom-vue/vue';
import swan from 'kuat';

interface GlobalData {
    title: string;
    [key: string]: any;
}

swan.App({
    globalData: ref<GlobalData>({
        title: 'swan-app'
    })
});
```

* page.ts:

```ts
<script lang="ts">
import {ref} from '@atom-vue/vue';
import swan from 'kuat';

export default {
    setup(props) {
        const loading = ref(false);

        function setLoading(bool: boolean): void {
            loading.value = bool;
        }

        return {
            loading
        };
    }
};
</script>
```

* [TypeScrip官方文档](https://www.typescriptlang.org/)

## Vue 模板

1、我们vue模板的组成
2、标签体系，后续我们要链接到组件文档那里，说明一下样式体系都是flutter的

小度小程序使用类似Vue的模板语法，但与Vue模板语法有些许不同，小度小程序的模板语法中使用flutter进行渲染，需要使用flutter提供的组件和样式规范进行编码，具体模板类型如下：

```ts
// 模板结构
<template>
    <container class="page-container">
        <text class="page-title">hello world</text>
    </container>
</template>

// 样式结构
<script data-is-style>
atom.reusableStylesManager.add([
    [
        'page-container',
        ContainerStyles.c({
            color: Color.fromRGBO(255, 255, 255, 1)
        })
    ],
    [
        'page-title',
        TextStyles.c({
            fontSize: 32,
            color: Color.fromRGBO(0, 0, 0, 1)
        })
    ]
]);
</script>

// js结构
<script lang="ts">
export default {
    setup() {
        return {};
    }
};
</script>
```

### 标签体系

如上案例所示，在标签语法中，跟微信小程序有所不同，小度小程序需要遵循atom-flutter的标签语法规范：

```html
<template>
    <container>
        <text>hello world<text>
    </container>
</template>
```

* 详见 [flutter标签语法](http://10.24.7.83:8080/docs/)

### class样式

重点说明一下我的class样式，大概就是下边这种形式

在小度小程序的样式使用中，class样式的需要定义在`atom.reusableStylesManager`中，单个class样式使用数据结构存储，在小度小程序中，同样支持class类名和style样式这两种引入方式：

* class样式

  * 类名
  * 样式结构

``` html
<template>
    <container class="page-container">
        <text>hello world<text>
    </container>
</template>

<script data-is-style>
atom.reusableStylesManager.add([
    [
        'page-container', // 类名
        ContainerStyles.c({
            color: Color.fromRGBO(255, 255, 255, 1)
        })
    ]
]);
</script>
```

如果是存在动态样式需要使用$style包裹class类名:

```html
<template>
    <container :class="[$style['page-container'], active ? $style['page-container-active'] : null">
        <text>hello world<text>
    </container>
</template>
<script lang="ts">
export default {
    setup() {
        return {
            active: true
        };
    }
};
</script>

```

* style样式

``` html
<template>
    <container :style="
        ContainerStyles.c({
            width: 800,
            height: 200,
            color: Color.fromRGBO(255, 255, 255, 1)
        })
    ">
        <text>hello world<text>
    </container>
</template>
```
