---
title: 初探React
date: 2021-07-04 20:00:00
author: 安小盼
categories: 前端
tags:
  - React
  - 前端进阶
---

## 目标

- [x] jsx介绍
- [x] 开启项目
- [x] 函数组件和class组件
- [x] 组件生命周期
- [x] 常⻅错误和性能问题

## 知识要点

### 一、jsx介绍

使⽤ `react` 时，我们可以使⽤ `jsx` 语法来书写我们的模版。

### 1.1. 定义

它是类似 `DOM` 的 `xml` 结构的语法，区别是可以在 `jsx` 中使⽤ `{}` 来使⽤ `js` 表达式。

```html
<div className="foo">
  {something ? "something is true" : "something is false"}
</div>
```

### 1.2. 总结

1. `jsx` 是⼀种语法糖，我们需要将他们编译为 `React.createElement` 的形式
2. 写 `jsx` 需要注意类型必须合法，尤其是写布尔表达式
的时候需要额外注意，尽量使⽤三⽬运算符来书写 jsx
3. 需要注意 `class` 和 `for` 标签在书写时需要改为
`className` 和 `htmlFor`

### 二、创建项目

### 1. `CDN` 链接引入

[CDN链接 - React中文官网](https://react.docschina.org/docs/cdn-links.html)

### 2. 使用官方脚手架 `creact-react-app`

### 2.1. `npx` 方式

```cmd
// 创建项目
npx create-react-app <project-name>
// 进入项目目录并启动
cd <project-name>
npm run start
```

### 2.2. `npm` 方式

```cmd
// 全局安装create-react-app
npm install -g create-react-app
// 创建项目
create-react-app <project-name>
// 进入项目目录并启动
cd <project-name>
npm run start
```

### 三、函数组件和class组件

### 3.1. 函数组件

是一个函数去返回 `jsx`。

```jsx
function Foo(props) {
  return (
    <div>
      {props.text || 'Foo'}
    </div>
  );
}
```

### 3.2. class组件

以继承的形式，`render` 也返回一个 `jsx`

```jsx
class Bar extends React.Component {
  render() {
    return (
      <div>
        {this.props.text || 'Bar'}
      </div>
    );
  }
}
```

### 3.3. 区别

本质：是否要维护内部状态

1. 加载的 `props` ⽅式不同：获取传参
  * 函数式定义组件：从组件函数的参数加载
  * `class` 形式的组件：通过 `this.props` 获取传⼊的参数
2. 函数式组件⽐较简单，内部⽆法维护状态。`class` 形式内部可以通过 `this.state` 和 `this.setState` ⽅法更新内部 `state`，同时更新 `render` ⾥⾯的函数渲染的结果
3. `class` 组件内部可以定义更多的⽅法在实例上，但是函数式组件⽆法定义

### 四、组件生命周期

`componentWillMount` -> `render` -> `componentDidMount`(发送请求，服务端渲染友好)
`componentWillReceiveProps`(弃用) -> `componentWillUpdate` ->
`render` -> `componentDidUpdate`

### 五、常⻅错误和性能问题

### 5.1. 异步过程使⽤单例的 event 对象

`React` 中全局单例的 `event` 对象。 
异步操作最好将对象内部需要的值先进⾏拷⻉赋值。

### 5.2. 性能优化⽅式

* `react dev tools`：检测组件是否出现不必要的重新渲染
* [`why-did-you-render`](https://www.npmjs.com/package/@welldone-software/why-did-you-render)：能检测⻚⾯中的元素是否出现了不必要的重渲染
* `class` 中提前声明箭头函数：保证 `render` 执⾏过程中
的函数不会因为引⽤问题导致重新渲染。

### 5.3. immutable 库：immutable-js 和 immer

配合 `shouldComponentUpdate` 进⾏性能优化。通过判定对象是否为同一个引用，决定子组件是否重新渲染。

`immutable-js`和`immer`是 `js` 通用库。都可以做到让一个引用类型，`key` 改变了引用会断掉；不改变的话保持引用。

👍**`immer`**原生使用，`api`少，上手简单。
