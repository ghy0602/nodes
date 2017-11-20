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