---
title: JavaScript 忍者秘籍阅读记录
date: 2018-07-03 08:12:08
categories:
- JavaScript
tags:
- JavaScript
copyright: true
---

## 第一部分、准入训练

### 第一章、进入忍者世界

#### 通体介绍

JavaScript 库的产生是用来解决浏览器之间的差异和兼容性的，不同的库虽然在方法、内容和复杂性方面有很大的差异，但唯一不变的是：**它们需要简单而易用，产生最少开销，并能兼容所有浏览器，这些都是我们所希望的。**

通过了解如何构建最优秀的 JavaScript 库，可以为我们提供很好的洞察力，从而编写自己的代码来实现这些目标。

一个 JavaScript 库的组成可以分为三个方面：

1. JavaScript 语言的高级使用。
2. 跨浏览器代码的精心构建。
3. 当前能够聚众合一的最佳实践应用。

##### 理解 JavaScript 语言

JavaScript 中， **对象**、**函数**和**闭包**有着很密切的关系。理解三个概念之间的牢固关系，可以大大提高我们的 JavaScript 编程能力，为我们进行任意类型程序的开发打下坚实的基础。

另外，**定时器** 和 **正则表达式** 需要充分的对其了解和利用，熟练掌握定时器如何在浏览器内运行，可以让我们有能力解决复杂的编码任务，如长时间运行的计算和平滑的动画。而理解正则表达式是如何工作的，可以让我们简化原本相当复杂的代码片段。

> 学会如何高效使用高级语言特性，以及如何发挥其最大的优势，将代码质量提升到更高的水平。提升我们运用这些概念和特性的能力，提升我们的理解力，熟练掌握如何创建任意类型的 JavaScript 应用程序。这些基础知识，将为我们开始编写稳定跨浏览器代码的道路尊定坚实的基础。

##### 跨浏览器注意事项

权衡支持各种浏览器的成本和收益。主要考虑以下几点：

* 目标受众的期望和需求
* 浏览器的市场份额
* 支持浏览器所需要的工作量

##### 当前最佳实践

* 测试
* 性能分析
* 调试技巧

大量的测试技术和测试用例，以确保代码的运行符合我们的预期。
功能稳定，平台稳定，接下来就是对代码的性能分析，从而提高代码质量。

以下是一个简单的收集性能信息的代码：

```js
start = new Date().getTime();
for (let n = 0; n < maxCount; n++) {
    /*功能测试代码*/
}
elapsed = new Date().getTime() - start;
assert(true, "Measured time: " + elapsed)
```

通过上述代码，来记录代码执行时间，以 `maxCount` 来控制代码执行次数，反复的试验，获取可衡量的值。

##### 结尾

* 跨浏览器的 Web 应用程序开发是困难的
* 为了圆满完成跨浏览器开发，不仅要掌握 JavaScript 语言，还要全面了解浏览器以及它们的怪异模式和矛盾，并要具备当前最佳实践方面的良好基础。

### 第二章、利用测试和调试武装自己

掌握 JavaScript 调试，可以提高代码排查问题的能力、提高代码编写速度、理解代码运行的过程，所以掌握代码调试是程序员必备的能力之一。

#### JavaScript 调试代码的两个重要方法：

1. 日志记录
2. 断点，特定的代码上暂停脚本的执行，从暂停浏览器运行，获取当前代码的状态。包括所有可访问的变量、上下文以及作用域链

> `alert` 函数，也是用于调试的一种方法，但是 `alert` 有其一定的局限性，只能简单的验证变量的值，随着浏览器的调试工具的出现和飞速发展，`alert` 代码调试已被 `console.log` 替代，不推荐使用。

#### 测试

> 篱笆筑的牢，邻居处得好。Web应用程序也是如此，不管是何种编程准则，“好”的测试铸就好的代码。

##### 测试用例

优秀的测试用例具有三个特征：

1. 可重用性（repeatability）—— 测试结果应该是高度可再生的。
2. 简单性（simplicity）—— 测试应该只专注于测试一件事。
3. 独立性（independence）—— 测试用例应该独立执行，不依赖于另外一个测试结果。

构建测试的主要两种方法：**解构性测试** 和 **构建性测试**。

* 解构性测试用例（deconstructive test case）—— 解构型测试用例，在消弱代码隔离时进行创建，以消除任何不恰当的问题。
* 构建性测试用例（constructive test case）—— 构建性测试用例，从一个熟知的良好精简场景开始，构建用例，直到能够重现 bug 为止。针对某一个功能开展构建测试用例。

##### 测试框架

JavaScript 测试框架主要功能涵盖：

1. 能够模拟浏览器行为 （单击按键等）
2. 测试交互式控制（暂停和恢复测试）
3. 处理异步测试超时问题
4. 能够过滤哪些会被执行的测试

比较老的测试框架： Qunit（单元测试框架）、YUI Test （构建并开发的测试框架）、JsUnit（Java Junit 测试框架在 JavaScript 语言的体验，不支持新的 API）

目前流行的测试框架：Mocha、Jasmine、Jest...

**测试里的一些基本知识：**

* **测试套件**，主要目的是聚合代码中所有单个测试，将其组合成为一个单位，这样它们可以批量运行，提供一个可以轻松反复运行的单一资源。
* **断言**，单元测试框架的核心是断言方法，通常叫 `assert()`。该方法接收一个值，需要断言的值，以及一个表示该断言目的的描述。如果该值执行结果为 true，断言通过。否则断言失败。

##### 实现一个简单 `assert()`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Test Suite</title>
    <style>
        /* 定义断言结果样式 */
        #results li.pass{ color: green; }
        #results li.fail{ color: red; }
    </style>
</head>
<body>
<ul id="results"></ul>
<script>
    /**
    * 断言函数
    * @param {Boolean} value 需要断言的值
    * @param {String} desc 断言目的描述
    */
    function assert(value, desc) {
        var li = document.createElement("li");
        li.className = value ? "pass" : "fail";
        li.appendChild(document.createTextNode(desc));
        document.getElementById("results").appendChild(li);
    }
    // 使用断言测试
    window.onload = function () {
        assert(true, 'The test suite is running.');
        assert(false, "Fail");
    }
</script>
</body>
</html>

```

##### 测试组

测试组就是代表一组断言的集合。一个测试组代表某一个特定的任务，而任务里又有很多划分的一个个单一的小任务。

在测试组里任何一个断言失败，都会终止程序，标记整个测试组为失败。

**测试分组实现：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Test Suite</title>
    <style>
        /* 定义断言结果样式 */
        #results li.pass{ color: green; }
        #results li.fail{ color: red; }
    </style>
</head>
<body>
<ul id="results"></ul>
<script>
    (function(){
        var results;
        this.assert = function assert(value, desc) {
            var li = document.createElement("li");
            li.className = value ? "pass" : "fail";
            li.appendChild(document.createTextNode(desc));
            results.appendChild(li);
            // 一处断言失败，整个测试组都为失败
            if (!value) {
                li.parentNode.parentNode.className = "fail"
            }
            return li;
        };
        this.test = function test (name, fn) {
            results = document.getElementById("results");
            results = assert(true, name).appendChild(
                document.createElement('ul')
            );
            fn();
        };
    })();

    // 使用断言测试
    window.onload = function () {
        test("A test", function () {
            assert(true, 'First assertion completed.');
            assert(true, "Second assertion completed.");
            assert(true, "Third assertion completed.");
        });

        test("B test", function () {
            assert(true, 'First assertion completed.');
            assert(false, "Second assertion failed.");
            assert(true, "Third assertion completed.");
        });

        test("C test", function () {
            assert(null, 'fail.');
            assert(5, "pass.");
        });
    }
</script>
</body>
</html>

```

##### 异步测试

异步测试多数使用场景如 Ajax 请求 和 动画。处理异步测试，需要遵循简单的步骤：

1. 将依赖相同的异步操作的断言组合成一个统一的测试组。
2. 每个测试需要放在一个队列上，在先前其他的测试组完成运行之后再运行。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Test Suite</title>
    <style>
        /* 定义断言结果样式 */
        #results li.pass{ color: green; }
        #results li.fail{ color: red; }
    </style>
</head>
<body>
<ul id="results"></ul>
<script>
    (function(){
        var queue = [], // 接受测试组的队列
            paused = false, // 是否执行断言的标志
            results;
        // 接收一个包含一个多个断言的函数，可以身同步的也是可以是异步的。一并放置在队列中等待执行
        this.test = function test (name, fn) {
            queue.push(function () {
                results = document.getElementById("results");
                results = assert(true, name).appendChild(
                    document.createElement('ul')
                );
                fn();
            });
            console.log('队列：', queue)
            runTest();
        };

        // test 函数内部调用，通知该测试套件暂停执行测试，直到测试组完成。
        this.pause = function () {
            paused = true;
        };

        // 恢复测试，经过短暂的延迟，进行下一个测试的运行
        this.resume = function () {
            paused = false;
            setTimeout(runTest, 1)
        };

        // 执行测试
        function runTest () {
            if (!paused && queue.length) {
                // 移除队列第一个参数，并执行测试
                queue.shift()();
                // 检测是否测试套件还有任务，判断是否暂停测试，不暂停就继续执行
                if (!paused) {
                    resume();
                }
            }
        }

        this.assert = function assert(value, desc) {
            var li = document.createElement("li");
            li.className = value ? "pass" : "fail";
            li.appendChild(document.createTextNode(desc));
            results.appendChild(li);
            // 一处断言失败，整个测试组都为失败
            if (!value) {
                li.parentNode.parentNode.className = "fail"
            }
            return li;
        };
    })();

    // 使用断言测试
    window.onload = function () {
        test("Async test #1", function () {
            pause();
            setTimeout(function() {
                assert(true, 'First assertion completed.');
                resume();
            }, 1000)
        });

        test("Async test #2", function () {
            pause();
            setTimeout(function() {
                assert(true, 'Second assertion completed.');
                resume();
            }, 1000)
        });
    }
</script>
</body>
</html>

```

## 第二部分、见习训练

### 第三章、函数是根基

JavaScript 是一门**函数式**语言。代码编写的好不好就取决于是否理解这一点。对象的本质归根结底是对**对象**实质的理解。

最重要的是，JavaScript 中，函数是第一型对象（first-class object），也就是说函数可以共处，可以将其视为其他任意类型的 JavaScript 对象。就像普通的 JavaScript 数据类型，函数可以被任意变量进行引用，或声明成对象字面量，甚至可以将其作为函数参数进行传递。

#### JavaScript 的函数式特性为何如此重要

函数和函数式概念在 JavaScript 中如此重要的原因之一是，函数是代码执行的主要模块化单元。

#### 函数是第一型对象

对象在 JavaScript 中有如下功能：

* 它们可以通过字面量进行创建
* 它们可以赋值给变量、数组或其他对象的特性
* 它们可以作为参数传递给函数
* 它们可以作为函数的返回值进行返回
* 它们可以拥有动态创建并赋值的属性

在 JavaScript 中，函数拥有全部这些功能，也就是说可以像这门语言的其他对象一样使用，因此，我们说函数是第一型（first-class）对象。函数还拥有一个特殊的功能就是被调用。

#### 浏览器事件轮询

在 JavaScript 浏览器编程中，代码不负责事件轮询和事件派发，由浏览器帮我们处理。而我们只要为浏览器中发生的各种事件建立事件的处理程序（handler）。这些事件在触发时被放置在一个事件队列中（先进先出列表 【FIFO】），然后浏览器将调用已经为这些事件建立好的处理程序。

这些事件发生的时间和顺序都是不可预知的，所以事件处理函数的调用也是异步的。例如：

* 浏览器事件，页面完成加载和卸载的时候
* 网络请求（Ajax 请求）
* 用户事件（鼠标点击、鼠标移动或者按键）
* 计时器事件（setTimeout、setInterval）

> ⚠️注意：
> 浏览器的事件轮询是单线程（single-threaded）的，单线程都不能同时处理两个程序。每个事件都是按照在队列中所放置的顺序来处理（先进显出 FIFO）。

![Browser_loop_event.jpg](https://upload-images.jianshu.io/upload_images/735083-a788ed64e537c1a0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 回调概念

定义一个函数稍后执行时，无论何时定义，在浏览器执行还是其他地方执行，我们定义的就是所谓的**回调**（callback）。该术语源于：**我们定义一个函数，以便其他一一些代码在适当的时机回头再调用它**。

回调是高效利用 JavaScript 必不可少的一部分。

以一个简单的例子，来描述下回调：

```js
function useless (callback) {
    return callback();
}

# 数组排序中，根据自定义的比较器进行排序, 也是使用的回调
var arr = [213, 101, 66, 88, 22, 44, 0, 8, 8999]
arr.sort(function(a, b) { return b - a})
```

> JavaScript 语言最重要的功能之一是可以在代码的任何地方创建函函数。

#### 函数声明

JavaScript 是使用函数字面量（function literal）进行声明从而创建函数值的，就像使用数字字面量创建数字值一样。

函数字面量由四个部分组成：

1. function 关键字
2. 可选名称，如果指定名称，则必须是一个有效的 JavaScript 标示符。
3. 括号内部，一个已逗号分隔参数的列表。各个参数名称必须是有效的标示符。参数列表允许为空，即使参数列表为空圆括号也必须存在。
4. 函数体。包含在大括号内的一系列 JavaScript 语句。函数体可以为空，但大括号必须始终存在。

函数名是可选的，例如：匿名函数。命名一个函数时，该名称在整个函数声明范围内是有效的。此外，如果一个命名函数声明在顶层，window 对象上的同名属性则会引用到该函数（基于浏览器的）。

所有函数都有一个 name 属性，该属性保存的是该函数名称的字符串。没有名称的函数也仍然又 name 属性，只是该属性值为空字符串。（声明式函数的 name 属性就是函数名称，匿名函数 name 属性则是空字符串）

#### 作用域和函数

声明一个函数，不仅要关注该函数可用的作用域，还要关注该函数自身创建的作用域，以及函数内部的声明是如何影响这些作用域的。

在 JavaScript 中，作用域是由 function 进行声明的，而不是代码块。声明的作用域创建于代码块，但不是终结于代码块。

```js
if (window) {
    var a = 666;
}
alert(a)
```

在其他语言里，a 终结于 if 语句的关闭大括号，弹出 undefined 值，但，在 JavaScript 则不没有，依然可以访问到 a 的值 666；这是因为 JavaScript 在大括号关闭处并没有终止其作用域。

* 变量声明的作用域开始于声明的地方，结束于所在函数的结尾，与代码块嵌套无关。
* 命名函数的作用域是指声明该函数的整个函数范围，与代码嵌套。（有些人称之为机制提升）
* 对于作用域声明，全局上下文就像一个包含页面所有代码的超大型函数。

```js
function outer() {
    var a = 1;
    function inner () { /* does nothing */}
    var b = 2;
    if (a == 1) {
        var c = 2;
    }
    console.log(c) // 还是能访问到 c
}
```

inner() 函数在整个 outer() 函数内部都是可以用的，而数字变量a、b、c 却只能从它们的声明处到 outer() 结尾处才可用。这清楚的表明，函数可以在其作用域范围内提前被引用，但变量不行。

#### 函数调用

**本小节主旨**：函数被调用的时候到底发生了什么？研究调用函数的多种方法。从比较深层次的理解函数调用，来推进在 JavaScript 中函数的重要性。

事实证明，函数调用的方式对其函数内部的代码是如何执行的，有着巨大的影响，尤其是在 `this` 参数的创建中。

实际上有**四种**不同的方式可以进行函数调用，每种方式都有自己的细微差别。

1. 作为一个函数进行调用，是最简单的方式
2. 作为一个方法进行调用，在对象上进行调用，支持面向对象编程。
3. 最为构造器进行调用，创建一个新对象实例。
4. 通过 `apply()` 或 `call()` 方法进行调用，这种方式很复杂。

以上除了最后一种方式，其他方式的函数调用，都是通过在表达式后面加上圆括号这一操作符，来执行函数调用。

```js
expression(arg1, arg2 [,...])
```

##### 从参数到函数形参

当一个参数列表作为函数调用的一部分时，这些参数会按照函数声明里的行参声明顺序，将参数值分别赋值这些行参。如果传入的参数数个数和声明的新参数量不一致，不会抛错，JavaScript 可以完美的解决这种问题，具体处理策略如下：

* 如果实际传递参数数量大于函数声明的行参数量，超出的参数则不会进行匹配给行参名称。
    ```js
        function whatever(a, b, c) { ... }

        whatever(1, 2, 3, 4, 5) // 参数 1、2、3 分别赋值给 a、b、c, 而4、5则不会赋值给任何行参。可以通过 arguments 来进行获取
    ```

* 如果声明的行参数量大于实际传递的参数数量，则没有对应参数的行参会赋值为 `undefined`.

所有的函数调用都会传递两个**隐式参数**： `arguments` 和 `this`。

所谓的**隐式（implicit）**, 也就是这些参数不会显示列在函数签名里，但是它们默认地传递给函数并存在于函数作用域内。函数内部可以像其他显示命名的参数一样使用。

###### arguments 参数

`arugments` 参数传递给函数的所有参数的一个集合。集合有一个 `length` 属性，获取全部参数的个数。`aruguments` 不是一个数组，避免将其作为数组进行调用。它是一个类数组结构，并且拥有数组的某些特性，例如：`length` 属性 和 `arugments[0]`索引方式访问参数值

###### this 参数

`this` 参数在函数调用时被隐士传入，它引用了与该函数调用进行隐士关联的一个关联的一个对象，被称之为**函数上下文（function context）**。

函数上下文概念，来自于像 Java 这样的面向对象的语言，面向对象语言认为 this 是方法声明所在的类的一个实例。

但要注意的是，JavaScript 中的 this 和 Java 的 this 则完全不同，Java 中的 this 依赖于函数声明，而 JavaScript 种的 this 则依赖于函数的调用方式。基于这个事实，将 this 称为**调用上下文 （invocation context）** 可能更为清晰。

在四种调用机制的不同，会发现它们之间的主要区别在于，**如何定义每种调用类型 this**。

##### 作为函数进行调用

在现实中，我们说一个函数“作为函数”进行调用，是区别于其他调用机制：方法、构造器以及 apply/call。如果一个函数不是作为方法、构造器，或通过 apply() 或 call() 进行调用的，则认为它是“作为函数”进行调用的。

```js
function ninjia() {}

ninjia()

var samurai = function () {}

samurai()
```
以这种方式调用时，函数的上下文是全局上下文 -- window 对象（node 里是 global）。

“函数作为函数” 进行调用的概念，实际是“作为方法进行调用”的一个特殊情况，因为函数的所有者是 window，而在全局对象上，可以省略 `window`的书写，所以通常被认为是自己的机制。

##### 作为方法进行调用

当函数被赋值给对象的一个属性，并使用引用该函数的这个属性进行调用时，那么函数就是作为该对象的一个方法进行调用的。

```js
var o = {}
o.whatever = function () {}

o.whatever()
```

一个方法所属的对象在该方法体内可以通过 `this` 的形式进行引用。将函数作为对象的一个方法（method）进行调用时，该对象就变成了函数上下文，并且在函数内部可以以 `this` 参数的形式进行访问。这是 JavaScript 作为面向对象代码进行编写的主要手段之一。（构造器是另外一个。）

作为“方法”进行调用，此时函数的上下文指向的是其所属对象。

##### 作为构造器进行调用

构造器函数的声明和其他函数声明一样，不同的地方是在于如何调用该函数。

**构造器的超能力**

将函数作为构造器进行调用，是 JavaScript 的一个超级特性，因为构造器调用时，如下特殊行为就会发生：

* 创建一个新的空对象。
* 传递给构造器的对象是 this 参数，从而成为构造器的函数上下文。（新创建的控对象）
* 如果没有显式的返回值，新创建的对象则作为构造器的返回值进行返回。

**构造器的目的**是要创建一个新对象并对其进行设置，然后将其作为构造器的返回值进行返回。任何干扰这种意图的函数，都不适合作为构造器。

```js
function Ninja() {
    this.skulk = function () {return this;}
}

var ninja1 = new Ninja();
var ninja2 = new Ninja();

assert(ninja1.skulk() === ninja1, "The 1st ninja is skulking")
assert(ninja2.skulk() === ninja2, "The 2nd ninja is skulking")
```
上述代码，创建一个名为 Ninja 函数，用于构建忍者（ninjas）。使用 new 关键字进行调用时，将会创建一个空对象实例，并作为 this 参数传递给该函数。

**构造器编码注意事项**

* 函数和方法的命名通常以动词开头，来描述它们所做的事情（skulk()）,并且以小写字母开头。构造器命名通常是由一个描述所构造对象的名词来描述，并且以大写字母开发。（Ninja()）
* 使用构造器进行调用时，必须使用关键字 new 进行


##### **使用 apply() 和 call() 方法进行调用**

函数调用方式之间的**主要差异**是：作为 this 参数传递给执行函数的上下文对象之间的区别。作为方法进行调用，该上下文是方法的拥有者；作为全局函数进行调用，其上下文永远是 window；作为构造器进行调用，其上下文对象则是新创建的对象实例。

每个函数都有 apply() 和 call() 方法，用来显示的指定任何一个对象作为其函数上下文。也就是所谓绑定其 this 指向。

**apply() 和 call() 功能一样，区别在于参数的传入方式：**

* aplly() 接收两个参数，一个参数作为函数上下文的对象；另一个是作为函数参数所组成的数组。
* call() 给函数传入的参数是一个参数列表，而不是单个数组

```js
function juggle() {
    var result = 0;
    for (var n = 0; n < arguments.length; n++) {
        result += arguments[n];
    }

    this.result = result; // 特定的使用 this，为了更好的指明函数上下文
}

var ninja1 = {}
var ninja2 = {}

juggle.apply(ninja1, [1, 2, 3, 4])
juggle.call(ninja2, 5, 6, 7, 8)

assert(ninja1.result === 10, 'juggle via apply')
assert(ninja2.result === 26, 'juggle via call')
```

**在回调中强制指定函数上下文**

从一个遍历数组条目并执行操作的简单函数出发，来了解下 “命令式编程” 和 “函数式编程”：

* 命令式编程，通常是讲数组传递给一个方法，并使用 for 循环语句遍历每一个条目，然后再对每个条目进行执行操作

```js
function arrayEach(collection) {
    for (var i = 0; i < collection.length; i++) {
        /* do something to collection[i]*/
    }
}
```

* 函数式编程，则是创建一个函数来执行单个条目，并将每个条目都传递给该函数。

```js
function arrayEach(item) { /* do something to item */ }
```

两者之间的区别在于思维层面： 函数是程序的构件块而不是命令式语句。
