title: react-native学习中遇到的问题

tags: [question,react-native]
-----------------------------

### Xcode7打包遇到问题：

1、General

> 如果有安装手势插件，需要添加QuartzCore.framework

```
|--General
    |--Linked Frameworks and Libraries 添加QuartzCore.framework
```

2、如果打包后APP不能访问远程服务器，则添加以下属性

> 原因其实这是苹果加大安全的管控，将以往HTTP协议强制改为HTTPS协议

```
NSAppTransportSecurity 类型 Dictionary Dictionary
添加 NSAllowsArbitraryLoads 类型 Boolean ,值设为 YES
```

<!-- more -->

3、提示CDVViewController.h file not found.

```
Build Settings 选项
搜索 Header Search ,Header Search Paths添加
"$(OBJROOT)/UninstalledProducts/$(PLATFORM_NAME)/include"
```

4、提示Undefined symbols for architecture arm64等错误.

```
Build Settings 选项
搜索 dead, Dead Code Stripping(去除死代码选项)
改为No
```

5、Xcoede provisioning prifles需要手动删除

```
com+shift+g，输入以下路径
~/Library/MobileDevice/Provisioning Profiles
```
