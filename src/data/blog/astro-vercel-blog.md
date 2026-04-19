---
author: xprzmd
pubDatetime: 2026-04-19T13:48:22.131+08:00
modDatetime:
title: Astro+Vercel个人博客
slug: astro-vercel-blog
featured: false
draft: false
tags: ["others"]
description: 基于 Astro + Vercel + Obsidian 的三端同步个人博客搭建指南
---


介绍本站的基于Astro + Vercel + Obsidian + Git的三端同步个人博客方案。
___

## Github建立新仓库
在 GitHub 上建博客，仓库名字决定了你未来的网址：

- **特殊仓库（推荐）**：如果你把仓库命名为 `你的用户名.github.io`，你的博客网址就会非常简短漂亮：`https://用户名.github.io`。
![](/images/Pasted image 20260402165615.png)
- **普通仓库**：一般的命名如test，它的网址会带上后缀`https://用户名.github.io/test/`。

## 安装Node.js
在开始之前，请确保你的电脑上安装了Node.js。Astro 依赖它来运行。 可以在终端输入 `node -v` 检查是否安装成功。
![](/images/Pasted image 20260402165642.png)

## 本地构建Astro框架
建立博客文件夹进入输入`npm create astro@latest`, 如报错npm找不到命令可能是Node.js没设置好，打开终端权限即可，选Use blog template，后面都是yes。
![](/images/Pasted image 20260402170027.png)

### Github设置（可选）
装好后Git到github仓库，在仓库settings里面选择pages，sources选择github actions。这样每次push完github actions会自动使用astro构建网页。不过pages部署速度慢，网络环境也不好，这里不推荐，建议使用下文的Vercel。

![](/images/Pasted image 20260402164949.png)

构建成功后会deploy到pages，访问`https://用户名.github.io`即可。

![](/images/Pasted image 20260402164758.png)
## 改变样式
Astro和hexo不同的一点是样式和框架绑定，在hexo只要把样式文件丢进themes文件夹改一下配置文件直接push就能切换，而astro就比较麻烦了，需要把整个框架换掉，也就是把整个库换掉。我们换了个astropapr的主题，直接`clone` + `git init`。后续编写.github/workflows/deploy.yml(如果没有的话)，用于教github actions怎么构建网页。写好了直接push。
![](/images/Pasted image 20260404011329.png)
## 部署到Vercel
Github Actions主要有4个问题
- 必须编写deploy.yml，如果模版不内置需要自行学习YAML编写
- 解释器过于老旧，经常版本冲突
- 部署速度慢
- 网络环境非常差

Vercel**用来把你push的代码变成网页**，比github actions强大，速度快，方便部署。
直接添加repository连接到GitHub的博客仓库。能看到下面就算成功。
![](/images/Pasted image 20260404004125.png)

## 配置域名与DNS解析
Vercel的域名访问还是非常缓慢。
去[腾讯云](https://buy.cloud.tencent.com/domain?from=domain-console&position=domain-add-btn&_t=1775074038093)/[阿里云](https://www.alibabacloud.com/zh/domain?_p_lc=1&spm=a3c0i.7911826.nav-v2-dropdown-menu-2.d_main_12_0_0.6bb26cf4Oy6LPA&scm=20140722.X_data-d8ed229dd5ab5a3752a0._.V_1)买个域名，一年10块左右。还有dns解析
![](/images/屏幕截图 2026-04-02 040711 1.png)
回到Vercel配置一下域名和dns解析，即可正常使用。
![](/images/Pasted image 20260415164544.png)