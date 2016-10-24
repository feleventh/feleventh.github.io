---
layout: post
title:  "react初体验——制作简易计算器web app"
categories: javascript
description: "react初体验——使用reactjs制作简易计算器web app"
main-class: 'dev'
color: '#632321'
tags:
- "react"
twitter_text: "react初体验——使用reactjs制作简易计算器web app"
introduction: "react初体验——使用reactjs制作简易计算器web app"
---

上个月angular2.0正式发布，可以预见由微软和谷歌合作推出的angular2.0将在未来一段时间内和reactjs、vuejs一道成为最流行的三大前端框架。
我决定先从当下最热门的reactjs开始入手，在今年内对这三大框架进行一个系统的学习。于是有了今天这个计算器的demo。
![react-caculator](../assets/img/2016-10-24.jpg)
如下图所示，使用Key组件来将所有计算器的按键render到`.key-container`容器中去，并在组件中给所有按键赋予规定的文本值，并绑定点击事件。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
  <title>demo caculator</title>
  <link rel="stylesheet" href="assets/css/base.css">
  <script src="../build/react.js"></script>
  <script src="../build/react-dom.js"></script>
  <script src="../build/browser.min.js"></script>
  <script src="../build/jquery.min.js"></script>
</head>
<body>
  <div class="container">
    <div class="page">
      <div class="screen"><input type="text" disabled></div>
      <div class="key-container"></div>
    </div>
  </div>
  <script type="text/babel">
    var Key = React.createClass({
      render: function () {
        var keyNum = ['clear','=',7,8,9,'/',4,5,6,'*',1,2,3,'-',0,'.','+'];
        var keyNumDom = keyNum.map(function (ele, index) {
          var cName = '';
          if(typeof ele === 'number'||ele === '.'){
            cName = 'key-num';
            if(ele === 0){
              cName = 'key-num key-0'
            }
          }else{
            if(ele ==='clear'){
              cName = 'key-clear';
            }
            else if(ele === '='){
              cName = 'key-enter';
            }
            else{
              cName = 'key-operation';
            }
          }
          var handleClick = function(event){
            var input = $('.screen input');
            var key = event.target;
            if($(key).hasClass('key-num')){
              input.val(input.val()+key.innerHTML);
            }
            else if($(key).hasClass('key-operation')){
              if(input.val() === ''){
                input.val('0'+' '+key.innerHTML+' ');
              }else{
                input.val(input.val()+' '+key.innerHTML+' ');
              }
            }
            else if($(key).hasClass('key-clear')){
              input.val('');
            }
            else if($(key).hasClass('key-enter')){
              input.val(eval(input.val()));
            }
          };
          return (
                  <button key={index} className={cName} onClick={handleClick}>{ele}</button>
          );
        });
        return <div className="key-wrap">{keyNumDom}</div>;
      }
    });
    ReactDOM.render(<Key></Key>, document.querySelector('.key-container'));
  </script>
</body>
</html>
```



