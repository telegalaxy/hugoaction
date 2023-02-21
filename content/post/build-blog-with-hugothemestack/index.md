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

### 修改menu.toml

在基础上进行修改即可

### 修改params.toml

- footer

  since:填写博客创建日期，如2023

  customText:自定义页脚文字，效果见本站页脚

- dateFormat

  不用改，改了可能会出错

- sidebar

  emoji:头像右下角的图标，填写emoji即可

  subtitle:博客头像下的一段文字，不建议太长

- sidebar.avatar

  **local:头像是否在本地，如果在本地请填写true！**

  src:头像链接

其他的不用管

## 部署博客

修改`.github/workflows`内的deploy.yml(没有的新建)，删除内容后填写：

```yaml
name: Deploy to Github Pages

on:
    push:
        branches: [master]
    pull_request:
        branches: [master]

jobs:
    build:
        runs-on: ubuntu-latest

        steps:
            - uses: actions/checkout@v2

            - name: Cache Hugo resources
              uses: actions/cache@v2
              env:
                  cache-name: cache-hugo-resources
              with:
                  path: resources
                  key: ${{ env.cache-name }}

            - uses: actions/setup-go@v2
              with:
                  go-version: "^1.17.0"
            - run: go version

            - name: Cache Go Modules
              uses: actions/cache@v2
              with:
                  path: |
                      ~/.cache/go-build
                      ~/go/pkg/mod
                  key: ${{ runner.os }}-go-${{ hashFiles('**/go.sum') }}
                  restore-keys: |
                      ${{ runner.os }}-go-

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                  hugo-version: "latest"
                  extended: true

            - name: Build
              run: hugo --minify --gc

            - name: Deploy 🚀
              uses: JamesIves/github-pages-deploy-action@v4
              with:
                  branch: gh-pages
                  folder: public
                  clean: true
                  single-commit: true
```

新建分支

![新分支](https://s1.ax1x.com/2023/02/21/pSjlHzt.png)

点击 New branch

![新分支](https://s1.ax1x.com/2023/02/21/pSjlTJA.png)

打开仓库>settings>Actions>General，按图修改

![Action](https://s1.ax1x.com/2023/02/21/pSjlRsK.png)

上传到Github

输入

```bash
git init
git add .
git commit -m "commit"
git push origin master
```

