## $apply 方法作用：

Scope 提供$apply 方法传播 Model 的变化

## $apply 方法使用情景：

AngularJS 外部的控制器（ DOM 事件、外部的回调函数如 jQuery UI 空间等）调用了 AngularJS 函数之后，必须调用$apply。在这种情况下，你需要命令 AngularJS 刷新自已（模型、视图等）， $apply 就是用来做这件事情的

## $apply 方法注意事项：

只要可以，请把要执行的代码和函数传递给$apply 去执行，而不要自已执行那些函数然后再调用$apply。例如，你应该像下面这样来执行你的代码：

```html
<script type="text/javascript">
var app = angular.module("myApp", []);
app.controller('firstController',function($scope){
$scope.name = 'hello';
setTimeout(function(){
//$scope.name = 'hi';
$scope.$apply(function(){$scope.name = 'hi';
});
},2000);
/*$timeout(function(){
$scope.name = 'hi';
},2000);*/
$scope.show = function(){
$scope.name = 'hi 点击事件发生了';
};
});
</script>
```

## $watch 方法作用：

$watch 方法监视 Model 的变化。

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<script type="text/javascript" src="../angular.min.js"></script>
</head>
<body>
<div ng-app="myApp">
<div ng-controller="CartController">
<p>价格:<input type="text" ng-model="iphone.money"></p>
<p>个数:<input type="text" ng-model="iphone.num"></p>
<p>费用:<span>{{ sum() | currency:'￥' }}</span></p>
<p>运费:<span>{{iphone.fre | currency:'￥'}}</span></p>
<p>总额:<span>{{ sum() + iphone.fre | currency:'￥'}}</span></p>
</div>
</div>
<script type="text/javascript">
var app = angular.module("myApp", []);app.controller('CartController',function($scope){
$scope.iphone = {
money : 5,
num : 1,
fre : 10
};
$scope.sum = function(){
return $scope.iphone.money * $scope.iphone.num;
};
/*$scope.$watch('iphone.money',function(newVal,oldVal){
console.log(newVal);
console.log(oldVal);
},true);*/
$scope.$watch($scope.sum,function(newVal,oldVal){
//console.log(newVal);
//console.log(oldVal);
$scope.iphone.fre = newVal >= 100 ? 0 : 10;
});
});
</script>
</body>
</html>
```