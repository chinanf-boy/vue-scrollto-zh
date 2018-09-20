# vue-scrollto [![explain]][source] [![translate-svg]][translate-list] 
    
<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 滚动元素从未如此简单! 」

[中文](./readme.md) | [english](https://github.com/rigor789/vue-scrollto)


---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'rigor789/vue-scrollto' -->
<!-- commit = 'd419a1b25c03c80b230750138910071d8233046a' -->
<!-- time = '2018 9.13' -->
翻译的原文 | 与日期 | 最新更新 | 更多
---|---|---|---
[commit] | ⏰ 2018 9.13 | ![last] | [中文翻译][translate-list]

[last]: https://img.shields.io/github/last-commit/rigor789/vue-scrollto.svg
[commit]: https://github.com/rigor789/vue-scrollto/tree/d419a1b25c03c80b230750138910071d8233046a

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---


# vue-scrollto

[![Vue 2.x](https://img.shields.io/badge/Vue-2.x-brightgreen.svg)](https://vuejs.org/v2/guide/)
[![npm](https://img.shields.io/npm/v/vue-scrollto.svg)](https://www.npmjs.com/package/vue-scrollto)
[![npm-downloads](https://img.shields.io/npm/dm/vue-scrollto.svg)](https://www.npmjs.com/package/vue-scrollto)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/rigor789/vue-scrollto/blob/master/LICENSE)

滚动元素从未如此简单!


### [DEMO](https://chinanf-boy.github.io/vue-scrollto-zh/#/examples.zh)


这是为了`vue 2.x`

对于`vue 1.x`请使用`vue-scrollTo@1.0.1`(注意大写字母T),但也请记住旧版本依赖于`jquery`.

## 在引擎盖下

`vue-scrollto`使用`window.requestAnimationFrame`执行动画,从而提供最佳性能.

使用[bezier-easing](https://github.com/gre/bezier-easing)完成动作曲线函数- 经过充分测试的微小库.

<p class="tip">
它甚至知道用户何时中断，并且不强制滚动会导致用户体验不良。
</p>

### 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [安装](#%E5%AE%89%E8%A3%85)
- [用法](#%E7%94%A8%E6%B3%95)
  - [作为vue指令](#%E4%BD%9C%E4%B8%BAvue%E6%8C%87%E4%BB%A4)
  - [周期函数](#%E5%91%A8%E6%9C%9F%E5%87%BD%E6%95%B0)
- [Options](#options)
    - [el / element](#el--element)
    - [container](#container)
    - [duration](#duration)
    - [easing](#easing)
- [缓动函数](#%E7%BC%93%E5%8A%A8%E5%87%BD%E6%95%B0)
    - [offset](#offset)
    - [force](#force)
    - [cancelable](#cancelable)
    - [onStart](#onstart)
    - [onDone](#ondone)
    - [onCancel](#oncancel)
    - [x](#x)
    - [y](#y)
- [同时滚动](#%E5%90%8C%E6%97%B6%E6%BB%9A%E5%8A%A8)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## 安装

这个包在npm上可用.

<p class="warning">
如果您之前使用过此软件包，请确保使用正确的软件包，因为它已从`vue-scrollTo`重命名为`vue-scrollto`

> 小写`t`
</p>

使用npm:

```bash
npm install --save vue-scrollto
```

使用yarn:

```bash
yarn add vue-scrollto
```

直接将其包含在html中:

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script src="https://cdn.jsdelivr.net/npm/vue-scrollto"></script>
```

<p class="tip">
当它包含在html中时，它会自动调用`Vue.use`,并设置一个你可以使用的'VueScrollTo`变量！
</p>

## 用法

`vue-scrollto`既可以用作vue指令,也可以用你的javascript编写.

### 作为vue指令

```js
var Vue = require('vue');
var VueScrollTo = require('vue-scrollto');

Vue.use(VueScrollTo)

// 你可以传递默认参数
Vue.use(VueScrollTo, {
     container: "body",
     duration: 500,
     easing: "ease",
     offset: 0,
     force: true,
     cancelable: true,
     onStart: false,
     onDone: false,
     onCancel: false,
     x: false,
     y: true
 })
```

如果您使用的是浏览器版本(直接在页面上包含脚本),则可以使用默认值设置:

```js
VueScrollTo.setDefaults({
    container: "body",
    duration: 500,
    easing: "ease",
    offset: 0,
    force: true,
    cancelable: true,
    onStart: false,
    onDone: false,
    onCancel: false,
    x: false,
    y: true
})
```

```html
<a href="#" v-scroll-to="'#element'">滚动 到 #element</a>

<div id="element">
    Hi. I'm #element.
</div>
```

如果需要自定义滚动选项,可以将对象文字传递给指令:

```html
<a href="#" v-scroll-to="{
     el: '#element',
     container: '#container',
     duration: 500,
     easing: 'linear',
     offset: -200,
     force: true,
     cancelable: true,
     onStart: onStart,
     onDone: onDone,
     onCancel: onCancel,
     x: false,
     y: true
 }">
    Scroll to #element
</a>
```

<p class="tip">
    有关可用选项的更多详细信息，请查看<a href="#Options">选项</a>部分。
</p>

### 周期函数

```js
var VueScrollTo = require('vue-scrollto');

var options = {
    container: '#container',
    easing: 'ease-in',
    offset: -60,
    force: true,
    cancelable: true,
    onStart: function(element) {
      // scrolling 开始
    },
    onDone: function(element) {
      // scrolling 结束
    },
    onCancel: function() {
      // scrolling 被取消啊
    },
    x: false,
    y: true
}

var cancelScroll = VueScrollTo.scrollTo(element, duration, options)

// 或者您可以在组件内部使用
cancelScroll = this.$scrollTo(element, duration, options)

// 要取消滚动，您可以调用返回的函数
cancelScroll()
```

## Options

#### el / element

要滚动到的元素.

#### container

需要滚动的容器.

*默认:* `body`

#### duration

滚动动画的持续时间(以毫秒为单位).

*默认:* `500` 

#### easing

动画时使用的曲线函数.阅读更多内容[缓动函数细节](#easing-detailed).

*默认:* `ease`

#### offset

滚动时应使用的偏移量.此选项接受回调函数 `v2.8.0`打上.

*默认:* `0`

#### force

指示是否应执行滚动,即使滚动目标已在视图中.

*默认:* `true`

#### cancelable

指示用户是否可以取消滚动.

*默认:* `true`

#### onStart

滚动开始时,应调用的回调函数.接收目标元素作为参数.

*默认:* `noop`

#### onDone

滚动结束时,应调用的回调函数.接收目标元素作为参数.

*默认:* `noop`

#### onCancel

滚动时已被用户中止(用户滚动,单击等),应调用的回调函数. 接收中止事件和目标元素作为参数.

*默认:* `noop`

#### x

我们是否想要滚动`x`轴

*默认:* `false`

#### y

我们是否想要滚动`y`轴

*默认:* `true`

<h2 id="easing-detailed">缓动函数</h2>

缓动函数使用[bezier-easing](https://github.com/gre/bezier-easing)计算,所以你可以将自己的具有4个值的数组的形式的值, 传递给`options.easing`,,或者您可以通过其特定的字符串名称, 来使用任何的默认缓动(`ease`,`linear`,`ease-in`,`ease-out`,`ease-in-out`).

`vue-scrollto`使用以下值作为默认缓动:

```js
let easings = {
    'ease': [0.25, 0.1, 0.25, 1.0],
    'linear': [0.00, 0.0, 1.00, 1.0],
    'ease-in': [0.42, 0.0, 1.00, 1.0],
    'ease-out': [0.00, 0.0, 0.58, 1.0],
    'ease-in-out': [0.42, 0.0, 0.58, 1.0]
}
```

## 同时滚动

如果需要同时滚动多个容器,可以直接导入`scroller`工厂,并创建多个实例.(由于性能原因,使用默认`scrollTo`方法一次只允许一个滚动操作.)

```js
import {scroller} from 'vue-scrollto/src/scrollTo'
const firstScrollTo = scroller()
const secondScrollTo = scroller()
firstScrollTo('#el1')
secondScrollTo('#el2')
```

## 执照

MIT
