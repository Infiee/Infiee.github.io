title: cordova文件上传/下载

tags: cordova
-------------

1、[file](http://ngcordova.com/docs/plugins/file/) 文件系统

> 文件系统相关资料参考apihttps://github.com/apache/cordova-plugin-file
>
> cordova.file.applicationDirectory app程序目录
>
> cordova.file.applicationStorageDirectory app程序沙盒目录
>
> cordova.file.cacheDirectory 缓存目录
>
> cordova.file.tempDirectory临时文件目录

2、[file Transfer](http://ngcordova.com/docs/plugins/fileTransfer/) 文件传输（下载/上传）

<!-- more -->

> 下载文件，命名本地相同路径文件名，本地文件可以被覆盖
>
> ionic下载文件，切换视图，不会打断文件后台下载

```
document.addEventListener('deviceready', function () {

  var url = "http://cdn.wall-pix.net/albums/art-space/00030109.jpg";
  var targetPath = cordova.file.documentsDirectory + "testImage.png";
  var trustHosts = true;
  var options = {};

  $cordovaFileTransfer.download(url, targetPath, options, trustHosts)
    .then(function(result) {
      // Success!
    }, function(err) {
      // Error
    }, function (progress) {
      $timeout(function () {
        $scope.downloadProgress = (progress.loaded / progress.total) * 100;
      });
    });

 }, false);
```

3、[fileOpener2](http://ngcordova.com/docs/plugins/fileOpener2/) 文件打开（可以打开apk、zip文件等）

> 以上三种插件组合，可以实现文件下载、上传（图片上传等）、android自动更新等功能
