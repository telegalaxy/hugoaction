---
title: "简简单单搭建一个博客"
description: 小白向，此方式部署博客方便但无法魔改
date: 2023-02-21T09:57:59Z
image: 
math: 
license: 
hidden: false
comments: true
draft: false
---
## 文章的初衷

博客的目的是写作而不是展示自己技术的地方，所以本文以方便快速的角度出发，带小白们认识一下hugo的魅力。

## 需要准备的

* 能快速打开Github的电脑（推荐挂梯子，否则写文章容易丢失）
* 学习Markdown（很简单，工具推荐Typora，0学习成本，像编辑Word文件一样编辑Markdown）

## 搭建博客

1. 访问[CaiJimmy/hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)点击<kbd>Use this template</kbd> 按照提示完成操作

[![Step 1](https://user-images.githubusercontent.com/5889006/156916624-20b2a784-f3a9-4718-aa5f-ce2a436b241f.png)](https://user-images.githubusercontent.com/5889006/156916624-20b2a784-f3a9-4718-aa5f-ce2a436b241f.png)

2. 完成操作后，点击<kbd>Code</kbd> 创建新的Codespace[![Create codespace](https://user-images.githubusercontent.com/5889006/156916672-43b7b6e9-4ffb-4704-b4ba-d5ca40ffcae7.png)](https://user-images.githubusercontent.com/5889006/156916672-43b7b6e9-4ffb-4704-b4ba-d5ca40ffcae7.png)

## 配置博客

打开Codespace，打开`config/_default/`这里的文件就是博客配置。

### 修改config.toml

下面是各行需要修改的地方

| 名称                   | 需要的操作                                                   |
| ---------------------- | ------------------------------------------------------------ |
| baseurl                | 修改为自己博客的网址，格式：（//:网址）                      |
| languageCode           | 修改为网站的语言，这里写zh-cn                                |
| paginate               | 每页显示文章数，保持原样即可                                 |
| title                  | 网站标题，如"百度"                                           |
| DefaultContentLanguage | 支持en, fr, id, ja, ko, pt-br, zh-cn, zh-tw, es, de, nl, it, th, el, uk, ar。填写zh-cn |

其他的不用管
