title: ionic打包问题

tags: [ionic,cordova]
-----------------------------

### Xcode7打包遇到问题：

1、如果打包后APP不能访问远程服务器，则添加以下属性

> 原因其实这是苹果加大安全的管控，将以往HTTP协议强制改为HTTPS协议

```
NSAppTransportSecurity 类型 Dictionary Dictionary
添加 NSAllowsArbitraryLoads 类型 Boolean ,值设为 YES
```

<!-- more -->

2、提示CDVViewController.h file not found.

```
Build Settings 选项
搜索 Header Search ,Header Search Paths添加
"$(OBJROOT)/UninstalledProducts/$(PLATFORM_NAME)/include"
```

3、提示Undefined symbols for architecture arm64等错误.

```
Build Settings 选项
搜索 dead, Dead Code Stripping(去除死代码选项)
改为No
```

4、Xcoede provisioning prifles需要手动删除

```
com+shift+g，输入以下路径
~/Library/MobileDevice/Provisioning Profiles
```
