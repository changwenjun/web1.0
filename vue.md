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