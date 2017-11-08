## React

\1. react 运行原理

*2. 声明 react 的组件

​    继承了 React.Component 的类就是一个组件

​    至少有一个 render 方法

​        这个方法应该 return 一份 jsx 的对象,

​        这就是这个组件的样子

*3. jsx 语法

​    回去复习今天的 jsx 的语法 , 写到下面

​    begin here...

​        相邻的jsx 元素必须包含在一个闭合的标签里面

​        自己声明的组件要大写开头, 内置组件小写开头

​        jsx 本身可以是一个表达式

​        在 jsx 里面使用 {} 表示表达式

​        标签之间的内容就叫 children, 如果是类的组件的标签, 它的 children 通过实例(this)的 props.children 拿到

​        关键词要转成另外一种形式 : class->className for->htmlFor, 应该是驼峰式的

\4. 把 jsx 渲染到页面

​    reactDOM.render

\5. virtual DOM 的概念 怎么来的

\6. this.props.children

7.webpack 打包 css 文件

​    把 css 打包到 js 文件里面 , 一般是在开发阶段 css 的打包方式

​    把 css 打包成一个单独的 css 文件, 通过 link 引入(自动创建) 生产阶段

8.关于 css-loader

​    引入 css 文件的使用这个 loader 处理它

​    遇到 url 或 @import 帮你去引入里面的资源, 引入资源的过程中, 更根据资源的类型再使用相应的 loader 去处理

9.关于 file-loader

​    处理资源(字体, 图片, 视频)

​    转换出一个路径, 把资源搬到输出目录

**************************************************************************************************10. props: react的属性

​    传递属性: <Content a="8"></Content>

​    拿到: this.props

****************************************************************************************************************************************************************************************************11. state

​    组件有内部状态: this.state = {}

​    通过 this.setState() 来改变组件的内部状态, 这个时候页面会更新, 因为组件的 render 执行了, 得到了一份新的 jsx 的结构

​    父组件的 render 执行了, 子组件的 render 也会执行

​    改变页面状态, 应该通过 setState 更新

​    setState() 可以接收一个对象为参数, 也可以接收一个回调函数作为参数

​    关于 setState 的异步执行问题:

​        setState 更新状态的时候, 是异步更新的. (render 在 state 合并之后执行一次)

​        如果把 setState 放到异步函数里面执行, 他是同步更新的. ( render 马上执行, 马上更新视图 )

关于 webpack

​    html-webpack-plugin 自动创建 html 文件

​    clean-webpack-plugin 清理某一个文件夹在打包之前



### 小例子：todo

1. 组件受控
    某些组件有自己的行为, 比如 input, 你输入东西的时候, 页面状态就会变化, 这是组件本身的行为
    如果给 input 一个 value 值, 这样就收到了 react 的控制, 可以通过onChange 来 setState 来改变 input 的value.
    非受控组件 => 受控组件

2.合成的事件对象
    event
        nativeEvent: 访问浏览器 dom 元素的事件对象
        preventDefault
        stopPropagation
        target 拿到真实的 dom 元素
    
    和事件相关的文档: https://reactjs.org/docs/events.html

3. map 方法
    数组下的一个方法, 接收一个回调函数, 回调函数里面接收的参数是: (元素,索引,数组)
    回调函数的返回值会 替换掉原来的元素, 返回一个新数组
    原来被遍历的数组没有变化

4. 当把数组卸载 jsx 结构里面, react 会自动展开

5. key, 在数组里面的 jsx 元素应该在最外层的结构有一个 key, 应该保证相应数据的 key 是唯一的. 同一份结构, 永远保证不管如何视图变化, 相同的数据对应同一个 key 值

6. 组件之间的交流(数据传递), 组件之间公共 props 进行数据传递, 数据从顶层流向底层, 而且永远是这样. *不能修改 props*

7. 在元素上面声明 ref 属性, 可以通过组件拿到真实的 dom 元素
    ref="df" => this.refs.df (现在已经不被推荐)
    ref={ (el)={ this.cont = el } } : this.cont 就可以拿到真实的 DOM 元素

8. (用类声明的)组件的生命周期
    mounting 阶段: 组件挂载阶段, 出生阶段,只能被出生一次,
    updating 阶段: 更新阶段, 活着时候的阶段,
    unmounting 阶段: 卸载, 死亡

9. 生命周期的函数
    mounting
        constructor
        componentWillMount 组件将要被挂载执行
        render 就是那一刻
        componentDidMount
            在这个函数里面发起请求
        
        在挂载完成之前, 所有的组件都应该 render
        所有组件 render 之后, 开始依次过载: 同层级的组件从先往后挂载, 父子组件 先挂载子组件
        如果要拿到真实的 dom 元素, 必须在组件挂载完成之后

    updatating
        componentWillReceiveProps() 奇葩, 不会在自身 setState 后执行, 父组件的 render 执行
        shouldComponentUpdate() 特殊
        
        componentWillUpdate() 更新之前
        render 就是那一刻
        componentDidUpdate() 更新之后
        
        注意事项:
            更新阶段不要 setState, 除了奇葩那个时候
    unmounting 卸载阶段
        componentWillUnmount 卸载之前

10. promise 异步问题, 解决回调函数的噩梦