###Welcome to use MarkDown
#1.下载核心版本库
##bower  info  vue
	npm	init --yes
	cnpm	install	vue	--save
#2.指令
              特点：mvvm       m=mvc   module 模型   v=view 视图    c=controller  控制器
         mvvm       m=mvc   module 模型   v=view 视图     vm (视图与数据之间的传递)
         vue1 双向数据绑定   vue2 单向数据流
             单页面应用
v-model   数据绑定
	data  返回对象用 return
	v-for   循环   格式  v-for="字段名 in(of) 数组json"
	v-show   显示 隐藏     传递的值为布尔值  true  false  默认为false
	v-if   显示与隐藏     和v-show对比的区别 就是是否删除dom节点   默认值为false
	v-else-if  必须和v-if连用
	v-else  必须和v-if连用  不能单独使用  否则报错   模板编译错误
	v-bind  动态绑定  作用： 及时对页面的数据进行更改
	v-on 绑定事件  函数必须写在methods里面
	@click  快捷方法
	v-text  解析文本
	v-html   解析html标签
	v-bind:class   三种绑定方法  1、对象型  '{red:isred}'  2、三目型   'isred?"red":"blue"'   3、数组型  '[{red:"isred"},{blue:"isblue"}]'
	v-once  进入页面时  只渲染一次 不在进行渲染
	v-cloak  防止闪烁
	v-pre  把标签内部的元素原位输出
	
#3.key  
###http://blog.csdn.net/qq_27626333/article/details/76130397
###Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。这么做，除了使 Vue 变得非常快之外，还有一些有用的好处。
#4.方法
	methods
#5.属性
###5.1属性的绑定和简写
	
#6事件对象#event

#7事件冒泡
###组织事件冒泡
	a>原生js方式，依赖事件对象，e.stopPropagation
	b>vue方式，@click.stop="show"

#8事件默认行为
###组织默认行为
		1>原生js,e.preventDefault
		2>vue,@click.prevent
#9.键盘事件
		@keydown
		@keypress
		@keyup

		@keydown.13/@keydown.enter按下回车
#10.模板
	1.Vue.js使用基于HTML的模板语法
	2.数据绑定的方式：
						方式一：使用双大括号{{}}，可能会闪烁，v-cloak   [v-cloak]{display:none;},必须配合样式使用。
						方式二：v-text  v-html
	3.其它指令：v-once 数据只绑定一次<span v-once>{{msg}}</span>
				v-pre 不编译，直接原样显示<span v-pre>{{msg}}</span>
#11。过滤器
	1语法：{{data|filter1(参数)}}
	2.内置过滤器：2.0全部取消
	3.解决方法：
		 			1>第三方工具库：loadash、date-fns(日期处理)、accounting.js(货币处理)
		 			2>自定义过滤器
		 						全局过滤器
		 									Vue.filter(id,方法())
		 									Vue.filter("app",(data)=>{
		 										return data<10?'0'+data:data;
		 									})

		 						局部过滤器

		 									filter:{
		 										app:(data)=>{
													return data<10?'0'+data:data;
		 										}
		 									}
		 									
#12.使用axios/vue-resource发送http请求
	1.vue-resource(1.0):2.0之后不再跟新。
	2.axios(2.0):基于Promise的http请求客户端。
		axios([options]).then((res)=>{}).catch((error)=>{});
		axios.get(url,{params:{name:19}}).then((res)=>{}).catch((error)=>{})
		axios.post(url,{name:19},[options]).then((res)=>{}).catch((error)=>{})数据格式：Request.Payload，并非常用的form  date，必须要以键值对，不能以json传参数
			1.post传参方试：
				1》自己拼接字符串{name=19&age=20}  
				2》选项数据转换：

				axios.post(
					url,
					{name:19},
					{
						transformRequest:[
							function(data){
								let params=''
								for(let index in data){
									 params+=index+'='+data[index]+'&';
								}
								return params;
							}
						]
					}
				).then((res)=>{

					})
				.catch((error)=>{

					})
				3>如果使用模块化开发，可以使用qs模块进行转换

#13.axios本身不支持跨域请求	。使用第三方库跨域	
	vue-resource
				this.$http.jsonp(url,{
						params:{
							wd:"a"
						},
						jsonp:"cd"
					}).then(res=>{
						console.log(res.data)
					})
#14.生命周期
			vue实例创建到销毁的过程：
				beforeCreate:实例创建之后
				Create：数据，事件渲染之后
				beforeMount：末班编译渲染
				mounted：已经挂在
				beforeUpdate:数据修改之前
				Updated:数据修改之后
				beforeDestroy:数据销毁之前
				Destroyed：数据销毁之后
#15.计算属性
			1.基本用法
					计算属性用来存储数据，几个特点
						a.数据可以逻辑处理
						b.对计算属性中的数据进行监视
			2.计算属性VS方法
					a.计算属性基于它的依赖进行跟新的，只有在想干依赖发生改变是才能更行变化
					b.计算属性有缓存，依赖没变，多次计算的得到的值是之前缓存的结果。
#16.vue实例属性和方法
			1. vm.$el$el  vue关联元素
			2. vm.$data   获取数据
			3. vm.$options 用来获取自定义属性  vm.$options.name
			4. vm.$refs   用来获取页面中所有添加的属性元素  <h2 ref="hello">live</h2>    vm.$refs.hello//获取带有ref h2元素对象


			a.方法
			 vm.$mount()手动挂载vue实例  vm.$mount("#app")
			 vm.$destroy()销毁实例 vm.$destroy()
			 vm.$nextTick()下次DOM更行完后在执行 vm.$nextTick(function(){}),一般在修改数据之后使用该方法。
			 

			 $set(object,key,value)为对象添加一个属性，并添加值。可以实时监视  this.$set()   vue.set()
			 $delect(object,key)删除属性    vue.delect()      this.$delect()
			 $watch(属性,回调函数(新值，就值){},[options])侦听数据变化    vue.$watch()   this.$watch()


			 watch选项   watch:{
			 						age:(new,old)=>{
			 							console.log(new,old)
			 						},
			 						user:{
			 							handler:()=>{

			 							},
			 							deep:true//深度监视，当对象中的属性发生变化的时候也会被监视。

			 						}
								}
#17.自定义指令
		1.全局指令
				a. Vue.directive(id,[definition]) 
				<div v-hello></div>  
				   Vue.directive("hello",{
				   		bind:()=>{}//指令第一次绑定到元素上时调用，调用一次，初始化操作。
				   		inserted:()=>{}//被绑定元素插入到DOM中时调用。
				   		update:()=>{}//被绑定元素所在模板更新时调用
				   		componentUpdated:()=>{}//被绑定元素所在模板完成一次更新时调用
				   		unbind:()=>{}//指令与元素解绑时调用，只调用一次

				   	})  
				<div v-world:type="name"></div> 

				   	Vue.directive('world',{
				   		bind(el,binding){
				   			el.style.color="red";
				   			//el.value
				   		}
				   	})

				   	//传入一个简单的函数
				   	<div v-wbs></div> 
				   		Vue.directive('wbs',function(){
				   				alert("wbs1231245")
				   		})
		2.局部指令
#18、过度动画
		1.组件动画：transtion、animation
			transtion:将要执行动画的元素包含在该组件中
			<transition>

			</transition>
			钩子函数：8个
		2.结合第三方动画库animate.css

		3.多元素动画

		<transition-group>
			<p :key='1'>666</p>
			<p :key='2'>333</p>
		</transition>
#19、组件component
	1.自定义的元素，可扩展html元素，封装重用代码。
	2.定义组件的方式
		a.第一种创建组件的构造器，然后又组建构造器创建组件。
		b.第二种直接创建组件
	3.组建的分类
		a.全剧组件

		b.局部组件
#20、引用模板、动态引用
		将组建的内容放到模板<template>中并引用

	 动态组件
	 	<component :is="flag"></component>

	 	<keep-alive></keep-alive>
#21、组件间的数据传递
	1.父子组件
		在一个组件内部定义另一个组价，称为父子组件
		默认情况下子父组件不能互相访问
	2.组件之间数据传递通信
		访问父组件数据
				<my-hello-son :fmsg="msg"></my-hello-son>
				使用props选项
				在调用子组件时，绑定想要获取的父组件中的数据
				崽子组件内部，使用props选项声明获取的数据，即接受来自父组件的数据
				总结：父组件同过props向下传递数据给子组件

		访问子组件数据
				a在子组件中使用vm.$emit(事件名，数据)发送数据给父组件
				b父组件在使用子组件的地方监听子组件除法的事件，并在父组件中定义方法，用来获取数据
				总结，组组件通过event给子组件发送消息，实际上是组组件把自己的数据发送到父组件


		组建中的数据总共有3中形式 data、props、computed
#22、单向数据流，父子组件间修改数据
		1.props是单向绑定的，当父组件的属性变化时，将传导给子组件，但是不会反过来,而且不允许子组件直接修改父组件中的数据，报错。
		解决方法：
				a如果子组件想把它作为局部数据来使用，可以将数据存入另一个变量中在操作，不影响父组件中的数据。
				b如果子组件项修改数据并且同步修改更新到父组件中，两个方法
						1》使用.sync(2.3版本后开始支持),需要显示的触发一个更新事件
						2》可以将父组件中的数据包装成对象，然后在子组件中修改对象的属性。

#23、非父子组件间的通信
		可以通过一个空的Vue实例作为事件总线（事件中心）。可用来侦听事件和触发事件
#24、slot内容分发
	本意：位置、槽。
	作业：用来获取组件中的原内容，类似angular中的transclude指令。

#25、vue-router路由
		1.简介
			使用vue.js开发spa单页面应用
			根据不同url地址，显示不同的内容，单显示在同一个页面中，成为单页面应用。
		【参考】(https://router.vuejs.org/zh-cn)
		bower	info	vue-router
		2.基本用法
			a.布局
#26、路由嵌套、参数传递、路由结合动画
	
		传参数的两种方式：
			a.查询字符串：login?name=tom&age=23   {{$route.query}}

			b.rest风格url:regist/aclice/456			{{$route.params}}
		路由实例方法
		router.push()添加路由、功能上与<route-link>相同
		router.replace()替换路由、不产生历史记录
#27、单文件组件
	1.vue文件
		.vue文件、称为单文件组件，是Vue.js自定义的一种文件格式，一个.vue文件就是一个单独的组件，在文件内封装了组件相关的代码。html/css/js

		.vue文件又三部分组成<template>、<style>、<script>
	2.vue-loader加载器，加载vue文件解析
		html-loader  css-loader style-loader
		需要注意的是vue-loader是基于webpackd的
	3.webpack
	webpack是一个前端资源模板化加载器和打包工具，它能够吧各种资源都作为模块来使用和处理。
	实际上，webpack是通过不同的loader讲这些资源加载后打包，然后输出打包后文件
	简单来说：webpack是一个模块加载器。
	webpack核心配置文件webpack.config.js,必须在项目的根目录下

	4.步骤、实例
		创建项目、目录结构
		webpack-demo
			|-index.js
			|-main.js主函数入口
			|-App.vue  
			|-package.json  工程文件
			|-webpack.config.jswebpack核心配置文件
			|-.babelrc  Babel配置文件

		安装相关模板
			npm  install vue 生产依赖



			npm  install webpack 开发依赖
			npm  install webpack-dev-server 
			npm  install vue-loader 
			npm  install vue-html-loader 
			npm  install css-loader 
			npm  install vue-style-loader 
			npm  install file-loader 
			npm  install babel-loader 
			npm  install babel-core 
			npm  install babel-preset-env //自动根据配置的运行环境自动启用需要的babel插件
			npm  install vue-templte-compiler //预编译模板
		编写main.js

		webpack配置文件


		编写.babelrc

		编写package.json

		运行测试
		npm  run  dev

		npm  install  -D  webpack  webpack-dev-server vue-loader vue-html-loader css-loader  vue-style-loader file-loader babel-loader babel-core babel-preset-env vue-template-compiler




#28.vue-cli脚手架
###简介

   vue模板
	webpack  包含ESLint代码规范检测和unit单元测试
	webpack-simple 没有代码规范检测和单元测试
	browserify  热加载
	browserify-simple  
	pwa
	simple 很少简单
###实例
	
	cnpm  install -g vue-cli安装,配置命令环境

	vue  --version

	vue  list
###初始化项目
vue init 末班名称  项目名

cd  项目名

cnpm  install

cnpm  run  dev启动测试服务


cnpm  run  build将项目打包dist目录

ESLint统一代码规范和风格

###模块化开发
1.vue-router
	cnpm install vue-router -S
2.编辑main.js
3.编辑App.vue
4.编辑router.config.js
###axios模块化
	cnpm  install axios  -
	使用axios的两种方法
		1.每个组件中引入axios
		2.在main.js全局引入axios并添加到VUE圆形中。 this.axios.get
###为自定义组件添加事件
	@click.native="send"   .native侦听组件根元素的原生事件

@29.Elment UI组件库
##1.简介
	Elment UI饿了么团队提供的vue2.0组件库。可以快速搭建网站。
		http://element.eleme.io/（pc）
	Mint UI 饿了么团队提供的vue2.0组件库。可以快速搭建网站。
		http://mint-ui.github.io/#!/zh-cn（移动端口）

	安装
	 	cnpm i element-ui -S
	main.js导入模块并使用
		import Element from 'element-ui';
		import 'element-ui/lib/theme-chalk/index.css';需要loader加载器
		需要在webpack配置文件中添加loader（cnpm install style-loader -D）
		  {
	      	test:/\.(eot|svg|ttf|woff|woff2)(\?\S*)?$/,
	      	loader:'file-loader'
	      }
		使用Vue.use(Element)
		这种方式引入了elementui 的所有组件
	按需引入

	使用组件

#30.less

	安装less loader    less   less-loder

	cnpm install less less-loader  -D

	webpack配置文件loader添加
	{
        test: /\.less$/,
		loader:'less-loader'
    }

	style标签指定语言为less才可以 <style lang="less">
#31自定义全剧插件
	全剧组件
		可以在main.js中使用Vue.use全局引入，然后其他组件都可以使用。
		Vue.use(obj)

	普通插件(组件)
		每次使用都要引入，但是可以添加到圆形上去。
#32.vuex使用
		Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

		简单来说，用来集中管理数据，都是基于flux的前端状态管理框架。

	1.基本用法
		安装
			cnpm  install vuex -S
		创建store.js文件

			main.js配置store选项，指定为store对象，自动将store对象注入到所有的子组件中。子组件中通过瘫痪$store访问该store对象


		编辑store.js文件
			Vuex核心是Store(仓库)，相当于与是一个容器，一个store实例中可以包含以下方法：

				state		定义属性（状态、数据）
				getters     获取属性的
				actions     定义方法的
				commit      提交变化，修改数据的唯一方式，就是显示的提交muyations
				mutations	突变，定义变化
				*不能直接修改数据，必须显示的提交变化，目的是为了追踪到状态的变化。
		编辑App.vue
			在子组件中访问store对象
				1.通过this.$store访问
				2.通过mapGetters、mapActions访问，Vuex提供了两个方法。
				mapGetters：获取属性
				mapActions：获取方法
				mapState：	获取state
	2.分模块组织Vuex(更好的组织Vuex项目结构)

		|-src
			|-store
				|-index.js
				|-getters.js
				|-actions.js
				|-mutations.js
				|-modules//分为多个模块，每个模块拥有自己的state getters......
					|-user.js
					|-cart.js
					|-goods.js
					|......


#33.项目实例
	1.初始化项目

	vue  init webpack itany

	cd itany

	cnpm install

	cnpm install less less-loader -D

	cnpm insatll vuex -S

	cnpm install axios -S

	npm run dev


	2.项目资源


	3.创建目录结构

		清除项目部分内容

		目录如下
				|-static
					|-css
						|-reset.css



