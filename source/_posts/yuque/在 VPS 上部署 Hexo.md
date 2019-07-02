
---

title: 在 VPS 上部署 Hexo

date: 2019-06-14 16:41:55 +0800

tags: []

---
Hexo博客架构<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560501737421-4656534d-8aad-4ddb-834a-c974e81bc942.png#align=left&display=inline&height=420&name=image.png&originHeight=480&originWidth=800&size=61881&status=done&width=700)

简单地说，在本地用 markdown 写好文章，用 hexo 生成静态的 html 文件并 push 到远程服务器（vps），vps 再通过 git-hooks 同步网站目录。<br />其实这两个是可以合成一个的，不过每次写文章都要 ssh 登录到 vps，体验可能没那么好。

<a name="oFwP6"></a>
## 流程大纲

1. 本地 – 环境搭建，安装 Hexo,包括 hexo-cli, Nodejs, git;
1. 本地 – 写文章；
1. 远程 VPS – 环境搭建，包括 Nodejs, git, Nginx 配置和创建 git 用户;使用 git 自动化部署发布博客
1. 使用 Git 自动化部署发布博客

[]()
<a name="L8lnb"></a>
## [](https://www.xxb.me/Hexo/yuque-hexo01/#%E6%9C%AC%E5%9C%B0-Hexo-%E5%AE%89%E8%A3%85%E5%92%8C%E9%85%8D%E7%BD%AE)本地 Hexo 安装和配置
首先要安装 Nodejs 和 git , mac 系统可用 brew 安装，其它系统自行摸索

```bash
brew install nodejs git
```
安装 hexo-cli

```bash
npm install -g hexo-cli
```
找个地方放 Hexo 程序

```bash
mkdir -p ~/Documents/code
cd ~/Documents/code
hexo init blog
```
然后安装两个插件，分别是 git 自动部署插件 [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git) 和简单的本地web服务器 [hexo-server](https://hexo.io/zh-cn/docs/server.html)

```bash
cd ~/Documents/code/blog
npm install hexo-deployer-git --save
npm install hero-server --save
```
至此本地环境算搭建好了，下面是写文章
<a name="UF0B7"></a>
## 本地 Hexo 发表文章
使用命令新建文章

```bash
cd ~/Documents/code
hexo new "hello Hexo"
```
该命令会成一个对应的 .md 文件放置在 sources/_posts 文件夹

```bash
sources/_posts/hello-hexo.md
```
接下来用你喜欢的编辑器编辑 hello-hexo.md 文件，记得要用 markdown 语法。<br />
写好以后， 使用 hexo g 命令将 .md 文件渲染成静态文件

```bash
hexo g
```
然后启动本地 web 服务器 hexo-server

```bash
hexo server
```
该命令可简写为 hexo s, 现在可以用浏览器打开 [http://localhost:4000](http://localhost:4000/) 访问博客了。<br />
（注：以上本地环境搭建完成可以放在远程服务器 vps 上，当然写文章也得在 vps 上写，传统的做法是像架构图那样分离开。）

<a name="ISZZf"></a>
## 远程 VPS 环境搭建

同样要安装 Nodejs 和 git，根据自己的系统自行摸索，此步略过<br />Nginx 配置，我用宝塔 linux 面板一键安装，不用手动配置，如果要手动改，参考配置如下（抄来的，仅供参考）：

```nginx
server
{
    listen 80;
    #listen [::]:80;
    server_name www.xxb.me xxb.me;
    index index.html index.htm index.php default.html default.htm default.php;
    #这里要改成网站的根目录
    root  /path/to/www;  

    include other.conf;
    #error_page   404   /404.html;
    location ~ .*\.(ico|gif|jpg|jpeg|png|bmp|swf)$
    {
        access_log   off;
        expires      1d;
    }

    location ~ .*\.(js|css|txt|xml)?$
    {
        access_log   off;
        expires      12h;
    }

    location / {
        try_files $uri $uri/ =404;
    }

    access_log  /home/wwwlogs/blog.log  access;
}
```
<a name="lKz1m"></a>
## 未完待续

