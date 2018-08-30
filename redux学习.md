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
  每个action的构造函数都会返回一个action对象。创建全局唯一的Store
  ```
  import { createStore } from './redux'
  import reducer from './reducer' // 更新状态的reducer
  const initValue = { a:1, b:2} // store的初始值
  const store = createStore(reducer,initValue)
  ```