---
layout: post
title:  "react制作Chrome风格取色器"
categories: javascript
description: "使用react制作Chrome控制台风格取色器"
main-class: 'dev'
color: '#632321'
tags:
- "react"
twitter_text: "使用react制作Chrome控制台风格取色器"
introduction: "使用react制作Chrome控制台风格取色器"
---

在前面的博客里面我使用react做了一个简易计算器的demo，这一次则做了一个稍微复杂的取色器demo。
如下图所示，该取色器参照了Chrome浏览器控制台的css样式功能区的取色器。
![Chrome风格取色器](../assets/img/2016-11-18.jpg)
#### demo目标需求
取色器的目标需求基本与chrome控制台的取色器功能基本一致，具体如下：
* 用2个range类型的input来分别模拟色调滑块控制条和alpha透明度滑块控制条，滑动控制条，上方的矩形取色板的色调和右侧的圆形色块背景色以及下方的hex/rgba/hsla色值会相应地改变。
* 矩形取色板上有一个小圆点来进行取色，鼠标点击不同的位置可以选择相应位置的颜色，同时右侧的圆形色块背景色以及下方的hex/rgba/hsla色值会相应地改变。
* 右侧有一个吸管图标和圆形区域来实时地显示当前选中的颜色。
* 最下方是显示当前颜色的色值，色值的格式可以在hex/rgba/hsl三者之间切换。
同时，也可以在上面手动填写颜色的值，手动填写的值发生改变时，滑块、取色板以及取色板上圆点的位置都会发生对应的变化。

#### 创建react类及其render方法


```javascript
var ColorWrap = React.createClass({//取色器类
})

```