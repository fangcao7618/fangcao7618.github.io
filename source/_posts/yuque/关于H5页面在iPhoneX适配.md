
---

title: 关于H5页面在iPhoneX适配

date: 2019-06-28 17:06:05 +0800

tags: []

---
<a name="jm68R"></a>
# 1.  iPhoneX的介绍
<a name="J6wrT"></a>
#### **屏幕尺寸**
我们熟知的iPhone系列开发尺寸概要如下：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771746-074f2d6f-568c-4ba3-8c54-fed0db48173c.png#align=left&display=inline&height=328&originHeight=328&originWidth=815&size=0&status=done&width=815)<br />△ iPhone各机型的开发尺寸<br />转化成我们熟知的像素尺寸：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771737-c1dce0c7-48b3-46ef-b26f-8231ff0a54ae.png#align=left&display=inline&height=183&originHeight=183&originWidth=647&size=0&status=done&width=647)<br />△ 每个机型的多维度尺寸<br />倍图其实就是像素尺寸和开发尺寸的倍率关系，但这只是外在的表现。倍图核心的影响因素在于PPI（DPI），了解屏幕密度与各尺寸的关系有助于我们深度理解倍率的概念：[《基础知识学起来！为设计师量身打造的DPI指南》](http://www.uisdc.com/designers-guide-to-dpi)<br />iPhone8在本次升级中，屏幕尺寸和分辨率都遗传了iPhone6以后的优良传统；<br />然而iPhone X 无论是在屏幕尺寸、分辨率、甚至是形状上都发生了较大的改变，下面以iPhone 8作为参照物，看看到底iPhone X的适配我们要怎么考虑。<br />我们看看iPhone X尺寸上的变化：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771631-b0ab8ad2-3f03-4902-8165-a47b1fa9feec.png#align=left&display=inline&height=629&originHeight=629&originWidth=802&size=0&status=done&width=802)
<a name="T9Pab"></a>
## 2.  iPhoneX的适配---安全区域(safe area)
苹果对于 iPhone X 的设计布局意见如下：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771687-fc7146fa-22d7-4fc1-ae55-b85b1f13e398.png#align=left&display=inline&height=311&originHeight=311&originWidth=627&size=0&status=done&width=627)

核心内容应该处于 Safe area 确保不会被设备圆角(corners)，传感器外壳(sensor housing，齐刘海) 以及底部的 Home Indicator 遮挡。也就是说 我们设计显示的内容应该尽可能的在安全区域内；
<a name="jjVyB"></a>
# 3.  iPhoneX的适配---适配方案viewport-fit
<a name="mXXtE"></a>
###     3.1  PhoneX的适配，在iOS 11中采用了viewport-fit的meta标签作为适配方案；viewport-fit的默认值是auto。
　　  viewport-fit取值如下：

|                                                   auto | 默认：viewprot-fit:contain;页面内容显示在safe area内 |
| --- | --- |
|                                                   cover | viewport-fit:cover,页面内容充满屏幕 |

　　    viewport-fit meta标签设置(cover时)<br /> <br /><meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover"><br />
<a name="trt5s"></a>
###     3.2  css constant()函数 与safe-area-inset-top & safe-area-inset-left & safe-area-inset-right & safe-area-inset-bottom的介绍
 ![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771749-fb1d12ce-20f5-4b3a-be0b-60ca67320d3b.png#align=left&display=inline&height=447&originHeight=447&originWidth=892&size=0&status=done&width=892)<br /> 

   如上图所示 在iOS 11中的WebKit包含了一个新的[CSS函数constant()](https://github.com/w3c/csswg-drafts/pull/1817)，以及一组[四个预定义的常量](https://github.com/w3c/csswg-drafts/pull/1819)：safe-area-inset-left, safe-area-inset-right, safe-area-inset-top和 safe-area-inset-bottom。当合并一起使用时，允许样式引用每个方面的安全区域的大小。<br />    3.1当我们设置viewport-fit:contain,也就是默认的时候时;设置safe-area-inset-left, safe-area-inset-right, safe-area-inset-top和 safe-area-inset-bottom等参数时不起作用的。<br />    3.2当我们设置viewport-fit:cover时：设置如下<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771675-32c7c482-3496-4cfc-986a-c8d0e6d86923.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br />body {<br />    padding-top: constant(safe-area-inset-top);   //为导航栏+状态栏的高度 88px            <br />    padding-left: constant(safe-area-inset-left);   //如果未竖屏时为0                <br />    padding-right: constant(safe-area-inset-right); //如果未竖屏时为0                <br />    padding-bottom: constant(safe-area-inset-bottom);//为底下圆弧的高度 34px       <br />}<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771759-50225b3c-6f7a-41cb-a7c6-4908c4090436.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)
<a name="fSJwi"></a>
# 4.   iPhoneX的适配---高度统计
    viewport-fit:cover + 导航栏<br />　　![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771737-029c9ed2-c76e-4d04-be0a-57f1bedb5064.png#align=left&display=inline&height=936&originHeight=936&originWidth=517&size=0&status=done&width=517)<br />
<a name="zJRiF"></a>
# 5.iPhoneX的适配---媒体查询
注意这里采用的是690px(safe area高度)，不是812px;

```css
@media only screen and (width: 375px) and (height: 690px){
    body {
        background: blue;
    }
}
```

<a name="y3XXl"></a>
# 6.iphoneX viewport-fit  问题总结
1.关于iphoneX 页面使用了渐变色时；如果viewport-fit:cover;<br />    1.1在设置了背景色单色和渐变色的区别，如果是单色时会填充整个屏幕，如果设置了渐变色 那么只会更加子元素的高度去渲染；而且页面的高度只有690px高度，上面使用了padding-top:88px;<br />　　![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771781-bf60fc85-74b8-469b-9273-4cefdca5a3e7.png#align=left&display=inline&height=528&originHeight=528&originWidth=563&size=0&status=done&width=563)<br />body固定为：

```html
<body><div class="content">this is subElement</div></body>
```

1.单色时：<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771715-875d1aad-9ade-4566-944f-09a8516bb4e6.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br />       * {<br />           padding: 0;<br />           margin: 0;        <br />       }        <br />       body {<br />           background:green;<br />           padding-top: constant(safe-area-inset-top); //88px            <br />           /*padding-left: constant(safe-area-inset-left);*/            <br />           /*padding-right: constant(safe-area-inset-right);*/            <br />           /*padding-bottom: constant(safe-area-inset-bottom);*/        <br />       }<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771665-9fd3b6a1-3a0a-4a70-b970-bbfd0dc8307e.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br />2.渐变色<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771708-a8c480fa-23bb-4ad9-91ca-d972f94023df.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br />       * {<br />           padding: 0;<br />           margin: 0;<br />       }<br />       body {<br />           background:-webkit-gradient(linear, 0 0, 0 bottom, from(#ffd54f), to(#ffaa22));<br />           padding-top: constant(safe-area-inset-top); //88px<br />           /*padding-left: constant(safe-area-inset-left);*/<br />           /*padding-right: constant(safe-area-inset-right);*/<br />           /*padding-bottom: constant(safe-area-inset-bottom);*/<br />       }<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771720-df50a7fb-f617-4440-b0f1-03c1bdd8906c.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> <br />解决使用渐变色 仍旧填充整个屏幕的方法；CSS设置如下<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712772195-15b0ec18-50fe-406e-8855-a8ecd3eb7534.png#align=left&display=inline&height=536&originHeight=536&originWidth=292&size=0&status=done&width=292)<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771707-e90af427-6f92-410b-8c3b-d73f350866eb.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /><!DOCTYPE html><br /><html><br /><head><br />   <meta name="viewport" content="initial-scale=1, viewport-fit=cover"><br />   <title>Designing Websites for iPhone X: Respecting the safe areas</title><br />   <style>        * {<br />       padding: 0;<br />       margin: 0;<br />   }<br />   html, body {<br />       height: 100%;<br />   }<br />   body {<br />       padding-top: constant(safe-area-inset-top);<br />       padding-left: constant(safe-area-inset-left);<br />       padding-right: constant(safe-area-inset-right);<br />       padding-bottom: constant(safe-area-inset-bottom);<br />   }<br />   .content {<br />       background: -webkit-gradient(linear, 0 0, 0 bottom, from(#ffd54f), to(#ffaa22));<br />       width: 100%;<br />       height: 724px;<br />   }    </style><br /></head><br /><body><br /><div class="content">this is subElement</div><br /></body><br /></html><br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771717-093bf484-fe55-457a-aaca-f34250851412.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> <br />2.页面元素使用了固定定位的适配即：{position:fixed;}<br />        2.1 子元素页面固定在底部时；使用viewport-fit:contain时;可以看到bottom:0时只会显示在安全区域内；<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771764-6addaf58-490c-4018-aaa4-2023b12d993e.png#align=left&display=inline&height=534&originHeight=534&originWidth=285&size=0&status=done&width=285)<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771761-d4ae25ff-4a24-44bc-aba0-06e6be261ee3.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /><!DOCTYPE html><br /><html><br /><head><br />   <meta name="viewport" content="initial-scale=1"><br />   <!--<meta name="viewport" content="initial-scale=1, viewport-fit=cover">--><br />   <title>Designing Websites for iPhone X: Respecting the safe areas</title><br />   <style><br />       * {<br />           padding: 0;<br />           margin: 0;<br />       }<br />       /*html,body {*/<br />           /*height: 100%;*/<br />       /*}*/<br />       body {<br />           background: grey;<br />           /*padding-top: constant(safe-area-inset-top);*/<br />           /*padding-left: constant(safe-area-inset-left);*/<br />           /*padding-right: constant(safe-area-inset-right);*/<br />           /*padding-bottom: constant(safe-area-inset-bottom);*/<br />       }<br />       .top {<br />           width: 100%;<br />           height: 44px;<br />           background: purple;<br />       }<br />       .bottom {<br />           position: fixed;<br />           bottom: 0;<br />           left: 0;<br />           right: 0;<br />           height: 44px;<br />           color: black;<br />           background: green;<br />       }<br />   </style><br /></head><br /><body><br />   <div class="top">this is top</div><br />   <div class="bottom">this is bottom</div><br /></body><br /></html><br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771726-74d83eaf-538d-4353-bd6c-28bb8a2696d0.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> <br />2.1 子元素页面固定在底部时；使用viewport-fit:cover时;可以看到bottom:0时只会显示在安全区域内；<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771852-3cd44b4e-9674-4b00-9434-068bb897a933.png#align=left&display=inline&height=477&originHeight=477&originWidth=236&size=0&status=done&width=236) 

```css
* {

    padding: 0;

    margin: 0;

}

/*html,body {*/

    /*height: 100%;*/

/*}*/

body {

    background: grey;

    padding-top: constant(safe-area-inset-top);

    /*padding-left: constant(safe-area-inset-left);*/

    /*padding-right: constant(safe-area-inset-right);*/

    /*padding-bottom: constant(safe-area-inset-bottom);*/

}

.top {

    width: 100%;

    height: 44px;

    background: purple;

}

.bottom {

    position: fixed;

    bottom: 0;

    left: 0;

    right: 0;

    height: 44px;

    color: black;

    background: green;

}
```

 <br />添加html,body   {width:100%;heigth:100%}<br /> ![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771759-00ecb674-8dbe-4df0-b378-abc4a6891242.png#align=left&display=inline&height=482&originHeight=482&originWidth=706&size=0&status=done&width=706)<br /> <br />图1：<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771795-fe4ebd30-d589-450f-b8bb-28cfc480f498.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> * {<br />           padding: 0;<br />           margin: 0;<br />       }<br />       html,body {<br />           height: 100%;<br />       }<br />       body {<br />           background: grey;<br />           padding-top: constant(safe-area-inset-top);<br />           padding-left: constant(safe-area-inset-left);<br />           padding-right: constant(safe-area-inset-right);<br />           padding-bottom: constant(safe-area-inset-bottom);<br />       }<br />       .top {<br />           width: 100%;<br />           height: 44px;<br />           background: purple;<br />       }<br />       .bottom {<br />           position: fixed;<br />           bottom: 0;<br />           left: 0;<br />           right: 0;<br />           height: 44px;<br />           color: black;<br />           background: green;<br />       }<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771758-465bb57b-e53d-4003-9e6c-06dc4bac77de.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> <br />图2：<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771797-559f89da-8205-439a-a5c9-26ac0014c380.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br />       * {<br />           padding: 0;<br />           margin: 0;<br />       }<br />       html,body {<br />           height: 100%;<br />       }<br />       body {<br />           background: grey;<br />           padding-top: constant(safe-area-inset-top);<br />           padding-left: constant(safe-area-inset-left);<br />           padding-right: constant(safe-area-inset-right);<br />           /*padding-bottom: constant(safe-area-inset-bottom);*/<br />       }<br />       .top {<br />           width: 100%;<br />           height: 44px;<br />           background: purple;<br />       }<br />       .bottom {<br />           position: fixed;<br />           bottom: 0;<br />           left: 0;<br />           right: 0;<br />           height: 44px;<br />           color: black;<br />           background: green;<br />       }<br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771770-ddcc4bfe-ccd0-4232-b6ab-9500ec21aeed.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> <br />2.3 关于alertView弹框 遮罩层的解决方案<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561712771861-983e93a3-1470-426a-8845-79845b963199.png#align=left&display=inline&height=531&originHeight=531&originWidth=277&size=0&status=done&width=277)<br /> <br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771801-fbb4e6b0-d251-4edb-9b3d-7f92e13da6aa.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /><!DOCTYPE html><br /><html lang="en"><br /><head><br />   <meta charset="UTF-8"><br />   <!--<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">--><br />   <meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover"><br />   <meta http-equiv="pragma" content="no-cache"><br />   <meta http-equiv="cache-control" content="no-cache"><br />   <meta http-equiv="expires" content="0"><br />   <title>alertView</title><br />   <script data-res="eebbk"><br />       document.documentElement.style.fontSize = window.screen.width / 7.5 + 'px';<br />   </script><br />   <style><br />       * {<br />           margin: 0;<br />           padding: 0;<br />       }<br />       html,body {<br />           width: 100%;<br />           height: 100%;<br />       }<br />       body {<br />           font-size: 0.32rem;<br />           padding-top: constant(safe-area-inset-top);<br />           padding-left: constant(safe-area-inset-left);<br />           padding-right: constant(safe-area-inset-right);<br />           padding-bottom: constant(safe-area-inset-bottom);<br />       }<br />       .content {<br />           text-align: center;<br />       }<br />       .testBut {<br />           margin: 50px auto;<br />           width: 100px;<br />           height: 44px;<br />           border: 1px solid darkgray;<br />           outline:none;<br />           user-select: none;<br />           background-color: yellow;<br />       }<br />   </style><br />   <link href="alertView.css" rel="stylesheet" type="text/css"><br /></head><br /><body><br />   <section class="content"><br />       <button class="testBut" onclick="showLoading()">弹框加载</button><br />   </section><br />   <script type="text/javascript" src="alertView.js"></script><br />   <script><br />       function showLoading() {<br />           UIAlertView.show({<br />               type:"input",<br />               title:"温馨提示",              //标题<br />               content:"VIP会员即将到期",     //获取新的<br />               isKnow:false<br />           });<br />           var xx = new UIAlertView();<br />          console.log(xx);<br />       }<br />   </script><br /></body><br /></html><br />![](https://cdn.nlark.com/yuque/0/2019/gif/263301/1561712771795-4b5e5119-73b9-43be-9f57-4e1677edd033.gif#align=left&display=inline&height=20&originHeight=20&originWidth=20&size=0&status=done&width=20)<br /> <br />参考资料：<br />　[iPhone X的Web设计](https://www.w3cplus.com/mobile/designing-websites-for-iphone-x.html)<br />   [iPhone X适配没那么复杂，但也不是看上去这么简单](http://www.uisdc.com/iphone-x-adaptive)<br />   [剖析 iOS 11 网页适配问题](https://objcer.com/2017/09/21/Understanding-the-WebView-Viewport-in-iOS-11-iPhone-X/)<br />　[iPhone X(10)屏幕分辨率与适配](http://www.skyfox.org/iphone-x-10-screen-resolution-adaptation.html)<br />   [iPhone X 适配手Q H5 页面通用解决方案](https://cloud.tencent.com/community/article/686372)　

转自：[https://www.cnblogs.com/lolDragon/p/7795174.html](https://www.cnblogs.com/lolDragon/p/7795174.html)


