router

    Router
        browserHistoy
        hashHistory
    
    BrowserRouter
    HashRouter

关于浏览器的 history
    push push 一个新的 entry 到 history stack
    history stack
        所以的浏览记录都存放在这个 history stack 里面, 它就相当于一个数组
    entry
        每一个访问的页面(访问过的路径)
    
    点击一下 a 链接, 就是往历史堆里面放入一个地址

BrowserRouter
    使用 browserHistoy
    放到最顶层, 把其它的组件作为 children

Route
    path的属性: 如果地址匹配到了这个路径, 就会显示
    exact  只会在path匹配  location.pathname时才匹配
    component属性: 
      1.接收一个组件变量 会往组件里面传入3个 props: history, location, match
      2.可以接收一个回调函数，回往回调函数传入一个对象作为参数，这个对象里面有：	history, location, match，回调函数需要你反悔jsx结构
    render属性：接收一个回调函数，和component的第2点一样
    children和render一样，不过他无论如何都会被匹配到，
    
    不能嵌套元素


Link
    最后会被渲染成 a 链接
    to的属性: 跳转到哪里
    	接收字符串 ： '/rus' ，一个rul地址
    replach ： bool
    	true：跳转视图的时候，替换掉浏览器history stack  里面  当前的entry
    	false：跳转视图的时候，往history stack  里面  push一个新的entry
传入的三个属性：

​	history

​	location：history里面的location是可变的，是实时的，是不稳定的，如果你想要location，从props里面拿location，而不是从history里拿

NavLink

    activeStyle
    activeClassName
    exact
    其它和 Link一样

Redirect
    to 的属性, 如果他被渲染的时候, 会重定向到一个新的地方
        string 或 object
Switch
    一旦匹配到一个, 不再继续往下匹配

withRouter
    一个高阶组件, 接收一个组件作为参数(比如Aac), 然后导出一个组件, 这个时候 Aac 组件的 props 就有了那3个属性
replace  写在link里   是link的一个属性   值是布尔值，true不能后退，false可以后退，值用{}包着

react组件声明的两种方式：

​	使用类声明：可以有内部状态，有生命周期

​	使用函数声明：没有内部状态，没有生命周期，只做渲染，之渲染上面传下来的props

​	技巧：何时使用函数组件

​		只要不用到this.state