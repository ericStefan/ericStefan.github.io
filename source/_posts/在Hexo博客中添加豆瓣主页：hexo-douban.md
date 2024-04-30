---
title: 在Hexo博客中添加豆瓣主页：hexo-douban
categories: 
- 博客搭建
description: 如何使用Hexo-douban插件给Hexo博客添豆瓣主页信息
cover: https://s2.loli.net/2024/04/29/2KO3TEij78BkoxH.png
tags:
- hexo
- blog
---

使用`hexo-douban`插件可以在Hexo中展示豆瓣中添加的电影、书籍、音乐、游戏等信息，效果如下图：

<img src="https://s2.loli.net/2024/04/30/UOZC3xh8bVNj7aJ.jpg" style="zoom: 67%;" />

## 安装

```npm
$ npm install hexo-douban --save
```

将下面的配置写入站点的配置文件 `_config.yml` 里(不是主题的配置文件).

```
douban:
  id: 162448367
  builtin: false
  item_per_page: 10
  meta_max_line: 4
  customize_layout: page
  book:
    path: books/index.html
    title: 'This is my book title'
    quote: 'This is my book quote'
    option:
  movie:
    path: movies/index.html
    title: 'This is my movie title'
    quote: 'This is my movie quote'
    option:
  game:
    path: games/index.html
    title: 'This is my game title'
    quote: 'This is my game quote'
    option:
  song:
    path: songs/index.html
    title: 'This is my song title'
    quote: 'This is my song quote'
    option:
  timeout: 10000 
```



- **id**: 你的豆瓣ID(纯数字格式，不是自定义的域名)。在豆瓣的个人主页界面的url`https://www.douban.com/people/xxxxxxx/`，people后面就是豆瓣ID号。
- **builtin**: 是否将`hexo douban`命令默认嵌入进`hexo g`、`hexo s`，使其自动执行`hexo douban` 命令。默认关闭。
- **item_per_page**: 每页展示的条目数，默认 10 。
- **meta_max_line**: 每个条目展示的详细信息的最大行数，超过该行数则会以 "..." 省略，默认 4 。
- **customize_layout**: 自定义布局文件。默认值为 page 。无特别需要，留空即可。若配置为 `abcd`，则表示指定 `//theme/hexo-theme/layout/abcd.ejs` 文件渲染豆瓣页面。
- **path**: 生成页面后的路径，默认生成在 //yourblog/books/index.html 等下面。如需自定义路径，则可以修改这里。
- **title**: 该页面的标题。
- **quote**: 写在页面开头的一段话,支持html语法。
- **timeout**: 爬取数据的超时时间，默认是 10000ms ,如果在使用时发现报了超时的错(ETIMEOUT)可以把这个数据设置的大一点。
- **option**: 该页面额外的 Front-matter 配置，参考[Hexo 文档](https://hexo.io/docs/front-matter.html)。无特别需要，留空即可。

如果只想显示某一个页面(比如movie)，那就把其他的配置项注释掉即可。

## 使用

**展示帮助文档**

```
$ hexo douban -h
Usage: hexo douban

Description:
Generate pages from douban

Options:
  -b, --books   Generate douban books only
  -g, --games   Generate douban games only
  -m, --movies  Generate douban movies only
  -s, --songs   Generate douban songs only
```

使用命令生成对应的展示页面（不要使用主题的方式添加页面）：

```npm
$ hexo douban -b
```

**主动生成豆瓣页面**

```
$ hexo douban
INFO  Start processing
INFO  0 (wish), 0 (do),0 (collect) game loaded in 729 ms
INFO  0 (wish), 0 (do),20 (collect) song loaded in 761 ms
INFO  2 (wish), 0 (do),136 (collect) book loaded in 940 ms
INFO  30 (wish), 0 (do),6105 (collect) movie loaded in 4129 ms
INFO  Generated: books/index.html
INFO  Generated: movies/index.html
INFO  Generated: games/index.html
INFO  Generated: songs/index.html
```

博主，使用的是butterfly主题，生成的豆瓣页面存放在`public`文件夹下。

如果不加参数，那么默认参数为`-bgms`。当然，前提是配置文件中均有这些类型的配置。

果不加参数，那么默认参数为`-bgms`。当然，前提是配置文件中均有这些类型的配置。

**需要注意的是**，通常大家都喜欢用`hexo d`来作为`hexo deploy`命令的简化，但是当安装了`hexo douban`之后，就不能用`hexo d`了，因为`hexo douban`跟`hexo deploy` 的前缀都是`hexo d`。

如果 builtin:false 时，执行 hexo g 之后发现将 douban 生成的页面删除了:

```
INFO  Start processing
INFO  Files loaded in 343 ms
INFO  Deleted: games/index.html
INFO  Deleted: books/index.html
INFO  Deleted: movies/index.html
INFO  Deleted: songs/index.html
```

## 显示

本地预览:

```npm
$ hexo snpm
```

在浏览器中打开http://localhost:4000/

如果上面的配置和操作都没问题，就可以在生成站点之后打开 `//yourblog/books` 和 `//yourblog/movies`, `//yourblog/games`, 来查看结果。

以本站为例，在地址栏输入“ericstefan.github.io/books”，按下回车就会加载到书籍的页面，浏览器缓存可能会默认输入“ericstefan.github.io/books/index.html”，就会载入错误，可以清楚浏览器缓存或者换个浏览器试一下。

## 菜单

如果上面的显示没有问题就可以在主题的配置文件 `_config.yml` 里添加如下配置来为这些页面添加菜单链接.

```yml
menu:
  首页: / || fas fa-home
  导航||fas fa-compass||hide:
     归档: /archives/ || fas fa-archive
     标签: /tags/ || fas fa-tags
     分类: /categories/ || fas fa-folder-open
  清单||fas fa-list||hide:
     书籍: /books || fas fa-book
     电影: /movies || fas fa-video
     游戏: /games || fa-solid fa-gamepad
  友链: /link/ || fas fa-link
  关于: /about/ || fas fa-heart
```

**注意**：清单的次级列表下的导航按钮就是豆瓣相关信息的导航，输入对应标签名时候，使用`/books`，而不是`/books/`,后者会出现不能正常跳转的问题。