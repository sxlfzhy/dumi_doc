# 组件

参考文档：https://developers.weixin.qq.com/miniprogram/dev/component/

介绍我们有的swan-ui组件，展示swanui组件文档

介绍Flutter的标签文档

* 容器组件

| 名称 | 功能说明 |
| :---: | :-----------: |
| `Container` | 包含样式，定位和调整大小等功能的容器|
| `AnimatedContainer` | 支持动画的容器，能够渐变地改变内容 |
| `List` | 排列无限数量子控件的长列表，提供滚动功能 |
| `ColoredBox` | 容器内绘制背景颜色，再绘制子控件 |
| `PageView` | 按页排列子控件列表，提供轮播功能 |
| `WebView` | web-view可以展示网页内容，接收页面事件与操控页面内容 |
| `ScrollView` | 线性排列子控件列表，提供滚动功能 |

* 布局组件

| 名称 | 功能说明 |
| :---: | :-----------: |
| `Align` | 使用align对齐子控件，并可选根据子控件的大小重新调整自身大小 |
| `Flex` | 使用flex将所有子控件向一个方向排列
 |
| `Row` | 使用row将所有子控件在水平方向排列
 |
| `Column` | 使用column将所有子控件在垂直方向排列
 |
| `Expanded` | 使用expanded包裹flex, row和column的children（注意仅能在flex, row或column下使用）被包裹的child会在主轴上扩展可用的空间，主轴上多个expanded会均比扩展 |
| `Wrap` | 使用wrap排列子控件到多行多列，wrap会优先在主轴上排列子控件，如果主轴空间不足，会另起一行，继续排列子控件 |
| `ScrollView` | 线性排列子控件列表，提供滚动功能 |
| `Stack` | 相对容器盒子边界，定位子控件，同时能够层叠多个子控件,子控件重叠的区域会显示最后渲染的子控件内容
 |
| `Positioned` | 使用positioned对stack的子控件进行定位 |
| `Center` | 使用center使其包裹的子控件水平垂直居中 |

详情见：[flutter组件](http://10.24.7.83:8080/docs/)