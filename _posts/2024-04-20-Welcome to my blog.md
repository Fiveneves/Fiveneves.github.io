
## 一. 博客主题及其选取原因

Jekyll框架 gungnir主题

## 二. 博客页面布局及其设计思路

博客分为首页，归档，关于和搜索等页面。
首页：展示一定数量的博客，所有博客在归档可以有清晰的展示
归档：对所有博客以日期进行归档划分

分类：根据文章的 categories 值进行划分，方便分类查阅
标签：类似分类页，可依据标签页进行方便的查找
关于：自我展示页

首页
首页由顶部导航栏、顶部横幅、博客列表、汇总信息组成，左下角有音乐播放器，右下角有搜索功能和light/night切换等功能，下滑后还有回到顶部功能。修改后的博客页面基本保留了原有样式，在原基础上增添了“关于”页面，给出了博客作者的相关信息，删除了不需要的“好伙伴”页面和“链接”页面，除此之外对全部图片进行了替换，并且增加了一些博客来充实整体。

当前博客首页

博客详情页
博客详情页与首页大致相同，不同之处在于博客列表区域被替换为了博客详情页，右侧的汇总信息增加了当前博客的目录结构，目录结构也可选择不显示。

```
# Navigation menu settings
menus:
  - title: Home
    font: fab fa-fort-awesome
    url: /
  - title: About
    font: fas fa-id-card-o
    submenus:
      - title: Me
        font: fas fa-user-circle-o
        url: /about/
      - title: Theme
        font: fas fa-file-text
        url: /theme/
  - title: Archive
    font: fas fa-archive
    url: /archive/
  - title: Links
    font: fas fa-link
    url: /links/
```



## 三. 博客功能实现及其技术选择

### 1. 功能实现

本次博客主要实现了以下几个功能：

① 日间模式、夜间模式和阅读模式的切换

② 对文章打标签，并通过标签来找到文章

③ 在发布时间上对文章进行排序

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/fdbd04e4-f847-46f8-ab8e-b1c04fc64592)

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/b090a24c-e32c-470d-b343-d38e6eb6ccad)

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/79797252-add0-424f-b7c6-4bbe01256f1c)

## Client ID

```
f6cf3058e6bb5ed13ae3
```

## Client secrets

```
3da0d7ded3205425e02e94f94a66c74b69a65c64
```



从 GitHub 克隆项目：

```bash
git clone https://github.com/Renovamen/jekyll-theme-gungnir.git
cd jekyll-theme-gungnir
```

本地运行主题需要参考[这里](https://jekyllrb.com/docs/installation/)安装 Ruby 和 Jekyll。然后安装依赖包：

```bash
bundle config set path 'vendor/bundle'
bundle install
```

然后即可本地预览：

```bash
bundle exec jekyll serve --watch
```

如果想要改动代码，你可能需要 [Node.js](https://nodejs.org/en/)，并安装 [Grunt](https://gruntjs.com/)（用于压缩 js 文件）：

```bash
npm install
```

然后：

```bash
npm run dev
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

### 2. 技术选择

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

## 四. 博客制作过程中遇到的问题及其解决方法

### 1. 本地环境配置

通过 RubyInstaller 安装[固定链接](https://jekyllrb.com/docs/installation/windows/#installation-via-rubyinstaller)

安装 Ruby 和 Jekyll 的最简单方法是使用适用于 Windows 的 [RubyInstaller](https://rubyinstaller.org/)。

RubyInstaller 是一个独立的基于 Windows 的安装程序，包括 Ruby 语言、执行环境、 重要文档等。

1. 从 [RubyInstaller 下载](https://rubyinstaller.org/downloads/)下载并安装 **Ruby+Devkit** 版本。 使用默认选项进行安装。
2. 在安装向导的最后阶段运行该步骤。这是使用本机安装 Gem 所必需的 扩展。您可以在 [RubyInstaller 文档](https://github.com/oneclick/rubyinstaller2#using-the-installer-on-a-target-system)中找到有关此内容的其他信息。 从选项中选择 。`ridk install``MSYS2 and MINGW development tool chain`
3. 从“开始”菜单打开新的命令提示符窗口，以便对环境变量的更改生效。 使用 Jekyll 和 Bundler 安装`PATH``gem install jekyll bundler`

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/bfe04322-26e9-472c-b806-c599e241560d)

1. 检查 Jekyll 是否已正确安装：`jekyll -v`

![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/db9a1651-12b4-474c-a5a6-e3eac4a2e10e)



博客展示数学公式

遇到数学公式加载不成功的情况

解决方法：

查看官方文档[加载和配置 MathJax — MathJax 2.7 文档](https://docs.mathjax.org/en/v2.7-latest/configuration.html#)，在_includes/enhancements/mathjax.html内联配置中修改行内公式和行间公式规则
![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/ac6d875d-8ee9-4ea3-ad39-ab4739f0aa3d)

