---
title: AngularJS 学习记录
date: 2018-05-19 21:00:20
categories: AngularJS
tags:
- AngularJS
copyright: true
---

## AngularJS 初识篇

### Angular CLI 安装

```npm
# 全局安装
$ npm install -g @angular/cli
# 检验安装是否成功,出现以下图标就说明成功了
$ ng -v

    _                      _                 ____ _     ___
   / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
  / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
 / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
/_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
               |___/

Angular CLI: 1.7.4
Node: 8.11.1
OS: darwin x64
Angular:
```

### 初始化新项目

```npm
# 创建项目成功后，会自动 npm install
$ ng new helloAngular(project name)

# 启动项目（开启本地服务）
$ ng serve
// or 启动项目，并打开浏览器 （--open or -o）
$ ng serve --open
```

#### `ng serve`指令参数含义

`ng serve` 命令会启动开发服务器，监听文件变化，并在修改这些文件时重新构建此应用。

* `--open` or `-o` 自动打开浏览器并访问
* `--prod` 指定为生产模式，会自动打包项目

### 创建我的第一个组件

Angular CLI 命令行工具，自带指令集，可以让我们快速开发和遵循 Angular 的开发风格指南。

```ng
# 创建组件 组件名需要遵循大驼峰命名规则
$ ng generate component ComponentName
// or 简写
$ ng g c ComponentName
```

### Angular三大核心概念

Angular最核心的概念是“组件化”,新版本的 Angular 来说，一切都是围绕着“组件化”展开的，组件是 Angular 的核心概念模型。

1. Component
2. Module
3. Route

![components.png](https://upload-images.jianshu.io/upload_images/735083-22759909e041e978.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

以下是一个最简单的 Angular 组件定义：

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'Jun ting';
}
```

* @Component：这是一个 Decorator（装饰器），其作用类似于 Java 里面的注解。Decorator 这个语言特性目前（2017-10）处于 Stage 2（草稿）状态，还不是 ECMA 的正式规范。
* selector：组件的标签名，外部使用者可以这样来使用这个组件：<app-root>。默认情况下，ng 命令生成出来的组件都会带上一个 app 前缀，如果你不喜欢，可以在 angular-cli.json 里面修改 prefix 配置项，设置为空字符串将会不带任何前缀。
* templateUrl：引用外部的 HTML 模板。如果你想直接编写内联模板，可以使用 template，支持 ES6 引入的“模板字符串”写法。
* styleUrls：引用外部 CSS 样式文件，这是一个数组，也就意味着可以引用多份 CSS 文件。
* export class AppComponent：这是 ES6 里面引入的模块和 class 定义方式。

### 把 CSS 预编译器改成 SASS

`@angular/cli` 创建项目的时候没有自动使用 SASS 作为预编译器，我们需要自己手动修改一些配置文件,请按照以下步骤依次修改：

1、 `angular-cli.json` 里面的 `styles.css` 后缀改成 `.scss`

```json
  "apps": [
    {
      "root": "src",
      "outDir": "dist",
      "assets": [
        "assets",
        "favicon.ico"
      ],
      "index": "index.html",
      "main": "main.ts",
      "polyfills": "polyfills.ts",
      "test": "test.ts",
      "tsconfig": "tsconfig.app.json",
      "testTsconfig": "tsconfig.spec.json",
      "prefix": "app",
      // 这里
      "styles": [
        "styles.scss"
      ],
```

> 后面再使用 ng g c *** 自动创建组件的时候，默认就会生成 .scss 后缀的样式文件了。

2、 `angular-cli.json` 里面的 `styleExt` 改成 `.scss`

```json
  "defaults": {
    "styleExt": "scss",
    "component": {}
  }
```

3、 src 下面`.css`后缀的文件全修改为`.scss`

#### 引入 bootstrap、font-awesome

安装 bootstrap、font-awesome 依赖

```npm
# bootstrap
npm install bootstrap --save

# font-awesome
npm install font-awesome --save
```

在 `style.scss` 引入 bootstrap、font-awesome 的 css

```scss
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~font-awesome/css/font-awesome.min.css";
```

## AngularJS 模板语法

![模板生成流程图](https://upload-images.jianshu.io/upload_images/735083-4886b59c3d255e33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

模板是编写 Angular 组件最重要的一环，你至少需要深入理解以下知识点才能玩转 Angular 模板：

1. 对比各种 JS 模板引擎的设计思路
2. Mustache（八字胡）语法， `{}`
3. 模板内的局部变量
4. 属性绑定、事件绑定、双向绑定
5. 在模板里面使用结构型指令 *ngIf、*ngFor、ngSwitch
6. 在模板里面使用属性型指令 NgClass、NgStyle、NgModel
7. 在模板里面使用管道格式化数据

### 对比各种 JS 模板引擎的设计思路

`什么是模板引擎？` 是指利用某种模板语言将页面制成模板，再依据业务逻辑将该模板语言翻译成业务数据，从而生成最终展示页面。 简单的讲就是根据静态HTMl元素和业务逻辑处理的数据结合渲染生成浏览器器需要的页面。

* jQuery -> Handlebars
* React -> jsx 模板写法
* Angular -> 与“指令”紧密结合的模板语法 （vue 也是一样）

各种模板引擎的唯一目标就是提高开发效率、缩短时间成本。综合来说，无论是哪一种前端模板，大家都比较推崇“轻逻辑”（ logic-less ）的设计思路。

`何为“轻逻辑”?` 简而言之，所谓“轻逻辑”就是说，你不能在模板里面编写非常复杂的 JavaScript 表达式。比如，Angular 的模板语法就有规定：

* 你不能在模板里面 new 对象
* 不能使用=、+=、-=这类的表达式
* 不能用++、--运算符
* 不能使用位运算符

为什么要“轻逻辑”？

1. 本身的 Html 是不识别 if 、for 等操作的；模板引擎处于的地位就是帮忙编译转换纯HTMl元素。
2. 在 HTML 加入复杂的逻辑，会加大模板引擎编译的时间和计算能力；而且也不建议复杂逻辑处理放到HTMl里来做，保证 HTML 的单一纯洁性；使用模板也是来做简单的插值相关的操作
3. JS 版的编译器需要在浏览器里面运行，搞得太复杂浏览器拖不动！
4. 最根本还是`模板引擎不够强`, 并不是万能的；

对于 Angular 来说，强调“轻逻辑”还有另一个原因：在组件的整个生命周期里面，模板函数会被执行很多次。你可以想象， Angular 每次要刷新组件的外观的时候，都需要去调用一下模板函数，如果你在模板里面编写了非常复杂的代码，一定会增加渲染时间，用户一定会感到界面有“卡顿”。

人眼的视觉延迟大约是100ms到400ms之间，如果整个页面的渲染时间超过400ms，界面基本上就卡得没法用了。有一些做游戏的开发者会追求60fps刷新率的细腻感觉，60分之1秒约等于16.7ms，如果 UI 整体的渲染时间超过了16.7ms，就没法达到这个要求了。

轻逻辑（ logic-less ）带来了效率的提升，也带来了一些不方便，比如很多模板引擎都实现了 if 语句，但是没有实现 else，所以开发者们在编写复杂业务逻辑的时候模板代码会显得非常啰嗦。

目前来说，并没有完美的方案能同时兼顾运行效率和语法表现能力，这里只能取一个平衡。

### Mustache 语法

关于 Mustache 语法，双花括号语法,你需要掌握3点:

1. 它可以获取到组件里面定义的属性值。
2. 它可以自动计算简单的数学表达式，例如: 加减乘除、取模
3. 它可以获得方法的返回值。

插值语法关键代码实例：

```html
<h3>
    欢迎来到{{title}}！
</h3>
```

```ts
public title = 'Mustache 语法';
```

简单的数学表达式求值：

```html
<p>1 + 5 = {{ 1 + 5 }}</p>
```

调用组件里面定义的方法：

```html
<p> {{ getStr() }} </p>
```

```ts
public getStr(): string {
    return '调用方法！'
}
```

### 属性绑定（[属性名]）

属性绑定是用方括号来做的，写法：

```html
<img [src]="imgSrc" />
<button [disabled]="isUnchanged">是否禁用</button>
```

```ts
public imgSrc:string = './images.png';
public isUnchanged:boolean = true;
```

很明显，这种绑定是单向数据绑定，单一的读取值而已。

### 事件绑定 ( (事件名) )

事件绑定是用圆括号来做的，写法：

```html
<button (click)="btnClick($event)">点击事件</button>
```

```ts
pubic btnClick(e):void {
    alert('点击事件测试～');
}
```

### 双向绑定 （ [(...)] ）

你经常需要显示数据属性，并在用户作出更改时更新该属性。

在元素层面上，既要设置元素属性，又要监听元素事件变化。

双向绑定是通过方括号里面套一个圆括号 `[(...)]` 来做的，模板写法：

```html
<app-sizer [(size)]="fontSizePx"></app-sizer>
```

```ts
public fontSizePx:number = 14;
```

### 模板内的局部变量

### 在模板里面使用结构型指令

Angular 有3个内置的结构型指令：`*ngIf`、`*ngFor`、`ngSwitch`。`ngSwitch` 的语法比较啰嗦，使用频率小一些, 了解就好。

`*ngIf` 代码实例：

```html
<p *ngIf="isShow">显示还是不显示？</p>
<button (click)="toggleShow()">控制显示隐藏</button>
```

```ts
public isShow:boolean=true;

public toggleShow():void {
    this.isShow = !this.isShow;
}
```

`*ngFor` 代码实例：

```html
<ul>
    <li *ngFor="let item of items; let i = index;">
        {{i+1}} - {{ item.name }}
    </li>
</ul>
```

```ts
public items:Array<any>=[
    {name:"PyCoder"},
    {name:"Jun ting"},
    {name:"EcmaScript"}
];
```

`*ngSwitch` 代码实例：

```html
<div [ngSwitch]="mapStatus">
    <p *ngSwitchCase="0">下载中...</p>
    <p *ngSwitchCase="1">正在读取...</p>
    <p *ngSwitchDefault>系统繁忙...</p>
</div>
```

```ts
public mapStatus:number = 1;
```

> 特别注意：一个 HTML 标签上只能同时使用一个结构型的指令。

因为“结构型”指令会修改 DOM 结构，如果在一个标签上使用多个结构型指令，大家都一起去修改 DOM 结构，到时候到底谁说了算？

那么需要在同一个 HTML 上使用多个结构型指令应该怎么办呢？有两个办法：

* 加一层空的 div 标签进行包裹
* 加一层 `<ng-container>`

### 在模板里面使用属性型指令

使用频率比较高的3个内置指令是：`NgClass`、`NgStyle`、`NgModel`。

`NgClass` 使用案例代码：

```html
<div [ngClass]="currentClasses">同时批量设置多个样式</div>
<button (click)="setCurrentClasses()">设置</button>
```

```ts
public currentClasses: [];

public canSave: boolean = true;
public isUnchanged: boolean = true;
public isSpecial: boolean = true;

public setCurrentClasses ():void {
    this.currentClasses = {
        'saveable': this.canSave,
        'modified': this.isUnchanged,
        'special': this.isSpecial
    }
}
```
