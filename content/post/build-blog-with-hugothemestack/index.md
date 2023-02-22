---
title: "简简单单搭建一个博客"
description: 无法魔改但方便快捷自动化的博客
date: 2023-02-21T09:57:59Z
image: https://s2.loli.net/2023/02/22/EV8HOtimCGsfx6g.png
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

![Step 1](https://s2.loli.net/2023/02/22/B3d7nTQXRkhDsfm.png)

2. 完成操作后，点击<kbd>Code</kbd> 创建新的Codespace![Create codespace](https://s2.loli.net/2023/02/22/BmIt3KSjr8aox1z.png)

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

![新分支](https://s2.loli.net/2023/02/22/1jkYdXb2Oy95vqJ.png)

点击 New branch

![新分支](https://s2.loli.net/2023/02/22/eQhwtYGvAdDqM51.png)

打开仓库>settings>Actions>General，按图修改

![Action](https://s2.loli.net/2023/02/22/L6DT2f4SOdPtkgX.png)

上传到Github

输入

```bash
git init
git add .
git commit -m "commit"
git push origin master
```

## 部署至Netlify

先注册一个账号，然后新建站点，选择从Git仓库导入

![导入](https://s2.loli.net/2023/02/22/zNIfmM3wsodCFbY.png)

点击Github后等弹窗显示文字，关闭即可看到仓库，选择博客仓库，选择gh-pages

![示意图](https://s2.loli.net/2023/02/22/OqzRCIXgJ3EhLnN.png)

其他的不用管点Deploy site。到首页访问链接即可看到博客（每次更新博客不用手动重新部署，过程是自动的）