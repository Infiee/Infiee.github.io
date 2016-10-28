title: ionic调用原生页面切换动画

tags: [ionic,cordova]
---------------------

使用ionic一段时间，发现在ionic内使用$state.go()这个方法切换路由，会出现页面切换方向出错的问题。所以尝试找资料，找了好久发现无果...

后来偶尔看到[ionic-native-transitions](https://github.com/shprink/ionic-native-transitions) 这个插件，本地尝试了下，发现效果不错，还可以禁用ionic自带的页面切换动画，看简介貌似android只支持左右切换，上下和翻转不支持（没测试过）。

下面跟着github主页介绍一步一步走：

**1.首先下载js插件到本地,我采用bower的安装方式**

> bower install shprink/ionic-native-transitions

<!-- more -->

然后插入

```
<script src="./PathToBowerLib/dist/ionic-native-transitions.min.js"></script>
```

**2.下载cordova插件**

```
# Using Cordova
cordova plugin add https://github.com/Telerik-Verified-Plugins/NativePageTransitions#0.6.2

# Using Ionic CLI
ionic plugin add https://github.com/Telerik-Verified-Plugins/NativePageTransitions#0.6.2
```

> 在ios9系统可能会出现闪烁，防止这种情况，接着添加插件

```
# Using Cordova
cordova plugin add cordova-plugin-wkwebview

# Using Ionic CLI
ionic plugin add cordova-plugin-wkwebview
```

> 如果android添加了的Crosswalk版本大于1.3 ,需要在config.xml内添加一行配置。

```
<preference name="CrosswalkAnimatable" value="true" />
```

**3.在ionic内配置切换动画**

```
angular.module('yourApp', [
    'ionic-native-transitions'
]);
```

设置默认动画

```
.config(function($ionicNativeTransitionsProvider){
    $ionicNativeTransitionsProvider.setDefaultTransition({
        type: 'slide',
        direction: 'left'
    });
});
```

设置默认返回动画

```
.config(function($ionicNativeTransitionsProvider){
    $ionicNativeTransitionsProvider.setDefaultBackTransition({
        type: 'slide',
        direction: 'right'
    });
});
```

开启native动画，关闭ionic动画

```
$ionicNativeTransitions.enable(true);
```

**4.使用方法**

```
设置动画
.state('home', {
    url: '/home',
    nativeTransitions: {
        "type": "flip",
        "direction": "up"
    }
    templateUrl: "templates/home.html"
})
或不设置动画
.state('home', {
    url: '/home',
    nativeTransitions: null,
    templateUrl: "templates/home.html"
})
```

> 使用<ion-nav-back-button> 指令默认使用返回页面切换动画

更多api可参考

https://github.com/shprink/ionic-native-transitions
