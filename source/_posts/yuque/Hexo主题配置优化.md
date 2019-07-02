
---

title: Hexo主题配置优化

date: 2019-06-20 14:26:03 +0800

tags: []

---

<a name="xOxY5"></a>
## 1.基本信息配置
> 基本信息包括：博客标题.作者.描述.语言等等。

打开 站点配置文件 ，找到Site模块
> title: 标题
> subtitle: 副标题
> description: 描述
> author: 作者
> language: 语言（简体中文是zh-Hans）
> timezone: 网站时区（Hexo 默认使用您电脑的时区，不用写）

关于 站点配置文件 中的其他配置可参考[站点配置](https://hexo.io/zh-cn/docs/configuration.html)
<a name="qT0tD"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#2-%E8%8F%9C%E5%8D%95%E8%AE%BE%E7%BD%AE)2.菜单设置
> 菜单包括：首页、归档、分类、标签、关于等等

我们刚开始默认的菜单只有首页和归档两个，不能够满足我们的要求，所以需要添加菜单，打开 主题配置文件 找到Menu Settings
> menu:
> home: / || home                          //首页
> archives: /archives/ || archive          //归档
> categories: /categories/ || th           //分类
> tags: /tags/ || tags                     //标签
> about: /about/ || user                   //关于
> #schedule: /schedule/ || calendar        //日程表
> #sitemap: /sitemap.xml || sitemap        //站点地图
> #commonweal: /404/ || heartbeat          //公益404

看看你需要哪个菜单就把哪个取消注释打开就行了；
关于后面的格式，以archives: /archives/ || archive为例：
|| 之前的/archives/表示标题“归档”，关于标题的格式可以去themes/next/languages/zh-Hans.yml中参考或修改
||之后的archive表示图标，可以去[Font Awesome](https://link.jianshu.com/?t=http%3A%2F%2Ffontawesome.io%2Ficons%2F)中查看或修改，Next主题所有的图标都来自Font Awesome。
<a name="OhsvD"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#3-Next%E4%B8%BB%E9%A2%98%E6%A0%B7%E5%BC%8F%E8%AE%BE%E7%BD%AE)3.Next主题样式设置
我们百里挑一选择了Next主题，不过Next主题还有4种风格供我们选择，打开 主题配置文件 找到Scheme Settings
> # Schemes
> # scheme: Muse
> # scheme: Mist
> # scheme: Pisces
> scheme: Gemini

4种风格大同小异，本人用的是[Gemini](https://link.jianshu.com/?t=https%3A%2F%2Fyoungerli.github.io)风格，你们可以选择自己喜欢的风格。
<a name="YdUaZ"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#4-%E4%BE%A7%E6%A0%8F%E8%AE%BE%E7%BD%AE)4.侧栏设置
> 侧栏设置包括：侧栏位置.侧栏显示与否.文章间距.返回顶部按钮等等

打开 主题配置文件 找到sidebar字段
> sidebar:
> # Sidebar Position - 侧栏位置（只对Pisces | Gemini两种风格有效）
>  position: left        //靠左放置
>  #position: right      //靠右放置
> # Sidebar Display - 侧栏显示时机（只对Muse | Mist两种风格有效）
>  #display: post        //默认行为，在文章页面（拥有目录列表）时显示
>  display: always       //在所有页面中都显示
>  #display: hide        //在所有页面中都隐藏（可以手动展开）
>  #display: remove      //完全移除
>  offset: 12            //文章间距（只对Pisces | Gemini两种风格有效）
>  b2t: false            //返回顶部按钮（只对Pisces | Gemini两种风格有效）
>  scrollpercent: true   //返回顶部按钮的百分比

<a name="8Z8Qi"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#5-%E5%A4%B4%E5%83%8F%E8%AE%BE%E7%BD%AE)5.头像设置
打开 主题配置文件 找到Sidebar Avatar字段
> # Sidebar Avatar
> avatar: /images/header.jpg

这是头像的路径，只需把你的头像命名为header.jpg（随便命名）放入themes/next/source/images中，将avatar的路径名改成你的头像名就OK啦！
<a name="ZbVL5"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#6-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F)6.评论系统
|  | 推荐指数 | 优点 | 缺点 |
| :--- | :--- | :--- | :--- |
| [Valine](https://valine.js.org/) | 4 | 每天30000条评论，10GB的储存 | 作者评论无标识 |
| [来必力/livere](https://livere.com/) | 4 | 多种账号登录 | 评论无法导出 |
| [畅言](http://changyan.kuaizhan.com/) | 3 | 美观 | 必须备案域名 |
| [gitment](https://github.com/imsun/gitment) | 3 | 简洁 | 只能登陆github评论 |
| Disqus | 1 |  | 需要翻*墙 |

<a name="nBL5l"></a>
##### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#%E6%9D%A5%E5%BF%85%E5%8A%9B)来必力
2.1. 登陆 [来必力](https://livere.com/) 获取你的 LiveRe UID。<br />2.2. 填写LiveRe UID到主题配置文件_config.yml

<a name="QX724"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#7-%E6%B7%BB%E5%8A%A0%E6%A0%87%E7%AD%BE%E9%A1%B5)7.添加标签页
> 添加一个标签页面，里面包含您网站中的所有标签。[参考链接](https://www.jianshu.com/p/e17711e44e00)

一个创建³³名为tags页面
> hexo new page "tags"

编辑标签页，设置页面类型为tags。
> title: All tags
> date: 2014-12-22 12:39:04
> type: "tags"

添加tags到主题配置文件_config.yml里：
> menu:
>  home: /
>  archives: /archives
>  tags: /tags

详细解释：

<a name="NglJO"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#8-%E6%B7%BB%E5%8A%A0%E5%88%86%E7%B1%BB%E9%A1%B5)8.添加分类页
> 添加一个分类页面，里面包含您网站中的所有分类。

一个创建³³名为categories页面
> hexo new page "categories"

编辑分类页，设置页面类型为categories。
> title: All categories
> date: 2014-12-22 12:39:04
> type: "categories"

添加 categories到主题配置文件_config.yml里：
> menu:
> home: /
> archives: /archives
> categories: /categories

详细解释：

参考截图:

<a name="wnwNU"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#9-%E6%B7%BB%E5%8A%A0%E8%90%8C%E8%90%8C%E5%93%92%E5%AE%A0%E7%89%A9)9.添加萌萌哒宠物
具体参考官方文档：[点击跳转](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md#c-npm-%E6%A8%A1%E5%9D%97%E5%90%8D)
<a name="JPfvA"></a>
#### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#1-%E5%AE%89%E8%A3%85%E6%A8%A1%E5%9D%97)1.安装模块:
> npm install --save hexo-helper-live2d

<a name="aPSGH"></a>
#### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#2-%E9%85%8D%E7%BD%AE)2.配置
请向Hexo的 _config.yml 文件或主题的 _config.yml 文件中添加配置.
示例:

```yaml
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-wanko
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: true
```

详解:

```yaml
live2d:
  enable: true
  # enable: false
  scriptFrom: local # 默认
  pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
  pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
  pluginModelPath: assets/ # 模型文件相对与插件根目录路径
  # scriptFrom: jsdelivr # jsdelivr CDN
  # scriptFrom: unpkg # unpkg CDN
  # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
  tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
  debug: false # 调试, 是否在控制台输出日志
  model:
    use: live2d-widget-model-wanko # npm-module package name
    # use: wanko # 博客根目录/live2d_models/ 下的目录名
    # use: ./wives/wanko # 相对于博客根目录的路径
    # use: https://cdn.jsdelivr.net/npm/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
```

<a name="Xjq73"></a>
#### 3.模型
有许多方法来使用不同的模型:
<a name="MDcoq"></a>
##### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#a-live2d-models%E5%AD%90%E7%9B%AE%E5%BD%95%E5%90%8D%E7%A7%B0)a. live2d_models子目录名称

1. 在您博客根目录下创建一个 live2d_models 文件夹.
1. 在此文件夹内新建名为 shizuku （模型名字）的子文件夹.
1. 在这里应当有一个 .model.json 文件 (例如 shizuku.model.json)
1. 将子文件夹的名称输入 _config.yml 的 model.use 中.

<a name="ERXvg"></a>
##### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#b-%E7%9B%B8%E5%AF%B9%E4%BA%8E%E5%8D%9A%E5%AE%A2%E6%A0%B9%E7%9B%AE%E5%BD%95%E7%9A%84%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E5%BE%84)b. 相对于博客根目录的自定义路径
您可直接输入相对于博客根目录的自定义路径到 model.use 中.
示例: ./wives/wanko
<a name="GFKsM"></a>
##### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#c-npm-%E6%A8%A1%E5%9D%97%E5%90%8D)c. npm 模块名（走这步就可以了）
现有模型：[https://github.com/xiazeyu/live2d-widget-models](https://github.com/xiazeyu/live2d-widget-models)
对应的模型图片：[https://huaji8.top/post/live2d-plugin-2.0/](https://huaji8.top/post/live2d-plugin-2.0/)
[模型地址](https://github.com/xiazeyu/live2d-widget-models)
npm install --save live2d-widget-model-xxx 来安装
然后你就可以通过向 model.use 键入包名 (live2d-widget-model-wanko) 来使用了.
<a name="9Bjl2"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#10-%E9%A6%96%E9%A1%B5%E9%98%85%E8%AF%BB%E5%85%A8%E6%96%87)10.首页阅读全文
Hexo 的 Next 主题默认是首页显示你每篇文章的全文内容，但这会使你的首页篇幅过于冗长，针对这个问题我们可以这么做：
用编辑器打开themes/next 目录下的_config.yml文件
找到代码：
> auto_excerpt:
>    enable: false
>    length: 150

将enable的 false改成true，length可以设定文章预览的文本长度。
<a name="0xAL3"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#11-%E4%BF%AE%E6%94%B9%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87)11.修改背景图片
在 themes/*/source/css/_custom/custom.styl 中添加如下代码：
> | // 添加背景图 bg.jpg为图片名称body{    background:url(/images/bg.jpg);    background-size:cover;    background-repeat:no-repeat;    background-attachment:fixed;    background-position:center;} |
| :--- |

> 

<a name="lQ4zs"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#12-%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E5%87%BA%E7%8E%B0%E6%A1%83%E5%BF%83%E6%95%88%E6%9E%9C)12.实现点击出现桃心效果

1. 在/themes/*/source/js/src下新建文件click.js，接着把以下粘贴到click.js文件中。<br />代码如下：

```javascript
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
```


2. 在\themes\*\layout\_layout.swig文件末尾添加：

```javascript
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/click.js"></script>
```

<a name="pw3VR"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#13-%E4%B8%BB%E9%A1%B5%E6%96%87%E7%AB%A0%E6%B7%BB%E5%8A%A0%E8%BE%B9%E6%A1%86%E9%98%B4%E5%BD%B1%E6%95%88%E6%9E%9C)13.主页文章添加边框阴影效果
打开 themes/*/source/css/_custom/custom.styl ,向里面加代码:

```css
// 主页文章添加阴影效果
.post {
   margin-top: 0px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
}
```

<a name="XAJAU"></a>
## 14.显示当前浏览进度
修改themes/*/_config.yml，把 false 改为 true：

```yaml
# Back to top in sidebar
b2t: true

# Scroll percent label in b2t button
scrollpercent: true
```

<a name="FOJtq"></a>
## 15.博客文章置顶
安装插件

```bash
$ npm uninstall hexo-generator-index --save
$ npm install hexo-generator-index-pin-top --save
```

然后在需要置顶的文章的Front-matter中加上top即可：top值越大表示优先级越高

```markdown
---
title: 2018
date: 2018-10-25 16:10:03
top: 10
---
```

设置置顶标志<br />打开：/themes/*/layout/_macro/post.swig插入以下代码即可：

```html
{% if post.top %}
  <i class="fa fa-thumb-tack"></i>
  <font color=000000>置顶</font>
  <span class="post-meta-divider"> </span>
{% endif %}
```


<a name="fA5pE"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#16-%E7%94%9F%E6%88%90%E5%8D%9A%E6%96%87%E6%8F%92%E5%85%A5%E5%9B%BE%E7%89%87)16.生成博文插入图片
参考：[Nuub](https://blog.csdn.net/sugar_rainbow/article/details/57415705)<br />用Typora编写Markdown的可以修改成这样就直接复制图片过去了

<a name="EPAgT"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#17-%E5%8F%96%E6%B6%88%E6%96%87%E7%AB%A0%E7%9B%AE%E5%BD%95%E8%87%AA%E5%8A%A8%E7%BC%96%E5%8F%B7)17.取消文章目录自动编号
修改主题配置文件那里的number为false

<a name="Z7tHG"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#18-%E4%BF%AE%E6%94%B9%E6%96%87%E7%AB%A0%E5%BA%95%E9%83%A8%E6%A0%87%E7%AD%BE%E7%9A%84%E5%9B%BE%E6%A0%87)18.修改文章底部标签的图标
修改主题模板/themes/next/layout/_macro/post.swig，搜索 rel="tag">#，将 # 换成<i class="fa fa-tag"></i>
<a name="JMf2X"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#19-%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90%E5%8E%8B%E7%BC%A9)19.静态资源压缩
在站点目录下：

```bash
$ npm install gulp -g
npm install gulp
```

安装gulp插件：

```bash
npm install gulp-minify-css --save
npm install gulp-uglify --save
npm install gulp-htmlmin --save
npm install gulp-htmlclean --save
npm install gulp-imagemin --save
```

在 Hexo 站点下新建 gulpfile.js文件，文件内容如下：

```javascript
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');
// 压缩css文件
gulp.task('minify-css', function() {
  return gulp.src('./public/**/*.css')
  .pipe(minifycss())
  .pipe(gulp.dest('./public'));
});
// 压缩html文件
gulp.task('minify-html', function() {
  return gulp.src('./public/**/*.html')
  .pipe(htmlclean())
  .pipe(htmlmin({
    removeComments: true,
    minifyJS: true,
    minifyCSS: true,
    minifyURLs: true,
  }))
  .pipe(gulp.dest('./public'))
});
// 压缩js文件
gulp.task('minify-js', function() {
    return gulp.src(['./public/**/.js','!./public/js/**/*min.js'])
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
});
// 压缩 public/demo 目录内图片
gulp.task('minify-images', function() {
    gulp.src('./public/demo/**/*.*')
        .pipe(imagemin({
           optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
           progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
           interlaced: false, //类型：Boolean 默认：false 隔行扫描gif进行渲染
           multipass: false, //类型：Boolean 默认：false 多次优化svg直到完全优化
        }))
        .pipe(gulp.dest('./public/uploads'));
});
// 默认任务
gulp.task('default', [
  'minify-html','minify-css','minify-js','minify-images'
]);
```

只需要每次在执行 generate 命令后执行 gulp 就可以实现对静态资源的压缩，压缩完成后执行 deploy 命令同步到服务器：

```bash
hexo g
gulp
hexo d


hexo clean && hexo g && gulp && hexo d
```

<a name="akCd5"></a>
## 20.去掉图片边框
NexT主题默认会有图片边框，不太好看，我们可以把边框去掉。打开 themes\Next\source\css\_custom\custom.styl，添加如下CSS代码：

```css
/* 去掉图片边框 */
.posts-expand .post-body img {
    border: none;
    padding: 0px;
}
.post-gallery .post-gallery-img img {
    padding: 3px;
}
```

<a name="fvBUV"></a>
## 21.添加 关于页面
hexo new page “about” 新建一个 关于我 页面。<br />主题的 _config.yml 文件中的 menu 中进行匹配

```yaml
menu:
  home: /      //主页
  categories: /categories //分类
  archives: /archives   //归档
  tags: /tags   //标签
  about: /about   //关于                  （添加此行即可）
```

同理于标签页和分类页
<a name="2KyMz"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#22-%E6%B7%BB%E5%8A%A0%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1-%E9%98%85%E8%AF%BB%E6%97%B6%E9%95%BF)22.添加字数统计.阅读时长
<a name="Dpig1"></a>
### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#%E7%BB%9F%E8%AE%A1%E6%8F%92%E4%BB%B6)统计插件
<a name="1uaPC"></a>
#### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#%E9%85%8D%E7%BD%AE)配置
NexT 主题默认已经集成了文章【字数统计】.【阅读时长】统计功能，如果我们需要使用，只需要在主题配置文件 _config.yml 中打开 wordcount 统计功能即可。如下所示：

```yaml
# Post wordcount display settings
# Dependencies: https://github.com/willin/hexo-wordcount
post_wordcount:
  item_text: true
  wordcount: true         # 单篇 字数统计
  min2read: true          # 单篇 阅读时长
  totalcount: false       # 网站 字数统计
  separated_meta: true
```

修改完成主题配置文件后，启动服务预览：
> hexo server

访问 [http://localhost:4000/](https://link.jianshu.com/?t=http://localhost:4000/) 链接，如果出现字数统计和阅读时长失效的情况，一般是因为没有安装 hexo-wordcount 插件，查看 Hexo 插件：
> hexo --debug

<a name="mxFvn"></a>
#### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#%E5%AE%89%E8%A3%85)安装
如果没有安装 hexo-wordcount插件，先安装该插件：
> npm i --save hexo-wordcount

Node 版本 7.6.0 之前,请安装 2.x 版本 (Node.js v7.6.0 and previous) ，安装命令如下：
> npm install hexo-wordcount@2 --save

安装完成后，重新执行启动服务预览就可以了。
<a name="wQnut"></a>
#### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#%E6%98%BE%E7%A4%BA%E6%96%87%E5%AD%97)显示文字
打开post.swig文件，路径如下：/themes/next/layout/_macro/post.swig
修改【字数统计】，找到如下代码：

```html
<span title="{{ __('post.wordcount') }}">
    {{ wordcount(post.content) }}
</span>
添加 “字” 到 {{ wordcount(post.content) }} 后面，修改后为：

<span title="{{ __('post.wordcount') }}">
    {{ wordcount(post.content) }} 字
</span>
同理，我们修改【阅读时长】，修改后如下：

<span title="{{ __('post.min2read') }}">
    {{ min2read(post.content) }} 分钟
</span>
```


效果预览图：

<a name="00prm"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#23-%E6%B7%BB%E5%8A%A0%E7%A4%BE%E4%BA%A4)23.添加社交
在主题配置文件找到social，添加需要的就可以，具体如下图
可以自定义图标，默认的图标都是从[图标库](https://fontawesome.com/icons?d=gallery)自动匹配的，||后面的就是在图标库的图标名
[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561011982566-18a89b20-14d0-406e-bbb1-49ab0dfa5f86.png#align=left&display=inline&height=412&originHeight=412&originWidth=1438&size=0&status=done&width=1438)](https://i.loli.net/2018/12/31/5c2985637e570.png)
<a name="XHYwd"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#24-%E6%B7%BB%E5%8A%A0%E7%AB%99%E5%86%85%E6%90%9C%E7%B4%A2)24.添加站内搜索
1、安装 [hexo-generator-searchdb](https://github.com/flashlab/hexo-generator-search) 插件
> npm install hexo-generator-searchdb --save

2、打开 站点配置文件 找到Extensions在下面添加
> # 搜索
> search:
>  path: search.xml
>  field: post
>  format: html
>  limit: 10000

3、打开 主题配置文件 找到Local search，将enable设置为true
<a name="e02Jy"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#25-%E8%AE%BE%E7%BD%AE%E6%96%87%E5%AD%97%E5%B1%85%E4%B8%AD)25.设置文字居中
这一行需要居中
设置方法：
> <center>这一行需要居中</center>
> 
> 注意：简书中此方法无效

<a name="OPWd2"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#26-%E7%82%B9%E5%87%BB%E7%88%86%E7%82%B8%E6%95%88%E6%9E%9C)26.点击爆炸效果
实现方法
跟那个红心是差不多的，首先在themes/next/source/js/src里面建一个叫fireworks.js的文件，代码如下：

```javascript
"use strict";function updateCoords(e){pointerX=(e.clientX||e.touches[0].clientX)-canvasEl.getBoundingClientRect().left,pointerY=e.clientY||e.touches[0].clientY-canvasEl.getBoundingClientRect().top}function setParticuleDirection(e){var t=anime.random(0,360)*Math.PI/180,a=anime.random(50,180),n=[-1,1][anime.random(0,1)]*a;return{x:e.x+n*Math.cos(t),y:e.y+n*Math.sin(t)}}function createParticule(e,t){var a={};return a.x=e,a.y=t,a.color=colors[anime.random(0,colors.length-1)],a.radius=anime.random(16,32),a.endPos=setParticuleDirection(a),a.draw=function(){ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.fillStyle=a.color,ctx.fill()},a}function createCircle(e,t){var a={};return a.x=e,a.y=t,a.color="#F00",a.radius=0.1,a.alpha=0.5,a.lineWidth=6,a.draw=function(){ctx.globalAlpha=a.alpha,ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.lineWidth=a.lineWidth,ctx.strokeStyle=a.color,ctx.stroke(),ctx.globalAlpha=1},a}function renderParticule(e){for(var t=0;t<e.animatables.length;t++){e.animatables[t].target.draw()}}function animateParticules(e,t){for(var a=createCircle(e,t),n=[],i=0;i<numberOfParticules;i++){n.push(createParticule(e,t))}anime.timeline().add({targets:n,x:function(e){return e.endPos.x},y:function(e){return e.endPos.y},radius:0.1,duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule}).add({targets:a,radius:anime.random(80,160),lineWidth:0,alpha:{value:0,easing:"linear",duration:anime.random(600,800)},duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule,offset:0})}function debounce(e,t){var a;return function(){var n=this,i=arguments;clearTimeout(a),a=setTimeout(function(){e.apply(n,i)},t)}}var canvasEl=document.querySelector(".fireworks");if(canvasEl){var ctx=canvasEl.getContext("2d"),numberOfParticules=30,pointerX=0,pointerY=0,tap="mousedown",colors=["#FF1461","#18FF92","#5A87FF","#FBF38C"],setCanvasSize=debounce(function(){canvasEl.width=2*window.innerWidth,canvasEl.height=2*window.innerHeight,canvasEl.style.width=window.innerWidth+"px",canvasEl.style.height=window.innerHeight+"px",canvasEl.getContext("2d").scale(2,2)},500),render=anime({duration:1/0,update:function(){ctx.clearRect(0,0,canvasEl.width,canvasEl.height)}});document.addEventListener(tap,function(e){"sidebar"!==e.target.id&&"toggle-sidebar"!==e.target.id&&"A"!==e.target.nodeName&&"IMG"!==e.target.nodeName&&(render.play(),updateCoords(e),animateParticules(pointerX,pointerY))},!1),setCanvasSize(),window.addEventListener("resize",setCanvasSize,!1)}"use strict";function updateCoords(e){pointerX=(e.clientX||e.touches[0].clientX)-canvasEl.getBoundingClientRect().left,pointerY=e.clientY||e.touches[0].clientY-canvasEl.getBoundingClientRect().top}function setParticuleDirection(e){var t=anime.random(0,360)*Math.PI/180,a=anime.random(50,180),n=[-1,1][anime.random(0,1)]*a;return{x:e.x+n*Math.cos(t),y:e.y+n*Math.sin(t)}}function createParticule(e,t){var a={};return a.x=e,a.y=t,a.color=colors[anime.random(0,colors.length-1)],a.radius=anime.random(16,32),a.endPos=setParticuleDirection(a),a.draw=function(){ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.fillStyle=a.color,ctx.fill()},a}function createCircle(e,t){var a={};return a.x=e,a.y=t,a.color="#F00",a.radius=0.1,a.alpha=0.5,a.lineWidth=6,a.draw=function(){ctx.globalAlpha=a.alpha,ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.lineWidth=a.lineWidth,ctx.strokeStyle=a.color,ctx.stroke(),ctx.globalAlpha=1},a}function renderParticule(e){for(var t=0;t<e.animatables.length;t++){e.animatables[t].target.draw()}}function animateParticules(e,t){for(var a=createCircle(e,t),n=[],i=0;i<numberOfParticules;i++){n.push(createParticule(e,t))}anime.timeline().add({targets:n,x:function(e){return e.endPos.x},y:function(e){return e.endPos.y},radius:0.1,duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule}).add({targets:a,radius:anime.random(80,160),lineWidth:0,alpha:{value:0,easing:"linear",duration:anime.random(600,800)},duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule,offset:0})}function debounce(e,t){var a;return function(){var n=this,i=arguments;clearTimeout(a),a=setTimeout(function(){e.apply(n,i)},t)}}var canvasEl=document.querySelector(".fireworks");if(canvasEl){var ctx=canvasEl.getContext("2d"),numberOfParticules=30,pointerX=0,pointerY=0,tap="mousedown",colors=["#FF1461","#18FF92","#5A87FF","#FBF38C"],setCanvasSize=debounce(function(){canvasEl.width=2*window.innerWidth,canvasEl.height=2*window.innerHeight,canvasEl.style.width=window.innerWidth+"px",canvasEl.style.height=window.innerHeight+"px",canvasEl.getContext("2d").scale(2,2)},500),render=anime({duration:1/0,update:function(){ctx.clearRect(0,0,canvasEl.width,canvasEl.height)}});document.addEventListener(tap,function(e){"sidebar"!==e.target.id&&"toggle-sidebar"!==e.target.id&&"A"!==e.target.nodeName&&"IMG"!==e.target.nodeName&&(render.play(),updateCoords(e),animateParticules(pointerX,pointerY))},!1),setCanvasSize(),window.addEventListener("resize",setCanvasSize,!1)};
```

打开themes/next/layout/_layout.swig,在</body>上面写下如下代码：

```html
{% if theme.fireworks %}
   <canvas class="fireworks" style="position: fixed;left: 0;top: 0;z-index: 1; pointer-events: none;" ></canvas> 
   <script type="text/javascript" src="//cdn.bootcss.com/animejs/2.2.0/anime.min.js"></script> 
   <script type="text/javascript" src="/js/src/fireworks.js"></script>
{% endif %}
```

打开主题配置文件，在里面最后写下：

```yaml
# Fireworks
fireworks: true
```

完😀
[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561011982572-4fb8d3e3-e3ec-4d0a-9edd-699bcd982b82.png#align=left&display=inline&height=930&originHeight=930&originWidth=990&size=0&status=done&width=990)](https://i.loli.net/2018/12/31/5c298dab7dfd7.png)
<a name="ZoHVv"></a>
## [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#27-%E8%AE%BE%E7%BD%AE%E6%96%87%E7%AB%A0%E5%8A%A0%E5%AF%86%E8%AE%BF%E9%97%AE)27.设置文章加密访问
这里使用第三方插件[Hexo-Blog-Encrypt](https://github.com/MikeCoder/hexo-blog-encrypt/blob/master/ReadMe.zh.md)
<a name="0VXNs"></a>
#### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#1-%E9%A6%96%E5%85%88%EF%BC%8C%E4%BD%A0%E9%9C%80%E8%A6%81%E5%9C%A8%E7%AB%99%E7%82%B9-config-yml-%E4%B8%AD%E5%90%AF%E7%94%A8%E8%AF%A5%E6%8F%92%E4%BB%B6)1)首先，你需要在站点 _config.yml 中启用该插件

```yaml
# Security
##
encrypt:
    enable: true
```

<a name="vTVDr"></a>
#### 2)给文章添加密码：

```yaml
---
title: hello world
date: 2016-03-30 21:18:02
tags:
    - fdsfadsfa
    - fdsafsdaf
password: Mike
abstract: Welcome to my blog, enter password to read.
message: Welcome to my blog, enter password to read.
---
Eg：
password: 
abstract: 此处遭到了封印
message: 请输入正确的密码
```


- password: 是该博客加密使用的密码
- abstract: 是该博客的摘要，会显示在博客的列表页
- message: 这个是博客查看时，密码输入框上面的描述性文字
<a name="3pANf"></a>
### [](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/#%E5%AF%B9-TOC-%E8%BF%9B%E8%A1%8C%E5%8A%A0%E5%AF%86)对 TOC 进行加密
如果你有一篇文章使用了 TOC，你需要修改模板的部分代码。这里用 landscape 作为例子：

- 你可以在 hexo/themes/landscape/layout/_partial/article.ejs 找到 article.ejs。
- 然后找到 <% post.content %> 这段代码，通常在30行左右。
- 使用如下的代码来替代它:

```html
<% if(post.toc == true){ %>
    <div id="toc-div" class="toc-article" <% if (post.encrypt == true) { %>style="display:none" <% } %>>
        <strong class="toc-title">Index</strong>
        <% if (post.encrypt == true) { %>
            <%- toc(post.origin, {list_number: true}) %>
        <% } else { %>
            <%- toc(post.content, {list_number: true}) %>
        <% } %>
    </div>
<% } %>
<%- post.content %>
```

<a name="6V83I"></a>
## 28 设置首页缩略图
有两种方法，自行选择。

1. 这个需要使用<!-- more -->进行截断，<!-- more -->上面的内容就是显示在主页的摘要，把图片放在<!-- more -->上面就可以了。如果是文字也会进行分割。
1. 在编写md文章的时候在头部添加photos:，如下所示：

```yaml
---
title: 
categories: 
tags:
copyright: true
comments: false
description: 
date: 2017-11-09 14:33:32
top:
photos: 
- "https://i.loli.net/2019/01/19/5c42f345b6b2f.jpg"
```

- [遇见西门](https://www.simon96.online/2018/10/12/hexo-tutorial/)
- [JuLi距离](https://blog.csdn.net/qq_33699981/article/details/72716951)
- [Next官方文档](https://github.com/iissnan/hexo-theme-next/blob/master/README.cn.md)
- [Hexo瞎折腾系列](https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&tn=baidu&wd=Hexo%E7%9E%8E%E6%8A%98%E8%85%BE%E7%B3%BB%E5%88%97)
- [NIkkkki睡不醒](https://www.jianshu.com/p/21c94eb7bcd1)
- [二次元模型](https://huaji8.top/post/live2d-plugin-2.0/)
- [https://l2dwidget.js.org/dev.html](https://l2dwidget.js.org/dev.html)
- [hexo-helper-live2d](https://www.yuque.com/fangcao/api/xi5hss/hexo-helper-live2d)
- [live2d-widget.js](https://github.com/xiazeyu/live2d-widget.js)
<a name="RUitI"></a>
## 29 ECharts
常规做法<br />你可能也看到了，上面的图表在我的hexo搭建的博客中可以完美展示。这个是怎么做到的呢？

首先，如果你用的是Yelee或者类似的主题，你应该可以很简单地直接参照这个博客去做。

我也是在看上面的博客的时候遇到了问题，如果我用Yelee主题的话是很简单的可以实现上面的效果的，但是我现在更喜欢的是现在的Next主题。这两个主题的结构不一样。

安装上文说的在所用主题目录下layout\_partial文件夹中不存在，更不存在head.ejs

Next目录：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561109439961-abefa0c6-52e9-4695-9af2-1fbf18b0bacd.png#align=left&display=inline&height=216&name=image.png&originHeight=432&originWidth=823&size=55455&status=done&width=411.5)<br />
Yelee目录：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561109458824-55c8b679-57ba-490e-bbc1-e97e89cd4946.png#align=left&display=inline&height=309&name=image.png&originHeight=617&originWidth=834&size=85556&status=done&width=417)


Next主题做法<br />由此看出，如果你和我一样使用Next主题的话上面的教程不能用。需要像我这样做：

下载js<br />首先下载ECharts的js文件：[ECharts](https://echarts.baidu.com/download.html)

把js文件放到next主题的\source\js\src目录下：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561109537736-6d9e5b62-29cc-49f3-9a76-f77ff373cf40.png#align=left&display=inline&height=259&name=image.png&originHeight=518&originWidth=788&size=77241&status=done&width=394)


js文件的引用<br />然后在next\layout\文件夹下，找到_layout.swig文件，并用文本查看器打开，在下面代码:

```html
<main id="main" class="main">
    <div class="main-inner">
        <div class="content-wrap">
            <div id="content" class="content">
                {% block content %}{% endblock %}
            </div>
            {% include '_third-party/duoshuo-hot-articles.swig' %}
            {% include '_partials/comments.swig' %}
        </div>
        {% if theme.sidebar.display !== 'remove' %}
        {% block sidebar %}{% endblock %}
        {% endif %}
    </div>
</main>
```
的前面添加：

```html
<!-- echarts -->
<script type="text/javascript" src="/js/src/echarts.common.min.js"></script>
```

保存退出。

安装hexo-tag-echarts插件<br />在博客站点目录下执行npm install hexo-tag-echarts --save。


使用范例<br />可以简单的找个例子试下，把下面代码放到一个博客的markdown文件中即可。注意不要使用代码块！！

```markdown
{% echarts 400 '81%' %}
    {
        tooltip: {
            trigger: 'axis',
                axisPointer : { // 坐标轴指示器，坐标轴触发有效
                type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
            }
        },
        legend: {
            data: ['利润', '支出', '收入']
        },
        grid: {
            left: '3%',
                right: '4%',
                    bottom: '3%',
                        containLabel: true
        },
        xAxis: [
            {
                type: 'value'
            }
        ],
            yAxis : [
                {
                    type: 'category',
                    axisTick: { show: false },
                    data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
                }
            ],
                series : [
                    {
                        name: '利润',
                        type: 'bar',
                        itemStyle: {
                            normal: {
                                label: { show: true, position: 'inside' }
                            }
                        },
                        data: [200, 170, 240, 244, 200, 220, 210]
                    },
                    {
                        name: '收入',
                        type: 'bar',
                        stack: '总量',
                        itemStyle: {
                            normal: {
                                label: { show: true }
                            }
                        },
                        data: [320, 302, 341, 374, 390, 450, 420]
                    },
                    {
                        name: '支出',
                        type: 'bar',
                        stack: '总量',
                        itemStyle: {
                            normal: {
                                label: { show: true, position: 'left' }
                            }
                        },
                        data: [-120, -132, -101, -134, -190, -230, -210]
                    }
                ]
    };
    {% endecharts %}
```
之后你就应该能看到我的上面的ECharts图了。

<a name="bKXEI"></a>
## 优秀的设计博客：[https://clovertuan.github.io/resume/](https://clovertuan.github.io/resume/)

- 优秀的设计博客：[https://clovertuan.github.io/resume/](https://clovertuan.github.io/resume/)
- 优秀的星球博客：[https://tzvetkov75.github.io/demo_blog/public/2017/02/05/hello-world/](https://tzvetkov75.github.io/demo_blog/public/2017/02/05/hello-world/)
- [https://blinkfox.github.io/2018/09/28/qian-duan/hexo-bo-ke-zhu-ti-zhi-hexo-theme-matery-de-jie-shao/#toc-heading-18](https://blinkfox.github.io/2018/09/28/qian-duan/hexo-bo-ke-zhu-ti-zhi-hexo-theme-matery-de-jie-shao/#toc-heading-18)

转自：<br />[https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/](https://selfishluck.top/2018/12/21/Hexo%E4%B8%BB%E9%A2%98%E7%9A%84%E4%B8%80%E4%BA%9B%E9%85%8D%E7%BD%AE/)

