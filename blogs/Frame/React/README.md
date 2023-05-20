---
title: React
date: 2023-05-10
tags:
- React
categories:
- Frame
sidebar: auto
---

:::tip
React--- 一个专注于构建用户界面的 JavaScript 库，和vue和angular并称前端三大框架，不夸张的说，react引领了很多新思想，世界范围内是最流行的js前端框架，最新版本已经到了18，加入了许多很棒的新特性
:::

# React
## React的基本知识
#### React的特点
* **声明式UI（JSX）**
  > 使用JS进行页面、逻辑编写
  ```html
  <!-- Vue -->
  <ul>
    <li v-for="item in list">react</li>
  </ul>
  ```
  ```html
  <!-- React -->
  <ul>
    { list.map(item => <li>react</li>) }
  </ul>
  ```
* **组件化**
  > 组件是react最重要的内容，通过一个个组件进行搭建整个页面，通过组件抽象增加复用能力和提高维护性。
* **跨平台**
  > react既可以开发web应用也可以使用同样的语法开发原生应用（react-native），比如安卓和ios应用，甚至可以使用react开发VR应用，想象力空间十足，react更像是一个 元框架  为各种领域赋能.

## 环境初始化
### 脚手架创建项目
* 使用命令行进行项目创建
  ```bash
  $ npx create-react-app react-basic
  ```
* 说明：
  * `npx create-react-app`是固定命令，`create-react-app`是React脚手架名称。
  * npx 命令会帮助我们临时安装create-react-app包，然后初始化项目完成之后会自自动删掉，所以不需要全局安装create-react-app
* 启动项目
  ```bash
  yarn start
  npm start
  ```
### 项目目录说明调整
* 目录说明 
  * `src`目录是项目开发目录
  * `package.json`中的两个核心库：react、react-dom
* 入口文件说明
  ```jsx
  import React from 'react'
  import ReactDOM from 'react-dom'
  import './index.css'
  import App from './App'
  ReactDOM.render(
    <React.StrictMode>
      <App/>
    </React.StrictMode>
  )
  document.getElememtById('root')
  ```
## JSX基础
### 1.JSX介绍
> JSX是 JavaScript XML（HTML）的缩写，表示在 JS 代码中书写 HTML 结构。用于在React中创建HTML结构（页面UI结构）
JSX 并不是标准的 JS 语法，是 JS 的语法扩展，浏览器默认是不识别的，脚手架中内置的 `@babel/plugin-transform-react-jsx` 包，用来解析该语法

### 2.JSX中使用JS表达式
**语法：** `{ JS表达式 }`
```JSX
const name = 'admin'
<h1>Hello! I am {name}.</h1>
```
**表达式类型：**
  * 字符串，数值，布尔值，null，undefined，object
  * 函数方法
**注意：**
> if 语句/ switch-case 语句/ 变量声明语句，这些叫做语句，不是表达式，不能出现在 {} 中！！

### 3.JSX列表渲染
**vue中实现列表渲染使用`v-for`实现。react中使用数组方法`map`实现。**
```JSX
const people = [
  {id: 1, name: 'Admin'},
  {id: 2, name: 'Root'}
]

function App() {
  return (
    <div>
      <ul>
        {people.map(p => <li key={p.id}>{p}</li>)}
      </ul>
    </div>
  )
}
```
**注意：** 遍历列表同样和vue一样需要key值进行diff算法的提升。

### 4.JSX条件渲染
**可以使用三元运算符或逻辑与(&&)运算符实现。**
```JSX
// 来个布尔值
const flag = true
function App() {
  return (
    <div className="App">
      {/* 条件渲染字符串 */}
      {flag ? 'react真有趣' : 'vue真有趣'}
      {/* 条件渲染标签/组件 */}
      {flag && <span>this is span</span>}
    </div>
  )
}
export default App
```
**原则：** 模板中的逻辑尽量精简。
负责的多分支逻辑，收敛为一个函数。模板中只负责调用这个定义分支逻辑的函数。
```JSX
fucntion getHtag(type) {
  if(type === 1) {
    return <h1>h1</h1>
  }
  else if(type === 2) {
    return <h2>h2</h2>
  }
  else {
    return <h3>h3</h3>
  }
}

function App() {
  return (
    <div className="App">
      {getHtag(1)}
      {getHtag(2)}
      {getHtag(3)}
    </div>
  )
}
```

### 5.JSX样式处理
* **内联样式（行内样式）**
  * 即在元素身上绑定style属性。
  ```JSX
  function App() {
    return (
      <div className="App">
        <div style={{color:'red'}}>
          <span>Hello</span>
        </div>
      </div> 
    )
  }

  //精简版
  const styleObj = {
    color: 'red'
  }
  function App() {
    return (
      <div className="App">
        <div style={styleObj}>
          <span>Hello</span>
        </div>
      </div> 
    )
  }
  ```
* **类名样式**
  * 在元素身上绑定一个classname控制样式
  ```JSX
  function App() {
    return (
      <div className="App">
        <span className="active"> Hello </span>
      </div>
    )
  }
  ```
* **动态控制类名**
  * 在Vue中动态控制样式采用`:class={active:isActive}`形式操作。
  * 在React中动态控制样式采用三元运算符进行操作。
  ```JSX
  function App() {
    return (
      <div className="App">
        <span className={isActive ? 'active' : ''}></span>
      </div>
    )
  }
  ```

### 6.JSX注意事项
* **JSX中必须有一个根节点，若没有根节点，则使用 `<></>` 幽灵节点代替。**
* **所有标签必须闭合，成对闭合或自闭合均可。**
* **JSX中属性名使用驼峰命名法：`class -> className`、`for -> htmlFor`**
* **JSX支持多行、换行，若需要换行，则用（）进行包裹。**

## React组件
### 组件概念
> React 组件是一段可以 使用标签进行扩展 的 JavaScript 函数

### 函数组件
> 使用JS的函数创建的组件。
```JSX
// 定义函数组件
function HelloFn () {
  return <div>这是我的第一个函数组件!</div>
}

function App () {
  return (
    <div className="App">
      {/* 渲染函数组件 */}
      <HelloFn />
      <HelloFn></HelloFn>
    </div>
  )
}
export default App
```
**注意：**
  * 组件名称必须首字母大写，React内部会根据这个来判断是组件还是普通的HTML标签。
  * 函数组件必须有返回值，表示该组件的UI结构；若不需要渲染任何内容，则返回null。
  * 对于函数组件来说，渲染的内容就是函数的返回值。
  * 使用函数名称作为组件标签名称，可成对出现也可自闭和。

### 类组件
> 使用ES6的class创建的组件。
```JSX
// 引入React
import React from 'react'

// 定义类组件
class HelloC extends React.Component {
  render () {
    return <div>这是我的第一个类组件!</div>
  }
}

function App () {
  return (
    <div className="App">
      {/* 渲染类组件 */}
      <HelloC />
      <HelloC></HelloC>
    </div>
  )
}
export default App
```
**注意：**
  1. 类名称也必须以大写字母开头。
  2. 类组件应该继承`React.Component`父类，从而使用父类中提供的方法或属性。
  3. 类组件必须提供`render`方法`render`方法必须有返回值，表示该组件的`UI`结构。
  4. 组件可以渲染其他组件，但不能嵌套他们的定义！

## 事件绑定
### 绑定方法
* **语法：**
  * on + 事件名称 = {事件处理程序}，eg：`<div onClick={onClikc}></div>`
* **注意点：**
  * react事件采用驼峰命名法，例如：`onMouseEnter`、`onFocus`
* **样例**
  ```JSX
  function Fn() {
    const clickFn = () => console.log('函数组件事件')
    return (
      <>
        <button onClick={clickFn}>Click</button>
      </>
    )
  }

  class Obj extends React.Component {
    clickFn = () => console.log('类组件事件')
    render() {
      return (
        <>
          <button onClick={this.clickFn}>Click</button>
        </>
      )
    }
  }
  ```

### 获取事件对象
> 获取事件对象e只需要在事件的回调函数中补充一个形参e即可
```JSX
function Fn() {
  const clickFn = (e) => console.log(e)
  return (
    <div>
      <button onClick={clickFn}></button>
    </div>
  )
}
```

### 事件传值
> 改造事件绑定为箭头函数，在箭头函数中完成参数的传递。
**语法：** `onClick={() => clickFn(msg)}`
``` JSX
import react from "react"
const TestComponent = () => {
  const list = [
    {id: 1001, name: 'Admin'},
    {id: 1002, name: 'Root'}
  ]
}
```


## 组件状态
> 在React hook出现之前，函数式组件是没有自己的状态的，所以显示域类组件进行了解。
> 步骤：初始化状态 -> 读取状态 -> 修改状态 -> 影响视图
### 初始化状态
* 通过`class`的实例属性`state`来初始化。
* `state`的值是一个对象结构，表示一个组件可以有多种数据状态。
* 通过`this.state`来获取状态。
```JSX
class Counter extends React.Component {
  state = {
    count: 0
  }
  render() {
    return <div>{this.state.count}</div>
  }
}
```

### 修改状态
* 通过 **`this.setState({要修改的变量})`**
* setState方法作用
  * 修改state中的数据状态
  * 更新UI
* 思想
  * 数据驱动视图，只要修改数据状态，页面就会自动刷新，无需手动操作DOM。
* 注意事项
  * **不能直接修改`state`中的值，必须通过`setState`方法进行修改。**
```JSX
class Counter extends React.Component {
  state = {
    count: 0
  }
  changeCount = () => {
    this.setState({
      count: this.state.count + 1
    })
  }
  render() {
    return (
      <button onClick={this.changeCount}>{this.state.count}</button>
    )
  }
}
```
* **注意：**
  * 如果类组件中函数不去使用箭头函数定义，则this指向会变为undefined。
  * 解决方案：
    * 使用constructor进行this的绑定修改。
    ```JSX
    class Counter extends React.Component {
      constructor() {
        super()
        this.changeCount = this.changeCount.bind(this)
      }
      
      state = {
        count: 0
      }

      changeCount() {
        this.setState({
          count: this.state.count + 1
        })
      }
    }
    ```
    * onClick内部使用箭头函数修改
    ```JSX
    class Counter extends React.Component {
      state = {
        count: 0
      }

      changeCount() {
        this.setState({
          count: this.state.count + 1
        })
      }

      render() {
        return (
          <button onClick={()=>this.setState()}>{this.state.count}</button>
        )
      }
    }
    ```

### React状态不可变
> **不要直接去修改状态的值，而是基于当前状态创建新的状态值。**

* 错误的直接修改：
```JSX
state = {
  count : 0,
  list: [1,2,3],
  person: {
     name:'jack',
     age:18
  }
}
// 直接修改简单类型Number
this.state.count++
++this.state.count
this.state.count += 1
this.state.count = 1

// 直接修改数组
this.state.list.push(123)
this.state.list.spice(1,1)

// 直接修改对象
this.state.person.name = 'rose'
```

* 基于当前状态创建新值：
```JSX
this.setState({
  count: this.state.count + 1,
  list: [...this.state.list, 4],
  person: {
    ...this.state.person,
    name: 'Rose'
  }
})
```

## 表单处理
### 受控表单组件
:::tip
受控组件即 **可以被react状态控制的组件** <br/>
React组件状态存放处在state中，input表单元素自身状态在value中，React将state与表单元素的值（value）绑定在一起，由state的值来控制表单元素的值，从而保证数据单一性。
:::
* 实现步骤
  1. 在组件的state中声明组件的状态和数据。
  2. 将状态数据设置为input标签元素的value属性的值。
  3. 为input添加change事件，事件处理程序中，通过e.target获取到当前文本框值。
  4. 调用setState方法，将文本框值设置为state状态的值。
* 即Vue中v-model实现的逻辑。
```JSX
import React from 'react'
class Counter extends React.Component {
  state = {
    count: 'loading...'
  }

  changeCount = (e) => {
    this.setState({
      count: e.target.value
    })
  }

  render() {
    return (
      <>
        <input type="text" onChange={this.changeCount} value={this.state.count} />
        {this.state.count}
      </>
    )
  }
}

function App() {
  return (
    <div className="App">
      <Counter />
    </div>
  )
}

export default App
```

### 非受控表单组件
> 非受控组件即通过手动操作DOM方式获取文本框的值，文本框的状态不受react组件的state中的状态控制，直接通过原生DOM获取输入的值。

* 实现步骤
  1. 导入`createRef`函数。
  2. 调用createRef函数，创建一个ref对象，存储到名为msgRef的实例属性中。
  3. 为input添加ref属性，值为msgRef。
  4. 在按钮的事件处理程序中，通过`msgRef.current`即可拿到input对应的DOM元素，而其中`msgRef.current.value`拿到的是文本框的值。
  
```JSX
import React, { createRef } from "react";

class Counter extends React.Component {
  msgRef = createRef()
  
  logMsg = () => {
    console.log(this.msgRef.current.value);
  }

  render() {
    return (
      <>
        <input type="text" ref={this.msgRef} />
        <button onClick={this.logMsg}>click</button>
      </>
    )
  }
}

function App() {
  return (
    <div className="App">
      <Counter/>
    </div>
  )
}

export default App
```


## React组件间通信
组件是独立且封闭的单元，默认情况下组件只能使用自己的数据（state）<br/>
组件化开发的过程中，完整的功能会拆分多个组件，在这个过程中不可避免的需要互相传递一些数据 <br/>
为了能让各组件之间可以进行互相沟通，数据传递，这个过程就是组件通信 <br/>
  1. 父子关系
  2. 兄弟关系 - 自定义事件模式产生技术方法 eventBus / 通过共同的父组件通信
  3. 其他关系 - **mobx / redux / zustand**

### 父传子
**实现步骤：**
  1. 父组件提供需要传输的数据 - **state**
  2. 给子组件标签添加属性值为state中的数据
  3. 子组件通过 **props** 接收父组件传递过来的数据
    * 类组件使用 **this.props** 获取props对象。
    * 函数式组件直接通过 **props** 参数获取props对象。

![](https://cdn.nlark.com/yuque/0/2022/png/274425/1654490432739-ea283505-3ddd-4403-9fba-7735b04b451e.png)

**代码实现：**
```JSX
import React from 'react'

function Son(props) {
  // 函数组件通过props参数获取数据
  return (
    <>
      <h1>函数组件 - {props.msg}</h1>
    </>
  )
}

class Son2 extends React.Component {
  // 类组件通过this.props获取数据
  render() {
    return (
      <>
        <h1>类组件 - {this.props.msg}</h1>
      </>
    )
  }
}

class App extends React.Component {
  state = {
    msg: 'this is a message.'
  }

  render() {
    return (
      <div className='App'>
        <Son msg={this.state.msg} />
        <Son2 msg={this.state.msg} />
      </div>
    )
  }
}

export default App
```

### props说明
1. **props是只读对象（readonly）**
根据单向数据流的要求，子组件只能读取props中的数据，不能进行修改。<br/>
`this.props.msg = 'new msg'`是非法修改。
2. **props可以传递任意数据**
数字、字符串、布尔值、数组、对象、JSX、函数。
```JSX
class App extends React.Component {
  state = {
    message: 'this is message'
  }
  render() {
    return (
      <div>
        <div>父组件</div>
        <FSon 
          msg={this.state.message} 
          age={20} 
          isMan={true} 
          cb={() => { console.log(1) }} 
          child={<span>this is child</span>}
        />
        <CSon msg={this.state.message} />
      </div>
    )
  }
}
```

### 子传父
> **父组件给子组件传递回调函数，子组件进行调用。**
**实现步骤：**
  1. 父组件提供一个回调函数，用于接收数据。
  2. 将函数作为属性的值，传递给子组件。
  3. 子组件通过props调用回调函数。
  4. 将子组件中的数据作为参数传递给回调函数。

**代码实现：**
```JSX
import React from 'react'

// 子组件
function Son(props) {
  function handleClick() {
    // 调用父组件传递过来的回调函数 并注入参数
    props.changeMsg('this is newMessage')
  }
  return (
    <div>
      {props.msg}
      <button onClick={handleClick}>change</button>
    </div>
  )
}


class App extends React.Component {
  state = {
    message: 'this is message'
  }
  // 提供回调函数
  changeMessage = (newMsg) => {
    console.log('子组件传过来的数据:',newMsg)
    this.setState({
      message: newMsg
    })
  }
  render() {
    return (
      <div>
        <div>父组件</div>
        <Son
          msg={this.state.message}
          // 传递给子组件
          changeMsg={this.changeMessage}
        />
      </div>
    )
  }
}

export default App
```

### 兄弟传值
> **通过状态提升机制，利用共同的父组件实现兄弟通信。**
**实现步骤：**
  1. 将共享状态提升到最近的公共父组件中，由公共父组件管理这个状态。
    * 提供共享状态
    * 提供操作共享状态的方法
  2. 要接收数据状态的子组件通过props接收数据。
  3. 要传递数据状态的子组件通过props接收方法，调用方法传递数据。

**代码实现：**
```JSX
import React from 'react'

// 子组件A
function SonA(props) {
  return (
    <div>
      SonA
      {props.msg}
    </div>
  )
}
// 子组件B
function SonB(props) {
  return (
    <div>
      SonB
      <button onClick={() => props.changeMsg('new message')}>changeMsg</button>
    </div>
  )
}

// 父组件
class App extends React.Component {
  // 父组件提供状态数据
  state = {
    message: 'this is message'
  }
  // 父组件提供修改数据的方法
  changeMsg = (newMsg) => {
    this.setState({
      message: newMsg
    })
  }

  render() {
    return (
      <>
        {/* 接收数据的组件 */}
        <SonA msg={this.state.message} />
        {/* 修改数据的组件 */}
        <SonB changeMsg={this.changeMsg} />
      </>
    )
  }
}

export default App
```

### 跨组件通信Context
> **利用Context来实现跨层级组件传值，无需为每层组件手动添加props，即可机械能传递。**
**实现步骤：**
  1. 创建Context对象，导出Provider和Consumer对象。
  ```JSX
      const { Provider, Consumer } = createContext()
  ```
  2. 使用Provider包裹上层组件提供数据。
  ```JSX
    <Provider value={this.state.message}>
      {/** 根组件 */}
    </Provider>
  ```
  3. 需要用到数据的组件使用Consumer包裹获取数据。
  ```JSX
    <Consumer>
      {value => /* 基于context进行渲染 */}
    </Consumer>
  ```

**注意：**
   * 上层组件和下层组件的关系是相对的，只要存在就可以使用。
   * 语法一般为固定的。提供位置必须为`value`提供数据。获取位置必须是`{value => ...}`形式。

**代码实现：**
```JSX
import React, { createContext } from 'react'

const { Provider, Consumer } = createContext()

function A() {
  return (
    <>
      <h4>this is A</h4>
      <C />
    </>
  )
}

function C() {
  return (
    <>
      <h4>this is C</h4>
      <Consumer>
        {value => <span>{value}</span>}
      </Consumer>
    </>
  )
}


class App extends React.Component {
  state = {
    msg: 'this is a message'
  }

  render() {
    return (
      <Provider value={this.state.msg}>
        <div className='App'>
          <A />
        </div>
      </Provider>
    )
  }
}

export default App
```

## React组件进阶
### children属性
> **children表示该组件的子节点，只要组件内部有子节点，则props就具有children属性。**

children使用方式类似于Vue中的插槽。若并列传递，则接收时children为数组。

**类型：** 
  1. 普通文本
  2. 普通标签元素
  3. 函数 / 对象
  4. JSX

```JSX
import React from 'react'

function A({ children }) {
  return (
    <>
      {children}<br />
      <span>hello</span>
    </>
  )
}

class App extends React.Component {
  render() {
    return (
      <div className='App'>
        <A>
          this is a A
        </A>
      </div>
    )
  }
}

export default App
```

### props检验
> **利用prop-types包对传入props值进行类型校验。**
类似于vue中的defineProps中进行类型的校验。

**实现步骤：**
  1. 安装属性校验包：`npm i prop-types`。
  2. 导入`prop-types`包。
  3. 使用`组件名.propTypes = {}`给组件添加校验规则。

**核心代码：**
```JSX
import PropTypes from 'prop-types'

const List = props => {
  const arr = props.colors
  const lis = arr.map((item, index) => <li key={index}>{item.name}</li>)
  return <ul>{lis}</ul>
}

List.propTypes = {
  colors: PropTypes.array
}
```

### props检验-规则说明
**四种常见结构**
  1. 常见类型：array、bool、func、number、object、string
  2. React元素类型：element
  3. 必填项：isRequired
  4. 特定的结构对象：shape({})

**核心代码**
```JS
// 常见类型
optionalFunc: PropTypes.func,
// 必填 只需要在类型后面串联一个isRequired
requiredFunc: PropTypes.func.isRequired,
// 特定结构的对象
optionalObjectWithShape: PropTypes.shape({
	color: PropTypes.string,
	fontSize: PropTypes.number
})
```

### props校验-默认值
> **通过`defaultProps`可以对组建的props设置默认值，在未传入props时生效。**
> 
#### 函数组件
**直接使用函数参数默认值**
```JSX
function List({pageSize = 10}) {
  return (
    <div>
      此处展示props的默认值：{ pageSize }
    </div>
  )
}
```

**使用`组件.defineProps`属性**
```JSX
function List({pageSize}) {
  return (
    <div>
      此处展示props的默认值：{ pageSize }
    </div>
  )
}
List.defineProps = {
  pageSize: 10
}
```

#### 类组件
> **使用类静态属性声明默认值，`static defaultProps = {}`**
```JSX
class List extends Component {
  static defaultProps = {
    pageSize: 10
  }
  render() {
    return (
      <div>
        此处展示props的默认值：{this.props.pageSize}
      </div>
    )
  }
}
<List />
```

## 生命周期
:::tip
**组建的生命周期是指组件从被创建到挂载到页面中运行起来，再到组件不用时卸载的过程。**<br/>
**注意：只有类组件才有生命周期！**
:::
![生命周期](https://cdn.nlark.com/yuque/0/2022/png/274425/1654490712545-6bd28fa7-290b-48fb-8d51-bbf5578dad3f.png)

### 生命周期 - 挂载阶段
![挂载阶段](https://cdn.nlark.com/yuque/0/2022/png/274425/1654490729034-d2d80cce-7fab-4dd8-bcbc-29e33bdffb63.png)

#### constructor
**触发时机**
* 创建组件时最先执行，初始化的时候只执行一次。

**作用**
1. 初始化state
2. 创建Ref
3. 使用bind解决this指向等

#### render
**触发时机**
* 每次组件渲染时触发。

**作用**
* 渲染UI结构，此中不能调用`setState`会造成页面重新绘制而造成死循环。

#### componentDidMount
**触发时机**
* 组件挂载时（完成DOM渲染后）执行，初始化时执行一次。
* 类似于Vue中的`Mounted`

**作用**
1. 发送网络请求
2. DOM操作

### 生命周期 - 更新阶段
![更新阶段](https://cdn.nlark.com/yuque/0/2022/png/274425/1654490742583-b933202d-3de7-41ae-b9ba-75ae1d2af34c.png)

#### render
**触发时机**
* 每次组件渲染时都会触发。

**作用**
* 渲染UI（与挂载阶段的render是同一个render）

#### componentDidUpdate
**触发时机**
*  组件更新后触发（DOM渲染完毕）

**作用**
* 进行DOM操作，可以直接获取到更新后的DOM。
* 不能在此调用`setState`函数，会一直更新下去。
* 类似于Vue的Updated。

### 生命周期 - 卸载阶段
#### componentWillUnmount
**触发时机**
* 组件卸载（从页面消失）

**作用**
* 执行清理工作（清除定时器）

**如果组件中的数据会影响视图，则定义在`state`中，若不影响即可直接定义。（例如定时器参数）**

## Hooks基础

## Hooks进阶

# React Router

# Mobox

# Redux
