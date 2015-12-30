---
layout: post
title:  "学习node+mongodb过程中express4引发的问题"
description:  "学习node+mongodb过程中express4引发的问题"
categories:  essay
tags: [node]
---

在当前的node学习资源中，大部分都是基于express3.x来讲解的，而express已经进入4.x时代（Express是一个基于 Node.js 平台，快速、开放、极简的 web 开发框架）。

### Express4不再依赖中间件

Express 4 不再依赖 Connect，并且从核心中移除了所有内建的中间件，这意味着 Express 现在是一个不依赖路由和中间件的 Web 框架。

随着内建的中间件被移除，你必须显式添加所有依赖的中间件来运行你的应用，简单来说需要以下步骤：

* 安装模块：npm install –save 模块名称
* 在你的应用中，使用这个模块： require( 模块名称 )
* 基于模块的文档来使用模块

这里举个例子，bodyParser和static中间件的使用

```javascript
//express3.x
app.use(express.bodyParser());
app.use(express.static(path.join(__dirname, '/bower_components')));

//express4.x
var bodyParser = require('body-parser');
var serveStatic = require('serve-static');

app.use(require('body-parser').urlencoded({extended: true}));
app.use(bodyParser.json());
app.use(serveStatic(__dirname + '/bower_components'));
//注意，dirname前面是2个下划线，
```

#### Express 3 中的中间件中对应 Express 4 中的模块可查看[这个网站](http://daringfireball.net/projects/markdown/syntax)。

### app.use 可接受参数

在 Express 4 中，现在你可以使用带有一个可变参数的路径来加载中间件，并且从路由处理器中读取参数的值，例如：

```javascript
app.use('/book/:id',function(req,res,next){
   console.log('ID:',req.params.id);
   next();
})
```
#### 另外Express4.x还有很多新的特性和改变，如新加入express.router类，不再需要http模块来启动，直接是使用app.listen()就可启动服务，app.configure被移除等等，具体可以查看[express4.x中文文档]([http://www.expressjs.com.cn/4x/api.html](http://www.expressjs.com.cn/4x/api.html))。
