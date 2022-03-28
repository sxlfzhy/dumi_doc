# 小程序代码构成

上一章，我们通过 swan_app 命令初始化了一个 QuickStart 项目。你可以留意到这个项目里边生成了不同类型的文件:

1. `.json` 后缀的 `JSON` 配置文件
1. `.vue` 后缀的 `Vue` 模板文件
1. `.ts` 后缀的 `typescript` 脚本逻辑文件

## 配置文件

小程序中的静态配置文件主要有 `json` 和 `js` 两种形式。  

* JS 配置文件主要用于开发工具配置；
* JSON 是一种数据格式，并不是编程语言，在小程序中，JSON扮演的静态配置的角色；

在QuickStart项目中，我们可以看到以下配置：

* 根目录下有一个 `project.config.js`
* src 目录下有一个 `app.json`
* pages/home 目录下还有一个 `home.json`

我们依次来说明一下它们的用途。

### 工具配置 project.config.js

小程序开发者工具在每个项目的根目录都会生成一个 project.config.js，主要是开发过程中和小度设备实现联动所必须的个性化配置，
其中包括：技能ID、技能签名SK以及预览设备的相关信息。

> 该配置内容对应 `swan_app create` 命令过程中的输入项

#### 配置项

| 属性 | 必填 | 说明 |
| :---: | :---: | :---: |
| botId | 是 | 技能id，技能开放平台创建技能时生成的技能唯一标识，符合36位UUID规范 | 
| sk | 是 | 密钥（签名Key），技能开放平台创建技能时生成的访问密钥，见：技能基础信息中的签名Key | 
| cuid | 是 | 设备id（序列号），设备唯一标识，即设备底部sn，大写字母和数字组合 | 
| phone | 是 | 设备绑定的百度账号对应的手机号码 | 
| entryPagePath | 否 | debug进入小程序打开的页面路径，默认：小程序首页 | 


#### 示例

``` javascript
module.exports = {
    botId: 'aef6cfb5-fa7f-048d-2cc2-db8b8221de33',
    sk: '1683ebd9-e07b-bz79-8d88-c4ade13af366',
    cuid: '8B19429D10144208',
    phone: '187****4920',
    entryPagePath: ''
};
```


### 小程序配置 app.json

app.json 是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、权限、网络超时等。QuickStart 项目里边的 `app.json` 配置内容如下：

``` json
{
    "pages": [
        "pages/home/home"
    ],
    "window": {
        "backgroundColor": "#ff000000",
        "navigationBarTextStyle": "black"
    }
}
```

我们简单说一下这个配置各个项的含义:

1. `pages` 字段 —— 用于描述当前小程序所有页面路径，这是为了让客户端知道当前你的小程序页面定义在哪里。
1. `window` 字段 —— 定义小程序所有页面的背景颜色等。

其他配置项细节可以参考文档 [配置小程序](./config.md) 。

### 页面配置 page.json

这里的 page.json 其实用来表示 `pages/home` 目录下的 `home.json` 这类和小程序页面相关的配置。

其他配置项细节可以参考文档 [配置小程序](./config.md) 。

### JSON 语法

这里说一下小程序里JSON配置的一些注意事项。

JSON文件都是被包裹在一个大括号中 {}，通过key-value的方式来表达数据。JSON的Key必须包裹在一个双引号中，在实践中，编写 JSON 的时候，忘了给 Key 值加双引号或者是把双引号写成单引号是常见错误。

JSON的值只能是以下几种数据格式，其他任何格式都会触发报错，例如 JavaScript 中的 undefined。

1. 数字，包含浮点数和整数
1. 字符串，需要包裹在双引号中
1. Bool值，true 或者 false
1. 数组，需要包裹在方括号中 []
1. 对象，需要包裹在大括号中 {}
1. Null

还需要注意的是 JSON 文件中无法使用注释，试图添加注释将会引发报错。

## TS 逻辑交互

一个服务仅仅只有界面展示是不够的，还需要和用户做交互：网络请求、响应用户点击等等。
在小程序里边，我们就通过编写 `Typescript` 脚本文件来处理用户的操作。

> 使用TS的另外一个原因是：可以在开发过程中获得更友好的代码提示和补全。

在 `src/app.ts` 中我们可以处理小程序的全局交互：

``` typescript
import {ref} from '@atom-vue/vue';
import swan, {AppConfig} from 'kuat';

const appConfig: AppConfig = {
    globalData: ref({}),
    onLaunch() {
        // 监听小程序初始化
        swan.logger.info('进入小程序');
    },
    onShow() {
        // 监听小程序显示
        swan.logger.info('小程序显示');
    },
    onHide() {
        // 监听小程序隐藏
        swan.logger.info('小程序隐藏');
    },
    onPageNotFound() {
        // 监听页面不存在
        swan.logger.info('未找到目标页面');
    },
    beforePageChange(to, from, next) {
        // 页面变化前守卫
        next();
    },
    afterPageChange(to, from) {
        // 页面跳转完成
    },
    onError() {
        // 接收错误信息
    }
};

swan.App(appConfig);
```

也可以在 `VUE` 文件中使用 `Typescript`，如

``` vue
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

## 附录

* [TypeScrip官方文档](https://www.typescriptlang.org/)
* [Vue 3.0官方文档](https://vuejs.org/)

## Vue 模板

小程序使用类似Vue的模板语法来构建页面部分，采用 vue 3.* 的版本。但与Vue模板语法有些许不同。
小程序的 `vue` 模板分为：

* `<template>` -- 页面的dom结构，同 `vue` 文件中的template
* `<script data-is-style>` -- 页面的样式部分，采用 `javascript` 语法标准，类似与网页中的 `css`
* `<script lang="ts">` -- 页面的逻辑部分，推荐 `typescript` 语法标准，同 vue 3.* 的 `js` 部分

以下针对这三部分逐个介绍：

### template 描述页面的Dom结构


小程序的底层渲染引擎使用了Flutter，所以在渲染组件上需要使用flutter提供的组件和样式规范进行编码

1、我们vue模板的组成
2、标签体系，后续我们要链接到组件文档那里，说明一下样式体系都是flutter的

小度小程序使用类似Vue的模板语法，但与Vue模板语法有些许不同，小度小程序的模板语法中使用flutter进行渲染，需要使用flutter提供的组件和样式规范进行编码，具体模板类型如下：

``` vue
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

``` vue
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

``` vue
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

``` vue
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

``` vue
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
