title: hexo搭建部署及简单用法

tags: hexo
----------

欢迎来到 [Hexo](http://hexo.io/)! 它一个静态博客，相关API可以点击 [documentation](http://hexo.io/docs/) 查询.

快速开始，搭建本地hexo
----------------------

1、安装Node.js，[Node.js下载](https://nodejs.org/en/).

2、安装Git,[Git客户端](https://desktop.github.com/).记得勾选添加环境变量的选项,不然就自己配置环境变量.

3、安装hexo

<!-- more -->

```
    npm install hexo-cli -g
    npm install hexo --save

    # 如果命令无法运行，可以尝试更换taobao的npm源
    npm install -g cnpm --registry=https://registry.npm.taobao.org

    # 创建Hexo文件夹
    # 安装完成后，根据自己喜好建立目录（如E:\kuaipan\GitHub\hexo）

    hexo init

    # 安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
    $ hexo init <folder>
    $ cd <folder>
    $ npm install

    # 新建完成后，指定文件夹的目录如下
    .
    ├── _config.yml
    ├── package.json
    ├── scaffolds
    ├── scripts
    ├── source
    |      ├── _drafts
    |      └── _posts
    └── themes

    # 安装Hexo插件,部署到Git
    npm install hexo-deployer-git --save

    # 开启hexo服务
    hexo server

```

4、部署静态网页到GitHub

```
# 登录GitHub，注册自定义用户名如apple

# 在主页右下角创建New repository，name必须和用户名一致如apple.github.io
# (参考资料：https://pages.github.com/)

# 打开Github客户端，clone在Github上新建的资源库

# 配置本地hexo博客,_config.yml
#（具体配置参考：https://github.com/Infiee/infiee.github.io/tree/SourceCode）

url: http://infiee.github.io/
root: /

deploy:
  type: git
  repo: https://github.com/Infiee/infiee.github.io
  branch: master

# 配置完成后,发布静态博客到github仓库
hexo clean
hexo g
hexo d

```

### 创建一篇新文章

```bash
$ hexo new "My New Post"
```

相关介绍: [Writing](http://hexo.io/docs/writing.html)

### 运行服务

```bash
$ hexo server
```

相关介绍: [Server](http://hexo.io/docs/server.html)

### 生成静态文件

```bash
$ hexo generate
可以简写为hexo g
```

相关介绍: [Generating](http://hexo.io/docs/generating.html)

### 部署到远程站点

```bash
$ hexo deploy
可以简写为hexo d
```

相关介绍: [Deployment](http://hexo.io/docs/deployment.html)
