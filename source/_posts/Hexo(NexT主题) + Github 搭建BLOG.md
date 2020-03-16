---
title: Hexo(NexT主题) + Github 搭建BLOG
tags: []
date: 2020-03-14 15:16:03
permalink:
categories: Web
description: 使用Hexo和GitHub搭建个人Blog平台，记录搭建过程以及遇到的问题。该Blog主要记录自己关注和感兴趣的内容，包括科技、电影、计算机、人文历史等。
image: 
---
<p class="description"></p>

<!-- more -->

# 环境
> macOS High Sierra 10.13.6
node.js 6.4.0
git 2.17.2

> hexo由node.js开发，所以要安装hexo需要node.js环境。由于已经环境中已有node.js和git，此处不再介绍其安装过程。

# Github
在[Github](https://github.com/)上新建仓库(repository)，仓库名称格式为:Github用户名.github.io。
![](/images/github_repo.png)
# Hexo

- ## 安装[Hexo](https://hexo.io/zh-cn/)
```
$ npm install -g hexo-cli
```
- ## 创建项目
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
执行完以上指令，会在folder中创建hexo项目目录和文件。

- ## 项目结构
![](/images/project_structure.jpg)
 - _config.yml 
全局配置文件(不同于主题中的_config.yml)，用于配置项目的基本参数。
 - scraffolds
脚手架目录，用于配置创建文章时的结构内容。
 - source
用于保存文章和页面，其中的_post用于存放文章文件。
 -themes
主题目录，其中每个目录即使一个主题，默认主题为landscape。
 -package.json
框架的参数和依赖插件。

- ## 创建文章
```
$ hexo new "post-name"
```
执行以上指令，会在source/_posts中创建post-name.md文章文件，编辑该文件即可编辑文章。


- ## 创建页面
```
$ hexo new page "page-name"
```
执行以上指令，会在/source中创建page-name目录，并在目录中创建index.md文件.可以在指令中使用--path来指定文件名称。
```
$ hexo new page --path about/me
```
执行以上指令，会在/source中创建about目录，并在/source/about中创建me.md文件。

- ## 发布项目
  - ### 安装插件
```
$ npm install hexo-deployer-git --save
```
  - ### 修改配置
在项目配置文件_config.yml中找到deploy配置项，修改如下:
```
deploy:
  type: git
  repo: https://github.com/whichouno/whichouno.github.io
  branch: master
```
  - ### 发布项目
```
$ hexo deploy
```
执行以上指令，会把本地的hexo项目发布到Github的whichouno.github.io仓库。
- ## 启动项目
```
$ hexo generate
```
执行以上指令，生成静态网页。
```
$ hexo server
```
执行以上指令，启动服务器。
- ## 预览项目
本地浏览器输入[http://localhost:4000/](http://localhost:4000/)访问项目。


# 主题配置

- ## 安装NexT
```
$ git clone https://github.com/theme-next/hexo-theme-next.git themes/next
```
执行以上指令，会在/themes目录下安装next主题。
- ## 设置主题
在项目配置文件_config.yml中，找到theme配置项，修改如下：
```
theme: next
```
- ## 选择风格
在主题的配置文件/themes/next/_config.yml中，找到Schemes配置项，选择风格，去掉注释：
```
# Schemes
# scheme: Muse
# scheme: Mist
# scheme: Pisces
scheme: Gemini
```


# 指令说明
- ## clean 
清除缓存文件(db.json)和已生成的静态文件(public)。
```
$ hexo clean
```
- ## generate 
生成静态文件，简写g。
```
$ hexo generate
```
或者
```
$ hexo g
```
- ## server 
启动服务器，简写s。
```
$ hexo server
```
或者
```
$ hexo s
```
- ## deploy 
部署网站，简写d。
```
$ hexo deploy
```
或者
```
$ hexo d
```
- ## version 
显示Hexo版本。
```
$ hexo version
```
- ## list 
列出网站资料。
```
$ hexo list
```
- ## 组合
清空缓存，生成静态文件并启动服务器。
```
$ hexo clean && hexo g && hexo s
```
清空缓存，生成静态文件并部署。
```
$ hexo clean && hexo g && hexo d
```
清空缓存，生成静态文件后启动服务器。
```
$ hexo clean && hexo s -g
```
清空缓存，生成静态文件后部署。
```
$ hexo clean && hexo d -g
```

# 进阶配置
- ## 文章头设置
在项目目录/scaffolds中，修改post.md文件：
```
---
title: {{ title }}
date: {{ date }}
permalink:
categories:
tags: []
description:
image:
---
<p class="description"></p>

<!-- more -->

##

##

##

<hr />
```
以上修改，在创建新文章时以此为末班，方便文章编辑。
- ## 添加Github链接图标
在主题目录下/themes/next/layout/_layout.swig文件中，找到"headband"，在其下方添加如下代码：
```
<div class="headband"></div>


    <a href="https://github.com/whichouno" class="github-corner" aria-label="View source on Github"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a>
```
其中"a href"修改为自己的Github地址：https://github.com/whichouno
- ## 文章边框添加阴影效果
对于无文章边框阴影的风格，在主题目录下/themes/next/source/css/_schemes/Mist/_posts-expanded.styl文件中，修改.post属性如下：
```
.post { 
  margin-top: 60px; 
  margin-bottom: 60px; 
  padding: 25px; 
  -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5); 
  -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5); 
} 
```
- ## 设置边框作者图片
在主题配置文件/themes/next/_config.yml中，找到Sidebar Avatar配置项，去掉url注释并修改url为图片路径如下：
```
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  # url: /images/avatar.gif
  url: /images/sea.jpg
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```
- ## 设置边框作者图片圆形及动画效果
在主题目录下/themes/next/source/css/_common/outline/sidebar/sidebar-author.style中，添加如下代码：
```
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;

  /* 头像圆形 */
  border-radius: 80px;
  -webkit-border-radius: 80px;
  -moz-border-radius: 80px;
  box-shadow: inset 0 -1px 0 #333sf;
  
  /* 设置循环动画 [animation: (play)动画名称 (2s)动画播放时长单位秒或微秒 (ase-out)动画播放的速度曲线为以低速结束 
    (1s)等待1秒然后开始动画 (1)动画播放次数(infinite为循环播放) ]*/
  -webkit-animation: play 2s ease-out 1s 1;
  -moz-animation: play 2s ease-out 1s 1;
  animation: play 2s ease-out 1s 1; 

  /* 鼠标经过头像旋转360度 */
  -webkit-transition: -webkit-transform 1.5s ease-out;
  -moz-transition: -moz-transform 1.5s ease-out;
  transition: transform 1.5s ease-out;
}

img:hover {
  /* 鼠标经过停止头像旋转 
  -webkit-animation-play-state:paused;
  animation-play-state:paused;*/

  /* 鼠标经过头像旋转360度 */
  -webkit-transform: rotateZ(360deg);
  -moz-transform: rotateZ(360deg);
  transform: rotateZ(360deg);
}

/* Z 轴旋转动画 */
@-webkit-keyframes play {
  0% {
    -webkit-transform: rotateZ(0deg);
  }
  100% {
    -webkit-transform: rotateZ(-360deg);
  }
}
@-moz-keyframes play {
  0% {
    -moz-transform: rotateZ(0deg);
  }
  100% {
    -moz-transform: rotateZ(-360deg);
  }
}
@keyframes play {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(-360deg);
  }
}

.site-author-name {
  margin: $site-author-name-margin;
  text-align: $site-author-name-align;
  color: $site-author-name-color;
  font-weight: $site-author-name-weight;
}

.site-description {
  margin-top: $site-description-margin-top;
  text-align: $site-description-align;
  font-size: $site-description-font-size;
  color: $site-description-color;
}
```
- ## 设置网站图标
在主题配置文件/themes/next/_config.yml中，找到favicon配置项，为small和medium修改图标路径如下：
```
favicon:
  #small: /images/favicon-16x16-next.png
  #medium: /images/favicon-32x32-next.png
  small: /images/romans_16x16.png
  medium: /images/romans_32x32.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```
- ## 设置菜单
在主题配置文件/themes/next/_config.yml中，找到menu配置项，去掉子项的注释来增加菜单：
```
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  # schedule: /schedule/ || calendar
  # sitemap: /sitemap.xml || sitemap
```
- ## 设置站点(项目)信息
在项目配置文件_config.yml中找到Site配置项，修改如下:
```
# Site
title: OUNO'S BLOG #站点标题
subtitle: '' #站点副标题
description: '一事精致 便是动人' #站点描述
keywords: #关键字
author: ouno #作者名称
# language: en
language: zh-Hans #语言
timezone: '' #时区，默认使用计算机本地时区
```
- ## 隐藏底部"由Hexo强力驱动，主题..."
在主题目录下/themes/next/layout/_partials/footer.swig，注释如下代码：
```
<!--
{%- if theme.footer.powered.enable %}
  <div class="powered-by">
    {{- __('footer.powered', next_url('https://hexo.io', 'Hexo', {class: 'theme-link'})) }}
    {%- if theme.footer.powered.version %} v{{ hexo_version }}{%- endif %}
  </div>
{%- endif %}

{%- if theme.footer.powered.enable and theme.footer.theme.enable %}
  <span class="post-meta-divider">|</span>
{%- endif %}

{%- if theme.footer.theme.enable %}
  <div class="theme-info">
    {%- set next_site = 'https://theme-next.org' %}
    {%- if theme.scheme !== 'Gemini' %}
      {%- set next_site = 'https://' + theme.scheme | lower + '.theme-next.org' %}
    {%- endif %}
    {{- __('footer.theme') }} – {{ next_url(next_site, 'NexT.' + theme.scheme, {class: 'theme-link'}) }}
    {%- if theme.footer.theme.version %} v{{ next_version }}{%- endif %}
  </div>
{%- endif %}
-->
```
- ## 显示浏览进度
在主题配置文件/themes/next/_config.yml中，找到back2top配置项，修改enable为true，开启浏览进度条：
```
back2top:
  enable: true
  # Back to top in sidebar.
  sidebar: false
  # Scroll percent label in b2t button.
  scrollpercent: true
```
- ## 添加站内搜索
安装搜索插件：
``` bash
$ npm install hexo-generator-search --save
$ npm install hexo-generator-searchdb --save
```
在主题配置文件/themes/next/_config.yml中，找到local_search配置项，设置enable为true开启搜索：
```
local_search:
  enable: true
  # If auto, trigger search by changing input.
  # If manual, trigger search by pressing enter key or search button.
  trigger: auto
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  # Preload the search data when the page loads.
  preload: false
```
- ## 添加字数统计
安装字数统计插件：
``` bash
$ npm install hexo-symbols-count-time --save
```
在主题配置文件/themes/next/_config.yml中，找到symbols_count_time配置项，修改如下：
```
symbols_count_time:  
  # 是否另起一行（true的话不和发表时间等同一行）
  separated_meta: true
  # 首页文章统计数量前是否显示文字描述（本文字数、阅读时长）
  item_text_post: true
  # 页面底部统计数量前是否显示文字描述（站点总字数、站点阅读时长）
  item_text_total: true
```
- ## 添加评论
- ## 添加404页面

# 常见问题
- ## 文章边框添加阴影效果
之前版本的hexo支持/themes/next/source/css/_custom/custom.styl自定义设置，在其中添加.post{...}设置阴影效果，新版本需要在/themes/next/source/css/_schemes/Mist/_posts-expanded.styl中修改.post{...}设置阴影效果。