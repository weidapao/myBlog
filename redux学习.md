redux学习笔记

# 基本原则
- 唯一数据源(single source of truth)
- 保持状态只读(state is read-only)
- 数据改变只能通过纯函数完成(pure functions)
  
1. 唯一数据源
   ### 整个应用只用一个store，所有的全局状态都存在这里
2. 保持状态只读
   ### UI=render(state),不直接修改状态的值，返回一个新对象给Redux
3. 数据改变只能通过纯函数完成
   ### reducer是一个纯函数,根据state和action的值，产生一个新的对象返回。不产生副作用。只负责计算状态，不负责存储状态。只关心如何更新state,不管state怎么存。个人理解：会返回一个更新后的state对象。不能直接修改state，reducer是一个纯函数，不能有副作用。（个人感觉是要先深拷贝一下，返回一个新对象，扩展运算符相当于生成一个新对象）
# redux实例
  - 每个action的构造函数都会返回一个action对象。
  - redux提供的createStore函数来创建全局唯一的Store。
  - store.getState()能够获得store上的所有状态。
  - 组件往往只需要一部分状态，所以封装一个getOwnState函数。
  - 保持store上的状态和this.state同步
      1. onChange
      2. 组件装载时store.subscribe(this,onChange)
      3. 组件销毁时取消订阅
  ```
  import { createStore } from './redux'
  import reducer from './reducer' // 更新状态的reducer
  const initValue = { a:1, b:2} // store的初始值
  const store = createStore(reducer,initValue)
  ```

  # 容器组件和傻瓜组件
  ## 组件的两个功能
  1. 处理数据（容器）
  2. 根据props和state渲染页面（傻瓜）
  3. 无状态组件可以用一个函数来表示，参数为props
  # 组件Context
  个人理解:
  - 把store放在最外层组件的context上
  - 创造一个特殊的组件作为context的提供者(Provider))
  # React-Redux
  connect(mapStateToProps,mapDispatchToProps)(组件)