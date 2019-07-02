
---

title: Hexo同步语雀文章一

date: 2019-06-11 10:49:03 +0800

tags: []

---
<a name="LxHUJ"></a>
## 创建 Hexo 博客
已经有 Hexo 博客的可以跳过。如果你是 Jekyll ，也可以跳过。

- 安装 Node.js
- 安装 Hexo 脚手架

```bash
npm install -g hexo-cli
hexo init blog
cd blog
npm install or yarn install
hexo server
```

- Hexo建站参考[Hexo官方文档](https://hexo.io/zh-cn/docs/index.html)：[https://hexo.io/zh-cn/docs/](https://hexo.io/zh-cn/docs/)

<a name="DNcR6"></a>
## 安装语雀文章下载插件
[yuque-hexo](https://github.com/x-cold/yuque-hexo/) 是一个 Node.js 环境下的语雀下载器，使用 npm 安装

- 安装 yuque-hexo
- 注册语雀，创建知识库，获得你的个人路径和知识库的名字，比如我的博客的知识库是 :[https://www.yuque.com/fangcao/api](https://www.yuque.com/fangcao/api)
- 在 Hexo 博客的目录下面的 package.json 中，进行下面的配置

```json
{
    "name": "hexo-site",
    "version": "0.0.0",
    "private": true,
    "hexo": {
        "version": "3.8.0"
    },
    "dependencies": {
        "hexo": "^3.8.0",
        "hexo-generator-archive": "^0.1.5",
        "hexo-generator-category": "^0.1.3",
        "hexo-generator-index": "^0.2.1",
        "hexo-generator-tag": "^0.2.0",
        "hexo-renderer-ejs": "^0.3.1",
        "hexo-renderer-marked": "^1.0.1",
        "hexo-renderer-stylus": "^0.3.3",
        "hexo-server": "^0.3.3"
    },
    "yuqueConfig": {
        "baseUrl": "https://www.yuque.com/api/v2",
        "login": "fangcao",
        "repo": "api",
        "mdNameFormat": "title",
        "postPath": "source/_posts/yuque",
        "token": "放上自己的语雀token"
    },
    "scripts": {
        "clean": "hexo clean",
        "clean:yuque": "DEBUG=yuque-hexo.* yuque-hexo clean",
        "deploy": "hexo deploy",
        "publish": "npm run clean && npm run deploy",
        "dev": "hexo s",
        "sync": "DEBUG=yuque-hexo.* yuque-hexo sync",
        "reset": "npm run clean:yuque && npm run sync"
    },
    "devDependencies": {
        "yuque-hexo": "^1.6.1"
    }
}

```
| 参数名 | 含义 | 默认值 |
| --- | --- | --- |
| postPath | 文档同步后生成的路径 | source/_posts/yuque |
| cachePath | 文档下载缓存文件 | yuque.json |
| mdNameFormat | 文件名命名方式 (title / slug) | title |
| adapter | 文档生成格式 (hexo/markdown) | hexo |
| concurrency | 下载文章并发数 | 5 |
| baseUrl | 语雀 API 地址 | - |
| login | 语雀 login (group) | - |
| repo | 语雀仓库短名称 | - |
| onlyPublished | 只展示已经发布的文章 |  |

- 如果不是 Hexo 博客，则需要按照上面的文件保存一个 package.json 到博客目录，并且配置 postPath 为正确的文章目录
- 同步文章

```bash
yuque-hexo sync
```

- 语雀同步过来的文章会生成两部分文件；
  - yuque.json: 从语雀 API 拉取的数据
  - source/_posts/yuque/*.md: 生成的 md 文件
- 支持配置 front-matter, 语雀编辑器编写示例如下:
-  语雀编辑器示例，可参考[hexo的终极玩法](https://www.yuque.com/u46795/blog/dlloc7)

<a name="articleHeader0"></a>
# 配置GitHub pages
首先需要一个GitHub账号<br />然后可以<br />具体可参照[官方教程](https://pages.github.com/)

<a name="articleHeader5"></a>
## 改变主题
[这是](https://hexo.io/themes/)官方的主题网站<br />将主题clone到你的theme，在配置文件中<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560237648554-f64e1112-1f4d-4648-8fe2-9682dfebd1ff.png#align=left&display=inline&height=76&originHeight=76&originWidth=321&size=0&status=done&width=321)<br />将theme改变为你下载的主题名称<br />然后编译，运行，发布。

使用next主题的可以参考[官方网址](https://theme-next.iissnan.com/)

<a name="articleHeader4"></a>
### 配置Travis CI

之前也有不少文章用不同的方法解决上述的问题，例如[利用 Dropbox 同步](http://lucifr.com/2013/06/02/hexo-on-cloud-with-dropbox-and-vps/)或者[利用 Github 的 Webhooks](http://blog.sunnyyan.com/2015/05/01/hexo-auto-generate/) 进行自动部署。这些方法需要付出一定的成本，因为都需要利用到一台 VPS 去完成。而今有一个更加简单而且免费的方法去完成 hexo 的自动部署，就是利用 Travis CI。

重点来了，详细步骤可参考[用 Travis CI 自动部署 hexo](https://segmentfault.com/a/1190000004667156)，[手把手教你Travis CI](https://www.jianshu.com/p/e22c13d85659),作者已经说的比较详细。<br />需要注意的一点是：在package.json中增加depoly的命令行语句，防止travis在自动执行到npm run deploy这一步的时候报找不到该script的错。
```
"scripts": {
  "deploy": "hexo clean && hexo g -d"
},
```
上述代码加在dependencies同级即可。

查看TravisCi [https://travis-ci.org/fangcao7618/fangcao7618.github.io](https://travis-ci.org/fangcao7618/fangcao7618.github.io)

主题：

主题选择：[next 主题](https://theme-next.iissnan.com)<br />主题二：[https://hexo.io/themes/](https://hexo.io/themes/)

[https://theme-next.org/](https://theme-next.org/)

例子：[https://www.jinrishici.com/](https://www.jinrishici.com/)


