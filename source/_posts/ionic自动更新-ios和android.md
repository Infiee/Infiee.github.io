title: ionic自动更新(ios和android)

tags: [ionic,cordova]
---------------------

### 首先，感谢分享本篇技术文档的作者，

> 以下文档整理自https://www.bestguy.net/2015/11/05/关于ionic的版本升级，只升级www部分

**背景：**

ionic官方有介绍如何更新、回滚等，但deploy服务器在国外,故不翻墙大多数时候是无法下载的，故需要自己搭建本地服务器。

参考官方文档：http://docs.ionic.io/docs/deploy-overview

**ionic自动更新：**

讲下原理，ionic内部也是cordova的，在android平台下，他的webview默认加载assert下边的www里边的内容，我们更新的时候，通过native android 把更新包下载下来，解压到 data/data/xx.xx/www里边，然后用cordova的 webView.loadUrlIntoView 直接把新的版本载入，升级完成。

<!-- more -->

**操作步骤：**

1、这两个文件下载好，放到www/js 里边，在index.html 的之前，引入这两个js

这个是deploy依赖的ionic核心组件(修改自官方版)

> https://raw.githubusercontent.com/lngjy/ionic-service-core-private/master/ionic-core.js

deploy的组件(修改自官方版)

> https://raw.githubusercontent.com/lngjy/ionic-service-deploy-private/master/ionic-deploy.js

2、安装deploy插件

deploy插件（修改自官方版）

> cordova plugin add https://github.com/lngjy/ionic-plugin-deploy-private.git

3、app.js 部分：

angular.module 里边加入 'ionic.service.deploy','ionic.service.core'

这两个依赖.config 部分 ， 注入 $ionicAppProvider

```
$ionicAppProvider.identify({
//这个应用的标识
app_id: 'xc02',
//生产环境的域名
domain: 'http://www.bestguy.net',
//生产环境
channel_tag: 'prod'
});
```

4、检查更新：

检测升级实际上是post数据到 http://www.bestguy.net/update/check/xc02（根据自身服务器地址情况修改） 上边，json 格式如下

```
//device_app_version：这个是app自己的version，在config.xml 里边配置;
//device_deploy_uuid：这个是升级的uuid，理论上和你的最新版本保持一致，或者你自己定这个版本，具体怎么回事，下边会说;
//device_platform：这个android和ios channel_tag 这个是标志是哪个环境用的。
{
"device_app_version":1.0,
"device_deploy_uuid":1.0,
"device_platform":"android",
"channel_tag":"production"
}
```

好了。 这个post到服务器，服务器需要处理这个数据， 如果从来没更新过， 那么device_deploy_uuid这个会传NO_DEPLOY_AVAILABLE过去，表示客户端从来没升级过，这个时候，需要判断device_app_version这个版本。

好了，我们返回构造数据

```
//compatible_binary 和 update_available 都是true 的时候，就会下载更新。
//如果安装成功，下次就会给服务器传这个uuid的版本，所以，一定要自己搞明白对应关系，推荐和版本一致。
//url 是下载包的位置，相对路径哦，相对于你服务器路径如：http://baidu.com/test/www.zip
{
'compatible_binary': true,
'update_available': true,
'update':
      {
        'uuid': '1.0.3',
        'url': '/test/www.zip'
      }
}
```

写好了代码之后，压缩www目录下的所有文件（ps:不要压缩www,是www里面的所有文件)

```
ionic platform add android
ionic build android
cd platforms/android/assets/www
zip -r www.zip *
```

5.添加升级检测部分代码：

```
.factory("versionUpdateService", function (
        $ionicPopup,
        $ionicDeploy,
        $timeout,
        $ionicLoading) {
            var version ;
            /**
            * 获得version
            */
            function getAppVersion() {
               $ionicDeploy.info().then(function (data) {
                   var binaryVersion = data.binary_version;
                   var deployUuid = data.deploy_uuid;
                   version =  deployUuid != 'NO_DEPLOY_AVAILABLE' ? deployUuid : binaryVersion;
               });
            }

            /**
            * 检查更新
            */
            function checkUpdate() {
               $ionicLoading.show({
                   template: '正在检查更新...',
                   animation: 'fade-in',
                   showBackdrop: true,
                   duration: 3000,
                   showDelay: 0
               });

               $ionicDeploy.check().then(function (hasUpdate) {

                   if (hasUpdate) {
                       showUpdateConfirm();
                   } else {
                       $ionicLoading.show({
                           template: '恭喜你,你的版本已经是最新!',
                           animation: 'fade-in',
                           showBackdrop: true,
                           duration: 2000,
                           showDelay: 0
                       });
                   }
               }, function (err) {
                   $ionicLoading.show({
                       template: '更新失败,请检查您的网络配置!' + err,
                       animation: 'fade-in',
                       showBackdrop: true,
                       duration: 2000,
                       showDelay: 0
                   });

               });
            }

            function init() {
            }

            function showUpdateConfirm() {
               $ionicLoading.hide();
               var confirmPopup = $ionicPopup.confirm({
                   title: '版本升级',
                   template: "有新的版本了,是否要升级?",
                   cancelText: '取消',
                   okText: '升级'
               });
               confirmPopup.then(function (res) {
                   $ionicLoading.show({
                       template: '正在更新...',
                       animation: 'fade-in',
                       showBackdrop: true,
                       //duration: 2000,
                       showDelay: 0
                   });

                   if (res) {
                       $ionicDeploy.update().then(function (res) {
                           $ionicLoading.hide();
                           $ionicLoading.show({
                               template: '更新成功!',
                               animation: 'fade-in',
                               showBackdrop: true,
                               duration: 2000,
                               showDelay: 0
                           });
                       }, function (err) {
                           $ionicLoading.hide();
                           $ionicLoading.show({
                               template: '更新失败!' + err,
                               animation: 'fade-in',
                               showBackdrop: true,
                               duration: 2000,
                               showDelay: 0
                           });
                       }, function (prog) {
                           $ionicLoading.show({
                               template: "已经下载：" + prog + "%"
                           });
                           if (downloadProgress > 99) {
                               $ionicLoading.hide();
                           }
                       });
                   } else {
                       $ionicLoading.hide();
                   }
               });
            };

            return {
               init: function () {
                   getAppVersion();
               },

               getVersion: function () {
                   return version;
               },

               checkUpdate: function () {
                   checkUpdate();
               },

               update: function () {
                   update();
               }
            }
})
```

> 发现原作者博客打不开，补上另一个博主链接 http://www.scaperow.com/133
