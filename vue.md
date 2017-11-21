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