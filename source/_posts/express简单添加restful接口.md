title: express简单添加restful接口数据

tags: [node.js,express]
-----------------------

**准备工作**

1.安装express generator到全局,然后下载初始化项目到本地

```
npm install express-generator -g

express myapp

cd myapp

npm install

DEBUG=myapp:* npm start
```

2.myapp目录下添加model文件夹，并新建comments.js文件,代码如下：

<!-- more -->

```
exports.comments = [
    { author : '小明', text : "Nothing is impossible, the word itself says 'I'm possible'!"},
    { author : '小强', text : "You may not realize it when it happens, but a kick in the teeth may be the best thing in the world for you"},
    { author : '小兵', text : "Even the greatest was once a beginner. Don't be afraid to take that first step."},
    { author : '拉登', text : "You are afraid to die, and you're afraid to live. What a way to exist."}
];

```

3.routes目录下添加comment.js（只是测试，名字你高兴就好）,代码如下：

```
/*
 * GET comments listing.
 */

var comments = require('../model/comments').comments;

exports.list = function(req, res){
  res.json(comments);
};

exports.get = function(req, res){
   if(comments.length <= req.params.id || req.params.id < 0) {
    res.statusCode = 404;
    return res.send('Error 404: No comment found');
  }
  var q = comments[req.params.id];
  res.json(q);
};


exports.delete = function(req, res){
  if(comments.length <= req.params.id) {
    res.statusCode = 404;
    return res.send('Error 404: No comment found');
  }

  comments.splice(req.params.id, 1);
  res.json(true);
};


exports.update = function(req, res){
  res.setHeader('Content-Type', 'application/json;charset=utf-8');
  for(var i=0;i<comments.length;i++){
    if(comments[i].author==req.body.author){
      comments[i] = req.body;
      res.send({status:"success", message:"update comment success"});
      console.log(comments);
    }
  }

};


exports.add = function(req, res){
  if(!req.body.hasOwnProperty('author') ||
     !req.body.hasOwnProperty('text')) {
    res.statusCode = 400;
    return res.send('Error 400: Post syntax incorrect.');
  }

  var newComment = {
    author : req.body.author,
    text : req.body.text
  };

  comments.push(newComment);
  res.json(true);
};

```

4.修改app.js

添加

```
var comment = require('./routes/comment');

app.use('/comments',comment.list );
```

5.重新启动node服务

> ctrl+c停止命令并重启服务DEBUG=myapp:* npm start

访问 http://localhost:3000/comments 就可以访问到模拟的接口数据
