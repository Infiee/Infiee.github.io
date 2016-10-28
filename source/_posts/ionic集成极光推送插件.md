title: ionic集成极光推送插件

tags: [ionic,cordova]
---------------------

相关链接：

[极光推送官网](https://www.jpush.cn/)

[极光推送github主页](https://github.com/jpush/jpush-phonegap-plugin)

[相关api](https://github.com/jpush/jpush-phonegap-plugin/blob/master/document/Common_detail_api.md)

**准备工作**

1.添加极光推送插件和device插件,API_KEY为极光推送官网申请。

<!-- more -->

> cordova plugin add https://github.com/jpush/jpush-phonegap-plugin.git --variable API_KEY=your_jpush_appkey
>
> cordova plugin add https://github.com/apache/cordova-plugin-device.git

2.拷贝plugin目录的极光推送插件到项目根目录下，并修改以及删除plugin目录下的极光推送插件。

> 修改根目录极光推送插件(cn.jpush.phonegap.JPushPlugin)文件夹下src/android/JPushPlugin.java，大概第十行，修改import youpackge.R为 import cn.kigsir.jpushdemo.R

3.添加platform

然后添加根目录下的修改好的极光推送插件

> cordova plugin add cn.jpush.phonegap.JPushPlugin

4.修改ionic目录app.js,启用极光推送。

添加到$ionicPlatform.ready(function() {})方法内

```
$ionicPlatform.ready(function() {
document.addEventListener("deviceready", function () {
       //启动极光推送服务

         window.plugins.jPushPlugin.init();

         //调试模式

         window.plugins.jPushPlugin.setDebugMode(true);

         //接收消息并跳转相应的页面
         window.plugins.jPushPlugin.openNotificationInAndroidCallback = function (data) {
             var obj = JSON.parse(data);
             console.log(obj);
             var id = obj.extras['cn.jpush.android.EXTRA'].id;
             // $state.go('appealDetail', {appealid: id});
             alert(id);
         }
         alert('ready...');
         })
})
```

5.前往[极光推送官网](https://www.jpush.cn/)配置推送消息，如果不出错，手机应该会提示有推送消息了。

ps.但同时会提示统计缺少统计代码

不让提示的方法如下：

> 找到platforms/androdi/src/(你的app包名)/CordovaApp.java或activity.java文件，添加如下代码,并在public class CordovaApp extends CordovaActivity上面导入接口代码，import cn.jpush.android.api.JPushInterface;

```
@Override
protected void onResume() {
    super.onResume();
    JPushInterface.onResume(this);
}
@Override
protected void onPause() {
    super.onPause();
    JPushInterface.onPause(this);
}
```

接着运行ionic run android --deivce，再去添加推送消息就不会出现缺少统计代码的提示信息了。
