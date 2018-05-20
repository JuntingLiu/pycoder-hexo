---
title: Echo
date: 2018-05-21 00:29:53
categories:
- JavaScript
tags:
- Vue
- CSS
- CSS3
copyright: true
---

<div style="width: 100%; text-align: center">
  <img src="https://user-gold-cdn.xitu.io/2018/5/21/1637e6486e18bf28?w=1000&h=391&f=png&s=64928" width="400" />
</div>

---
![](https://user-gold-cdn.xitu.io/2018/5/21/1637e5e3f1e4c040?w=3358&h=1704&f=gif&s=477036)
# Echo

这是一个网络应用程序，与我的女朋友一起庆祝 5 月 20 日（意思是“我爱你”）。 ;P 它受 iMessage 中名为 echo 的消息效果的启发。

只是让你开心。

嗯，这就是此作者的原话，满满的撒狗粮 🐶🐶🐶，但是此程序还是很有趣的对不对～所以还是拉下代码，悄悄的 👀 一波（毕竟单身汪，周末也没什么事）

## 预览

[demo](https://twitchboy.github.io/echo_520/index.html)

## 将学到的知识点

* 单一 div 气泡绘制
* 随机大小位置
* 动画效果
* 内存回收

## 气泡绘制

可以看出它是由一个椭圆和一个小尾巴构成。

如何绘制下这个小尾巴？

先看下这篇文章了解下使用[CSS3绘制图形基本原理](https://www.jianshu.com/p/56256db2df2f)

![](https://user-gold-cdn.xitu.io/2018/5/21/1637e5ed508ef1a0?w=590&h=426&f=jpeg&s=15166)

```css
width: 10rem;
height: 10rem;
background-color: orangered;
border-left: 1rem solid orange;
border-bottom-left-radius: 10rem 7rem;
```

看此上，将背景色取掉；是不是一个小尾巴就出来了，缩小下尺寸，汽泡的小尾巴就就出来了～这里我们通过伪类元素来绘制气泡的小尾巴。

![](https://user-gold-cdn.xitu.io/2018/5/21/1637e5ef6041ede0?w=318&h=150&f=jpeg&s=12121)

## 随机大小位置

气泡是绝对定位的，控制随机出现的位置，其实就是控制 `left`和 `top`值。

1. 先获取当前可视窗口尺寸
2. 控制气泡出现的在可视窗口的范围内， `left` 和 `top` 小于可视窗口宽高的值
3. 大小，使用 CSS3 里的 `transform` 属性的 `scale()` 来控制（肯定不能比本身的小）

```js
const left = Math.ceil(Math.random() * 0.9 * screenSize.width)
const top = Math.ceil(Math.random() * 0.9 * screenSize.width)
const scale = 1 + Math.random(); // 缩放值
```

## 内存回收

内存回收实现原理，`good` 作为是否回收的标志（全 `false` 进行回收）。整个流程就是每一个消息 `good` 默认为 `true`, 当某条消息完成了消失动画以后，就会将 `good` 状态变为 `false`; 然后将固定的第一条消息以外的全部消息中的 `good` 提取出来。我们的最终目的是判断当前提取出来的新数组里是否还存在处于展示状态的消息，无论消息量有多少，只需要判断是否至少有一个 `good` 状态为 `true`即可，直到全部消息的 `good` 状态都为 `false`了，我们再进行内存回收 ♻️，也就是对 `msgs` 重置。

内存回收的实现:

```js
const hasMsgs = this.msgs
  .slice(1)
  .map(({ good }) => good)
  .reduce((left, right) => left || right);  // 找出任意一个为 true 的状态

if (!hasMsgs) this.msgs.splice(1);
```

[参考DEMO](https://github.com/iwillwen/echo)

## License

MIT Licensed.
