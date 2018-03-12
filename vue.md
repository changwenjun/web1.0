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


