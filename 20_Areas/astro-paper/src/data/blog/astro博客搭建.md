---
author: xprzmd
pubDatetime: 2026-04-15
modDatetime:
title: Astro + Vercel个人博客搭建方案
slug: adding-new-posts-in-astropaper-theme
featured: true
draft: false
share: true
tags:
  - blog
  - astro
description: 介绍了本博客搭建的全流程
---

# Astro+Vercel博客搭建流程

介绍本站的基于Astro + Vercel + Obsidian + [Git](app://obsidian.md/Git%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE)的三端同步个人博客方案。

---

## Github建立新仓库

在 GitHub 上建博客，仓库名字决定了你未来的网址：

- **特殊仓库（推荐）**：如果你把仓库命名为 `你的用户名.github.io`，你的博客网址就会非常简短漂亮：`https://用户名.github.io`。  
    ![Pasted image 20260402165615.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260402165615.png?1775120175382)
- **普通仓库**：一般的命名如test，它的网址会带上后缀`https://用户名.github.io/test/`。

## 安装[Node.js](app://obsidian.md/Node.js)

在开始之前，请确保你的电脑上安装了Node.js。Astro 依赖它来运行。 可以在终端输入 `node -v` 检查是否安装成功。  
![Pasted image 20260402165642.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260402165642.png?1775120202334)

## 本地构建Astro框架

建立博客文件夹进入输入`npm create astro@latest`, 如报错npm找不到命令可能是Node.js没设置好，打开终端权限即可，选Use blog template，后面都是yes。  
![Pasted image 20260402170027.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260402170027.png?1775120427965)

### Github设置（可选）

装好后[Git](app://obsidian.md/Git%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE)到github仓库，在仓库settings里面选择pages，sources选择github actions。这样每次push完github actions会自动使用astro构建网页。不过pages部署速度慢，网络环境也不好，这里不推荐，建议使用下文的Vercel。

![Pasted image 20260402164949.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260402164949.png?1775119789086)

构建成功后会deploy到pages，访问`https://用户名.github.io`即可。

![Pasted image 20260402164758.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260402164758.png?1775119678904)

## 改变样式

Astro和hexo不同的一点是样式和框架绑定，在hexo只要把样式文件丢进themes文件夹改一下配置文件直接push就能切换，而astro就比较麻烦了，需要把整个框架换掉，也就是把整个库换掉。我们换了个astropapr的主题，直接`clone` + `git init`。后续编写.github/workflows/deploy.yml(如果没有的话)，用于教github actions怎么构建网页。写好了直接push。  
![Pasted image 20260404011329.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260404011329.png?1775236409602)

## 部署到Vercel

Github Actions主要有4个问题

- 必须编写deploy.yml，如果模版不内置需要自行学习YAML编写
- 解释器过于老旧，经常版本冲突
- 部署速度慢
- 网络环境非常差

Vercel**用来把你push的代码变成网页**，比github actions强大，速度快，方便部署。  
直接添加repository连接到GitHub的博客仓库。能看到下面就算成功。  
![Pasted image 20260404004125.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260404004125.png?1775234485541)

## 配置域名与DNS解析

Vercel的域名访问还是非常缓慢。  
去[腾讯云](https://buy.cloud.tencent.com/domain?from=domain-console&position=domain-add-btn&_t=1775074038093)/[阿里云](https://www.alibabacloud.com/zh/domain?_p_lc=1&spm=a3c0i.7911826.nav-v2-dropdown-menu-2.d_main_12_0_0.6bb26cf4Oy6LPA&scm=20140722.X_data-d8ed229dd5ab5a3752a0._.V_1)买个域名，一年10块左右。还有dns解析  
![屏幕截图 2026-04-02 040711 1.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202026-04-02%20040711%201.png?1776242688930)  
回到Vercel配置一下域名和dns解析，即可正常使用。  
![Pasted image 20260415164544.png](app://236c08afd242e3cc021c12d3a80e6f0aaa3f/D:/DJL/Documents/Obsidian%20Vault/99_System/attachments/Pasted%20image%2020260415164544.png?1776242744679)