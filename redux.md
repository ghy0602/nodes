redux 的工作原理

    首先得到一个 store
    如果想拿state, 使用 store.getState()
    如果想改变数据,发起一个 action , store.dispatch(action)
    发起 action 之后, reducer 会计算出应用的下一个状态

store
    维护应用的状态
    *整个应用只有唯一的一个 store,
    
    getState, 得到整个应用的状态
    dispatch, 发布 action
    subscribe, 监听 action 的发起
        action 发起之后, 执行回调函数

action
    它是一个对象, 必须有一个 type 属性, 相当于 action 的名字

    如果你要改变数据(改变应用的状态), 你应该发起一个 action

state
    整个应用的状态
    通过 store.getState() 拿到
    *整个应用只有唯一的一个 state,

reducer
    一个函数, 返回整个应用的 state
    说明 reducer 的返回决定了 state 是什么样子
    
    接收两个参数: state 和 action
    根据这两个参数 计算出应用的下一个 state

createStore
    用来创建 store,

middleware 中间件

redux-thunk
    激活了这个中间件后, dispatch 可以接收更多的数据类型了

action creators
    它就是返回 action 的一个函数, 返回一个
    但是如果有中间件参与, 它可以返回其它数据类型, 不如 redux-thunk, 你就可以返回一个函数