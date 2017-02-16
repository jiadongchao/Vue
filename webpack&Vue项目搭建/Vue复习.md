---
title: Vue基础复习
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---
 * `Vue.js`是什么?
	* 一位华裔前`Google`工程师开发的前端js库，是一个构建数据驱动的web界面的库。
	* `Vue.js `的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。
    * 与`angular.js`类似的是声明式开发，但性能高于`angular`，体积小很多, 比较适合移动端开发
    * 它本身不是全能框架, 只关注UI, 如果需要`router/ajax`, 可以使用对应插件或使用别的库来实现。(关于`ajax`可以参见本人的Ajax总结)
    ![enter description here][1]
	![enter description here][2]
* `vue`包含一系列的扩展插件:
	* `vue-router`
	* `vue-resource`
	* `vue-cli`
	* `vuex`
* 基本使用
	* 引入`vue.js`
	* 创建Vue对象, 指定选项对象
		* `el` : 指定dom标签容器的选择器
		* `data` : 指定初始化状态属性数据的对象
		        对象/函数(返回一个对象)
	* 页面中
		* 使用`v-model`: 实现双向数据绑定(`Vue`实例对象就是`viewModel`)
		* 使用`{{}} `; 显示数据
### Vue对象的选项

	

* 扩展数组
	* `$remove(item)` : 删除数组中对应的元素
	* `$set(index, ele) `: 给数组中指定下标指定对应的元素 

* 页面指令
	* `v-text/v-html`: 指定标签体
		* `v-text` : 当作纯文本
		* `v-html` : 将`value`作为`html`标签来解析
	* `v-if v-else v-show`
		* `v-if` : 如果`vlaue`为`true`, 当前标签会输出在页面中
		* `v-else` : 与`v-if`一起使用, 如果`value`为`false`, 将当前标签输出到页面中
		* `v-show`: 就会在标签中添加`display`样式, 如果`vlaue`为`true`, `display=block`, 否则是`none`
		* 如果需要频繁切换 `v-show` 较好，如果在运行时条件不大可能改变 `v-if `较好
		* 切换多个元素不可以用`v-show`
	* `v-for `: 遍历
		* 遍历数组 : `v-for="person in persons"`   `$index`
		* 遍历对象 : `v-for="value in person" `  `$key`
	* `v-on` : 绑定事件监视
		* `v-on`:事件名, 可以缩写为: @事件名
		* 监视具体的按键: `@keyup.keyCode`   `@keyup.enter`
		* 阻止事件的冒泡和事件默认行为: `@click.stop`   `@click.prevent`
		* 隐含对象: `$event`
	* `v-bind` : 强制绑定解析表达式  
		* 很多属性值是不支持表达式的, 就可以使用`v-bind`
		* 可以缩写为: ` :id='name'`
		* `:class`
			* `:class="{classA : isA, classB : isB}"`
			* `:class="[classA, classB]"`
		* `:style`
			`:style="{color : color}"`
	* `v-model`
		* 双向数据绑定
	* `v-el` : 标识某个标签
		* `v-el:xxx`
		* 读取得到标签对象: `this.$els.xxx`
	* `v-text` :避免页面闪现表达式文本
	* `v-cloak` : 避免页面闪现表达式文本
		* 样式: `[v-cloak] { display: none }`
* 过滤器
    * 内置
        1. `capitalize` : 首字母大小
        2. `uppercase` : 全部大写
        3. `lowercase` : 全部小写
        4. `currency` : 货币化
        5. `pluralize` : 单数/复数处理
        6. `json` : `json`格式化
    
        7. `limitBy` : 限定数组的部分元素(下标)
        8. `filterBy` : 限定数组的部分元素(值)
        9. `orderBy` : 对数组进行排序
    * 自定义
        1. 全局过滤器
         
				Vue.filter('过滤器名', function(value, xxx, yyy) {
					//处理逻辑
					return result;
				});
        2. 局部过滤器
         
				new Vue({
					filters : {
						'过滤器名' : function(value, xxx, yyy) {
							//处理逻辑
							return result;
						}
					}
				})
* 指令
    * 内置
        `v:text` : 更新元素的 `textContent` 
        `v-html` : 更新元素的 `innerHTML`
        `v-if` : 如果为`true`, 当前标签才会输出到页面
        `v-else`: 如果为`false`, 当前标签才会输出到页面
        `v-show` : 通过控制`display`样式来控制显示/隐藏
        `v-for` : 遍历数组/对象
        `v-on` : 绑定事件监听, 一般简写为`@`
        `v-bind` : 强制绑定解析表达式, 可以省略`v-bind`
        `v-model` : 双向数据绑定
        `v-el` : 为某个元素注册一个唯一标识, `vue`对象通过`$els`属性访问这个元素对象
        `v-cloak` : 使用它防止闪现表达式, 与`css`配合:` [v-cloak] { display: none }`
    * 自定义
        1. 注册全局指令
         
				Vue.directive('my-directive', function(value){
					this.el.innerHTML = value.toUpperCase();
				})
        2. 注册局部指令
        
				directives : {
					'my-directive' : function(value) {
						this.el.innerHTML = value;
					}
				}
        3. 使用指令:
           ` v-my-directive='xxx'`
*  绑定监听:
	*  `v-on:xxx="fun"`
	*   `@xxx="fun"`
	*   `@xxx="fun(参数)"`
	*   隐含属性对象: `$event`			
* 事件修饰符:
	* `.prevent` : 阻止事件的默认行为 `event.preventDefault()`
	* `.stop` : 停止事件冒泡 `event.stopPropagation()`
* 按键修饰符
	* `.keycode` : 操作的是某个`keycode`值的健
	* `.enter` : 操作的是`enter`键
* 生命周期：  `data`创建早于所有事件，所以在以下生命周期中都可以使用`data`中的数据
	* `created`            =>   用的最多，一般做准备工作。例如发送ajax
	* `beforeCompile`          =>  编译模板之前
	* `compiled`         =>  编译模板之后
	* `ready`             =>  编译完成
	* `beforeDestroy`   =>  `vue.$destroy();`执行前
	*  `destroyed`        =>    `vue.$destroy();`执行后
* 简易`TodoList`：
	* Html
	```
	<div id="app">
	  <input type="text" @keyup.enter="handleEnter()" v-model="newContent"/>
	  <li v-for="todo in todos" >
     <span>{{todo.content}}</span>
     <button @click="deleteItem($index)">删除</button>
     </li>
	</div>
   ```
	 *   JS
	```   
	<script type="text/javascript" src="../js/vue.js"></script>
	<script type="text/javascript">
	  new Vue({
		el :'#app',
		data () {
		  return{
			todos : [
			  {content: 'add some todos'}
			],
			newContent: ''
		  }
		},
		methods : {
		  handleEnter (){
			this.todos.unshift({content: this.newContent})
			this.newContent = ''
		  },
		  deleteItem(index) {
			this.todos.splice(index, 1)
		  }
		}
	  })
	</script>
	
	```
## vue-cli插件使用(webpack模块化构建)
* 说明:
  * `vue-cli`是`vue`官方提供的脚手架工具包
  * `github`: https://github.com/vuejs/vue-cli
* 使用`vue-cli`快速创建工程化项目
  * 使用基于`webpack`的简单模板创建项目: `webpack-simple_demo`
	```
	npm install -g vue-cli    //下载脚手架包
	vue init webpack-simple webpack-simple_demo   //下载模板
	vue init webpack-simple#1.0 webpack-simple_demo   //下载模板
	cd webpack-simple_demo
	cyarn/npm install
	npm run dev
	访问: http://localhost:8080/
	```
  * 使用基于`webpack`的完整模板创建项目: `webpack_demo`
	```
	vue init webpack#1.0 webpack_demo
	cd webpack_demo
	cyarn/npm install
	npm run dev
	访问: http://localhost:8080/
	```
## 组件 
* 一个`.vue`文件就是一个`vue`组件
* 组成(3个部分)
  * 模板页面:   千万记得组件标签名和属性名不能有大写！！！！ 用-连接
	```
	<template>
	  页面模板
	</template>
	```
  * JS默认模块对象: 
	```
	<script>
	  export default {
		data() {return {}},
		methods: {},
		computed: {},
		components: {}
	  }
	</script>
	```
  * 页面样式: 
	```
	<style scoped>
	  样式定义
	</style>
	```
* 基本使用
  在父组件对象的`components`属性中配置组件模块对象
  ```
  <template>
	<hello>
  </template>
  <script>
	import Hello from './components/Hello'
	export default {
	  components: {
		Hello
	  }
	}
  </script>
  ```
* 关于标签名与标签属性名书写问题:
  * 标签名与标签属性名不区分大小写
  * 标签名: 如果组件名是`XxxYyy`, 标签名必须为`<xxx-yyy>`
  * 属性名: 如果标签属性名为`xxx-yyy`, 组件得到的属性名为: `xxxYyy`
* 使用props传递数据
  * 组件标签: <my-component name='tom' :age='myAge' :set-name='setName'></my-component>
	* 动态`props`: `:age='myAge'`
  * 组件: `MyComponent`
	* 所有`props`的属性都会成为`component`对象的属性, 模板页面可以直接引用
	* 在组件内的`prop`验证
	  ```
	  //简写
	  props: ['name', 'age', 'setName']
	  //详写
	  props: {
		name: {type: String},
		age: {type: Number},
		setNmae: {type: Function}
	  }
	  ```
* 组件间通信
  * 尽量通过`props`的方式实现组件间通信
  * 基本原则: 不要在子组件中直接修改父组件的状态数据
  * 可以使用`vue`的自定义事件机制实现组件间通信
	* 绑定事件监听
	  * 方式一: 通过$on()
		```
		this.$on('delete_todo', function (todo) {
		  this.deleteTodo(todo)
		})
		```
	  * 方式二: 通过`events`选项
		```
		events: {
		  'delete_todo': function (todo) {
			this.deleteTodo(todo)
		  }
		},
		```
	  * 方式三: 通过`v-on`绑定
		```
		@delete_todo="deleteTodo"
		```
	* 触发事件(3种情况)
	  ```
	  this.$emit(eventName, data): 在当前组件触发事件
	  this.$dispatch(eventName, data): 分给父辈组件(冒泡)
	  this.$broadcast(eventName, data): 广播给后代组件
	  ```
## 关于ESLint
* 说明
  * ESLint是一个代码规范检查工具
  * 官网: http://eslint.org/
  * 基本已替代以前的JSLint
* ESLint提供以下支持
	* ES6
	* AngularJS
	* JSX
	* Style检查
	* 自定义错误和提示
* ESLint提供以下几种校验
	* 语法错误校验
  * 不重要或丢失的标点符号，如分号
  * 没法运行到的代码块（使用过WebStorm的童鞋应该了解）
	* 未被使用的参数提醒
  * 漏掉的结束符，如}
  * 确保样式的统一规则，如sass或者less
	* 检查变量的命名
* 规则的错误等级有三种
  * 0：关闭规则。
  * 1：打开规则，并且作为一个警告（不影响exit code）。
  * 2：打开规则，并且作为一个错误（exit code将会是1）。
* 相关配置文件
  * .eslintrc.js : 规则相关配置文件, 可以在此修改规则
	* 在js/vue文件中指定
    ```
    /* eslint-disable no-new */
    new Vue({
      el: 'body',
      components: { App }
    })
    ```
	* .eslintignore: 指令检查忽略的文件,　可以在此添加想忽略的文件
    ```
    *.js
    *.vue
    ```
## npm与package.json
* npm
  * 全称: Node Package Manager
  * node服务器端与前端通用的基于命令的包管理工具
  * 包?: 可以简单的理解就是一个应用/库(具有特定功能)
  * 包管理器: 对当前应用依赖的其它包进行下载及管理的工具(包)
  * npm常用命令:
    * npm init
    * npm install
    * npm install packageName --save
    * npm install packageName@version --save
    * npm install packageName --save-dev
    * npm install packageName -g
    * npm info packageName
    * npm rm packageName
* package.json
  * 当前应用包的相关描述信息, 是一个json对象
  * 重要信息:
    * name: 当前包名
    * version: 当前包版本号
    * scripts: n个可执行的命令
    * dependencies: n个运行依赖的包
    * devDependencies: n个开发编译依赖的包

## vue-router插件使用
* 说明
  * 官方提供的用来实现SPA的插件
  * github: https://github.com/vuejs/vue-router
  * 对应vue1.x的版本为: 0.7.13
* 下载和引入
  ```
  npm install vue-router@0.7.13 --save
  import VueRouter from 'vue-router'
  ```
* 相关API说明
  * VueRouter(): 构建函数, 用来创建路由器对象
    * 配置: 在创建对象时可以指定一个配置对象
      ```
      new VueRouter({
        linkActiveClass: 'active', //指定当前路由链接的样式名
        history: true //去掉#!
      })
      ```
    * map(): 映射路由
      ```
      router.map({
          '/about': {
            component: About
          },
          '/home': {
            component: Home
          }
        })
      ```
    * start(): 启动应用
      ```
      router.start(App, '#app')
      ```
    * go(): 请求指定路由
      ```
      router.go('/about')
      ```
  * 指令与组件:
    * v-link: 用来指定路由路径
      ```
      <a v-link='{path:"/about"}'>About</a>
      ```
    * <router-view>: 用来显示当前路由组件界面
      ```
      <router-view></router-view>
      ```
* 实现简单路由
  * 路由组件:
    * home.vue
    * about.vue
  * 应用组件: App.vue
    ```
    <div>
      <!--路由链接-->
      <a v-link="{path:'/about'}">About</a>
      <a v-link="{path:'/home'}">Home</a>
      <!--用于渲染当前路由组件-->
      <router-view keep-alive></router-view>  
    </div>
    ```
  * 入口js: main.js
    ```
    import Vue from 'vue'
    import VueRouter from 'vue-router'
    import app from './components/app.vue'
    
    //使用插件
    Vue.use(VueRouter)
    
    //创建用来映射路由的路由器对象
    const router = new VueRouter({
      linkActiveClass: 'active', //指定当前路由链接的样式名
      history: true //去掉#!
    })
    
    //配置路由
    router.map({
      '/about': {component: about},
      '/home': {component: home}
    })
    
    //启动应用
    router.start(app, '#app')
    
    //初始请求一个路由
    router.go('/about')
    ```
* 实现嵌套路由
  * 配置嵌套路由
    ```
    subRoutes: {
      '/news': {
        component: news
      }
    }
    ```
  * 路由路径
    ```
    <a v-link="{path: '/home/news'}">News</a>
    ```
* 路由请求携带参数
  * 配置路由
    ```
    subRoutes: {
      '/mdetail/:id': {
        component: messageDetail
      }
    }
    ```
  * 路由路径
    ```
    <a v-link="{path: '/home/message/mdetail/2'}">{{m.title}}</a>
    ```
  * 路由组件中读取请求参数
    ```
    {{$route.params.id}}
    ```
* <route-view>使用
  * 参数keep-alive属性实现路由界面的缓存
  * 通过标签属性可动态向路由组件内部传递数据
    ```
    <router-view keep-alive :msg="msg"></router-view>
    ```
## vue-resource插件使用
* 说明:
  * vue-resource是非官方提供的ajax插件, 受众广
  * github: https://github.com/pagekit/vue-resource
  * vue官方推荐使用axios作为ajax库
  * 下载
    ```
    npm install vue-resource --save
    ```
  * 基本使用编码
    ```
    //引入模块
    import VueResource from 'vue-resource'
    //使用插件
    Vue.use(VueResource)
   
    // 发送get请求
    this.$http.get('/someUrl').then((response) => {
      // success callback
      console.log(response.data) //返回结果数据
    }, (response) => {
      // error callback
      console.log(response.statusText) //错误信息
    });
    
    // 发送post请求
    
    
    ```
  * 详细用法(查看在线文档)
    ```
    Vue.http.get('/someUrl', [options]).then(successCallback, errorCallback);
    Vue.http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);
    Vue.http.json('/someUrl', [options]).then(successCallback, errorCallback);
    ```
  [1]: ./images/00_vue%E7%9A%84%E7%89%B9%E7%82%B9.jpg "00_vue的特点.jpg"
  [2]: ./images/Vue%E7%9A%84MVVM%E6%9E%B6%E6%9E%84.jpg "Vue的MVVM架构.jpg"