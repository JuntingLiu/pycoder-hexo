---
title: 使用Hexo + Github 搭建个人静态博客
date: 2018-05-19 10:39:09
categories: Hexo
tags:
- Hexo
copyright: true
---

# 使用 Hexo 搭建静态博客

## 什么是 Hexo？

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

## 安装

### 前提

安装 Hexo 相当简单。然而在安装前，您必须检查电脑中是否已安装下列应用程序：

* Node.js
* Git

已经安装上述必备程序，那么恭喜您！接下来只需要使用 npm 即可完成 Hexo 的安装。


```npm
npm install -g hexo-cli

# 安装是否成功
 ~/Life  hexo version                                               14:35:29
hexo-cli: 1.1.0
os: Darwin 17.5.0 darwin x64
http_parser: 2.8.0
node: 8.11.1
v8: 6.2.414.50
uv: 1.19.1
zlib: 1.2.11
ares: 1.10.1-DEV
modules: 57
nghttp2: 1.25.0
openssl: 1.0.2o
icu: 60.1
unicode: 10.0
cldr: 32.0
tz: 2017c

```

## 工具都备好，开始搭建博客

请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件,⚠️ 要空文件夹哦～

```bash
# 初始化hexo项目仓库
$ hexo init <folder>
$ cd <folder>
$ npm install
```

初始化完成后，指定文件夹的目录如下：

```tree
.
├── _config.yml  // 网站配置信息
├── package.json // 应用程序的信息
├── scaffolds    // 模版 文件夹
│   ├── draft.md
│   ├── page.md
│   └── post.md
├── source       // 资源文件夹
│   └── _posts
└── themes       // 主题
    └── landscape
```

到这里一个最基础的博客就搭建出来了，让我们运行起来:

```hexo
hexo server
```

## 与GitHub关联上

GitHub Page 实现方式，目前我知道的是三种：

1. 创建一个跟你github账号相关的仓库，github默认给你的域名就是 `[username].github.io`
2. 创建仓库，在 `setting` 中通过设置 Github page 的方式
3. 创建 `gh-pages` 分支的方式

这三种方式其实属于两种基本的 GitHub Pages 类型：用户/组织 Pages 和 项目 Pages。

* 用户/组织 Pages 存在于一个特定的 GitHub Pages 文件专有库中。你将使用用户名来命名这个库，比如 `twitchbody.github.io`；**master分支** 上的内容将用于构建和发布你的 GitHub Pages 网页。
* 不像用户和组织的 Pages，`项目 Pages` 是作为一个项目保存在同一个库中, 以作为项目介绍和文档存在。**gh-pages分支**用来构建和发布项目 Pages 网站。如果没有 自定义的域名，`项目 Pages` 网站将服务在用户 Pages 网站的子域名下：`username.github.io/projectName`。

这里我使用方式3:

建立一个项目 Pages，你需要在你的库中新建一个新的 orphan 分支（一个与现存分支没有共同的历史的分支）。

```git
# 进入项目
$ cd pycoder-hexo

# 创建分支
$ git checkout --orphan gh-pages
# 清除分支所有内容，保证是一个干净的分支
$ git rm -rf .

```

然后，创建 `index.html` 文件做测试:

```git
# 创建
$ echo "My Page!" > index.html

$ git add .
$ git commit -m "my first page"
$ git push origin gh-pages

```

![gh-pages](./assets/images/gh-pages.png)

接着，进入`setting`，设置下 `Github page`:

![github_pages](./assets/images/github_page.png)

使用自定义域名，需要你到域名服务商里进行增加一个域名解析：

![domain](./assets/images/domain.png)

> ⚠️, 这里要是没有自定义域名，到时候部署 hexo 生成的静态文件的时候，站点访问静态资源会出现 404错误，你会发现路径出现问题。

![pyCoder](./assets/images/pycoder.png)

## 打造超酷的博客

### 安装主题

我选择的是比较火和流行的 `Next`主题：

```git
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### 启用主题

需要在 `_config.yml`文件进行配置：

```yml
# Extensions 扩展
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```

### 设定主题

Next是一个主题，三种外观，选您所好！挑选你看的顺眼的外观。

```yml

```

## 配置

站点相关信息的配置, 可以在 `_config.yml` 中修改大部份的配置。了解相关配置，可以参考 [配置文档](https://hexo.io/zh-cn/docs/configuration.html)，进行你的基础信息设置。

## 指令

之前我们初始化项目的时候已经使用过2个 `hexo` 指令了 `hexo init pyCoder
` 和 `hexo version`, 接下来我们详细了解其他的`hexo`指令，想要`hexo`玩出花，指令是必须的～

### new

新建一篇文章

```linux
hexo new [layout] <title>
```

如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

### generate

生成静态文件。

```js
hexo generate
# 简写
hexo g

# 文件生成后立即部署网站
hexo generate -d  // (-d,--deploy)

# 监视文件变动
hexo generate -w  // (-w, --watch)
```

### publish

发表草稿。

```hexo
hexo publish [layout] <filename>
```

### server

启动服务器。默认情况下，访问网址为： http://localhost:4000/。

```js
hexo serve

# 重设端口
hexo serve -p 8080 // (-p, --port)

# 只使用静态文件
hexo serve  -s // (-s, --static)

# 启动日记记录，使用覆盖记录格式
hexo serve -l // (-l, --log)
```

### deploy

部署网站。

```js
hexo deploy
# 简写
hexo d

# 部署之前预先生成静态文件
 hexo deploy -g // (-g, --generate)
```

### render

渲染文件。

```js
hexo render <file1> [file2] ...

# 设置输出路径
 hexo render <file1> [file2] -o path  // (-o, --output)
```

### migrate

从其他博客系统 迁移内容

```hexo
hexo migrate <type>
```

### clean

清除缓存文件 (db.json) 和已生成的静态文件 (public)。

```hexo
hexo clean
```

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

### list

```hexo
hexo list <type>
```

列出网站资料。

### version

显示 Hexo 版本。

```hexo
hexo version
```

### 安全模式

```hexo
hexo safe
```

在安全模式下，不会载入插件和脚本。当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

### 调试模式

```hexo
hexo --debug
```

在终端中显示调试信息并记录到 debug.log。当您碰到问题时，可以尝试用调试模式重新执行一次，并 提交调试信息到 Hexo GitHub 的 issue 上 。

### 简洁模式

```hexo
hexo --silent
```

隐藏终端信息。

### 自定义配置文件的路径

```hexo
hexo --config custom.yml
```

自定义配置文件的路径，执行后将不再使用 _config.yml。

### 显示草稿

```hexo
hexo --draft
```

显示 source/_drafts 文件夹中的草稿文章。

### 自定义 CWD

```hexo
hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。
