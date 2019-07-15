
---

title: CSS 与 JS 动画的底层机制 + 如何优化它们的性能

date: 2019-07-09 10:55:41 +0800

tags: []

---

原文链接： [blog.sessionstack.com](https://blog.sessionstack.com/how-javascript-works-under-the-hood-of-css-and-js-animations-how-to-optimize-their-performance-db0e79586216)<br />转载：[https://www.zcfy.cc/article/under-the-hood-of-css-and-js-animations-how-to-optimize-their-performance](https://www.zcfy.cc/article/under-the-hood-of-css-and-js-animations-how-to-optimize-their-performance)

这是致力于探索 JavaScript 及其组件的系列文章中的第 13 篇。在找寻与介绍这些核心组件的过程中，我们也分享了我们在开发[SessionStack](https://www.sessionstack.com/?utm_source=medium&utm_medium=blog&utm_content=js-series-networking-layer-intro)时的一些规则（SessionStack 是一个用来帮助用户实时发现与重现其应用弱点的 JavaScript 应用，因此非常注重鲁棒性与高性能。）<br />如果你没看过之前的文章，可以看一下这里：

- [引擎、运行时、调用栈的介绍](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf?source=collection_home---2------1----------------)<br />
- [Google’s V8 引擎内部 + 如何写优化过代码的5个贴士](https://blog.sessionstack.com/how-javascript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e?source=collection_home---2------2----------------)<br />
- [内存管理 + 处理 4 种常见的内存泄漏](https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec?source=collection_home---2------0----------------)<br />
- [异步编程中的 event loop + 5 个写更好的 async/await 的方法](https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5)<br />
- [深入了解 WebSockets 和 HTTP/2与SSE +如何选择正确的方法](https://blog.sessionstack.com/how-javascript-works-deep-dive-into-websockets-and-http-2-with-sse-how-to-pick-the-right-path-584e6b8e3bf7?source=collection_home---4------0----------------)<br />
- [对 WebAssembly 的比较 + 为什么在某些情况下，它比JavaScript更好](https://blog.sessionstack.com/how-javascript-works-a-comparison-with-webassembly-why-in-certain-cases-its-better-to-use-it-d80945172d79)<br />
- [Web Workers 的组成 + 5 个使用场景](https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a)<br />
- [Service Workers 的生命周期与使用场景](https://blog.sessionstack.com/how-javascript-works-service-workers-their-life-cycle-and-use-cases-52b19ad98b58)<br />
- [Web 推送通知的机制](https://blog.sessionstack.com/how-javascript-works-the-mechanics-of-web-push-notifications-290176c5c55d)<br />
- [使用 MutationObserver 来追踪 DOM 变化](https://blog.sessionstack.com/how-javascript-works-tracking-changes-in-the-dom-using-mutationobserver-86adc7446401)<br />
- [渲染引擎与优化性能小贴士](https://blog.sessionstack.com/how-javascript-works-the-rendering-engine-and-tips-to-optimize-its-performance-7b95553baeda)<br />
- [在网络层之下 + 如何提高网络层的性能与安全性](https://blog.sessionstack.com/how-javascript-works-inside-the-networking-layer-how-to-optimize-its-performance-and-security-f71b7414d34c)<br />
<a name="8HGYL"></a>
### 概览
正如大家所知，动画在创建引人注目的 web 应用程序中扮演着重要的角色。随着用户越来越多地将注意力转移到用户体验上，企业开始意识到完美无缺、令人愉快的用户体验的重要性，web应用程序变得越来越重，并具有更动态的UI。这一切都需要更复杂的动画，以便在在用户的整个使用过程中更流畅地进行状态转换 —— 今天，这甚至被认为不是什么特别的事情。用户正变得越来越高级，默认情况下，他们期望具有快速响应和交互性棒的用户界面。<br />然而，让你的界面动起来并不一定是简单的。什么交互需要动画，什么时候应该动画，动画应该有什么样的感觉，这些都是棘手的问题。
<a name="9v7Gd"></a>
### JavaScript 动画 vs CSS 动画
创建web动画的两种主要方法是使用JavaScript和CSS，两者本身没有对与错。所以这种 PK 完全取决于你想实现什么。
<a name="iU8ez"></a>
#### CSS 动画
想让屏幕上东西动起来的话，最简单的方法就是 CSS 动画。<br />我们从一个小例子开始：把一个元素在 X 和 Y 轴上都位移 50px，通过 CSS transition 来设置一个 1000ms 的动画<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562640949513-0107b5e9-f70f-46c4-93c9-cd6261bf2c41.jpeg#align=left&display=inline&height=40&originHeight=40&originWidth=40&size=0&status=done&width=40)<br />当 move class 被添加上时，transform 值被改变，运动开始了<br />除了过渡时间（transition duration），还有一个 缓动（easing） 选项，这就完成了动画了。我们将会在下面进一步介绍缓动<br />如果您像上面的代码片段一样创建单独的CSS类来管理动画，那么您可以使用JavaScript来切换每个动画。<br />如果你有以下元素:<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562640949324-9edabe70-ba91-4147-a9cb-d1d85801f63c.jpeg#align=left&display=inline&height=40&originHeight=40&originWidth=40&size=0&status=done&width=40)<br />然后你可以使用JavaScript来切换每个动画的开关:<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562640949209-60cff598-b982-4a4d-9d15-8bf669e619b1.jpeg#align=left&display=inline&height=40&originHeight=40&originWidth=40&size=0&status=done&width=40)<br />上面的代码片段获取box类的所有元素，并添加move类以触发动画。<br />这样做会给你的应用提供很好的平衡。您可以专注于使用JavaScript管理状态，并简单地在目标元素上设置适当的类，让浏览器处理动画。然后，您可以侦听元素上的transitionend事件，但前提是您能够放弃对Internet Explorer旧版本的支持：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948303-243cc372-0fae-4b99-a5db-edbc55954242.png#align=left&display=inline&height=452&originHeight=452&originWidth=1177&size=0&status=done&width=1177)<br />侦听在转换结束时触发的转换事件，如下所示：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562640949950-17d15077-ab72-4223-bee7-4f9e8d8a00f3.jpeg#align=left&display=inline&height=40&originHeight=40&originWidth=40&size=0&status=done&width=40)<br />除了使用CSS转换，您还可以使用CSS动画（animation），这允许您对单个动画关键帧（keyframes）、持续时间和迭代（iterations）有更多的控制。
> 关键帧用于指示浏览器在给定的点上CSS属性需要具有哪些值，并填补空白。

让我们看一个例子:<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562640949575-10f6bb9f-6465-4a1e-9fd9-dfa58d22baca.jpeg#align=left&display=inline&height=40&originHeight=40&originWidth=40&size=0&status=done&width=40)<br />这是它的样子(quick demo)—— [https://sessionstack.github.io/blog/demos/keyframes/](https://sessionstack.github.io/blog/demos/keyframes/)<br />使用CSS动画，您可以将定义动画与元素本身分离开，并使用animation-name属性选择所需的动画。<br />CSS动画有时还需要加供应商前缀，在Safari、Safari Mobile和Android中使用-webkit。Chrome、Opera、Internet Explorer和Firefox都没有前缀。许多工具可以帮助您创建所需CSS的前缀版本，允许您在源文件中编写无前缀版本。
<a name="aluUZ"></a>
#### JavaScript 动画
与使用CSS转换或动画相比，使用JavaScript创建动画更加复杂，但它通常会为开发人员提供更强大的功能。<br />JavaScript动画是作为代码的一部分编写的。您还可以将它们封装在其他对象中。要重新创建前面描述的CSS转换，可以用 JavaScript 这么搞：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562640949677-cb3243ba-9ead-4410-90ab-f4e801120d7c.jpeg#align=left&display=inline&height=40&originHeight=40&originWidth=40&size=0&status=done&width=40)<br />默认情况下，Web动画只修改元素的表示。如果您想让您的对象保持在它被移动到的位置，那么您应该在动画完成时修改它的底层样式。这就是为什么我们在上面的例子中监听 finish 事件，并设置 box.style。将属性转换为相等的translate(150px, 200px)，这与动画执行的第二个转换相同。<br />使用JavaScript动画，您可以在每一步完全控制元素的样式。这意味着您可以减慢动画、暂停动画、停止动画、反转动画，并根据需要操作元素。如果您正在构建复杂的、面向对象的应用程序，这尤其有用，因为这时你往往需要对动画有一个更好的封装。
<a name="1hhc9"></a>
### 缓动是什么？
更自然的动效能让用户对你的web应用程序感到更舒服，从而带来更好的用户体验。<br />在大自然中，其实没有什么东西是从一点线性地移动到另一点的。事实上，因为我们不是在真空中，会有不同的因素导致物体在我们周围的物理世界中运动时会加速或减速。人类的大脑天生就期待这种运动，所以当你在为网络应用程序制作动画时，你应该充分理解这一点。<br />有一些术语你需要理解:

- “ease in” — 这是一个开始缓慢，然后加速的运动。<br />
- “ease out” —这是一个开始很快，然后减速的运动<br />

这两者可以组合在一起，例如 “ease in out”.<br />缓动让你的动画看起来更自然。
<a name="i2m3c"></a>
#### 缓动的关键词
CSS转换和动画允许您选择您想要使用的缓动类型。有不同的关键字影响缓动效果。你也可以完全定制自己的缓动动画。<br />下面是一些你可以在CSS中使用的缓动关键字：

- linear（线性）<br />
- ease-in（加速）<br />
- ease-out（减速）<br />
- ease-in-out（先加速后减速）<br />

让我们把它们通读一遍，看看它们到底是什么意思。
<a name="IjQaF"></a>
#### Linear 动画
没有任何缓动效果的动画称为线性（linear）动画。<br />下面是线性变化的示意图：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948629-88fab868-0bf0-4d3b-b038-64100b7231d0.png#align=left&display=inline&height=560&originHeight=560&originWidth=560&size=0&status=done&width=560)<br />随着时间的推移，值均匀变大。线性运动时，物体往往会看起来不自然。一般来说，你应该避免线性运动。<br />这是一个线性动画的简单实现:
<a name="rERFK"></a>
#### 减速(Ease-out) 动画
正如前面提到的，与线性动画相比，缓动会使动画开始得更快，而在最后会变慢。它的示意图是这样的：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948365-06c4e5c3-ed56-42b5-9106-fe63877c50db.png#align=left&display=inline&height=506&originHeight=506&originWidth=503&size=0&status=done&width=503)<br />一般来说，对于UI工作来说，减速缓动效果最好，因为快速的开始会给动画一种响应的感觉，而结尾的慢速则可以理解为是运动末尾的自然效果。<br />有很多方法可以达到放松效果，但最简单的是CSS中的 easy-out 关键字:
```
transition: transform 500ms ease-out;
```
<a name="5iisN"></a>
#### 加速(Ease-in)动画
这与减速（ease-out）动画相反——开始慢，结束快。这是示意图：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948518-0aaa96c8-4bea-4e26-a0a9-5b0b13378dd4.png#align=left&display=inline&height=556&originHeight=556&originWidth=553&size=0&status=done&width=553)<br />与减速缓动动画相比，加速缓动动画会给人一种不寻常的感觉，因为它们启动缓慢，会产生一种无响应的感觉。结束时运动很快也会让用户产生一种奇怪的感觉，因为现实世界中的物体在趋于停止时往往会减速。<br />要使用加速缓动动画，与使用减速缓动与线性动画一样，你可以用如下关键字：
```
transition: transform 500ms ease-in;
```
<a name="axBu2"></a>
#### （先加速后减速）Ease-in-out 动画
这个动画是加速动画和减速动画的结合。示意图如下：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948316-a338afe9-6b38-44be-ad1a-8739de81059b.png#align=left&display=inline&height=508&originHeight=508&originWidth=504&size=0&status=done&width=504)<br />不要让动画持续时间太长，因为这会让你的 UI 看起来像是没有响应。<br />要使用先加速后减速动画, 可以使用如下关键字：
```
transition: transform 500ms ease-in-out;
```
<a name="efwws"></a>
#### 自定义缓动
您可以定义自己的缓动曲线，以更好的控制缓动效果。<br />事实上， ease-in, ease-out, linear, ease 关键字都是在 [贝塞尔曲线（Bézier curves）](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) 预定义好的, 这三个关键字对应的曲线在 [CSS transitions specification](http://www.w3.org/TR/css3-transitions/) 与 [Web Animations specification](https://w3c.github.io/web-animations/#scaling-using-a-cubic-bezier-curve) 都有详细的说明
<a name="uSA4G"></a>
#### 贝塞尔曲线（Bézier curves）
让我们看看贝塞尔曲线的是怎么工作的。一条贝塞尔曲线需要四个值，或者更准确地说，它需要两对数字。每一对描述了贝塞尔曲线控制点的X和Y坐标。Bezier曲线的起始点坐标为(0,0)，结束点坐标为(1,1)。这两个控制点的X值必须在[0,1]范围内，而虽然规范没有明确具体是多少，但每个控制点的Y值是可以超过[0,1]限制的。<br />即使每个控制点的X和Y值稍有变化，也会得到完全不同的曲线。让我们来看看两幅贝塞尔曲线的图形，这两幅曲线上的点虽然距离很近，但坐标不同。<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948334-e9d499f4-b652-4f3c-8c62-2b5643bb184f.png#align=left&display=inline&height=510&originHeight=510&originWidth=509&size=0&status=done&width=509)<br />再看这个：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948269-17f7e2d2-4cde-42cf-a0dc-8758e193093a.png#align=left&display=inline&height=514&originHeight=514&originWidth=513&size=0&status=done&width=513)<br />如你所见，这两张图大相径庭。第一个控制点有(0.045,0.183)的向量差，第二个控制点有(-0.427，-0.054)的向量差。<br />第二个曲线的CSS是这样的:
```
transition: transform 500ms cubic-bezier(0.465, 0.183, 0.153, 0.946);
```
前两个数字是第一个控制点的X和Y坐标，后两个数字是第二个控制点的X和Y坐标。
<a name="VFVcq"></a>
### 性能优化
动画应该保持60fps，否则会对用户体验造成负面影响。<br />和世界上的其他事物一样，动画也不是没有代价的。动画的一些属性要比其他属性代价更小一些。例如，动画元素的宽度和高度会改变其几何形状，并可能导致页面上的其他元素移动或改变大小。这个过程称为布局。我们在[之前的一篇文章](https://blog.sessionstack.com/how-javascript-works-the-rendering-engine-and-tips-to-optimize-its-performance-7b95553baeda)中更详细地讨论了布局和渲染。<br />通常，您应该避免动画的属性触发 reflow 或 repaint。对于大多数现代浏览器，这意味着将动画限制在了 opacity 和 transform 上。
<a name="piQ0f"></a>
#### Will-change
您可以使用will-change通知浏览器您打算更改元素的属性。这允许浏览器在进行更改之前进行最适当的优化。但是，不要过度使用will-change，因为这样做会导致浏览器浪费资源，从而导致更多的性能问题。<br />为 transforms 和 opacity 添加 will-change 如下所示:
```
.box {
  will-change: transform, opacity;
}
```
这项特性在 Chrome、Firefox和Opera 中都支持的很好。<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948404-1df85592-95b3-48c3-a31e-47633135aea3.png#align=left&display=inline&height=580&originHeight=580&originWidth=1175&size=0&status=done&width=1175)
<a name="VRgwd"></a>
#### 在 JavaScript 与 CSS 中的选择
你可能已经预料到了——这个问题没有正确答案。你只需要记住以下几件事：

- 基于css的动画，以及原生支持的Web动画，通常在名为“合成线程”的线程上处理。它不同于浏览器的“主线程”，在“主线程”中执行样式、布局、绘制和JavaScript。这意味着，如果浏览器在主线程上运行一些昂贵的任务，这些动画可以继续运行而不会被中断。<br />
- transforms 与 opacity 的变化，在很多情况下，也可以被合成线程来处理。<br />
- 如果任何动画触发了 repaint 、reflow 或两者，则需要“主线程”来完成工作。无论动画基于CSS，还是基于 JavaScript，都是如此，repaint 或 reflow 的开销可能大过你的 CSS 和 JavaScript 执行逻辑，从而使动画本身变得毫无意义。<br />
<a name="2kT2B"></a>
#### 选择合适的东西来制作动画
很棒的动画可以为你的用户添加乐趣和互动性。你可以对你喜欢的任何东西(无论宽度、高度、位置、颜色或背景)加动画，但你需要注意潜在的性能瓶颈。选择不当的动画会对用户体验产生负面影响，因此动画需要有效而适度。动画越少越好。动画只是为了让你的用户体验感觉自然，但不要过度动画。
<a name="YdnBj"></a>
#### 使用动画来支持交互
不要因为你能做就去做动画。相反，你的目的是使用巧妙的动画来加强用户交互。要避免你的动画不必要地打断或阻碍了用户活动。
<a name="QTVHm"></a>
#### 避免动画的那些昂贵属性
唯一比动画放置不当更糟的是那些导致页面卡顿的动画。这种类型的动画会让用户非常不爽。<br />在[SessionStack](https://www.sessionstack.com/?utm_source=medium&utm_medium=blog&utm_content=js-series-rendering-engine-outro)中使用动画非常简单。一般来说，我们遵循上面提到的实践，但是由于UI的复杂性，我们也有更多使用动画的场景。SessionStack必须将终端用户在浏览web应用程序时遇到问题时发生的一切重建为视频。为此，SessionStack 仅利用我们的库在会话期间收集的数据：用户事件、DOM更改、网络请求、异常、调试消息等。我们的播放器经过高度优化，能够正确呈现和使用收集到的所有数据，以便从视觉和技术角度对终端用户的浏览器及其中发生的一切进行像素级的完美模拟。<br />为了确保复制的感觉是自然的，特别是在用户会话又长又重的情况下，我们使用动画来适当地指示加载/缓冲，并遵循关于如何实现它们的最佳实践，这样我们就不会占用太多CPU时间，让 event loop 保持空闲来呈现会话。<br />如果你愿意，有一个免费的计划 [试一试 sessionstack](https://www.sessionstack.com/signup/).<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562640948382-d2e30576-fc4b-423b-aa3f-7617cef54622.png#align=left&display=inline&height=458&originHeight=458&originWidth=880&size=0&status=done&width=880)
<a name="B3H65"></a>
#### 资源

- [https://developers.google.com/web/fundamentals/design-and-ux/animations/css-vs-javascript](https://developers.google.com/web/fundamentals/design-and-ux/animations/css-vs-javascript)<br />
- [https://developers.google.com/web/fundamentals/design-and-ux/animations/](https://developers.google.com/web/fundamentals/design-and-ux/animations/)<br />
- [https://developers.google.com/web/fundamentals/design-and-ux/animations/animations-and-performance](https://developers.google.com/web/fundamentals/design-and-ux/animations/animations-and-performance)<br />

