## $scope 多控制器单独作用域

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<script type="text/javascript" src="angular.min.js"></script>
</head>
<body>
<div ng-app="myApp">
<div ng-controller="firstController">
{{name}}
</div>
<div ng-controller="secondController">
{{name}}
</div>
</div>
<script type="text/javascript">
var app = angular.module("myApp", []);
app.controller('firstController',function($scope){
$scope.name='张三';
});
app.controller('secondController',function($scope){
$scope.name='李四';
})
</script>
</body>
</html>
```

## $rootScope 服务

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
<div ng-controller="firstController">
姓名： {{name}} <br>
年龄： {{age}}
</div>
<div ng-controller="secondController">
姓名： {{name}}
年龄： {{age}}
</div>
</div>
<script type="text/javascript">
var app = angular.module("myApp", []);
app.controller('firstController',function($scope,$rootScope){
$scope.name='张三';
$rootScope.age='30';
});
app.controller('secondController',function($scope){
$scope.name='李四';
})
</script>
</body>
</html>
```

## 控制器继承

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
<div ng-controller="firstController">
{{name}}
{{age}}
{{sex}}<div ng-controller="secondController">
{{name}}
{{age}}
{{sex}}
</div>
</div>
</div>
<script type="text/javascript">
var app = angular.module("myApp", []);
app.controller('firstController',function($scope){
$scope.name='张三';
$scope.age='40';
});
app.controller('secondController',function($scope){
$scope.name='李四';
$scope.sex='男';
})
</script>
</body>
</html>
```

## 依赖注入中代码压缩的问题

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
<div ng-controller="firstController">
{{name}}
{{age}}
{{sex}}<div ng-controller="secondController">
{{name}}
{{age}}
{{sex}}
</div>
</div>
</div>
<script type="text/javascript">
var app = angular.module("myApp", []);
app.controller('firstController',['$scope',function($scope){
$scope.name='张三';
$scope.age='40';
}]);
app.controller('secondController',['$scope',function($scope){
$scope.name='李四';
$scope.sex='男';
}])
</script>
</body>
</html>
```

## Angularjs 模块的 run 方法

run 方法初始化全局的数据 ,只对全局作用域起作用 如$rootScope

<script type="text/javascript">
var m1 = angular.module('myApp',[]);
m1.run(['$rootScope',function($rootScope){
$rootScope.name = 'hello';
}]);
console.log( m1 );
</script>