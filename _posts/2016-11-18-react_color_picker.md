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
首先创建一个组件类，render出取色器的dom结构， 

```javascript
var ColorWrap = React.createClass({//取色器组件类
   render: function () {
      var value = this.state.value;
      var alpha = this.state.alpha;
      var x = this.state.x;
      var y = this.state.y;
      var hex = this.state.hex;
      var pickRgb = this.state.pickRgb;
      var hsl = this.state.hsl;
      return <div className="color-wrap">
        <canvas className="color-block"></canvas>
        <div className="color-picker-wrap" onClick = {this.handlePickerWrapClick}>
          <div className="color-picker" style={{left:x-6,top:y-6}}></div>
        </div>
        <div className="mask"></div>
        <div className="color-switch">
          <svg className="icon"  viewBox="0 0 1024 1024" width="20" height="20" fill={hex}>
            <path d="M825.196613 278.276576c15.172154-15.172154 15.172154-39.736595 0-54.908749L798.344309 196.515522c-15.172154-15.172154-39.736595-15.172154-54.908749 0l-65.866416 65.866416 81.761054 81.761054L825.196613 278.276576z">
            </path>
            <path d="M831.337723 416.752587l-226.378175-226.378175c-11.800564-11.800564-30.946378-11.800564-42.746943 0l-79.954845 79.954845c-11.800564 11.800564-11.800564 30.946378 0 42.746943l46.35936 46.35936L201.452493 686.479774c-20.109125 20.109125-20.109125 52.620884 0 72.730009l67.672625 67.672625c20.109125 20.109125 52.620884 20.109125 72.730009 0l327.164628-327.164628 39.495767 39.495767c11.800564 11.800564 30.946378 11.800564 42.746943 0l79.954845-79.954845C843.138288 447.578551 843.138288 428.553151 831.337723 416.752587zM333.185325 804.605833c-15.533396 15.533396-40.699906 15.533396-56.233302 0l-52.982126-52.982126c-15.533396-15.533396-15.533396-40.699906 0-56.233302L544.270931 374.968956l109.215428 109.215428L333.185325 804.605833z">
            </path>
            <path d="M201.813735 803.040452c0 13.125118 10.596425 23.721543 23.721543 23.721543l42.506115 0-66.227658-66.227658L201.813735 803.040452z">
            </path>
          </svg>
          <div className="circle" style={{background: hex,opacity:alpha/255}}></div>
        </div>
        <input className="rgb-range" type="range" min="0" step="1" max="1535" value={value} onChange={this.handleValueChange} />
        <input className="alpha-range" type="range" min="0" step="1" max="255" value={alpha} onChange={this.handleAlphaChange} />
        <ul className="color-show">
          <li className="hex">
            <input type="text" value={hex} onChange={this.handleHexChange} />
            <p>HEX</p>
          </li>
          <li className="rgba hide">
            <input type="text" value={pickRgb[0]} onChange={this.handleRgbChange} />
            <input type="text" value={pickRgb[1]} onChange={this.handleRgbChange} />
            <input type="text" value={pickRgb[2]} onChange={this.handleRgbChange} />
            <input type="text" value={alpha} onChange={this.handleAChange} />
            <p><span>R</span><span>G</span><span>B</span><span>A</span></p>
          </li>
          <li className="hsla hide">
            <input type="text" value={hsl[0]} onChange={this.handleHslChange} />
            <input type="text" value={hsl[1]} onChange={this.handleHslChange} />
            <input type="text" value={hsl[2]} onChange={this.handleHslChange} />
            <input type="text" value={alpha} onChange={this.handleAChange} />
            <p><span>H</span><span>S</span><span>L</span><span>A</span></p>
          </li>
        </ul>
        <svg className="switch" viewBox="0 0 1024 1024"  width="24" height="24" fill="#515151" onClick={this.handleSwitch}>
          <path d="M512 859.615l-260.711-260.711h521.422z"></path><path d="M512 164.385l-260.711 260.711h521.422z"></path>
        </svg>
      </div>;
    }
})

```