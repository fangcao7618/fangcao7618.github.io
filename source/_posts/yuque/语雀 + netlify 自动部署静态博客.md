
---

title: 语雀 + netlify 自动部署静态博客

date: 2019-06-11 10:23:31 +0800

tags: []

---
<a name="pZPAM"></a>
### 语雀 + netlify

<a name="YO4tg"></a>
#### 1. netlify 配置1
一、使用github或者gitlab登陆netlify<br />
首先，打开netlify网站(https://app.netlify.com/)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560219963361-e59950a8-7d00-4544-9a43-93398b583307.png#align=left&display=inline&height=574&name=image.png&originHeight=574&originWidth=1080&size=159308&status=done&width=1080)然后使用github或者gitlab账号登录。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560219990592-2070099f-d7e2-4915-a4e6-9e7fdabf59f5.png#align=left&display=inline&height=332&name=image.png&originHeight=332&originWidth=668&size=20085&status=done&width=668)<br />二、根据github/gitlab仓库创建网站<br />
点击New site from Git按钮：

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220013088-faa80222-1226-43e7-b650-dd1b3baa4019.png#align=left&display=inline&height=325&name=image.png&originHeight=325&originWidth=1080&size=38036&status=done&width=1080)


根据你的仓库所在平台选择，以下三选一：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220027954-70001ff4-4c87-4130-88e5-28c36ca7bfd0.png#align=left&display=inline&height=63&originHeight=128&originWidth=1080&size=0&status=done&width=530)<br />选择你需要部署的仓库：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560220027963-a8800002-19fd-4627-b9f2-b5caa5b71da7.jpeg#align=left&display=inline&height=287&originHeight=585&originWidth=1080&size=0&status=done&width=530)<br />设置部署选项，包括三点：

1. 部署分支（对应下图中 Branch to deploy）:<br />顾名思义就是你的git仓库的分支，默认选择为master分支<br />
1. 打包命令（对应下图中 Build command）：<br />就是你的打包命令，诸如 npm run build，gulp build 之类；如果本身已是静态文件，不需打包编译，这一栏则不填<br />
1. 打包后目录（对应下图中 Publish directory）：<br />即执行完打包命令之后静态文件所在目录，诸如 dist，_site 之类；如果本身已是静态文件，这一栏则不填<br />

![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560220058523-f6155f0c-4399-4973-b181-f28765ede6d5.jpeg#align=left&display=inline&height=642&originHeight=1080&originWidth=892&size=0&status=done&width=530)<br />完成之后点击途中 deploy site 按钮<br /> <br />三、设置域名，绑定域名<br />进行完第二步，我们可以看到自动化部署已经开始运行了，而且过不多久，我们的网站就已经可以利用netlify域名就行访问了，如下图：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560220058481-6850ecd0-e19a-42c3-8f17-94ac3ac47699.jpeg#align=left&display=inline&height=280&originHeight=570&originWidth=1080&size=0&status=done&width=530)<br />可以看到netlify为我们随机生成了一个netlify下的域名，这里我们可以更改其前缀，并绑定到我们自己的域名下：<br />>> 更改netlify域名前缀：<br />首先，点击上图中 Site settings 按钮，然后在下方点击 Change site name 按钮，然后在弹出框中输入自己需要更改的前缀名，点击保存即可，如下图所示：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560220058517-f99dd770-b5dd-4dd8-be44-f95b708a6581.jpeg#align=left&display=inline&height=438&originHeight=626&originWidth=758&size=0&status=done&width=530)<br />>> 绑定到自己的域名下：<br />首先，点击上上图中 Domain settings 按钮，然后在下方点击 Add custom domain 按钮，然后在弹出框中输入自己需要绑定的完整域名，点击保存，如下图所示：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220058538-72a726ec-d38f-4587-8d82-63ede31a41de.png#align=left&display=inline&height=310&originHeight=438&originWidth=750&size=0&status=done&width=530)<br />这个时候会显示 ！Check DNS configuration，因为我们还没有设置域名解析到netlify服务器，所以这个时候需要到你自己域名的相应服务商网站登录之后在需要绑定的域名下添加一条CNAME解析，解析的主机记录即对应的netlify域名值（这里即 codernie.netlify.com）<br />ok，过一会儿就可以使用自己的域名访问自己的网站啦<br /> <br />四、生成HTTPS证书，实现HTTPS访问<br />第四部中的Domain settings 中往下拉，可以看到 HTTPS 几个大字母：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560220058509-931e334c-54e0-471f-b981-547c96e2685e.jpeg#align=left&display=inline&height=406&originHeight=827&originWidth=1080&size=0&status=done&width=530)<br />点击 Verify DNS configuration 按钮，待它变成下方绿色按钮之后，再点击：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220058518-364fe111-6c8f-4969-a359-f5964dceeefc.png#align=left&display=inline&height=151&originHeight=138&originWidth=484&size=0&status=done&width=530)<br />然后在弹出框中点击确认，过一会儿之后就可以使用https访问你的小站啦：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220059081-79b8b532-fb36-4018-8c91-b946620e8c81.png#align=left&display=inline&height=62&originHeight=54&originWidth=462&size=0&status=done&width=530)<br />看到自己的小站前面可以有绿色的安全字样，是不是很酷炫，而且很放心，再也不用担心运营商在自己的网站上挂广告啦，哈哈哈。。。等等，是不是还差了点什么：<br />对啊，还没有强制跳转https，OK，继续<br /> <br />五、强制HTTP跳转HTTPS访问<br />在第四步 Domain settings 再往下翻一点，可以看到 Force HTTPS，只需点击 Force HTTPS 即可实现，是不是很方便，如下图：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560220058574-7d4caf90-9109-4647-af0b-0e271b2fb1e9.jpeg#align=left&display=inline&height=416&originHeight=628&originWidth=800&size=0&status=done&width=530)

 <br />六、设置redirect<br />利用netlify实现自动化部署和HTTPS就写到这里了。

[https://app.netlify.com/sites/stoic-murdock-f3d33b/settings/general](https://app.netlify.com/sites/stoic-murdock-f3d33b/settings/general)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220255014-076f6ed2-0449-4426-b25c-4d01ccea22e0.png#align=left&display=inline&height=367&name=image.png&originHeight=367&originWidth=1010&size=54950&status=done&width=1010)

<a name="t8aQE"></a>
#### 2. netlify 配置2
前往 Settings -> Build & Deploy 找到 Build hooks，添加一个 build hook

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560219835172-1e2dfc9b-e93f-4eb2-aab3-071b401b1635.png#align=left&display=inline&height=523&name=image.png&originHeight=523&originWidth=1181&size=97354&status=done&width=1181)

<a name="Idey1"></a>
#### 3. 语雀配置
URL 填入刚刚从 netlify 生成的 hook 链接

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560219853510-10fffb6b-cc7c-4d38-94f3-cf2b44c9a4d5.png#align=left&display=inline&height=508&name=image.png&originHeight=508&originWidth=1341&size=154639&status=done&width=1341)

> - 所有更新触发：该知识库下的任何一篇文档的更新都会触发 WebHook
> - 仅主动推送更新触发：只在文档发布或更新的时候勾选了「文档有较大更新，推送给关注人」才会触发 WebHook

[<br />](https://cdn.nlark.com/yuque/0/2019/png/123526/1547759387222-a374e7cd-69dc-4cb6-9433-dad75898b191.png)![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560219869885-0f9c5cc0-ea06-444e-a9e1-2d734ec5ffc2.png#align=left&display=inline&height=458&name=image.png&originHeight=458&originWidth=784&size=93316&status=done&width=784)

3. 同步语雀文章<br />
Gatsby -> [https://github.com/Raincal/gatsby-source-yuque](https://github.com/Raincal/gatsby-source-yuque)<br />
VuePress -> [https://github.com/ulivz/vuepress-plugin-yuque](https://github.com/ulivz/vuepress-plugin-yuque)<br />
Hexo -> [https://github.com/x-cold/yuque-hexo](https://github.com/x-cold/yuque-hexo)<br />
完成上面三步后，就可以尝试发布新文章啦！<br />
参考文章<br />
Hexo 博客终极玩法：云端写作，自动部署

