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
  - 插值
    - 文本
      - "Mustache"语法,{{  }}插值
      - v-once指令组织绑定节点上所有数据更新
    - 纯HTML: v-html指令输出真正的html
    - 属性: v-bind:key="value"指令绑定html属性
    - 使用js表达式
      - 不能使用语句: 比如var if()else()
      - 不能访问用户定义的全局变量,可用Math和Date
  - 指令: 指令属性的值预期是 **单一JavaScript表达式**
    - 参数
    - 修饰符
  - Filters
    - 过滤器: 添加在 **mustache插值** 的尾部,用管道符 **|** 指示
  - 缩写
    - v-bind => :
    - v-on => @
- 计算属性:
  - computed: { your computed function }
  - 计算属性 vs Methods
    - 计算属性只会在依赖改变时才会取值,否则返回之前调用的结果,而methods会每次调用取值
  - 计算属性 vs Watched Property
  - 计算 setter
  - 观察 Wactchers: 数据变化响应时,需要执行异步操作或开销较大的操作
- vue如何绑定class和style
  - v-bind:class="yours": yours可以是字符串或者数组或者对象
  - 组件上的class会被绑定在跟元素上
  - v-bind:style="yours": yours使用对象更加直观
  - 内敛样式的绑定是自动走鞥家前缀
- 条件渲染
  - **v-if** 和 **v-else**
  - **<template>**　中使用 **v-if** 适用于条件组,<template>不会被渲染
  - 带 **key** 的元素会从新渲染,否则会复用
  - v-show:切换元素的display属性
- 列表渲染
  - v-for: (item, index) in items, (item, index) of items 或者 (value, key, index) in object
  - **<template>** 中的v-for可以渲染多个元素块
  - 整数迭代: n in 10
  - 组件和v-for: 数据不会传递到组件中,必须使用v-bind
  - 数组更新测试
- 事件处理器
  - v-on:
    - 监听DOM事件,直接执行js代码
    - 绑定方法名
    - 绑定内联js语句
    - 可传递特殊变量 **$event**
  - 事件修饰符
    - v-on:click.stop 组织单击事件冒泡
    - v-on:submit.prevent 提交事件不再重载页面
    - v-on:click.stop.prevent 修饰符可以串联
    - v-on:submit.prevent 只有修饰符
    - v-on:click.capture="doThis" 添加事件侦听器时使用事件捕获模式
    - v-on:click.self="doThis" 只在事件在该元素本身(而不是子元素)触发时触发回调
    - v-on:click.once 单击事件最多执行一次
  - 按键修饰符
    - v-on:keyup.13='submit'
    - v-on:keyup.enter='submit'
    - @keyup.13='submit'
- 表单控件绑定
  - v-model
  - 修饰符
- 组件
  - 什么是组件
  - 如何注册组件
  -

## 进阶

- 深入响应式原理
  - vue不能检测到对象属性的添加或删除,属性必须存在在data对象上才可以监听变化
  - 使用 **Vue.set(obj, key, value)** 或者 **vm.$set(obj, key, value)** 将响应属性添加到嵌套的对象上
  - 使用 **Object.assign()** 或 **_.extent()** 方法来添加属性,必须创建新对象的方式更新对象
  - **vm.nextTick(callback)** 可以在组件更新完后调用。
- 过渡效果和过渡状态
  - **v-enter**, **v-enert-active**, **v-leave**, **v-leave-active**
- Render函数的使用
  - return createElement(tagName, this.$slots.default)
- 如何自定义指令
  - 钩子函数
    - bind:只调用一次，指令第一次绑定到元素上使用，可以执行初始化
    - inserted: 被绑定元素插入父节点时调用(父节点存在即可调用,不必存在于document中)
    - update: 被绑定元素所在的模板更新时调用
    - componentUpdated: 被绑定元素所在模板完成一次更新周期时调用
    - unbind: 只调用一次,解绑时调用
  - 钩子函数参数
    - el
    - binding: object
      - name: 指令名
      - value: 指令的绑定值
      - oldValue: 指令绑定的前一个值
      - expression: 绑定值的字符串形式
      - arg: 传给指令的参数
      - modifiers: 一个包含修饰符的对象
    - vnode: Vue编译生产的虚拟节点
    - oldVnode: 上一个虚拟节点
- 混合
- vue插件
  - MyPlugin.install
  - Vue.use(MyPlugin)
- 单文件组件
- 生产环境的部署
- 路由
- 状态管理
- 单元测试
- 服务端渲染
