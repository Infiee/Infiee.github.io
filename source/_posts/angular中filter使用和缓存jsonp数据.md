title: angular中filter使用和缓存jsonp数据

tags: [angular,javascript]
--------------------------

angular缓存jsonp数据:

> 参考自：https://www.chedanji.com/angularjs-cache-for-jsonp/

```
angular.module('app',[])
.factory("myCache", function($cacheFactory){
    return $cacheFactory("me");
})
.controller("AppCtrl", function($http, myCache){
    var app = this;
    app.load = function(){
        $http.get("apiurl",{cache:myCache})
        .success(function(data){
        app.data = data;
        })
    }
    app.clearCache = function(){
        myCache.remove("apiurl");
    }
})
```

<!-- more -->

$filter使用方法:

```
$filter('filter')(objData, { $: n });
```
