
---

title: Hexo 优化设置

date: 2019-06-14 16:28:48 +0800

tags: []

---
<a name="UywVi"></a>
### 修改博客标题简介语言等
编辑 _config.yml

```yaml
# Site
title: Xxb
subtitle: Linux,crypto,mining
description:
keywords: Linux,crypto,mining
author: xxb.me
language:
  - zh-CN
  - zh-TW
  - en
```
[]()
<a name="Jf2d6"></a>
### [](https://www.xxb.me/Hexo/yuque-hexo02/#%E4%BF%AE%E6%94%B9%E7%BD%91%E7%AB%99-URL-%E5%92%8C%E9%93%BE%E6%8E%A5%E6%A0%BC%E5%BC%8F)修改网站 URL 和链接格式
编辑 _config.yml

```yaml
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://www.xxb.me
root: /
permalink: :category/:title/
permalink_defaults:
```


<a name="RqKOi"></a>
### [](https://www.xxb.me/Hexo/yuque-hexo02/#%E5%88%9B%E5%BB%BA%E5%88%86%E7%B1%BB%E9%A1%B5)创建分类页
运行命令新建page页

```bash
hexo new page categories
```

运行后提示

```bash
INFO  Created: ~/Documents/code/blog/source/categories/index.md
```

找到 index.md 这个文件，为其添加 type 属性

```yaml
---
title: tags
date: 2019-01-30 17:37:12
type: "categories"
---
```

修改主题 _config.yml 文件的menu段落，反注释掉tags那一行

```yaml
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat

```

<a name="OZ2T0"></a>
### 创建标签页
方法和创建分类页一样，只是把 categories 改为 tags
<a name="vLnLU"></a>
### [](https://www.xxb.me/Hexo/yuque-hexo02/#%E5%88%9B%E5%BB%BAabout%E9%A1%B5)创建about页
参考创建标签页
<a name="X5U86"></a>
### [](https://www.xxb.me/Hexo/yuque-hexo02/#%E6%B7%BB%E5%8A%A0%E8%AF%97%E8%AF%8D%E6%8F%92%E4%BB%B6)添加诗词插件
今日诗词 API 根据不同地点、时间、节日、季节、天气、景观、城市、事件进行智能推荐，每次刷新都不同。<br />官网： [https://www.jinrishici.com/](https://www.jinrishici.com/)<br />调用文档： [https://www.jinrishici.com/doc/](https://www.jinrishici.com/doc/)<br />在想放置诗词的地方添加以下代码：（我放在_partials/header/brand.swig）

```html
<div id="jinrishici-sentence" class="shici"></div>
<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
```

自定义样式，修改主题样式文件source/css/_custom/custom.styl

```css
.shici {font-size: 15px;text-align: center;font-weight: 300;color: #444;font-style: italic;}
```

在线演示： [www.xxb.me](http://www.xxb.me/)
<a name="3oTZQ"></a>
### [](https://www.xxb.me/Hexo/yuque-hexo02/#%E6%9C%AA%E5%AE%8C%E5%BE%85%E7%BB%AD-%E2%80%A6)未完待续 …

