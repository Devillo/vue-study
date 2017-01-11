# vue-study

## 基础

- vue是什么？
  - vue是一套构建用户界面的 **渐进式框架** 。vue的核心库只关注视图层。
  - 声明式渲染：采用简洁的模板语法来声明式的将数据渲染进DOM的系统
  - 响应式:可以实时更新
  - 条件和循环
    - v-if: 切换一个元素的显示
    - v-for: 绑定数据到数组来渲染一个列表
  - 处理用户输入
    - v-on: 监听一个Vue实例中定义的方法
    - v-model表单输入和应用状态中做双向数据绑定
  - 用组件构建: 拥有预定义选项的一个 Vue 实例
- vue实例是什么？怎么创建？
  - 构造器
    - 构造函数 **Vue** 创建vue根实例
    - 扩展Vue构造器: **Vue.extend**
  - 属性与方法
    - data
      - 只有实例创建时的data属性才会被代理,之后添加的新属性不会触发视图更新
    - 暴露的属性和方法
      - vm.$data === data
      - vm.$el === document.getElementById('example')
      - vm.$watch(key, function(newValue, oldValue){  }): key改变后调用cb
        - 注意key和回调方法不要使用箭头函数(如 ** vm.$watch('a', newVal => this.myMethod())** ),因为箭头函数承接上下文,所有 **this** 不会指向vue实例.
    - 实例的生命周期
- 模板语法: DOM绑定Vue实例的数据;虚拟DOM渲染
  - 文本
    - "Mustache"语法,{{  }}插值
    - v-once指令组织绑定节点上所有数据更新
  - 纯HTML: v-html指令输出真正的html
  - 属性: v-bind:key="value"指令绑定html属性
  - 使用js表达式
    - 不能使用语句: 比如var if()else()
    - 不能访问用户定义的全局变量,可用Math和Date
- 计算属性
- vue如何绑定class和style
- 条件渲染和列表渲染
- 事件处理器
- 表单控件绑定
- 组件


## 进阶

- 深入响应式原理
- 过渡效果和过渡状态
- Render函数的使用
- 如何自定义指令
- 混合
- vue插件
- 单文件组件
- 生产环境的部署
- 路由
- 状态管理
- 单元测试
- 服务端渲染
