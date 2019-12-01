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
