# Libra

> Love is a serious mental disease —— Plato

## Libra项目写作指南

### 0 前言

**(1) 工具：**

项目文档总体上使用typora编写，Gitbook构建静态资源，托管在GitHub Page，借助GitHub Action持续集成。

**(2) 仓库配置：**

- `libraire/libraire.github.io`: 是GitHub Page仓库，用来托管Gitbook生成的静态资源(`_book`文件夹)
- `libraire/action`：是GitHub Action的脚本仓库，提供Gitbook的持续集成

==cookbook源文件和静态文件需要分开管理，具体待会儿补充TODO==

### 1 Quick Start

==道理我都懂，想直接开始TODO==

### 2 Gitbook

##### 安装环境

先要安装[Nodejs](https://nodejs.org/zh-cn/)，建议把源换到国内。

```bash
$ npm -v
$ npm config set registry https://registry.npm.taobao.org
$ npm config get registry
```

安装Gitbook-cli工具。

```bash
$ npm install gitbook-cli -g
```

因为Gitbook已经创建好，所以直接把项目clone下来就行了。

```bash
$ git clone git
```

##### 输出

`libra-cookbook`项目中，README.md文件用来介绍该书籍，SUMMARY.md文件为该书籍的目录。

```bash
# 构建命令，会生成_book文件夹，这就是部署需要的全部静态资源
$ gitbook build
```

```bash
# 构建并本地预览，在localhost:4000
$ gitbook serve
```

```bash
# 生成电子书(还没测试过，自行踩坑哈哈)
$ gitbook pdf ./ ./mybook.pdf
$ gitbook epub ./ ./mybook.epub
$ gitbook mobi ./ ./mybook.mobi
```

##### 配置

所有的配置都以JSON格式存储在名为 book.json 的文件中。

##### 插件

在[nmp官网](https://www.npmjs.com/ )上搜索关键词`gitbook-plugin`或`gitbook`即可。

添加至`book.json`文件后，再执行命令`gitbook install`将插件下载至本地即可

```json
{
	"plugins": ["myPlugin", "anotherPlugin"]
}
```

如果不想使用自带的插件，在插件名称前面加`-`：

```json
{
	"plugins":[ "-search"]
}
```

如果不是自带的，将其从插件列表中去掉即可。

==Libra项目预装插件TODO==

##### 自动生成SUMMARY.md文件

```bash
# 安装
$ npm install -g gitbook-summary
```

```bash
# 生成命令
$ book sm
```

==Libra项目默认SUMMARY.md配置TODO==

### 3 Github Page

似乎不用展开，先空着。

### 4 Github Action

这个也是提供通用的部署脚本，等搞完在补充吧。

### ∞ 代办与变更记录

- [ ] 分开管理cookbook的源文件和静态资源
- [ ] 写作的预装插件
- [ ] SUMMARY.md默认配置