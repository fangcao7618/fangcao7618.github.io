
---

title: create-react-app创建的项目中registerServiceWorker.js文件的作用

date: 2019-07-04 15:08:19 +0800

tags: []

---
使用React官方的脚手架工具create-react-app创建的项目，目录中会存在registerServiceWorker.js这个文件，这个文件的作用是什么呢？<br />这个文件可以使用也可以不使用，使用它可以使你的react项目变成一个PWA（Progressive Web Application）, 也就是说，在线上，只要访问过一次你的网站，下一次即使没有网络，这个应用依然可以被访问。当然，它的好处不仅这么一点点，在移动端打开项目时，如果你用的是chrome或者firefox这样的高级浏览器，浏览器会给你的页面不太一样的显示，你的网页看起来会更像原生App，实际上体验也更爽。<br />在项目的public目录下，存在一个manifest.json文件，你可以在这里对你的网页做一些配置，当用户访问网页，生成一个网页的桌面快捷方式时，会以这个文件中的内容作为图标和文字的显示内容。<br />配置好manifest.json, 使用registerServiceWorker.js，用户完全可以把你的网页快捷方式放到桌面上，因为你的网页此时支持离线访问，所以用起来和原生app的体验很接近。<br />大家可以做这样一个试验：

1. 创建一个项目
1. 运行npm run build
1. 然后在本地开一个服务器，把build目录中的内容放在服务器的根目录下
1. 通过localhost的域名访问服务器
1. 访问过一次之后，断掉网络，重新访问

你会发现，即使没有网络，这个时候依然可以访问你的应用。需要注意的是，只有打包生成线上版本的react项目时，registerServiceWorker.js才会有效。本地开发时，这个文件没什么效果，因为如果本地开发使用这个文件，有可能会因为缓存造成调试问题。<br />还需要注意的是，项目在本地，通过localhost域名访问，支持http协议。如果真正放到线上，如果想让registerServiceWorker.js生效，服务器必须采用https协议，这也是为什么很多同学本地测试好用，线上就不好用的原因。<br />registerServiceWorker.js中的这些功能，并不是React所独创的内容，而是React对PWA的一个实现，PWA未来的发展前景不错，从扩展视野角度也值得大家一看，如果你想了解更多，可以访问PWA的官方手册，这里讲解了PWA底层关于serviceWorker很多的内容，非常有趣：<br />[https://codelabs.developers.google.com/codelabs/your-first-pwapp/#0codelabs.developers.google.com](https://link.zhihu.com/?target=https%3A//codelabs.developers.google.com/codelabs/your-first-pwapp/%230)<br />发布于 2018-02-08<br />[](https://www.zhihu.com/topic/20013159)<br />[React](https://www.zhihu.com/topic/20013159)<br />[](https://www.zhihu.com/topic/20073560)<br />[渐进式网络应用程序（PWA）](https://www.zhihu.com/topic/20073560)

