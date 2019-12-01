# AngularJS

基于JavaScript开发的客户端应用框架；

Google的很多项目就使用了这个框架；

angular适合CRUD应用和SPA单页面网站开发。

适合频繁的前后端数据交换，不适合界面优化。

[教程](https://www.angularjs.net.cn/tutorial/)

AngularJS应用引导过程的3个重要点：

 - 注入器将用于创建词应用程序的依赖注入（dependency injection）

# AngularJS--PhoneCat

[教程](https://www.angularjs.net.cn/phonecat/)

# AngularJS种子项目--angular-seed

[教程](https://www.angularjs.net.cn/angular-seed)

	node_moduels:项目需要的npm工具包；
	app/bower_components:angular的框架文件；

# angular的两种测试

## 单元测试

使用Karma测试运行器运行它，默认的Karma文件运行它；

 -`karma.conf.js`查看单元测试的配置；
 -每个运行的代码下有一个对应的单元测试代码`..._test.js`;

执行单元测试：

	npm test

运行简单单元测试后退出；

	npm run test-single-run

## 端对端的测试

使用Protractor端对端运行器运行端对端的测试脚本，

 -可以在`e2e-tests/protractor-conf.js`查看端对端的测试配置；
 -运行`e2e-tests/scenarios.js`进行端对端的测试；

首先打开服务器，以便`Protractor`能与它互动：

	npm start

运行`Protractor`需要先安装`WebDriver`：

	npm run update-webdriver

web服务器环境运行起来了，`WebDriver`更新过了，进行端对端的测试：

	npm run protractor

# angularjs的特性

 - MVC模式
 - 模块系统
 - 指令系统
 - 依赖注入
 - 双向数据绑定

# MVC模式

model:主要是数据；

view:视图，将数据显示在桌面上

controller:控制器，联系model和view；

[demo](demo/01-MVC模式.html):这个例子中用的angularjs是1.3.0以下的版本！

# $scope的作用域

上面的例子中的`name`挂载到了`$scope`上;

controller会定义一个作用域，这个作用域就是函数的`scope`，`scope`是一个局部作用域；

`rootscope`是一个全局作用域，全局作用域下就是`scope`；

`ng-controller`在访问变量时，会先在指定的作用域中查找，然后向上查找，最后才到全局作用域中查找

局部作用域`scope`还可以向下继续分别配更小的作用域；

# 依赖注入

**$scope形参不能被修改**：angularjs规定了参数的名称，函数会根据参数的名称将依赖注入到函数中；

# 指令系统

**ng-app**:angularjs的作用域，可以写在任意地方；写在html标签中，就会让它作用域整个html页面中。

**ng-controller**:控制器，用于绑定数据(model)和视图(view).

# 双向数据绑定

## MVVM:

数据->视图/视图->数据；数据改变会影响视图，视图改变会影响数据。

[demo](demo/02-数据的双向绑定.html)

**M->V**:

注意：

原生定时器`setTimeout`不会刷新视图，所以我们需要注入angular中提供的定时器`$timeout`;

还可以使用**ng-click**指令，改变视图；

除了`ng-click`其他原生的事件angular中也有；

**V->M**:

使用**ng-model**指令，在视图上绑定数据，实现改变视图时影响数据；

[例子:购物金额计算](demo/03-购物金额计算.html)

**过滤器**

帮助我们进行一些常用的数据操作

	currency:"￥"；//格式化货币数据，默认是$;

**监听器**

监听相关数据的变化：

	$scope.$watch(parameter,function(newValue,oldValue)[,true]);

parameter:被监听的对象,可以是变量、对象、函数；

function:回调函数；

true:第三个参数可选，表示监听的深度；如果不填，只能监听单个值，true表示监听整个对象；

newValue:改变后的值；

oldValue:改变前的值；

# 模块化

减小全局的污染，和命名冲突；

能让模块之间实现依赖；

在之前的[demo](demo/01-MVC模式.html)中，函数定义在了全局的js环境下，很容易与其他函数产生冲突！

**解决方法，实现模块化**：

	angular.module('myApp',[]);

anguler:是angularjs中的访问接口，类似于JQuery中的`$`;

module:是angular中的方法，用于创建模块

'myApp':是module方法的第一个参数，是当前创建的模块的名字；

[]:第二个参数是一个数组，当前模块所要**依赖**的其他模块；

当指定了模块后，之前在html标签中添加的`ng-app`指令就要去指定具体的模块名称；

	ng-app='模块的名字';

对之前的demo进行模块化:[demo](demo/04-模块化.html)

**压缩问题**

当使用工具对js代码压缩时，会改变函数的参数，比如`$scope`；这就违背了angularjs**依赖注入**的原则；

解决办法：

angular提供了一种写法，将函数改写程数组的方式:

	m1.controller('fn1',['$scope',function($s){
		$s.name='hi angular'
	}]);

# 工具方法

[demo](demo/05-工具方法.html)

## angular.bind()

与JQuery中的`$.proxy()`类似：用于改变this的指向；

	angular.bind(thisArg,arg);

thisArg:this的当前指向；

arg:调用的对象；如果是函数：

	angular.bind(thisArg,fn,arg1)(arg1);//传参的方式由几种

## angular.copy()

拷贝对象的方法：

	var c=angular.copy(a,b);//b也变成了a对象，a覆盖了所有的值

## angular.extend()

对象继承：

	var d=angular.extend(b,a);//拥有了a的属性和b的属性
	
## 与判断相关的工具方法

	angular.isArray//判断是否是数组
	angular.isDate//判断是否是日期对象
	angular.isDefined//判断元素是否定义
	angular.isUndefined//判断是否是未定义
	angular.isFunction//判断是否是Function对象（函数）
	angular.isNumber
	angular.isObject
	angular.isString
	angular.isElement//判断是否是一个元素


