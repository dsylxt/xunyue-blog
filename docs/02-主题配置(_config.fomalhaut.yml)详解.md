# 02 · 主题配置 `_config.fomalhaut.yml` 逐块详解

> 文件位置：`D:\Blog\my-blog\_config.fomalhaut.yml`
> 它是 **Fomalhaut 主题**的配置。你日常改得最多的就是它：导航、头像、背景、主题色、评论、侧栏、特效、AI 助手……全在这。
>
> **为什么文件名这么怪？** Hexo 的规则：根目录放一个 `_config.<主题名>.yml`，就会**覆盖**主题自带的 `themes/fomalhaut/_config.yml`。你的主题名是 `fomalhaut`（见 `_config.yml` 的 `theme:`），所以配置放这里。
> ⚠️ **永远改这个文件，不要改 `themes/fomalhaut/_config.yml`**（那是出厂默认值，升级会被覆盖）。
>
> **改完必须重启**：`Ctrl+C` 停掉 `npm run server`，再重新启动。

---

## 目录

- [A. 导航与社交](#a-导航与社交)
- [B. 代码块与复制](#b-代码块与复制)
- [C. 搜索与数学公式](#c-搜索与数学公式)
- [D. 图片：图标 / 头像 / 顶部图 / 封面 / 404](#d-图片图标--头像--顶部图--封面--404)
- [E. 文章页](#e-文章页)
- [F. 分享功能](#f-分享功能)
- [G. 评论区](#g-评论区)
- [H. 页脚 / 统计 / 广告 / 站长验证](#h-页脚--统计--广告--站长验证)
- [I. 外观：主题色 / 背景 / 特效 / 字体 / 副标题 / 加载动画](#i-外观)
- [J. 侧栏](#j-侧栏)
- [K. 右下角按钮与显示模式](#k-右下角按钮与显示模式)
- [L. 图片查看与标签外挂](#l-图片查看与标签外挂)
- [M. 性能与其它开关](#m-性能与其它开关)
- [N. inject —— 代码注入（本站魔改核心）](#n-inject--代码注入本站魔改核心)
- [O. CDN](#o-cdn)
- [P. 其它插件与页面](#p-其它插件与页面)
- [Q. 全站速查表](#q-全站速查表)

---

## A. 导航与社交

### A1. `menu` —— 顶部导航菜单 ⭐

```yaml
menu:
  首页: / || icon-home || faa-tada
  文章 || icon--article || faa-tada || hide:
    归档: /archives/ || icon-guidang1 || faa-tada
    文章统计: /tags/ || icon-shujutongji1 || faa-tada
    随便逛逛: javascript:randomPost(); || icon-zuji1 || faa-tada
  八宝箱 || icon-xiangzi || faa-tada || hide:
    八音盒: /life/music/ || icon-yinle || faa-tada
    画廊: /box/gallery/ || icon-tubiaozhizuomoban || faa-tada
    天文馆: /box/astronomy/ || icon-wangyuanjing || faa-tada
    网址导航: /box/nav/ || icon-zhifengche || faa-tada
  社交 || icon-shejiaoxinxi || faa-tada || hide:
    朋友圈: /social/fcircle/ || icon-pengyouquan || faa-tada
    留言板: /comments/ || icon-liuyan || faa-tada
    友人帐: /social/link/ || icon-lianjie || faa-tada
  网站 || icon-wangye || faa-tada || hide:
    网站统计: /site/census/ || icon--tongjibiao || faa-tada
    旧时光: /site/time/ || icon-xianxingshalou || faa-tada
    关于: /personal/about/ || icon-paperplane || faa-tada
```

**作用**：顶部那条导航栏的所有菜单项（含下拉子菜单）。

**每行的格式**：`显示名: 链接 || 图标类名 || 动画类名`

| 位置 | 含义 | 例子 |
| --- | --- | --- |
| 第 1 段（冒号前） | 菜单上显示的文字 | `首页` |
| 第 2 段 | 点击跳转的地址 | `/archives/`、`https://xxx.com`、`javascript:randomPost();` |
| 第 3 段 | 图标类名（iconfont） | `icon-home`、`icon-yinle` |
| 第 4 段 | 悬停动画类名 | `faa-tada` |

**带下拉子菜单的写法**：主项后面加 `|| hide:`，下一层**缩进两格**写子项（看「文章」「八宝箱」就是这样）。

**怎么改**：
| 想做的事 | 做法 |
| --- | --- |
| 加一个菜单项 | 照抄一行，改名字和链接，例：`标签: /tags/ \|\| icon-biaoqian \|\| faa-tada` |
| 删一个菜单项 | 把那一行（含子项）删掉，或前面加 `#` 注释 |
| 调整顺序 | 直接上下移动行 |
| 加外链 | `百度: https://www.baidu.com \|\| icon-wangye \|\| faa-tada` |
| 随机文章 | 保持 `javascript:randomPost();`（主题内置函数） |

> 💡 图标名从哪来？站点用 iconfont 字体图标。想换图标就去 iconfont.cn 找名字（如 `icon-rili`），或直接复用文件里已出现过的。

### A2. `social` —— 侧栏社交图标 ⭐

```yaml
social:
  # 格式： 名称: 链接 || 图标类名 || 动画类名
  Github: https://github.com/dsylxt || icon-github || faa-tada
  # B站: https://space.bilibili.com/12345678 || icon-bilibili || faa-tada
  # 邮箱: mailto:you@example.com || icon-youxiang || faa-tada
  # 微信: /assets/wechat-qr.webp || icon-weixin || faa-tada
  # RSS: /atom.xml || icon-RSS || faa-tada
```

**作用**：侧栏（作者卡下方）那排社交图标。

**当前只开了 GitHub**。想加别的，把对应行的 `#` 去掉并改成你的地址：
```yaml
social:
  Github: https://github.com/dsylxt || icon-github || faa-tada
  B站: https://space.bilibili.com/你的UID || icon-bilibili || faa-tada
  邮箱: mailto:你的邮箱@qq.com || icon-youxiang || faa-tada
  RSS: /atom.xml || icon-RSS || faa-tada
```

> ⚠️ `mailto:` 后面**直接跟邮箱**，不要加 `//`。
> 💡 文件里还给了「用 iconfont 图标」的另一种写法（`iconfont icon-github: 链接 || 名称`），效果一样，任选。

---

## B. 代码块与复制

```yaml
highlight_theme: mac        # 代码块配色
highlight_copy: true        # 代码块右上角「复制」按钮
highlight_lang: true        # 代码块左上角显示语言名
highlight_shrink: false     # 代码块是否默认折叠
highlight_height_limit: 230 # 超过这个高度就折叠（px）
code_word_wrap: false       # 代码是否自动换行

copy:
  enable: true              # 全站复制时自动加版权信息
  copyright:
    enable: false
    limit_count: 50
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `highlight_theme` | `mac` | **代码块配色方案** | 可选：`darker / pale night / light / ocean / mac / mac light / false` |
| `highlight_copy` | `true` | 显示「复制」按钮 | 关掉改 `false` |
| `highlight_lang` | `true` | 显示代码语言名 | 关掉改 `false` |
| `highlight_shrink` | `false` | 代码块是否折叠 | `true` 折叠 / `false` 展开 / `none` 展开且隐藏按钮 |
| `highlight_height_limit` | `230` | 超过多少 px 折叠 | 数字越大越少折叠 |
| `code_word_wrap` | `false` | 代码是否自动换行 | 长代码想换行改 `true` |
| `copy.enable` | `true` | 复制正文时自动追加来源信息 | 不想要改 `false` |
| `copy.copyright.limit_count` | `50` | 复制超过多少字才加版权 | 按需改 |

---

## C. 搜索与数学公式

### C1. 搜索（二选一）

```yaml
# Algolia 搜索（云端全文搜索）
algolia_search:
  enable: true
  hits:
    per_page: 5
  labels:
    input_placeholder: Search for Posts
    hits_empty: "我们没有找到任何搜索结果: ${query}"
    hits_stats: "找到${hits}条结果（用时${time} ms）"

# 本地搜索
local_search:
  enable: false
  preload: true
  CDN:
```

| 字段 | 当前值 | 作用 |
| --- | --- | --- |
| `algolia_search.enable` | `true` | 用 Algolia 云端搜索 |
| `algolia_search.hits.per_page` | `5` | 每页显示几条结果 |
| `local_search.enable` | `false` | 用本地搜索（无需外部服务） |

> ⚠️ **当前搜索不可用**：这里开了 Algolia，但 `_config.yml` 里 Algolia 的 4 个键还是 `YOUR_...` 占位符。
> 二选一：① 去 algolia.com 建索引、填键；② 把这里 `algolia_search.enable` 改 `false`、`local_search.enable` 改 `true`。

### C2. `mathjax` —— 数学公式

```yaml
mathjax:
  enable: true
  per_page: false
```

| 字段 | 当前值 | 作用 |
| --- | --- | --- |
| `enable` | `true` | 启用 MathJax 公式 |
| `per_page` | `false` | `false` = 只有文章写了 `mathjax: true` 才加载；`true` = 每页都加载 |

> 公式的 CDN 地址在文件末尾 `CDN.option.mathjax`（已改成国内镜像）。
> 文件里 `katex` 段是注释掉的备选方案，与 MathJax 二选一。

---

## D. 图片：图标 / 头像 / 顶部图 / 封面 / 404

```yaml
favicon:                          # 浏览器标签页小图标（留空用默认）

avatar:
  img: /assets/touxiang.jpg       # 侧栏头像
  effect: false                   # 头像是否转圈

disable_top_img: false            # true = 全站关掉顶部大图
index_img:                        # 首页顶部大图（留空 = 不显示）
default_top_img:                  # 其它页顶部大图
archive_img:                      # 归档页顶部图
tag_img: false                    # 子标签页顶部图
tag_per_img:                      # 按标签分别设顶部图
category_img:                     # 子分类页顶部图
category_per_img:                 # 按分类分别设顶部图

cover:
  index_enable: true              # 首页文章卡片显示封面
  aside_enable: true              # 侧栏推荐显示封面
  archives_enable: true           # 归档页显示封面
  position: both                  # 封面位置 left/right/both
  default_cover:                  # 文章没设封面时的默认封面池
    - https://picsum.photos/id/1036/1200/675
    - ...（一长串，随机分配给没封面的文章）
```

| 字段 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `favicon` | 空 | 标签页小图标 | 想换：填 `/assets/你的图标.png` |
| `avatar.img` | `/assets/touxiang.jpg` | **侧栏头像** | ⭐ 换头像：图片放 `source/assets/`，改这里 |
| `avatar.effect` | `false` | 头像是否旋转 | 想要转圈改 `true` |
| `disable_top_img` | `false` | 关掉所有顶部大图 | 想全关改 `true` |
| `index_img` | 空 | 首页顶部大图 | 填图片地址就显示 |
| `default_top_img` | 空 | 其它页顶部大图 | 同上 |
| `cover.position` | `both` | 首页卡片封面在左/右/两侧 | `left` / `right` / `both` |
| `cover.default_cover` | 一长串 picsum 图 | **没设封面的文章随机用这里的图** | 换成你自己的图（本地写 `/assets/xxx.jpg`） |

**换头像步骤**：把图片放进 `source/assets/`，改 `avatar.img`，例：`avatar.img: /assets/my-avatar.jpg`。
**文章单独设封面**：文章 front-matter 里写 `cover: /assets/xxx.jpg`。
**封面池太长**：`default_cover` 里重复很多，保留几张即可（随机分配）。

```yaml
error_404:
  enable: true
  subtitle: "此页面不存在哦٩͡[๏̯͡๏]"
  background: /assets/404_1.jpg
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `enable` | 404 页开关 | 不动 |
| `subtitle` | 404 页文案 | 随意改 |
| `background` | 404 页背景图（文件在 `source/assets/404_1.jpg`） | 换成你的图 |

---

## E. 文章页

### E1. `post_meta` —— 文章元信息显示

```yaml
post_meta:
  page:                       # 首页卡片
    date_type: both           # created/updated/both
    date_format: relative     # date（日期）/ relative（相对，如「3天前」）
    categories: true
    tags: true
    label: true
  post:                       # 文章页
    date_type: both
    date_format: relative
    categories: true
    tags: true
    label: true
```

| 字段 | 作用 |
| --- | --- |
| `date_type` | 显示创建日 / 更新日 / 都显示 |
| `date_format` | 显示绝对日期还是「相对日期」 |
| `categories` / `tags` | 是否显示分类 / 标签 |
| `label` | 是否显示「发表于 / 更新于」这类文字 |

### E2. 其它文章相关开关

| 配置块 | 当前值 | 作用 | 怎么改 |
| --- | --- | --- | --- |
| `wordcount.enable` | `true` | **字数统计**（约 N 字 / 阅读 N 分钟） | 关掉改 `false` |
| `index_post_content.method` | `2` | 首页摘要方式：`1`=description / `2`=智能（有 description 用它，否则自动摘要）/ `3`=自动摘要 / `false`=不显示 | 按需 |
| `index_post_content.length` | `500` | 自动摘要的字数 | 改数字 |
| `anchor` | `false` | 滚动时 URL 是否跟着标题变 | 一般不动 |
| `toc.post` | `true` | **文章页显示目录** | 不要目录改 `false` |
| `toc.number` | `false` | 目录是否显示序号 | 想要序号改 `true` |
| `toc.expand` | `false` | 目录是否默认展开 | 想默认展开改 `true` |
| `post_copyright.enable` | `true` | 文章底部版权声明 | 关掉改 `false` |
| `post_copyright.license` | `CC BY-NC-SA 4.0` | 版权协议 | 换协议改这里 |
| `reward.enable` | `false` | 文章底部「投喂作者」按钮（关闭中） | 想开改 `true` 并填收款码 |
| `post_edit.enable` | `false` | 「在线编辑本文」按钮 | 想开改 `true` 并填 `url` |
| `related_post.enable` | `true` | 文章底部**相关文章推荐** | 关掉改 `false` |
| `related_post.limit` | `6` | 推荐几篇 | 改数字 |
| `post_pagination` | `1` | 上一篇/下一篇链接方向：`1`=下一篇指旧文 / `2`=指新文 / `false`=关 | 按需 |
| `noticeOutdate.enable` | `false` | 文章过期提醒（超过 N 天提示） | 想开改 `true`，`limit_day` 设天数 |

---

## F. 分享功能

```yaml
addThis:  { enable: false }
sharejs:  { enable: false, sites: facebook,twitter,wechat,weibo,qq }
addtoany: { enable: false }
```

**作用**：文章底部的「分享到…」按钮，三种方案**任选一个**开启（把 `enable` 改 `true`）。

| 方案 | 特点 |
| --- | --- |
| `addThis` | 需注册 addthis.com |
| `sharejs` | 国内常用，支持微信/微博/QQ |
| `addtoany` | 需注册 addtoany.com |

---

## G. 评论区

```yaml
comments:
  use:
    - Twikoo          # 当前用 Twikoo
  text: true
  lazyload: true
  count: false
  card_post_count: false

twikoo:
  envId: https://comment.example.com
  region:
  visitor: false
  option:
```

**作用**：文章底部的评论系统。`use` 里填系统名，再配对应的配置段。

**支持的评论系统**（`use` 里填哪个，就填哪个的配置段）：

| 系统 | 配置段 | 说明 |
| --- | --- | --- |
| `Twikoo` | `twikoo.envId` | **当前在用**，需自建后端 |
| `Waline` | `waline.serverURL` | 支持登录，需自建后端 |
| `Valine` | `valine.appId` / `appKey` | 基于 LeanCloud，免后端 |
| `Giscus` | `giscus.repo` / `repo_id` / `category_id` | 基于 GitHub Discussions，免费 |
| `Utterances` | `utterances.repo` | 基于 GitHub Issues |
| `Disqus` / `Disqusjs` | `disqus.shortname` | 国外 |
| `Gitalk` | `gitalk.client_id` 等 | 基于 GitHub Issues |
| `Livere` | `livere.uid` | 来必力 |
| `Remark42` | `remark42.host` / `siteId` | 自建 |
| `Facebook Comments` | `facebook_comments.app_id` | 国外 |

| 字段 | 作用 |
| --- | --- |
| `text` | 评论按钮旁是否显示文字 |
| `lazyload` | 滚动到评论区才加载（省流量，但评论数会失效） |
| `count` | 文章顶部图显示评论数 |

> ⚠️ **当前评论打不开**：`twikoo.envId` 还是 `https://comment.example.com` 占位符，要换成你自己部署的 Twikoo 地址。
> **换评论系统**：改 `comments.use` 的名字，填对应配置段即可。**关评论**：`use` 清空，或单篇文章 front-matter 写 `comments: false`。

### G2. 聊天服务（Chat）

```yaml
chat_btn: false
chat_hide_show: true
chatra:    { enable: false }
tidio:     { enable: false }
daovoice:  { enable: false }
gitter:    { enable: false }
crisp:     { enable: false }
```

**作用**：右下角的在线客服/聊天窗口。默认全关，用不到就别管。

---

## H. 页脚 / 统计 / 广告 / 站长验证

### H1. `footer` —— 页脚

```yaml
footer:
  owner:
    enable: true
    since: 2022          # 起始年份 → 页脚显示 © 2022 - 2026
  custom_text:           # 自定义页脚文字（支持 HTML）
  copyright: false       # 是否显示主题版权
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `owner.enable` | 显示版权信息 | 不动 |
| `owner.since` | 起始年份 | ⭐ 改成你建站那年 |
| `custom_text` | 自定义页脚文字 | 想加就写 |
| `copyright` | 显示「由 Hexo + Fomalhaut 驱动」 | 想显示改 `true` |

### H2. 网站统计（Analytics）

```yaml
baidu_analytics:        # 百度统计 ID
google_analytics:       # 谷歌统计 ID
cnzz_analytics:         # CNZZ（友盟）ID
cloudflare_analytics:   # Cloudflare 统计 token
microsoft_clarity:      # 微软 Clarity ID
```

**作用**：把对应平台的统计 ID 填进去即可启用。**当前都留空 = 都没开**。
> 注：本站另有 51LA 统计，在 `inject.bottom` 里引入（`/js/51la.js`）。

### H3. 广告 / 站长验证

```yaml
google_adsense:
  enable: false
  auto_ads: true
  js: https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js
  client:
  enable_page_level_ads: true

site_verification:
  # - name: google-site-verification
  #   content: xxxxxx
  # - name: baidu-site-verification
  #   content: xxxxxxx
```

| 配置块 | 作用 |
| --- | --- |
| `google_adsense` | 谷歌广告（关闭中） |
| `site_verification` | 站长验证（如百度/谷歌收录验证），按格式加 `name` + `content` |

---

## I. 外观

### I1. `theme_color` —— 全站主题色 ⭐

```yaml
theme_color:
  enable: true
  main:                       # 主色（留空 = 主题默认青绿）
  paginator:                  # 分页按钮色
  button_hover:               # 按钮悬停色
  text_selection:             # 文字选中色
  link_color: "#a591e0"       # 链接颜色（当前淡紫）
  meta_color: "#858585"       # 元信息灰色
  hr_color: "#A4D8FA"         # 分割线色
  code_foreground:            # 代码前景色
  code_background:            # 代码背景色
  toc_color:                  # 目录高亮色
  blockquote_padding_color:   # 引用块左边框色
  blockquote_background_color:# 引用块背景色
  scrollbar_color:            # 滚动条色
  meta_theme_color_light: "ffffff"
  meta_theme_color_dark: "#0d0d0d"
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `main` | **全站主色** | 填十六进制，如 `"#49b1f5"`（蓝） |
| `link_color` | 链接颜色 | 当前 `#a591e0`（淡紫） |
| `meta_color` | 日期/分类等灰色文字 | 当前 `#858585` |
| `hr_color` | 分割线颜色 | 当前 `#A4D8FA` |

> ⚠️ 颜色值**必须带引号**（`"#49b1f5"`），否则 YAML 解析报错。
> 留空的项 = 沿用主题默认。访客也能在**右下角齿轮面板**自己选主题色（存本地，不影响别人）。

### I2. 首页 / 分类页 UI

```yaml
index_site_info_top:      # 主页标题距顶部距离（如 300px / 10%）
index_top_img_height:     # 主页顶部图高度（如 300px）
category_ui:              # 分类页 UI：留空=跟归档页；index=跟首页
tag_ui:                   # 标签页 UI：同上
```

| 字段 | 作用 |
| --- | --- |
| `index_site_info_top` | 主页标题离顶部多远 |
| `index_top_img_height` | 主页顶部图多高 |
| `category_ui` / `tag_ui` | 分类/标签页是否用首页同款卡片布局（填 `index`） |

### I3. `background` —— 网站背景 ⭐⭐

```yaml
background:
  default: var(--default-bg)          # PC 日间
  darkmode: var(--darkmode-bg)        # PC 夜间
  mobileday: var(--mobileday-bg)      # 手机日间
  mobilenight: var(--mobilenight-bg)  # 手机夜间

footer_bg: false                      # 页脚是否也铺背景图
rightside-bottom:                     # 右下角按钮距底部距离
enter_transitions: true               # 网页进入过渡动画
```

**这里引用的 `var(--default-bg)` 是 CSS 变量，真正的图片地址不在这段**，而在下面 `inject.head` 的 `#defineBg` 那一行：

```yaml
- <style id="defineBg">:root{--default-bg:url(...);--darkmode-bg:url(...);--mobileday-bg:url(...);--mobilenight-bg:url(...);}</style>
```

**换背景三种办法（推荐度从高到低）**：

| 方法 | 怎么做 | 谁看得到 |
| --- | --- | --- |
| **A. 齿轮面板** | 点右下角齿轮 →「六、背景设置」→ 选壁纸/色彩/自定义链接/动态 API | 只有你自己（存浏览器） |
| **B. 改 `#defineBg`** | 改 `inject.head` 里那 4 个 `url(...)` | 所有人 |
| **C. 纯色/渐变** | 把 `background.default` 直接写成 `"#e4f4f6"` 或 `linear-gradient(...)` | 所有人 |

> ⚠️ 改 `#defineBg` 时，**夜间那张地址必须和 `source/js/modules/settings.js` 的 `resetBg_()` 逐字一致**，否则同一张图会下载两份。

### I4. 背景特效（`canvas_*` / 点击效果）

```yaml
canvas_ribbon:            { enable: false }   # 静止彩带
canvas_fluttering_ribbon: { enable: false }   # 动态彩带
canvas_nest:              { enable: false }   # 线条背景
activate_power_mode:      { enable: false }   # 打字粒子特效
fireworks:                { enable: false }   # 点击烟花
click_heart:              { enable: false }   # 点击爱心
ClickShowText:            { enable: false }   # 点击出文字
```

| 配置块 | 效果 |
| --- | --- |
| `canvas_ribbon` | 背景上的静止彩带 |
| `canvas_fluttering_ribbon` | 动态飘动的彩带 |
| `canvas_nest` | 鼠标连线粒子背景 |
| `activate_power_mode` | 打字时冒粒子 + 抖动 |
| `fireworks` | 点击处放烟花 |
| `click_heart` | 点击处冒爱心 |
| `ClickShowText` | 点击处冒文字（`text` 里配置） |

> 全部默认关闭。想开把对应 `enable` 改 `true` 即可（大多有 `mobile` 选项控制手机端）。
> 💡 本站还有**雪花、星空、萤火虫、点击涟漪**等，主要由 `source/js/modules/` 脚本 + 齿轮面板控制，别和这里搞混。

### I5. `display_mode` / `beautify` / `font` / `hr_icon` / `subtitle`

```yaml
display_mode: light          # 默认显示模式 light/dark

beautify:
  enable: true               # 标题前加小图标
  title-prefix-icon: '\f863'
  title-prefix-icon-color: "#F47466"

font:
  global-font-size: 15.5px   # 正文字号
  code-font-size: 14.7px     # 代码字号
  font-family: var(--global-font), ...       # 正文字体
  code-font-family: var(--code-font, JetBrainsMono), ...  # 代码字体

blog_title_font:
  font-family: var(--global-font), ...       # 站名字体

hr_icon:
  enable: true
  icon: '\f2dc'              # 水平分割线图标
  icon-top: -10px

subtitle:
  enable: true               # 首页打字机副标题
  effect: true               # 打字效果
  loop: true                 # 循环
  source: false              # 一言服务（1=一言 2=一句 3=今日诗词）
  sub:
    - "Welcome to DemoのTiny Home!🤣🤣🤣"
    - "Hope you have a nice day!🍭🍭🍭"
    - "我迎着风,淋着雨,追寻漫天星光"
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `display_mode` | 默认日间/夜间 | `light` / `dark` |
| `beautify.enable` | 标题前的小图标 | 不要改 `false` |
| `font.global-font-size` | 正文字号 | ⭐ 觉得字小改大，如 `16px` |
| `font.code-font-size` | 代码字号 | 按需 |
| `subtitle.sub` | **首页打字机轮播的几句话** | ⭐ 换成你喜欢的句子 |
| `subtitle.source` | 用「一言」等接口自动取句 | 想用改 `1`/`2`/`3` |
| `hr_icon` | 分割线图标 | 不动 |

> 💡 字体、副标题也能在**齿轮面板**里改（访客可自选）。想改**默认值**（所有人看到）才动这里。

### I6. `preloader` —— 首屏加载动画

```yaml
preloader:
  enable: true
  load_color:          # 动画颜色
  load_style: heo      # 动画样式
  load_image:          # 自定义图片（load_style: image 时用）
```

| 字段 | 作用 | 可选值 |
| --- | --- | --- |
| `enable` | 加载动画开关 | `true` / `false` |
| `load_style` | 动画样式 | `default / gear / ironheart / scarecrow / triangles / wizard / image / spincat / heo` |

> 样式文件在 `themes/fomalhaut/layout/includes/loading/load_style/`。不想要就 `enable: false`。

---

## J. 侧栏

### J1. `aside` —— 侧栏 ⭐

```yaml
aside:
  enable: true
  hide: false              # true = 默认收起
  button: true             # 显示展开/收起按钮
  mobile: true             # 手机上也显示
  position: right          # 侧栏在左(left)还是右(right)
  display:
    archive: false         # 归档页不显示侧栏
    tag: true
    category: true
  card_author:
    enable: true
    description:
    button:
      enable: true
      icon:
      text: Github主页
      link: https://github.com/yourname      # ← 改成你的
  card_announcement:
    enable: true
    content: |             # 公告卡（HTML），当前是模板介绍
      <div class="anno2">...</div>
  card_recent_post:   { enable: false, limit: 5 }
  card_categories:    { enable: false, limit: 8 }
  card_tags:          { enable: false, limit: 20 }
  card_archives:      { enable: false, type: monthly }
  card_webinfo:       { enable: true }        # 小站资讯卡（文章数/运行天数）
  card_weibo:         { enable: false }
  card_friend_link:   { enable: false }       # 友链通讯录卡
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `position` | 侧栏左右 | ⭐ `left` / `right` |
| `hide` | 默认是否收起 | ⭐ 想默认收起改 `true` |
| `mobile` | 手机端是否显示 | 按需 |
| `display.archive/tag/category` | 各页面是否显示侧栏 | 按需 |
| `card_author.button.link` | 作者卡按钮链接 | ⭐ 改成你的 GitHub |
| `card_author.button.text` | 按钮文字 | 按需 |
| `card_announcement.content` | **公告卡内容**（HTML） | ⭐ 改成你自己的公告 |
| `card_recent_post` | 最近文章卡 | 想开改 `enable: true` |
| `card_categories` | 分类卡 | 同上 |
| `card_tags` | 标签云卡 | 同上 |
| `card_archives` | 归档卡 | 同上 |
| `card_webinfo` | 小站资讯卡 | 已开 |
| `card_friend_link` | 友链通讯录卡 | 已关 |

> 💡 侧栏还有两张自定义卡（**日历 / 倒计时**），数据在 `source/_data/widget.yml`，不在这个文件。

### J2. 访问量 / 运行时间 / 最新评论

```yaml
busuanzi:
  site_uv: true      # 站点访客数
  site_pv: true      # 站点访问量
  page_pv: true      # 单页访问量

runtimeshow:
  enable: false      # 网页运行时间（从 publish_date 算起）
  publish_date: 8/9/2022 00:00:00

newest_comments:
  enable: false      # 侧栏最新评论
  limit: 5
```

| 配置块 | 作用 | 怎么改 |
| --- | --- | --- |
| `busuanzi` | 不蒜子访问统计（PV/UV） | 不想要某项改 `false` |
| `runtimeshow` | 「本站已运行 N 天」 | 想开改 `true`，`publish_date` 设建站日期 |
| `newest_comments` | 侧栏最新评论 | 按需 |

---

## K. 右下角按钮与显示模式

```yaml
translate:
  enable: false          # 简繁转换按钮
  default: 繁

readmode: 2              # 阅读模式

darkmode:
  enable: true
  button: true           # 显示日夜切换按钮
  autoChangeMode: false  # false=不自动 / 1=跟随系统 / 2=晚6点到早6点
  am: 7
  pm: 7

rightside_item_order:
  enable: false
  hide:
  show:
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `translate.enable` | 简繁切换按钮 | 想开改 `true` |
| `readmode` | 阅读模式（沉浸阅读） | 数字控制，不动 |
| `darkmode.button` | 显示日夜切换按钮 | 不要按钮改 `false` |
| `darkmode.autoChangeMode` | 自动切夜间 | `false`/`1`（跟系统）/`2`（按时间） |
| `rightside_item_order` | 自定义右下角按钮顺序 | 高级用法，一般不动 |

---

## L. 图片查看与标签外挂

```yaml
medium_zoom: false      # 图片放大方案 A
fancybox: true          # 图片放大方案 B（当前用这个）

mermaid:
  enable: false         # Mermaid 图表

note:
  style: flat           # 提示块样式 simple/modern/flat/disabled
  icons: true
  border_radius: 3
  light_bg_offset: 0
```

| 配置块 | 作用 | 说明 |
| --- | --- | --- |
| `medium_zoom` / `fancybox` | 点击图片放大的方案 | **只能选一个**，当前用 `fancybox` |
| `mermaid` | 支持 `{% mermaid %}` 画流程图 | 想用改 `enable: true` |
| `note.style` | `{% note %}` 提示块的样式 | `flat`（当前）/ `simple` / `modern` / `disabled` |

---

## M. 性能与其它开关

```yaml
pjax:
  enable: true           # 站内跳转不整页刷新（快）
  exclude:

aplayerInject:
  enable: true           # 注入 aplayer/meting（音乐）
  per_page: false

snackbar:
  enable: false          # 右下角弹窗提示
  position: top-right

instantpage: true        # 鼠标悬停链接时预加载
pangu:
  enable: false          # 中英文之间自动加空格
  field: post
lazyload:
  enable: true           # 图片懒加载
  field: site
  blur: true

pwa:
  enable: false          # 渐进式网页应用（可安装到桌面）
Open_Graph_meta: true    # 分享卡片 meta
css_prefix: true         # CSS 兼容前缀
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `pjax.enable` | 站内跳转不整页刷新 | ⭐ 想更快保持 `true`；有兼容问题改 `false` |
| `instantpage` | 悬停预加载 | 保持 `true` |
| `pangu.enable` | 中英文间自动空格 | 想开改 `true` |
| `lazyload.enable` | 图片懒加载 | 保持 `true` |
| `pwa.enable` | 可安装为 App | 按需 |
| `Open_Graph_meta` | 分享到微信/QQ 显示卡片 | 保持 `true` |

---

## N. inject —— 代码注入（本站魔改核心）⭐⭐

```yaml
inject:
  head:
    - <link rel="preconnect" href="https://registry.npmmirror.com">
    - <link rel="stylesheet" href="/css/stats.css?v=20261005">
    - <link rel="stylesheet" href="/css/twikoo.css?v=20261006b">
    - <style id="themeColor"></style>
    - <style id="defineBg">:root{--default-bg:url(...);...}</style>
    - <link rel="stylesheet" href="/css/site-inject.css?v=20261015-fps4">
    - <link rel="stylesheet" href="/css/archive-page.css?v=20261013b">
    - <script defer src="/js/inject/archive-page.js?v=20261013b"></script>
    ...（几十行）
  bottom:
    - <script src="https://registry.npmmirror.com/jquery/3.6.0/files/dist/jquery.min.js"></script>
    - <script defer src="/js/modules/settings.js?v=20261015-custom1"></script>
    - <script defer src="/js/fomal.js"></script>
    ...（几十行）
```

**作用**：这是你**整个站点所有自定义功能**的总入口。`head` 里的代码插到 `</head>` 前，`bottom` 里的插到 `</body>` 前。

**能干什么**：
| 想做的事 | 做法 |
| --- | --- |
| 全站加一段 CSS | css 放 `source/css/`，这里加 `<link rel="stylesheet" href="/css/你的文件.css?v=1">` |
| 全站加一段 JS | js 放 `source/js/`，这里加 `<script defer src="/js/你的文件.js?v=1"></script>` |
| 插第三方统计/脚本 | 直接把 `<script src="...">` 加进来 |
| 改网站背景 | 改 `#defineBg` 那行的 4 个 `url(...)` |

**⚠️ 两个必须知道的坑**：

1. **`?v=` 版本号**：很多行末尾有 `?v=20261015` 这种串，是**缓存版本号**。你改了对应的 css/js 后，**必须把它也改成新值**（随便换个日期），否则浏览器和访客会一直吃旧缓存、看不到修改。
2. **空的 `<style id="xxx"></style>` 不能删**：`#themeColor`、`#rightSide`、`#transPercent`、`#bgFilterParam`、`#defineBg`、`#menu_shadow`、`#nav-display`、`#aside-show`、`#aside-pos` 这些是**运行时空槽**，右下角美化面板的 JS 会往里面写 CSS。删了面板就失效。

**`head` 里主要引了什么**（节选）：
| 类型 | 例子 | 作用 |
| --- | --- | --- |
| 预连接 | `<link rel="preconnect" href="...">` | 提前建连，提速 |
| 站点样式 | `site-inject.css`、`navigation.css`、`mobile-drawer.css`… | 你的各种魔改样式 |
| 页面专属 | `about-page.css`、`archive-page.css`、`timeline-archive.css` | 特定页面改版 |
| 运行时空槽 | `<style id="themeColor">` 等 | 美化面板写入 |
| 站点脚本 | `typewriter.js`、`archive-page.js`… | 你的各种魔改脚本 |

**`bottom` 里主要引了什么**（节选）：
| 类型 | 例子 | 作用 |
| --- | --- | --- |
| 统计 | `51la.js`、`sdk.51.la` | 访问统计 |
| 库 | `jquery`、`clipboard`、`winbox` | 依赖库 |
| 图标字体 | `at.alicdn.com/...` | iconfont |
| 画布 | `<canvas id="universe">`、`<canvas id="snow">` | 星空/雪花 |
| 站点 JS | `/js/modules/*.js`、`/js/fomal.js` | 你的核心脚本（`fomal.js` 是主引导） |

> 💡 想彻底搞懂这些脚本，先看 `source/js/fomal.js` 顶部的「模块地图 + 全局入口清单」。

---

## O. CDN

```yaml
CDN:
  internal_provider: local      # 主题内部 js 用本地
  third_party_provider: cdnjs   # 第三方库用 CDN
  version: false
  option:
    main: /js/main.js?v=20261005-scroll1
    utils: /js/utils.js?v=20261005-scroll1
    algolia_search_v4: https://registry.npmmirror.com/...
    pjax: https://lib.baomitu.com/pjax/0.2.8/pjax.min.js
    twikoo: https://registry.npmmirror.com/twikoo/2.0.12/files/dist/twikoo.all.min.js
    mathjax: https://registry.npmmirror.com/mathjax/3.2.2/files/es5/tex-mml-chtml.js
    lazyload: https://registry.npmmirror.com/vanilla-lazyload/17.3.1/files/dist/lazyload.iife.min.js
    fancybox_v4: https://registry.npmmirror.com/@fancyapps/ui/4.0.31/files/dist/fancybox.umd.js
    fontawesomeV6: https://registry.npmmirror.com/@fortawesome/fontawesome-free/6.0.0/files/css/all.min.css
    aplayer_css / aplayer_js / meting_js: ...
```

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `internal_provider` | 主题自己的 js 从哪加载 | `local`（当前，用本地） |
| `third_party_provider` | 第三方库从哪加载 | `local / jsdelivr / unpkg / cdnjs / custom` |
| `option.xxx` | **每个第三方库的具体地址** | 某个库挂了/想换镜像时改这一行 |

> 一般**不用动**。只有当某个 CDN 地址失效（国内被墙）时，才改对应那行的地址。文件里已经改过几处（如 `mathjax` 换成了 npmmirror 镜像）。

---

## P. 其它插件与页面

### P1. `wowjs` —— 滚动入场动画

```yaml
wowjs:
  enable: true
  mobile: false
  animateitem:
    - class: recent-post-item     # 首页文章卡片
      style: animate__zoomIn
      duration: 2s
      delay: 200ms
      offset: 30
    - class: card-widget          # 侧栏卡片
      style: animate__zoomIn
      ...
```

| 字段 | 作用 |
| --- | --- |
| `enable` | 开关 |
| `mobile` | 手机端是否启用 |
| `animateitem[].class` | 给哪个元素加动画 |
| `animateitem[].style` | 动画名（`animate__zoomIn` 等） |

> 注释里给了更多可加的 class（置顶栏、分类磁贴、分页按钮、友链卡片…），去掉注释即可启用。

### P2. `envelope_comment` —— 留言板信封

```yaml
envelope_comment:
  enable: true
  custom_pic:
    cover: .../violet.jpg
    line: .../line.png
    beforeimg: .../before.png
    afterimg: .../after.png
  message:
    - 本站有哪些做得好或者不好的地方？
    - 或者你有什么改进的建议？
    - 又或者你有什么具体的问题需要咨询？
    - 都可以在下方评论区留言哦~~~
  bottom: 加班加点修复bug中
  height:
  path:
  front_matter:
    title: 留言板
    comments: true
```

**作用**：`/comments/` 留言板页的信封动画 + 信笺文案。

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `message` | 信笺正文（多行） | ⭐ 改成你想说的话 |
| `bottom` | 信笺底部一行文字 | 按需 |
| `custom_pic` | 信封的图片 | 可换成自己的图 |

### P3. 友链样式 / 错误图 / 标签外挂 / 首页卡片 / 灯笼

```yaml
flink_style: volantis      # 友链卡片样式 butterfly/volantis/flexcard

error_img:
  flink: /img/friend_404.gif   # 友链头像加载失败时的占位图
  post_page: /img/404.jpg      # 文章内图片失败时的占位图

tag_plugins:
  enable: true             # 标签外挂增强（anima 等）
  link:
    placeholder: "/assets/coffee.png"
  CDN: ...

index_card_style: multicard # 首页卡片样式 slidecard/multicard

lantern:
  enable: false            # 灯笼（建议只春节开）
```

| 配置块 | 作用 | 怎么改 |
| --- | --- | --- |
| `flink_style` | 友链卡片外观 | `volantis`（当前，站点卡片样式） |
| `error_img` | 图片加载失败的占位图 | 换成自己的图 |
| `tag_plugins` | 标签外挂（`{% anima %}` 等） | 保持开 |
| `index_card_style` | 首页卡片布局 | `multicard`（当前）/ `slidecard` |
| `lantern` | 春节灯笼 | 春节时改 `true` |

### P4. `ai_chat` —— 页面 AI 助手 ⭐

```yaml
ai_chat:
  enable: true
  api_base: https://api.deepseek.com
  api_key: ''                  # 不要直接写这里（会进 git）
  api_key_file: .ai-chat-key   # Key 放这个文件里（已在 .gitignore）
  model: deepseek-chat
  temperature: 0.7
  max_tokens: 8192
  max_history: 12
  max_page_chars: 32000
  storage_key: ai_chat_history_v1
  panel_width: 460
  panel_height: 640
  panel_right: 88
  timeout_ms: 10000
  welcome: 你好，我是这个页面的 AI 助手……
  first_question: 请用中文总结这个页面的内容：先用一句话概括，再列 3-5 条要点。
  system_prompt: |
    你是这个博客的页面助手，语气自然、简洁、像朋友聊天……
```

**作用**：右侧悬浮的 AI 对话面板，能总结当前页面、解释名词。

| 字段 | 作用 | 怎么改 |
| --- | --- | --- |
| `enable` | 总开关 | 关掉改 `false` |
| `api_base` | 服务商地址 | 换服务商改这里 |
| `api_key` / `api_key_file` | API Key | ⭐ 见下方 |
| `model` | 模型名 | ⭐ 换模型改这一行 |
| `welcome` | 打开面板时的欢迎语 | 随意改 |
| `system_prompt` | 系统提示词（AI 的角色设定） | 想调语气/行为改这里 |

**怎么让它能用**：
1. 在站点根目录建文件 `.ai-chat-key`，里面只写一行你的 DeepSeek API Key；
2. 或（公网部署推荐）在 Cloudflare/Vercel 加环境变量 `DEEPSEEK_API_KEY`，走同源代理，Key 不下发到浏览器。

> ⚠️ 直接把 Key 写进 `api_key` 会随页面发给所有人（F12 可见），**只在本地测试时这么干**。

---

## Q. 全站速查表

| 我想改…… | 去哪改 |
| --- | --- |
| **顶部导航菜单** | `menu` |
| **社交图标** | `social` |
| 代码块配色 | `highlight_theme` |
| **搜索方式** | `algolia_search` / `local_search`（+ `_config.yml` 的键） |
| **头像** | `avatar.img` |
| 首页/其它页顶部大图 | `index_img` / `default_top_img` |
| **文章默认封面池** | `cover.default_cover` |
| 404 页 | `error_404` |
| 首页摘要方式 | `index_post_content.method` |
| **文章目录** | `toc` |
| 相关文章推荐 | `related_post` |
| 文章版权协议 | `post_copyright.license` |
| **评论区** | `comments.use` + 对应系统段（如 `twikoo.envId`） |
| **页脚起始年份** | `footer.owner.since` |
| 网站统计 ID | `baidu_analytics` 等 |
| **主题色** | `theme_color.main` / `link_color` |
| **网站背景** | `inject.head` 的 `#defineBg`（或齿轮面板） |
| 背景特效（彩带/烟花…） | `canvas_ribbon` / `fireworks` 等 |
| **正文字号** | `font.global-font-size` |
| **首页打字机副标题** | `subtitle.sub` |
| 首屏加载动画 | `preloader` |
| **侧栏左右/显隐** | `aside.position` / `aside.hide` |
| **公告卡内容** | `aside.card_announcement.content` |
| 作者卡 GitHub 链接 | `aside.card_author.button.link` |
| 本站运行时间 | `runtimeshow` |
| 日夜切换 | `darkmode` |
| 图片放大方式 | `fancybox` / `medium_zoom` |
| 中英文自动空格 | `pangu.enable` |
| **全站自定义样式/脚本** | `inject`（head/bottom） |
| 某个库的 CDN 地址 | `CDN.option.xxx` |
| 滚动入场动画 | `wowjs` |
| 留言板信笺文案 | `envelope_comment.message` |
| 友链卡片样式 | `flink_style` |
| **AI 助手** | `ai_chat` |

---

*本文件基于 `D:\Blog\my-blog\_config.fomalhaut.yml` 当前内容编写。配套文档：《01 · 站点配置 `_config.yml` 详解》《03 · 命令手册》。*
