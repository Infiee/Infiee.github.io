title: angular实现checkbox单选和取消

tags: [angular,javascript]
--------------------------

template:

```
<form novalidate>
	选择名字:{{chooseArr}}
    <ion-list>
    	<ion-checkbox ng-model="checkItem" ng-repeat="item in checkGroup" ng-click="chooseItem(item,checkItem)">
    		{{item}}
    	</ion-checkbox>
    </ion-list>
    <a class="common-button"
       ng-click="getCheckBox()"
       ng-disabled="!checkStatus"
       ng-class="{true:'btn-disable',false:'btn-enable'}[!checkStatus]"
       style="margin-top:15px;">
    		点击
    </a>
</form>
```

<!-- more -->

controller:

```
$scope.checkGroup = ['中国','印度','澳大利亚','马来西亚'];
$scope.chooseArr = [];
$scope.checkStatus = false;
var str='';

$scope.chooseItem=function(item,checkItem){
   if (checkItem == true) {
       //选中
       str = str + item + ',';
       $scope.checkStatus = true;
   } else {
       //取消选中
       str = str.replace(item + ',','');
   }
   $scope.chooseArr=(str.substr(0,str.length-1)).split(',');
   //如果选中小于1或数组第一个为空则禁用按钮
   if($scope.chooseArr.length<1||$scope.chooseArr[0]==''){
       console.log('按钮已被禁用');
       $scope.checkStatus = false;
   }
};

$scope.getCheckBox = function () {
   // 选择checkbox的时候已经禁用按钮,故这里不需要再次判断
   console.log($scope.chooseArr);
};
```
