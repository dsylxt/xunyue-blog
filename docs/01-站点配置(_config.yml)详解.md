# 01 · 站点配置 `_config.yml` 逐块详解

> 文件位置：`D:\Blog\my-blog\_config.yml`
> 它是 **Hexo 框架**的配置（不是主题的）。管：站点叫什么、网址是什么、文章链接长什么样、每页几篇、部署到哪、用哪些插件。
> 主题相关的东西（导航、背景、头像、评论……）**不在这里**，在 `_config.fomalhaut.yml`（见《02 · 主题配置》）。
>
> **改完必须重启**：这个文件在 `hexo server` 启动时读一次，改完要 `Ctrl+C` 停掉再 `npm run server`。

---

## 目录

- [0. 一分钟速览：这个文件里都有啥](#0-一分钟速览)
- [1. Site —— 站点基本信息](#1-site--站点基本信息)
- [2. URL —— 网址与文章链接](#2-url--网址与文章链接)
- [3. abbrlink —— 短链接算法](#3-abbrlink--短链接算法)
- [4. Directory —— 目录与渲染控制](#4-directory--目录与渲染控制)
- [5. Writing —— 写作与代码高亮](#5-writing--写作与代码高亮)
- [6. Home / Archive —— 每页显示几篇](#6-home--archive--每页显示几篇)
- [7. Category & Tag / 时间格式 / 分页](#7-category--tag--时间格式--分页)
- [8. Extensions & Deployment —— 主题与部署](#8-extensions--deployment--主题与部署)
- [9. 插件配置区（搜索 / 轮播 / 磁贴 / 日历 / 统计）](#9-插件配置区)
- [10. 全站速查表](#10-全站速查表)

---

## 0. 一分钟速览

| 区块 | 管什么 | 要不要改 |
| --- | --- | --- |
| `Site` | 站名 / 作者 / 描述 | ⭐ 常改 |
| `URL` | 域名 / 文章链接格式 | ⭐ 必改（域名） |
| `abbrlink` | 短链接算法 | 一般不动 |
| `Directory` | 目录名 / 跳过渲染 | 加第三方文件时才动 |
| `Writing` | 新建文章命名 / 代码高亮 | 偶尔改 |
| `index_generator` / `archive_generator` | 首页 / 归档每页篇数 | ⭐ 常改 |
| `theme` | 用哪个主题 | 不动 |
| `deploy` | 部署方式 | 本站在用 Cloudflare，基本不动 |
| 插件区（`algolia`/`swiper`/`search`/`magnet`/`gitcalendar`…） | 搜索 / 轮播 / 分类磁贴 / 贡献日历 | 按需 |

---

## 1. Site —— 站点基本信息

```yaml
# Site
title: xunyue
subtitle: ''
description: "一个基于 Hexo + Fomalhaut 主题的演示站点"
keywords: "Hexo,Butterfly,Fomalhaut,博客,主题,卡片式UI"
author: xunyue
language: zh-CN
timezone: ""
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `title` | `xunyue` | **站点名**，显示在左上角、主页大标题、浏览器标签 | 改成你的站名，如 `小月的博客` |
| `subtitle` | `''`（空） | 站点副标题（一般留空） | 留空即可；**首页打字机副标题在主题文件里**（`_config.fomalhaut.yml` 的 `subtitle.sub`） |
| `description` | `一个基于 Hexo + Fomalhaut 主题的演示站点` | **SEO 描述**，搜索引擎抓取、分享卡片用 | 写一句话介绍你的站 |
| `keywords` | `Hexo,Butterfly,...` | **SEO 关键词**，逗号分隔 | 换成你站的主题词 |
| `author` | `xunyue` | **作者名**，页脚版权、文章版权卡用 | 改成你的名字 |
| `language` | `zh-CN` | 语言，影响主题内置文案（如「阅读更多」） | 中文站保持 `zh-CN` |
| `timezone` | `""` | 时区 | 留空自动用系统时区 |

> 💡 **改站点名**只需改 `title`；**改作者**改 `author`。这两处改完，全站标题和版权会同步变。

---

## 2. URL —— 网址与文章链接

```yaml
# URL
url: https://xunyue-blog.pages.dev/
permalink: posts/:abbrlink.html
permalink_defaults:
pretty_urls:
  trailing_index: true
  trailing_html: true
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `url` | `https://xunyue-blog.pages.dev/` | **站点域名**（必须带 `https://`、结尾带 `/`） | ⭐ 改成你自己的域名 |
| `permalink` | `posts/:abbrlink.html` | **文章链接格式** | 见下方说明 |
| `permalink_defaults` | 空 | 链接默认变量（用不到） | 不动 |
| `pretty_urls.trailing_index` | `true` | 链接结尾是否带 `index.html` | 不动 |
| `pretty_urls.trailing_html` | `true` | 链接结尾是否带 `.html` | 不动 |

**`url` 为什么必须改**：它影响 RSS 订阅、站点地图、分享链接、评论系统回调、SEO。填错了会导致「别人点分享链接打不开」。
例：`url: https://your-domain.com/`

**`permalink` 是什么**：决定每篇文章的网址长啥样。当前用 `:abbrlink`（把标题转成一段短哈希），所以文章链接形如：
```
https://xunyue-blog.pages.dev/posts/7a776471.html
```
好处：**改标题不会改链接**，链接短、稳定。

其它常见写法（想换就改这一行）：
| 写法 | 效果 |
| --- | --- |
| `posts/:abbrlink.html` | 当前：`/posts/7a776471.html` |
| `:year/:month/:day/:title/` | `/2026/10/14/我的第一篇文章/` |
| `posts/:year-:month-:day-:title.html` | `/posts/2026-10-14-我的第一篇文章.html` |

> ⚠️ 已经发布过的文章**不要随便改** `permalink`，否则老链接全部失效。

---

## 3. abbrlink —— 短链接算法

```yaml
# abbrlink config
abbrlink:
  alg: crc32
  rep: hex
```

| 字段 | 当前值 | 作用 |
| --- | --- | --- |
| `alg` | `crc32` | 生成短码的算法：`crc16`（默认，短）/ `crc32`（冲突更少） |
| `rep` | `hex` | 输出格式：`dec`（十进制）/ `hex`（十六进制） |

> 这决定 `:abbrlink` 长什么样（如 `7a776471`）。**改它会让所有已有文章的链接变化**，不建议动。

---

## 4. Directory —— 目录与渲染控制

```yaml
# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:
  - 'js/tag-map/*'
  - 'js/ai-chat.js'
  - 'box/astronomy/voyager.html'
```

| 字段 | 作用 | 改不改 |
| --- | --- | --- |
| `source_dir` | 源码目录（默认 `source`） | 不动 |
| `public_dir` | 构建产物目录（默认 `public`） | 不动（Cloudflare 输出目录也填这个） |
| `tag_dir` / `archive_dir` / `category_dir` | 标签页 / 归档页 / 分类页的网址前缀 | 不动 |
| `code_dir` / `i18n_dir` | 代码下载 / 多语言目录 | 不动 |
| `skip_render` | **跳过渲染的清单**（原样复制，不当模板解析） | 加了独立 HTML/JS 报错时才动 |

**`skip_render` 详解**：Hexo 默认会把 `source/` 下所有文件用模板引擎（Nunjucks）解析一遍。但有些文件内部含 `{{ }}`、`{% %}` 这种字面量，会被误当成模板语法而报错。
把这类文件列进来，它们就会**原样复制**到 `public/`，不做解析。

当前列的 3 项：
| 路径 | 为什么跳过 |
| --- | --- |
| `js/tag-map/*` | leaflet / proj4 第三方库原文件 |
| `js/ai-chat.js` | AI 助手前端，含大段 CSS/JS 字面量 |
| `box/astronomy/voyager.html` | 旅行者号独立交互页面 |

**什么时候要加**：你放了一个完整的第三方 JS 或独立 HTML 页面，构建时报「unknown block tag」之类的错，就把它加进这个列表。

---

## 5. Writing —— 写作与代码高亮

```yaml
# Writing
new_post_name: :year-:month-:day-:title.md
default_layout: post
titlecase: false
external_link:
  enable: true
  field: site
  exclude: ""
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: true
  tab_replace: ""
  wrap: true
  hljs: false
prismjs:
  enable: false
  ...
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `new_post_name` | `:year-:month-:day-:title.md` | 新建文章的**文件名格式** | 不动（生成的如 `2026-10-15-标题.md`） |
| `default_layout` | `post` | 默认布局 | 不动 |
| `titlecase` | `false` | 是否把标题自动转成首字母大写 | 中文站保持 `false` |
| `external_link.enable` | `true` | **外链在新标签页打开** | 想同页打开就改 `false` |
| `external_link.field` | `site` | 作用范围：`site`（全站）/ `post`（仅文章） | 不动 |
| `render_drafts` | `false` | 是否渲染草稿（`source/_drafts/`） | 想本地预览草稿改 `true` |
| `post_asset_folder` | `false` | 是否为每篇文章建同名资源文件夹 | 不动 |
| `future` | `true` | 是否渲染「未来日期」的文章 | 不动 |
| `highlight.enable` | `true` | **代码块高亮**总开关 | 不动 |
| `highlight.line_number` | `true` | 代码块显示行号 | 不想要行号改 `false` |
| `highlight.auto_detect` | `true` | 自动识别语言 | 不动 |
| `prismjs.enable` | `false` | 用 Prism.js 高亮（与 `highlight` 二选一） | 保持 `false` |

> ⚠️ `highlight` 和 `prismjs` **只能开一个**。当前用 `highlight`（`prismjs` 关着），别两个都开。
> 💡 代码块**配色**（`mac`/`light`/`ocean`…）不在这个文件，在主题文件的 `highlight_theme`。

---

## 6. Home / Archive —— 每页显示几篇

```yaml
# Home page setting
index_generator:
  path: ""
  per_page: 9
  order_by: -date

# Archive page setting
archive_generator:
  per_page: 12
  yearly: true
  monthly: true
  daily: false
  order_by: -date
```

| 区块 | 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- | --- |
| `index_generator` | `per_page` | `9` | **首页每页显示几篇文章** | ⭐ 改这个数字 |
| | `order_by` | `-date` | 排序（`-` 表示倒序，最新在前） | 不动 |
| `archive_generator` | `per_page` | `12` | **归档页每页篇数** | 12 是 3 列 4 行整；改 9/15 也成整行 |
| | `yearly` / `monthly` / `daily` | `true/true/false` | 是否生成按年 / 按月 / 按日的归档页 | 不动 |

> 💡 首页和归档**互不影响**，可以分别设。改完 `npm run clean && npm run server` 看效果。

---

## 7. Category & Tag / 时间格式 / 分页

```yaml
# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Metadata elements
meta_generator: true

# Date / Time format
date_format: YYYY-MM-DD
time_format: HH:mm:ss
updated_option: "mtime"

# Pagination
per_page: 10
pagination_dir: page
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `default_category` | `uncategorized` | 文章没写分类时的默认分类 | 可改成你想要的默认名 |
| `category_map` / `tag_map` | 空 | 分类/标签的**别名映射**（如把 `js` 映射成 `JavaScript`） | 需要时按 `原名: 别名` 写 |
| `meta_generator` | `true` | 是否输出 `<meta name="generator">` | 不动 |
| `date_format` | `YYYY-MM-DD` | 日期显示格式 | 想显示成 `2026年10月15日` 就改 `YYYY年MM月DD日` |
| `time_format` | `HH:mm:ss` | 时间显示格式 | 不动 |
| `updated_option` | `mtime` | 文章「更新时间」取哪个（文件修改时间） | 不动 |
| `per_page` | `10` | 分页默认每页条数 | 一般不动（首页/归档已单独设） |
| `pagination_dir` | `page` | 分页网址前缀（`/page/2/`） | 不动 |

**`category_map` 用法示例**（把英文分类名显示成中文）：
```yaml
category_map:
  algorithm: 算法
  database: 数据库
```

---

## 8. Extensions & Deployment —— 主题与部署

```yaml
# Include / Exclude file(s)
include:
exclude:
ignore:

# Extensions
theme: fomalhaut

# Deployment
deploy:
  - type: git
    repository: https://github.com/yourname/yourname.github.io.git
    branch: main
  - type: baidu_url_submitter
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `include` / `exclude` / `ignore` | 空 | 强制包含/排除文件（对 `source/`） | 一般不动 |
| `theme` | `fomalhaut` | **使用哪个主题** | 不动（改了要同步改主题配置文件名） |
| `deploy` | git + 百度推送 | `hexo deploy` 时的部署目标 | ⚠️ 见下方 |

**关于 `deploy`（重要）**：
- ⚠️ **本站上线不走这里**。你的站点是 **Cloudflare Pages 连 GitHub 自动构建**，上线方式 = `git push`（见《03 · 命令手册》）。
- 上面 `repository` 还是占位符 `yourname/yourname.github.io.git`——**直接跑 `npm run deploy` 会推到不存在的仓库而失败**。
- 这一段是主题自带的备用部署方式，只在 `hexo deploy` 时才用到。不用它就别管。

---

## 9. 插件配置区

这些是 Hexo **插件**（写在 `package.json` 里）的配置，插件在构建时读取。

### 9.1 搜索：`search`（本地）+ `algolia`（云端）

```yaml
# 本地搜索（生成 search.xml）
search:
  path: search.xml
  field: post
  content: true

# Algolia 云端搜索
algolia:
  appId: "YOUR_ALGOLIA_APP_ID"
  apiKey: "YOUR_ALGOLIA_SEARCH_KEY"
  adminApiKey: "YOUR_ALGOLIA_ADMIN_KEY"
  indexName: "your_index_name"
  fields:
    - content:strip:truncate,0,30000
    - excerpt:strip
    - gallery
    - permalink
    - photos
    - slug
    - tags
    - title

plugins:
  - hexo-algoliasearch
```

| 区块 | 作用 | 说明 |
| --- | --- | --- |
| `search` | 本地搜索，生成 `search.xml` | 无需外部服务，配置简单 |
| `algolia` | 云端全文搜索（Algolia） | 需注册 Algolia 填 4 个键 |
| `plugins` | 声明启用 `hexo-algoliasearch` 插件 | 不动 |

> ⚠️ **当前搜索不可用**：主题文件里 `algolia_search.enable: true`（走 Algolia），但这里的键还是 `YOUR_...` 占位符。二选一：
> - **用 Algolia**：去 algolia.com 建索引，填上 `appId/apiKey/adminApiKey/indexName`，再构建上传索引；
> - **用本地搜索（省事）**：把主题文件的 `algolia_search.enable` 改 `false`、`local_search.enable` 改 `true`。

### 9.2 首页轮播图 `swiper`

```yaml
swiper:
  enable: false
  priority: 1
  enable_page: /
  timemode: date
  layout:
    type: id
    name: recent-posts
    index: 0
  ...
```

| 字段 | 当前值 | 作用 |
| --- | --- | --- |
| `enable` | `false` | **首页轮播图开关**（关闭中） |
| `layout` | `recent-posts` | 轮播挂在首页哪个容器上 |
| `swiper_css/js` 等 | CDN 地址 | 轮播依赖的样式/脚本 |

> 打开它需要自建 gitcalendar 数据仓库（见 README「GitHub 贡献日历」）。想开就改 `enable: true` 并按 README 配置。

### 9.3 分类磁贴 `magnet`

```yaml
magnet:
  enable: true
  priority: 2
  enable_page: /
  type: categories
  devide: 3
  display:
    - name: 算法
      display_name: 算法学习笔记
      icon: 🍡
    - name: 计算机基础
      display_name: 计算机基础笔记
      icon: 🍼
    - name: 魔改教程
      display_name: 博客魔改教程
      icon: 🍉
    - name: Java基础
      display_name: Java基础笔记
      icon: 🍟
    - name: 数据库
      display_name: 数据库笔记
      icon: 🍨
    - name: 嵌入式知识点总结
      display_name: 嵌入式知识总结
      icon: 🧀
  color_setting:
    text_color: black
    text_hover_color: white
    background_color: "#e9e9e9"
    background_hover_color: var(--text-bg-hover)
  layout:
    type: id
    name: recent-posts
    index: 0
  temple_html: '<div class="recent-post-item" style="width:100%;height: auto"><div id="catalog_magnet">${temple_html_item}</div></div>'
```

**这是首页那排「算法 / 计算机基础 / 魔改教程…」的磁贴格子。**

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `enable` | 开关 | `true` 开 / `false` 关 |
| `devide` | 一行分几列（当前 3） | 改列数 |
| `display[].name` | **对应文章的分类名**（必须和文章 `categories` 完全一致） | ⭐ 按你的分类改 |
| `display[].display_name` | 磁贴上显示的名字 | 可随意起 |
| `display[].icon` | 磁贴图标（emoji） | 换成别的 emoji |
| `color_setting` | 磁贴文字/背景颜色 | 按需改 |

**加一个磁贴**：在 `display:` 下照抄一项，改 `name`（要和你的分类对上）/`display_name`/`icon`。
> ⚠️ `name` 写错（和文章分类对不上）磁贴就点不出文章。

### 9.4 GitHub 贡献日历 `gitcalendar`

```yaml
gitcalendar:
  enable: true
  priority: 5
  enable_page: /site/census/
  layout:
    type: id
    name: gitZone
    index: 0
  user: yourname
  apiurl: "https://gitcalendar.example.com"
  jsonurl: "https://cdn.jsdelivr.net/gh/yourname/gitcalendar-data@main/data.json"
  minheight:
    pc: 320px
    mibile: 0px
  color: "['#d9e0df', '#c6e0dc', ...]"
  container: .recent-post-item(style='width:100%;height:auto;padding:10px;')
  gitcalendar_css: /css/gitcalendar.css
  gitcalendar_js: /js/gitcalendar.js
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `enable` | `true` | 开关 | 不动 |
| `enable_page` | `/site/census/` | 只在这个页面显示 | 不动 |
| `user` | `yourname` | **你的 GitHub 用户名** | ⭐ 改成你的 |
| `apiurl` | `https://gitcalendar.example.com` | gitcalendar 服务地址 | 改成你的服务地址 |
| `jsonurl` | `.../yourname/gitcalendar-data...` | 定时更新的数据 JSON | 改成你的数据仓库 |
| `color` | 一串颜色 | 日历热力色 | 注释里有多套预设，可换 |

> ⚠️ `user` / `apiurl` / `jsonurl` 三处还是占位符，**贡献日历现在显示不出来**，要按 README 自建数据仓库后替换。

### 9.5 RSS 订阅 `feed` / 站点地图 `sitemap` / 百度推送

```yaml
# RSS 订阅
plugin:
  - hexo-generator-feed
feed:
  type: atom
  path: atom.xml
  limit: 20

# 站点地图
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml

# 主动推送百度
baidu_url_submit:
  count: 10
  host: https://example.com
  token: YOUR_BAIDU_TOKEN
  path: baidu_urls.txt

# 外链 nofollow
nofollow:
  enable: false
  field: site
  exclude: ""
```

| 区块 | 作用 | 怎么改 |
| --- | --- | --- |
| `feed` | 生成 RSS（`/atom.xml`），`limit: 20` = 最多 20 篇 | 想改数量改 `limit` |
| `sitemap` / `baidusitemap` | 生成给搜索引擎的站点地图 | 不动 |
| `baidu_url_submit` | 主动把新链接推给百度收录 | ⭐ `host`/`token` 换成百度站长平台的，否则无效 |
| `nofollow` | 给外链加 `rel=nofollow` | 关闭中，一般不动 |

### 9.6 目录跳转层级 `markdown`

```yaml
markdown:
  anchors:
    level: 1
```

| 字段 | 当前值 | 作用 |
| --- | --- | --- |
| `anchors.level` | `1` | 文章目录（TOC）只抓**一级标题**生成跳转锚点 |

> 想让目录包含二级标题，把 `level` 改成 `2`。层级越深，目录越长。

### 9.7 其它：`math`（公式）、`aplayer`（音乐）

```yaml
math:
  engine: "mathjax"
  mathjax:
    src: custom_mathjax_source
    config:

aplayer:
  meting: true
  asset_inject: false
```

| 区块 | 作用 | 说明 |
| --- | --- | --- |
| `math` | 数学公式引擎（用 MathJax） | 文章 front-matter 写 `mathjax: true` 才加载 |
| `aplayer` | 音乐播放器插件（八音盒用） | `meting: true` 支持网易云歌单 |

---

## 10. 全站速查表

| 我想改…… | 改哪一行 |
| --- | --- |
| 站点名 | `title` |
| 作者名 | `author` |
| 站点描述 / 关键词 | `description` / `keywords` |
| **域名** | `url` |
| 文章链接格式 | `permalink` |
| 新建文章的命名格式 | `new_post_name` |
| 外链是否新标签打开 | `external_link.enable` |
| 代码块行号 | `highlight.line_number` |
| **首页每页篇数** | `index_generator.per_page` |
| **归档页每页篇数** | `archive_generator.per_page` |
| 日期显示格式 | `date_format` |
| 分类别名 | `category_map` |
| 使用哪个主题 | `theme` |
| 首页分类磁贴 | `magnet.display` |
| GitHub 贡献日历用户名 | `gitcalendar.user` |
| 百度推送域名 / 密钥 | `baidu_url_submit.host` / `.token` |
| 目录跳转层级 | `markdown.anchors.level` |
| 搜索（本地/云端） | `search` / `algolia` + 主题文件的 `algolia_search`/`local_search` |

---

*本文件基于 `D:\Blog\my-blog\_config.yml` 当前内容编写。配套文档：《02 · 主题配置 `_config.fomalhaut.yml` 详解》《03 · 命令手册》。*
