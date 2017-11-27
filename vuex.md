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
    
    


