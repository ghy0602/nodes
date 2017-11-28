## vuex

	安装vuex

	npm i vuex --save

	使用：

	import Vuex from 'vuex'
	Vue.use(Vuex)
	
	let store = new Vuex.Store({
		state: {
			// 定义状态
			n：0
		},
		mutations :{
			自定义事件名(state,要变的数){
				state.n = 要变的数
			}
		}
	})
	
	new Vue({
		...
		store
	})
	组件中取值 this.$store.state取值
	
	改变state中的值
	this.$store.commit('自定义事件名', 数字)

### 2.刷新获取数据的例子

在store下的index.js中的样式

      import Vue from 'vue'

    import Vuex from 'vuex'

    import Axios from 'axios'

    Vue.use(Vuex)

    let store = new Vuex.Store({

      state: {

    list: []
      },
    
      mutations: {
    
    changeList (state, payload) { // {list:[]}
      state.list = payload.list;
    }
    },
    
      actions: {
      getDataAction (store) {
      Axios.get('http://192.168.2.75:3000/info')
      .then(function (params) {  // 当请求成功之后，会触发then的第一个函数
        console.log(params.data.data)
        store.commit('changeList', {
          list: params.data.data
        })
      })
     // store.commit('changeList')
    }
     }
    
    })
    
    export default store

  在main.js中的写法
    import store from './store'
     在App.vue中的写法
    
    <template>
    
      <div id="app">
      <button @click="getDataMethod">请求数据</button>
    <ul>
      <li v-for="item in list">
        <p>id:{{item.id}}</p>
        <p>标题为:{{item.title}}</p>
      </li>
    </ul>
    </div>
    
    </template>
    
    <script>
    
    // 组件中要用到vuex中的state中的值
    
    import Hello from './components/HelloWorld'
    
    export default {
    
      computed: {
      list () {
      return this.$store.state.list
    }
     },
    
      methods: {
    getDataMethod () {
      this.$store.dispatch('getDataAction')
    }
      }
    
    }
    
    </script>
    
    <style>
    
    app {
    
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
    
      -webkit-font-smoothing: antialiased;
    
      -moz-osx-font-smoothing: grayscale;
    
      text-align: center;
    
      color: #2c3e50;
    
      margin-top: 60px;
    
    }
    
    </style>

    ### 3.router

	多页应用
	网站有多个页面，切换页面跳转链接，页面的资源会重新加载
	单页应用
	只有一个页面，好处就是首次把资源加载之后，再切换别的链接的时候并不会重新刷新页面，不会重复的加载资源
	手机端 和后台管理
	一个路径或者hash对应一个视图，当访问这个路径或hash的时候，就渲染指定的视图
	有一个库帮我们管理这种路径和视图的映射关系，vue-router
	配置步骤：
	
	vue-router的模式
	默认是hash模式
		地址栏中带上hash  #/home  #/about
	切换为history模式
		地址栏中 /home /about
		vue-router两个标签
		<router-view />  在配置的配置项中，让路径对应的组件渲染在指定的这个标签位置	
	<router-link />  生成链接，自动监听点击的事件，帮助渲染对应路径的组件	传入的props,
			to='路径'
			tag="标签名" 生成的标签
			exact 访问嵌套的路径的时候，要排除掉不必要的匹配，只匹配当前机会的导航添加样式
	控制当前的激活状态的导航的样式
	默认提供class为：router-link-active 
	子路由
	children:[]
	http://localhost:8080/homa=1?a=1&b=2
	
	?a=1&b=2 search值
	
	a=1&b=2 queryString
	
	









