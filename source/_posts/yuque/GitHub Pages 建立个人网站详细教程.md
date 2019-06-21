
---

title: GitHub Pages 建立个人网站详细教程

date: 2019-06-12 17:37:06 +0800

tags: []

---
<a name="dViqm"></a>
### GitHub Pages是免费的静态站点，三个特点：
- 免费托管、
- 自带主题、
- 支持自制页面和Jekyll。
<a name="PDsFN"></a>
### 为什么使用github pages

- 搭建简单而且免费；
- 支持静态脚本；
- 可以绑定你的域名；
- DIY自由发挥，动手实践一些有意思的东西git,markdown,bootstrap,jekyll；
- 理想写博环境，git+github+markdown+jekyll；
<a name="rXgvq"></a>
### 创建github pages

1. 安装git工具
> [http://windows.github.com/](https://link.zhihu.com/?target=http%3A//windows.github.com/)
> [http://mac.github.com/](https://link.zhihu.com/?target=http%3A//mac.github.com/)

2.两种pages模式
> - 使用自己的用户名，每个用户名下面只能建立一个；
> - 资源命名必须符合这样的规则username/[http://username.github.com](https://link.zhihu.com/?target=http%3A//username.github.com)；
> - 主干上内容被用来构建和发布页面

- gh-pages分支用于构建和发布；
- 如果user/org pages使用了独立域名，那么托管在账户下的所有project pages将使用相同的域名进行重定向，除非project pages使用了自己的独立域名；
- 如果没有使用独立域名，project pages将通过子路径的形式提供服务[http://username.github.com/projectname](https://link.zhihu.com/?target=http%3A//username.github.com/projectname)；
- 自定义404页面只能在独立域名下使用，否则会使用User Pages 404；
- 创建项目站点步骤：

```bash
$ git clone https://github.com/USERNAME/PROJECT.git PROJECT
$ git checkout --orphan gh-pages
$ git rm -rf .
$ git add .
$ git commit -a -m "First pages commit"
$ git push origin gh-pages
```
可以通过User/Organization Pages建立主站，而通过Project Pages挂载二级应用页面。

<a name="51Eug"></a>
### 创建步骤
第一步：创建个人站点<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560332866938-f699421b-8375-4b27-9ec4-1837ccdfae75.png#align=left&display=inline&height=293&name=image.png&originHeight=585&originWidth=822&size=85219&status=done&width=411)<br />第二步：设置站点主题

![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560332777697-f916c7ba-6411-4f33-89df-be3e753ee1f8.png#align=left&display=inline&height=247&originHeight=493&originWidth=998&status=done&width=499)

<a name="AFNAx"></a>
### 常用命令
```bash
$ git clone git@github.com:username/username.github.com.git 
//本地如果无远程代码，先做这步，不然就忽略
$ cd .ssh/username.github.com //定位到你blog的目录下
$ git pull origin master 
//先同步远程文件，后面的参数会自动连接你远程的文件
$ git status //查看本地自己修改了多少文件
$ git add . //添加远程不存在的git文件
$ git commit * -m "what I want told to someone"
$ git push origin master //更新到远程服务器上
```
<a name="knVVJ"></a>
### 使用Jekyll搭建博客

<a name="rCmVj"></a>
#### 1 什么是jekyll
Jekyll是一种简单的、适用于博客的、静态网站生成引擎。它使用一个模板目录作为网站布局的基础框架，支持Markdown、Textile等标记语言的解析，提供了模板、变量、插件等功能，最终生成一个完整的静态Web站点。<br />说白了就是，只要安装Jekyll的规范和结构，不用写html，就可以生成网站。[jekyll介绍][jekyll on github][jekyllbootstrap]。<br />Jekyll使用Liquid模板语言，{{page.title}}表示文章标题，{{content}}表示文章内容。我们可以用两种Liquid标记语言：输出标记（output markup）和标签标记 (tag markup)。输出标记会输出文本（如果被引用的变量存在），而标签标记不会。输出标记是用双花括号分隔，而标签标记是用花括号-百分号对分隔。[Liquid模板语言] [Liquid模板变量参考]。<br />jekyll与github的关系：GitHub Pages一个由 GitHub 提供的用于托管项目主页或博客的服务，jekyll是后台所运行的引擎。
<a name="e0B11"></a>
#### 2 jekyll本地环境搭建
1.下载最新的RubyInstaller并安装(我下载的是rubyinstaller-1.9.3-p194.exe)，设置环境变量，path中配置C:Ruby193bin目录，然后在命令行终端下输入gem update --system来升级gem；<br />2.下载最新的DevKit，DevKit是windows平台下编译和使用本地C/C++扩展包的工具。它就是用来模拟Linux平台下的make,gcc,sh来进行编译。但是这个方法目前仅支持通过RubyInstaller安装的Ruby，并双击运行解压到C:DevKit。然后打开终端cmd，输入命令进行安装。<br />3.完成上面的准备就可以安装Jekyll了,因为Jekyll是用Ruby编写的,最好的安装方式是通过RubyGems(gem):
```bash
gem install Jekyll
```
并使用命令检验是否安装成功
```
jekyll --version
```
4.安装Rdiscount，这个用来解析Markdown标记的包，使用如下命令：
```
gem install rdiscount
```
5.运行本地工程：<br />cd 到工程目录，启动服务：
```
jekyll --server
```
<a name="elQef"></a>
#### 3 jekyll目录结构
<a name="tlBbP"></a>
#### _posts：
_posts中的数据文档，通过注入_layouts定义的模板，通过jekyll --server最终生成的静态页面在_sites目录。目录是用来存放你的文章的，一般以日期的形式书写标题。
<a name="eUKC9"></a>
#### _layouts：
_layouts中的模板一般指向了_includes/themes中的模板。目录是用来存放模板的，在这里你可以定义页面中不同的头部和底部。
<a name="vPddy"></a>
#### _includes：

- _includes/JB中有一些常用的工具，用于列表显示、评论等；
- _includes/themes中可参看主题的相关html文档。
- _includes/themes中的主题一般包含default.html、post.html和page.html三个文档。default.html定义了网站的最上层框架（模板），post.html和page.html是其子框架（模板）。
- 生成好的html子页面通过default.html的{{ content }}变量调用，生成整个页面。
<a name="hHlg5"></a>
#### assets
渲染页面的CSS和JS文档在assets/themes中
<a name="9a9sP"></a>
#### _config.yml
站点生成需要用到_config.yml配置文件，站点的全局变量在_config.yml中定义，用site.访问；页面的变量在YAML Front Matter中定义，用page.访问，更多的模板变量可参考模板数据。
<a name="BUJjy"></a>
#### index.html
你的页面首页。
<a name="ImVbZ"></a>
### Jekyll-Bootstrap创建博客
1.创建个人站点，即创建一个新资源，格式为[http://username.github.com](https://link.zhihu.com/?target=http%3A//username.github.com)；<br />2.安装Jekyll-Bootstrap：
```bash
$ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com
$ cd USERNAME.github.com
$ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git
$ git push origin master
```
3.访问创建好的个人站点：
> [http://username.github.com](https://link.zhihu.com/?target=http%3A//username.github.com)
4.在本地测试查看效果：
```bash
cd USERNAME.github.comjekyll --server
```


详细的教程看：<br />[http://jekyllcn.com/](http://jekyllcn.com/)<br />[https://www.zhihu.com/question/30018945?sort=created](https://www.zhihu.com/question/30018945?sort=created)

