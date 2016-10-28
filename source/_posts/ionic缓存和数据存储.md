title: ionic缓存和数据存储

tags: [ionic,cordova]
---------------------

**1、ionic图片缓存**

可采用方法:

1.图片转base64存本地缓存或数据库;

2.通过[file](http://ngcordova.com/docs/plugins/file/)、[file transfer](http://ngcordova.com/docs/plugins/fileTransfer/)、[device](http://ngcordova.com/docs/plugins/device/)插件，把文件下载到app内。

3.通过[imgcache.js](https://github.com/chaddjohnson/imgcache.js)使用html5文件存储到本地，可选择和[angular-imgcache.js](https://github.com/jBenes/angular-imgcache.js)结合使用效果更佳。

> 注意打包到手机上需要仔细阅读[cordova.md](https://github.com/chaddjohnson/imgcache.js/blob/master/CORDOVA.md)

**2、ionic数据缓存**

可采用方法:

<!-- more -->

1、通过html5离线存储如（localstorage、sessionstroage）等方式,websql目前还没测试过。

2、通过[sqlLite](http://ngcordova.com/docs/plugins/sqlite/)插件存储到手机自带数据库。

可参考文档

[PouchDB](https://pouchdb.com/api.html#overview)api

[ionic 通过PouchDB ＋ SQLite来实现app的本地存储（Local Storage）](http://www.cnblogs.com/ailen226/p/ionic.html)

[How To Use PouchDB + SQLite For Local Storage In Your Ionic App](http://gonehybrid.com/how-to-use-pouchdb-sqlite-for-local-storage-in-your-ionic-app/)
