## vue

### 1.使用vue

​	特点：

​                    响应的数据绑定

​                    可组合的视图组件

	// 在模板中渲染数据 {{任意表达式}}		
			let arr = ['miaov','ketang'];
			// 启动应用
			// 选项对象
			new Vue({
				el:'#app', // document.getELementById('list')  // element  模板位置
				data: {  // 要呈现的数据
					arr:arr,
					message: 'hello'
				}
			});
### 2.指令

	指令 		
			/*
				写在标签上作为行间的自定义属性 以v-开头
				是Vue提供的特殊属性，用来完成某项功能的
	
				v-bind 动态绑定数据 简写为:
				语法： v-bind:属性名="data中的数据"
			*/
			let vm = new Vue({
				el:'#app',
				data: {  
					message: 'hello',
					tip: '这是一个提示，我很长很长很长我很长很长很长我很长很长很长我很长很长很长我很长很长很长我很长很长很长我很长很长很长我很长很长很长我很长很长很长',
					customSrc:'./img/1.jpg'
				}
			});
	
			console.log(vm);
	
			document.onclick = function (){
				vm.message = 'abc'	
			}
	指令			
				v-for 做循环
				语法:
					v-for="value,key in 数组"
					v-for="value in 数组"
					v-for="value,key of 数组"
					v-for="value of 数组"
			*/
	
			let arr = ['miaov','ketang'];
			// 循环 遍历 枚举 一个数组 拿两种值： 数组中的每一个值；值对应的下标； key value
	
			let vm = new Vue({
				el:'#app',
				data: {
					list: arr
				}
			});
### 3.显示隐藏

	v-show 切换display为block还是none			
				语法：v-show="表达式"
					表达式的值为true，元素显示
					表达式的值为false，元素不显示
				v-if
					语法：v-show="表达式"
						表达式的值为true，元素渲染
						表达式的值为false，元素不渲染
	
				切换元素显示隐藏 v-show
				数据没有就不渲染结构的 v-if
### 4.事件


	绑定事件 指令 v-on				
					语法：v-on:事件名 = '表达式|事件处理函数'			
				把定义的事件处理函数放在一个地方 选项对象中的methods中			
				click
				mouseover
				mouseout
			*/
	
			// 内部会把data中的数据放在new Vue创建的实例身上
	
			let vm = new Vue({
				el:'#app',
				data: {  // 用来渲染到页面中的数据的
					message: 'hello'
				},
				methods: {
					changeMessage: function (){  // 函数
						console.log(123);
						console.log(this);  // 指向这个方法所在的对象（实例）
						
						this.message = 'miaov'	
					}
				}
			});
	
			console.log(vm);
### 5.事件处理函数传参

	语法：				
					@click="事件处理函数(传参,$event)" 模板中有一个全局的变量 $event
					@click="事件处理函数"  事件对象是事件处理函数的第一个参数
### 6.操作class

	// 在模板中循环，在循环的过程，拿到下标和showIndex进行对比，如果相同就添加class	
		/*
			操作样式
				class
					动态的计算
						语法：:class="{class名字:表达式}"
							如果表达式为true，则这个元素添加前面的class
							如果表达式为false，则不添加
				style
​			选项卡的例子

	<body>	
		<div id="app">
			<!-- <button>按钮1</button>
			<button>按钮2</button>
			<button>按钮3</button>
			<div>按钮1</div>
			<div>按钮2</div>
			<div>按钮3</div> -->
	
			<button 
				@click='changeIndex(i)' 
				v-for="item,i in list"
				:class="{yellow: i === showIndex}"
			>
				{{item}}
			</button>
			<div :class="{show: i === showIndex}" class="abc"  v-for="item,i in list">{{item}}</div>
		</div>
		<script>
			var arr = ['按钮1','按钮2', '按钮3'];
	
		// 在模板中循环，在循环的过程，拿到下标和showIndex进行对比，如果相同就添加class
	
		/*
			操作样式
				class
					动态的计算
						语法：:class="{class名字:表达式}"
							如果表达式为true，则这个元素添加前面的class
							如果表达式为false，则不添加
				style
		*/
	
			new Vue({
				el: '#app',
				data: {
					list: arr,
					showIndex: 0  // 用来确定哪一个应该是显示的
				},
				methods: {
					changeIndex(index){
						this.showIndex = index;
					}
				}
			})
		</script>
	</body>
### 7.reduce

	let arr = [1,2,3,4];		
			// 把数组每一项累加
			// 上一次累加的结果作为下一个的初始值
			// 回调函数的第一个参数，就是上一次函数执行后的返回值
	
			/*
				reduce
				参数：
					第一个参数是函数
					第二参数是初始值
			*/
	
			let total = arr.reduce(function (item1,item2){
				console.log(item1,item2);
				return item1+item2	
			},100)
	
			console.log(total);
	
			let arr2 = [{a:1,b:3},{a:2,b:4},{a:3,b:5}];
	
			let m = arr2.reduce(function (item1,item2){
				console.log(item1,item2);
				return {
					a: item1.a + item2.a,
					b: item1.b + item2.b
				}	
			},{a:1000,b:1000})
	
			console.log(m);
### 8.双向数据绑定		


​			
			// 双向数据绑定
			// 数据 -> 模板 -> 数据// 如果遇到的是input textarea 不需要手动的			写input监听
			// v-model指令
			// 根据input的类型，把v-model转成不同的值
			// input为text，转成value
			// input为checkbox,radio, 转成checked
	
			// MVVM模式
			/*
				M model 数据
				V view 视图
				VM view-model 视图-模型
			*/
​		例子

	<body>	
		<div id="app">
			<input v-model="messgae" type="text" />
			<input v-model="checked" type="checkbox" />
			<p>{{messgae}}</p>
			<p>{{checked}}</p>
		</div>
		<script>
			// 双向数据绑定
	
			// 数据 -> 模板 -> 数据
	
			// 如果遇到的是input textarea 不需要手动的写input监听
			// v-model指令
			// 根据input的类型，把v-model转成不同的值
			// input为text，转成value
			// input为checkbox,radio, 转成checked
	
			// MVVM模式
			/*
				M model 数据
				V view 视图
				VM view-model 视图-模型
			*/
	
			let messgae = 'hello';
			// vm
			new Vue({
				el: '#app',
				data: {
					messgae: messgae,
					checked: false
				}
			})
	
		</script>
	</body>
### 9.简易版留言


	/ 一上来把数据中message通过v-model绑定在input的value上		
			// v-model会监控value的变化，立马更新message的值		
			// 事件修饰符
			// 语法： @事件名.修饰符 = '事件处理函数'
			// https://cn.vuejs.org/v2/guide/events.html
	<body>
			<div id="app">
				<input v-model="messgae" @keydown.enter="addMessage" />
				<ul>
					<li v-for="item,i in arr">
						{{item}}
						<button @click="remove(i)">删除</button>
					</li>
				</ul>
			</div>
			<script>


				new Vue({
					el: '#app',
					data: {
						messgae: '',
						arr:[]
					},
					methods: {
						addMessage (ev) {
							// 只需要写逻辑，不需要处理和事件相关的
							console.log(this.messgae);
	
							this.arr.push(this.messgae)
							this.messgae = '';
							
						},
						remove(i){
							this.arr.splice(i,1)
						}
					}
				})
	
			</script>
		</body>
### 10.计算属性

			// 尽可能少的在模板中写业务逻辑，写的多，模板会很臃肿
			// 计算属性 就是一个属性 用来写关于data的一些逻辑的
			// 把处理data的逻辑放在计算属性中写
			// computed 计算
	<body>
			<div id="app">
				姓名：<input type="text" v-model="userName" />
				年龄：<input type="text" v-model="userAge" />
				<input type="button" @click="addUserHandle" value="添加" />
				<ul>
					<li v-for="item,index in users">
						姓名:{{item.name}}
						年龄:{{item.age}}
					</li>
				</ul>
				<p>统计：以上人的总年龄为{{totalAge}}岁</p>
				<p>上面的人总年龄为{{totalAge}}岁</p>
			</div>
			<script>
				let data = [
					{
						name:'leo',
						age:30
					},
					{
						name:'leo',
						age:30
					},{
						name:'leo',
						age: "30"
					}
				]
	
				let vm = new Vue({
					el:'#app',
					data: {
						users: data,
						userName: '',
						userAge: ''
					},
					computed: {
						// 计算属性中的值依赖于data中的值，如果data的值发生变化，那么计算属性就会重新计算
						// 这个计算属性的值，是函数的返回值
						totalAge: function (){
							// 写业务逻辑 this => 实例
	
							let m = this.users.reduce(function (n,item){
								return n + parseInt(item.age)
							},0)


							return m
						}
					},
					methods: {
						addUserHandle () {
							this.users.push({
								name: this.userName,
								age: this.userAge
							})
						}
					}
				})
	
				console.log(vm);
	
			</script>
		</body>
### 11.Object.definePropery

	// 定义属性的时候，属性对应的值不能被改写		
			// 使用Object.defineProperty()
			/*
				Object.defineProperty(对象,key,描述)
				描述是一个对象：
					https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
					
				存 取  描述
					存 会触发setter对应的函数set
					取 会触发getter对应的函数get
					Object.defineProperty(对象,属性,{
						get(){
							
						},
						set(){
		
						}
					})
### 12.vue中的组件

			// 把html重复的部分封装成组件
			/*
				在较高层面上，组件是自定义元素，Vue.js 的编译器为它添加特殊功能
			*/
			/*	
				注册组件
					语法：
						Vue.component(组件名字,组件的选项)
					组件名字命名规则
						不能使用html规定的标签名
						烤串命名法，驼峰命名法
					在模板中使用的时候，必须使用烤串命名
			*/
### 13.定制组件

			定义一些 props		
					title 弹框标题     必填项
					okValue 确定文案
					cancleValue 取消文案
	
				父组件 -> 子组件 props
				子组件 -> 父组件 custom-event
	
				每一个组件都是独立的
				在模板中使用组件，写在一对标签组件中的内容，会被当做组件定制的结构
	
					在组件中就要把这个内容插入到某个地方，如果组件中没有地方要插入这个内容，组件便签中的内容会被忽略。
	
					“插槽”
						除非子组件模板包含至少一个 <slot> 插口，否则父组件的内容将会被丢弃。
							当子组件模板只有一个没有属性的插槽时，父组件传入的整个内容片段将插入到插槽所在的 DOM 位置，并替换掉插槽标签本身。
						最初在 <slot> 标签中的任何内容都被视为备用内容
				
				<div id="app">
				<custom-dialog
					title='登录'
					ok-value="登录"
					@ok="parentOk"
				></custom-dialog>
				<div v-show="isLogin">我是登录的用户名：miaov</div>
				<custom-dialog title='登录' ok-value="登录"></custom-dialog>
				<div v-show="isLogin123">我是登录的用户名：miaov</div>
			</div>
				
				Vue.component('custom-dialog', {
					//props: ['title','okValue', 'cancleValue']
					props: {
						title: {
							type: String,
							required: true
						},
						okValue: {
							type: String,
							default: '确定'
						},
						cancleValue: {
							type: String,
							default: '取消'
						}
					},
					template: `
						<div class="dialog">
							<h2>{{title}}</h2>
							<div class="content">
								这是内容
							</div>
							<div class="footer">
								<button @click="okHandle">{{okValue}}</button>
								<button>{{cancleValue}}</button>
							</div>
						</div>
					`,
					methods: {
						okHandle (){
							// 子组件发布一个事件
							//console.log(this);  // 当前所在组件的实例
							this.$emit('ok'); // 内部发布事件
						}
					}
				})
	
				// 根实例
				new Vue({
					el: '#app',
					data:{
						isLogin: false,
						isLogin123: true
					},
					methods: {
						parentOk () {
							console.log('触发了这个事件处理函数');
							this.isLogin = true
						}
					}
				})
### 14.作用域

当定制内容的时候，作用域是父组件的，但是定制的内容需要渲染子组件中的数据，需要用slot标签传到定制的内容上，定制内容使用slot-scope来接受

### 15.封装通用的组件

		在编写组件时，最好考虑好以后是否要进行复用。一次性组件间有紧密的耦合没关系，但是可复用组件应当定义一个清晰的公开接口，同时也不要对其使用的外层数据作出任何假设。		
				Vue 组件的 API 来自三部分——prop、事件和插槽：
					Prop 允许外部环境传递数据给组件；
					事件允许从组件内触发外部环境的副作用；
					插槽允许外部环境将额外的内容组合在组件中。

### 16.生命周期


	key值

	使用v-for的时候，要加上key值，来表明这个循环的元素是唯一的。

	生命周期：

	是一个组件在挂载，更新，销毁这么一个过程
	生命周期函数：
	在每一个阶段，会提供不同的函数，内部会自动的调用函数
	mounted 就是组件挂载完成之后触发的函数 也就是说组件的元素已经存在文档中了，能足够做什么事情呢？可以获取页面中的元素了。
	动态路径
	每一次不同的路径访问的时候，都会渲染不同的组件，组件都会重新挂载一次。但是使用了动态路径，这些路径都用的是同一个组件，路径发生变化，组件不会重新渲染了。
	当使用了动态路径，这个路径渲染的同一个组件内部，怎么知道路径发生变了呢？
	可以通过监控路由信息对象，来感知路径的变化。
	
	导航钩子函数
	导航发生变化（进入和离开）做一些控制
	写的位置：
		1. 写在vueRouter的实例上
			// 任何一个访问的路径，都会执行这个钩子函数
			vueRouter.beforeEach((to,from,next) => {
				to:  即将要进入的目标 路由对象
				from: 当前导航正要离开的路由
			})
	
		2. 写在配置路由信息上
			{
				...
				beforeEnter (to,from,next){
					next()
				}
			}
		3. 写在组件中
			{
				beforeRouteEnter (to, from, next) {
				   // 在渲染该组件的对应路由被 confirm 前调用
				   // 不！能！获取组件实例 `this`
				   // 因为当守卫执行前，组件实例还没被创建
				 },
				 beforeRouteUpdate (to, from, next) {
				   // 在当前路由改变，但是该组件被复用时调用
				   // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
				   // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
				   // 可以访问组件实例 `this`
				 },
				 beforeRouteLeave (to, from, next) {
				   // 导航离开该组件的对应路由时调用
				   // 可以访问组件实例 `this`
				 }
			}


			鉴权
			放在beforeEach中做，配合meta字段
	
	页面之间传递数据
		queryString的方式 ?
	
		http://localhost:8080/login?r=abc
	
	懒（按需）加载
		结合 Vue 的异步组件和 Webpack 的代码分割功能，轻松实现路由组件的懒加载。
	
		按组分割没成功？？？？？？
	
	
	上线，配置apache
	
		服务器的根路径是：/www
		上线的项目mock : /www/mock/
			mock文件件下有项目文件
				/static
					/css
					/js
				index.html
	
		在使用npm run build打包的时候，修改两个地方
			1. index.html引用css和js的路径
				修改过程：
					/config/index.js文件中
						build
							assetsPublicPath: "/mock/"
			2. 修改路由访问的根路径
					/router
						index.js文件中
							配置项中写上：
								 base:'/mock'
	
		在访问项目，刷新之后出现404
			1. 打开apache的配置 httpd.conf
				打开模块
					LoadModule rewrite_module modules/mod_rewrite.so
			2. 根路径/www目录下创建文件
				.htaccess文件
					<IfModule mod_rewrite.c>
					  RewriteEngine On
					  RewriteBase /
					  RewriteRule ^index\.html$ - [L]
					  RewriteCond %{REQUEST_FILENAME} !-f
					  RewriteCond %{REQUEST_FILENAME} !-d
					  RewriteRule . /mock/index.html [L]
					</IfModule>




