---
title: Vue3
date: 2023-02-11
tags:
- Vue
categories:
- Frame
sidebar: auto
---

## Vue3
2020年9月18日，Vue.js发布3.0版本，代号：One Piece

## Vue3优势
**性能提升：**
* 打包大小减少41%
* 初次渲染快55%，更新渲染快133%
* 内存减少54%

**源码升级：**
* 使用`Proxy`代替`defineProperty`实现响应式。
* 重写虚拟`DOM`的实现和`Tree-Shaking`
* Vue3可以更好的支持`TypeScript`

**新的特性：**<br/>
**① Composition API（组合API）**
* `setup`配置
* `ref`与`reactive`
* `watch`与`watchEffect`
* `provide`与`inject`
**② 新的内置组件**
* `Fragment`
* `Teleport`
* `Suspense`
**③ 其他改变**
* 新的生命周期钩子
* data选项应始终被声明为一个**函数**
* 移除`keyCode`支持作为`v-on`的修饰符

## 创建Vue3工程
### vue-cli创建工程
```bash
## 查看@vue/cli版本，确保@vue/cli版本在4.5.0以上
vue --version
## 安装或者升级你的@vue/cli
npm install -g @vue/cli
## 创建
vue create vue_test
## 启动
cd vue_test
npm run serve
```
### vite创建工程
* vite---新一代前端构建工具
* **优势：** ① 开发环境中，无需打包，可快速冷启动。② 轻量快速的热重载（HMR）③ 真正的按需编译，无需等待整个应用编译完成。
```bash
## 创建工程
npm init vite-app <project-name>
## 进入工程目录
cd <project-name>
## 安装依赖
npm install
## 运行
npm run dev
```

## Vue3入口文件
**旧版：**
```js
import Vue from 'vue'
import App from './App.vue'

new Vue({
    render: h => h(App)
}).$mount('#app')
```

**新版：**
* 引入的不再是Vue构造函数，而是`createApp`工厂函数。
* 创建实例对象app相当于Vue2中的vm实例对象，但app相比vm更加轻量。
```js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

## 常用Composition API
### setup核心
**① 理解：Vue3中新的配置项，值为一个函数。**<br/>
**② setup是所有Composition API的基础。**<br/>
**③ 组件中所用到的：数据、方法等等，均需配置在setup中。**<br/>
**④ setup的两种返回值：**
* 若返回一个对象，则对象中的属性、方法, 在模板中均可以直接使用。（重点关注！）
```vue
<script>
    export default {
        name: 'App',
        setup() {
            let data = '',

            function showData() {
                ...
            },

            return {
                data,
                showData(),
            }
        }
    }
</script>
```
* 若返回一个渲染函数：则可以自定义渲染内容。
```vue
<script>
    import { h } from 'vue',
    export default {
        name: 'App',
        setup() {
            return () => {
                return h('渲染标签值', '渲染内容')
            }
        }
    }   
</script>
```
:::tip
**注意：** <br/>
<strong style="color:#DD5145">尽量不要将Vue2与Vue3语法混用:</strong>
* Vue2.x配置（data、methods、computed）中可以访问搭配setup中的属性和方法。
* 在setup中<strong style="color:#DD5145">不能访问到</strong>Vue2.x配置
* 如果有重名情况，则setup优先
<strong style="color:#DD5145">setup不能是一个async函数</strong>，因为返回值不再是return的对象，而是promise，二模板无法查看return对象中的属性。若需要返回Promise实例，则需要Suspense和一部组件的配合使用。
:::

### ref函数
**作用：定义一个响应式的数据**<br/>
**语法：`const xxx = ref(initValue)`**
* 创建了一个包含响应式数据
* JS中操作数据：`xxx.value`
* 模板中读取数据：不需要`.value`，直接：`<div>{{ xxx }}</div>`
:::tip
**备注：**
* **接收的数据可以是：基本类型、对象类型。**
* <strong style="color:#DD5145">基本类型数据：响应式依然依靠`Obejct.defineProperty()`的`get`和`set`完成。</strong>
* <strong style="color:#DD5145">对象类型数据：内部使用了Vue3的新函数:----`reactive`函数。即Proxy的实现</strong>
:::