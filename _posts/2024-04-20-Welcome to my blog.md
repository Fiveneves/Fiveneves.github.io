---
layout: post
title: Welcome to my blog
subtitle: This is a report of assignment_1
header-img: img/in-post/2024-04-20/header.jpg
header-style: image
catalog: true
tags:
---


## 一. 博客简介

主要记录一些奇思妙想和算法学习、论文阅读笔记。

| 页面    | 内容                                              |
| ------- | ------------------------------------------------- |
| Home    | 展示博客简介和最新博客文章                        |
| About   | 个人介绍、教育背景、项目和论文情况。              |
| Archive | 对所有博客以日期进行归档划分，支持通过tag分类筛选 |
| Links   | 友情链接，可以展示自己其他平台的链接              |
| Search  | 搜索功能，根据关键词搜索所有满足条件的文章        |
| Post    | 以Markdown形式展示每篇文章的详细内容              |

### 首页

首页由顶部导航栏、博客简介、个人博客列表组成，右下角有light/reading/night切换、回到顶部和回到底部功能，同时以百分比的形式显示当前观看进度。

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/60639443-0da2-4794-b1d2-3be21951eec7)


![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/232d7c7c-30e2-47c3-9204-0dcff4da038c)


### 关于

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/97b0bd3c-a842-4c9e-9758-700ea42f112a)


### 归档

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/f26444e2-a643-40a6-83bc-728639f187cd)


### 链接

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/487e0446-3a20-4e90-afd2-89724013cac9)


### 搜索

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/e66bab7b-cb79-4c40-813b-918a58e60ca1)


### 详情页

和首页布局基本一致，把首页的博客简介替换成了文章简介，文章列表替换成了文章内容，右边还添加了文章目录，可以快速索引定位。

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/1731db9b-0285-4e47-a0ce-eb0fd84ada99)


## 二. 功能实现

本次博客主要实现了以下几个功能：

① 日间模式、夜间模式和阅读模式的切换

② 对文章打标签，并通过标签来找到文章

③ 在发布时间上对文章进行排序

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/414c67a9-5a71-4160-8067-4f8c6c89742c)


![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/785835e4-abc0-41e9-9776-bc46b7eadcba)




### Markdown 附加功能

#### 数学公式渲染

支持使用 [Mathjax](https://github.com/mathjax/MathJax) 或 [Katex](https://github.com/KaTeX/KaTeX) 来在文章中渲染数学公式。

Katex 渲染速度快于 Mathjax（可以参考[这里](https://katex.org/)），但支持的 Tex 公式少于 Mathjax（[这里](https://katex.org/docs/supported.html)是 Katex 支持的公式列表）。

如果 `_config.yml` 中 `math.enable: false`，则只有 Front-matter 中添加了 `mathjax: true` 的文章才会开启公式渲染：

```yaml
---
layout: post
mathjax: true
---

```

否则所有文章（包括 `post` 和 `keynote`）中都会开启此功能。

示例：

Inline math: 𝐸=𝑚𝑐2*E*=*m**c*2

Display math:

𝑖ℏ∂𝜓∂𝑡=−ℏ22𝑚(∂2∂𝑥2+∂2∂𝑦2+∂2∂𝑧2)𝜓+𝑉𝜓.*i*ℏ∂*t*∂*ψ*=2*m*−ℏ2(∂*x*2∂2+∂*y*2∂2+∂*z*2∂2)*ψ*+*V**ψ*.

```plaintext
$$ E = mc^2 $$
 
$$
i \hbar \frac{\partial \psi}{\partial t}
= \frac{-\hbar^2}{2m} ( \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2} + \frac{\partial^2}{\partial z^2} ) \psi + V \psi
$$
```

#### 图表

##### Chart.js

使用了 [Chart.js](https://github.com/chartjs/Chart.js) 以在文章中加入可交互的图表。可以参考 [Chart.js 文档](https://www.chartjs.org/docs/latest/)来创建表格。

示例：

~~~chart
```chart
{
    "type": "bar",
    "data": {
        "labels": ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
        "datasets": [{
            "label": "# of Votes",
            "data": [12, 19, 3, 5, 2, 3],
            "backgroundColor": [
                "rgba(255, 99, 132, 0.2)",
                "rgba(54, 162, 235, 0.2)",
                "rgba(255, 206, 86, 0.2)",
                "rgba(75, 192, 192, 0.2)",
                "rgba(153, 102, 255, 0.2)",
                "rgba(255, 159, 64, 0.2)"
            ],
            "borderColor": [
                "rgba(255, 99, 132, 1)",
                "rgba(54, 162, 235, 1)",
                "rgba(255, 206, 86, 1)",
                "rgba(75, 192, 192, 1)",
                "rgba(153, 102, 255, 1)",
                "rgba(255, 159, 64, 1)"
            ],
            "borderWidth": 1
        }]
    },
    "options": {
        "scales": {
            "yAxes": [{
                "ticks": {
                    "beginAtZero": true
                }
            }]
        }
    }
}
```
~~~

`注意`：`json` 中的 `key` 值一定要加**引号**，否则会渲染出错。

##### mermaid

使用了 [mermaid](https://github.com/knsv/mermaid) 以在文章中加入流程图、状态图、时序图、甘特图等。可以参考 [mermaid 文档](https://mermaid-js.github.io/mermaid/)来创建图。

示例：

~~~mermaid
Animal+int age+String gender+isMammal()+mate()Duck+String beakColor+swim()+quack()Fish-int sizeInFeet-canEat()Zebra+bool is_wild+run()
```mermaid
classDiagram
    Animal <|-- Duck
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
    class Fish{
        -int sizeInFeet
        -canEat()
    }
    class Zebra{
        +bool is_wild
        +run()
    }
```
~~~

#### 标签

```
消息标签
`消息标签`{:.info}
成功标签
`成功标签`{:.success}
警告标签
`警告标签`{:.warning}
错误标签
`错误标签`{:.error}
```

#### 提示

消息提示文案

```markdown
消息提示文案
{:.info}
```

成功提示文案

```markdown
成功提示文案
{:.success}
```

警告提示文案

```markdown
警告提示文案
{:.warning}
```

错误提示文案

```markdown
错误提示文案
{:.error}
```

#### 表情

##### emoji

使用了 [jemoji](https://github.com/jekyll/jemoji) 插件以在文章中插入 emoji，需要手动安装这个插件：

```bash
gem install jemoji
```

从[这里](https://pages.github.com/versions/)可以看到 Github Pages 上自带 jemoji 插件。[这里](https://www.webfx.com/tools/emoji-cheat-sheet/)是所有 emoji 的代码。

示例：

![:smile:](D:\Markdown\Fiveneves.github.io.assets\1f604.png) ![:smirk:](D:\Markdown\Fiveneves.github.io.assets\1f60f.png) ![:racehorse:](D:\Markdown\Fiveneves.github.io.assets\1f40e.png) ![:wolf:](D:\Markdown\Fiveneves.github.io.assets\1f43a.png)

```markdown
:smile: :smirk: :racehorse: :wolf:
```

##### 附加表情

也可以在文章中插入其他表情，目前支持 Bilibili 的小电视表情 ![img](D:\Markdown\Fiveneves.github.io.assets\斜眼笑.gif)（效果出乎意料的好）。

示例：

![img](D:\Markdown\Fiveneves.github.io.assets\斜眼笑.gif) ![img](D:\Markdown\Fiveneves.github.io.assets\doge.gif) ![img](D:\Markdown\Fiveneves.github.io.assets\白眼.gif)

```markdown
`斜眼笑`{:.emoji-plus} `doge`{:.emoji-plus} `白眼`{:.emoji-plus}
```

[附录](https://jekyll-theme-gungnir.vercel.app/theme/#附录)是所有支持的小电视表情和它们对应的代码，表情源文件来源于[这里](https://www.bilibili.com/video/av27621778/)。

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/5ae30771-c02c-44f9-9074-b27868bcb0bc)


![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/8ed2880e-5de0-4acd-a6e0-544bc5b4ee47)


![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/57168d07-88a7-4d80-89f1-6cc2f5ca5847)


从 GitHub 克隆项目：

```bash
git clone https://github.com/Renovamen/jekyll-theme-gungnir.git
cd jekyll-theme-gungnir
```

本地运行需要参考[这里](https://jekyllrb.com/docs/installation/)安装 Ruby 和 Jekyll。然后安装依赖包：

```bash
bundle config set path 'vendor/bundle'
bundle install
```

然后即可本地预览：

```bash
bundle exec jekyll serve --watch
```

### 导航菜单

一级菜单的配置如下：

```yaml
menus:
  - title: Home
    font: fab fa-fort-awesome
    url: /
  - title: Archive
    font: fas fa-archive
    url: /archive/
```

需要填入每个页面的名称、路径和图标。图标库使用了 [Font Awesome](https://fontawesome.com/)，可以在[这里](https://fontawesome.com/icons)查找图标。

如果要添加**二级菜单**，则需要在需要添加二级菜单的一级菜单下添加 `submenus` 关键字，然后在 `submenus` 下填入每个二级菜单页面的名称、路径和图标：

```yaml
menus:
  - title: About
    font: fas fa-paw
    submenus:
      - title: Me
        font: fas fa-user-astronaut
        url: /about/
```

### 评论功能

#### Gitalk

注册一个 [Github Application](https://github.com/settings/applications/new) 并搞到 Client ID 和 Client Secret，然后填入对应信息：

```yaml
comment: 
  provider: gitalk
  gitalk:
    clientID: # Github Application Client ID
    clientSecret: # Github Application Client Secret
    repo: # 用来放评论的 Github 仓库
    owner: # 上述 Github 仓库的拥有者 ID
    admin: 
      - 管理员1
      - 管理员2
      - ...
```

此处参考 [Gitalk 文档](https://github.com/gitalk/gitalk)

## 三. 技术选择

### Jekyll

1. **简单易用**：Jekyll是一个简单易用的静态网站生成器，特别适合用来搭建博客。它使用Markdown语法编写文章，生成静态网页，无需复杂的后台配置。
2. **快速部署**：Github Pages提供了免费的静态网站托管服务，可以直接将Jekyll生成的静态网页部署到Github上，无需购买额外的主机服务。
3. **社区支持**：Jekyll有庞大的社区支持，有大量的文档和教程可供参考，遇到问题时可以很容易地找到解决方案。

- **GitHub Pages**: 利用GitHub Pages进行博客的托管，保证了网站的稳定性和访问速度。
- 
- **Markdown**: 通过Markdown编写博客内容，保证了内容的可读性和编写效率。



### CSS

- [Bootstrap](https://github.com/twbs/bootstrap)
- [Font Awesome](https://github.com/FortAwesome/Font-Awesome)
- [Font Awesome Animation](https://github.com/l-lin/font-awesome-animation)

### JavaScript

- [jQuery](https://github.com/jquery/jquery)
- [ScrollReveal](https://github.com/jlmakes/scrollreveal)（图片模式下文章列表上浮效果，About 页面的时间轴上浮效果）
- [Tocbot](https://github.com/tscanlin/tocbot)（文章目录）
- [AnchorJS](https://github.com/bryanbraun/anchorjs/)（文章锚点）
- [Gitalk](https://github.com/gitalk/gitalk)（Gitalk 评论）
- [Chart.js](https://github.com/chartjs/Chart.js)（[图表](https://fiveneves.github.io/theme/#chartjs)）
- [mermaid](https://github.com/mermaid-js/mermaid)（[图表](https://fiveneves.github.io/theme/#mermaid)）
- [MathJax](https://github.com/mathjax/MathJax)（公式渲染）
- [Katex](https://github.com/KaTeX/KaTeX) （公式渲染）
- [hightlight.js](https://github.com/highlightjs/highlight.js) （代码高亮渲染）
- [hightlight-line-number.js](https://github.com/wcoder/highlightjs-line-numbers.js/) （给 hightlight.js 生成的代码块加行号的插件）
- [Simple-Jekyll-Search](https://github.com/christian-fei/Simple-Jekyll-Search)（搜索）
- [fastclick](https://github.com/ftlabs/fastclick)（解决移动设备上的点击延迟问题）

## 五. 遇到的问题及其解决方法

### 1. 本地环境配置

通过 RubyInstaller 安装[固定链接](https://jekyllrb.com/docs/installation/windows/#installation-via-rubyinstaller)

安装 Ruby 和 Jekyll 的最简单方法是使用适用于 Windows 的 [RubyInstaller](https://rubyinstaller.org/)。

RubyInstaller 是一个独立的基于 Windows 的安装程序，包括 Ruby 语言、执行环境、 重要文档等。

1. 从 [RubyInstaller 下载](https://rubyinstaller.org/downloads/)下载并安装 **Ruby+Devkit** 版本。 使用默认选项进行安装。
2. 在安装向导的最后阶段运行该步骤。这是使用本机安装 Gem 所必需的 扩展。您可以在 [RubyInstaller 文档](https://github.com/oneclick/rubyinstaller2#using-the-installer-on-a-target-system)中找到有关此内容的其他信息。 从选项中选择 。`ridk install``MSYS2 and MINGW development tool chain`
3. 从“开始”菜单打开新的命令提示符窗口，以便对环境变量的更改生效。 使用 Jekyll 和 Bundler 安装`PATH``gem install jekyll bundler`

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/88ef63da-b32c-4a98-aba8-0a23b1c0edf9)


检查 Jekyll 是否已正确安装：`jekyll -v`

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/dec20c2f-4812-4888-a591-2087d2bed455)




### 2. 文章展示数学公式

问题：遇到数学公式加载不成功的情况

解决方法：查看官方文档[加载和配置 MathJax — MathJax 2.7 文档](https://docs.mathjax.org/en/v2.7-latest/configuration.html#)，在_includes/enhancements/mathjax.html内联配置中修改行内公式和行间公式规则

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/f8c162eb-9e53-44eb-b7c0-09a2a40c5be2)

