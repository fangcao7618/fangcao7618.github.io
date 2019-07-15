
---

title: 是时候开始使用 CSS 自定义属性了

date: 2019-07-09 11:37:13 +0800

tags: []

---
原文链接： [www.smashingmagazine.com](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/)<br />在今天，css预加载已经成为了前端开发的一个标准。预加载的一个主要优势就是可以让你使用变量。它可以让你避免复制黏贴你的代码，并且简化了开发和重构。<br />我们用预加载来存储颜色、字体偏好，布局的细节——几乎是我们在css里面用到的所有东西。<br />但是预加载的变量有一些使用上的限制：

- 你不能动态的改变他们。<br />
- 他们不能认出DOM结构。<br />
- 他们不能用JavaScript读取和改变。<br />

为了解决这样或那样的问题，社区发明了CSS自定义属性。本质上这看上去和实现起来就像CSS变量。并且他们的实现方式就像他们的名字一样。<br />自定义属性为前端开发打开了新的大门。
<a name="jhZij"></a>
#### 深入阅读:

- [A Detailed Introduction To Custom Elements](https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/)<br />
- [Houdini: Maybe The Most Exciting Development In CSS You’ve Never Heard Of](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/)<br />
- [Turn Your AMP Up To 11: Everything You Need To Know About Google’s Accelerated Mobile Pages](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)<br />
- [A Better iOS Architecture: A Deep Look At The Model-View-Controller Pattern](https://www.smashingmagazine.com/2016/05/better-architecture-for-ios-apps-model-view-controller-pattern/)<br />
<a name="FfsAY"></a>
### 申明和使用自定义属性的语法
在你开始学习心得预处理器或者框架的使用通常的问题是你必须学习新的语法。<br />每一种预处理器都使用不同的方法申明变量。通常使用一个保留字符作为开始——举个例子，Sass的`$`、LESS的`@`。<br />CSS自定义属性同样也是用保留字符 `--`来引入声明。但是好处是你只需要学一遍语法就能在所有浏览器上使用。<br />你可能会问，“为什么不使用已经有的语法？”<br />[这是有原因的](http://www.xanthir.com/blog/b4KT0)。简单来说这提供了一种在任何预处理器中使用自定义属性的方式。在这种方式下我们可以使用自定义属性，预处理器也不会编译他们，所以这些属性会直接输出到编译后的CSS中。并且你也可以重复使用预处理器变量在源文件中，这个我稍后会细说。<br />（关于这个名字：因为他们的想法和目标非常相似，有些时候自定义属性被叫做CSS变量，尽管正确名称叫CSS自定义属性，往下读你就会明白为什么这个名字是最正确的。）<br />所以要声明一个变量来代替常用的CSS属性，就像`color`或者`padding`，用`--`连接一个自定义名称属性就可以：
```
.box{
  --box-color: #4d4e53;
  --box-padding: 0 10px;
}
```
属性的值可以是任何有效的CSS值：颜色、字符串、布局甚至是表达式。<br />这里是有效的自定义属性的例子：
```
:root{
  --main-color: #4d4e53;
  --main-bg: rgb(255, 255, 255);
  --logo-border-color: rebeccapurple;
  --header-height: 68px;
  --content-padding: 10px 20px;
  --base-line-height: 1.428571429;
  --transition-duration: .35s;
  --external-link: "external link";
  --margin-top: calc(2vh + 20px);
  /* Valid CSS custom properties can be reused later in, say, JavaScript. */
  --foo: if(x > 5) this.width = 10;
}
```
以防万一你不知道什么是[`:root`](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)匹配，在HTML里他就等同与`html`标签，但是具有更高的特异性。<br />自定义属性和其他的CSS属性一样是**动态的、级联的**。这意味着他们能在任何时候被改变是由浏览器来进行的。<br />为了使用自定义的变量，你需要使用`var()`CSS函数，并且提供属性参数：
```
.box{
  --box-color:#4d4e53;
  --box-padding: 0 10px;
  padding: var(--box-padding);
}
.box div{
  color: var(--box-color);
}
```
<a name="xQz5A"></a>
#### 声明和用例
`var()`函数有一个非常便利的提供默认值的方法。如果你不确信自定义属性已经被定义并且需要一个默认值，函数的第二个参数用来作为默认值的:
```
.box{
  --box-color:#4d4e53;
  --box-padding: 0 10px;
  /* 10px is used because --box-margin is not defined. */
  margin: var(--box-margin, 10px);
}
```
你可能会希望在声明新的变量的时候能重复使用已有的变量值：
```
.box{
  /* The --main-padding variable is used if --box-padding is not defined. */
  padding: var(--box-padding, var(--main-padding));
  --box-text: 'This is my box';
  /* Equal to --box-highlight-text:'This is my box with highlight'; */
  --box-highlight-text: var(--box-text)' with highlight';
}
```
<a name="AzPdr"></a>
### 运算：+，-，*，/
既然我们习惯使用预处理器和其他语言，我们也希望在处理变量的时候能使用基本运算。为了达到这个目的，CSS提供了`calc()`函数，作用当自定义属性的值被改变的时候浏览器会重新计算表达式：
```
:root{
  --indent-size: 10px;
  --indent-xl: calc(2*var(--indent-size));
  --indent-l: calc(var(--indent-size) + 2px);
  --indent-s: calc(var(--indent-size) - 2px);
  --indent-xs: calc(var(--indent-size)/2);
}
```
特别是当你想用一个没有单位的值得时候，就需要使用`calc()`函数：
```
:root{
  --spacer: 10;
}
.box{
  padding: var(--spacer)px 0; /* DOESN'T work */
  padding: calc(var(--spacer)*1px) 0; /* WORKS */
}
```
<a name="IGQX3"></a>
### 作用域和继承
在讨论CSS自定义属性的作用域之前，我们先来回顾一下JavaScript和预处理器的作用域。这样就能更好的认识他们之间的区别。<br />我们知道在JavaScript中如果在函数中使用`var`关键字声明变量，那么他的作用域就在函数里面。<br />同样的我们可以使用`let`和`const`关键字，但他们的作用域相对于变量的块作用域。<br />在JavaScript中**闭包(closure)**是一个可以访问外部函数变量的函数——作用域链。闭包有三个作用域链：

- 它自己的作用域（即 变量定义在大括号中）<br />
- 外部函数的变量<br />
- 全局变量<br />

[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562643459664-38b81b95-1fab-48f0-8f32-2126df61ae0a.png#align=left&display=inline&height=274&originHeight=274&originWidth=780&size=0&status=done&width=780)](https://www.smashingmagazine.com/wp-content/uploads/2017/03/closure-large-opt.png)<br />([View large version](https://www.smashingmagazine.com/wp-content/uploads/2017/03/closure-large-opt.png))<br />预处理器也是相同的，让我们用Sass来举个例子。因为这大概是今天最流行的预处理器了。<br />在Sass中有两种类型的变量：当前作用域变量(local) 和 全局变量。<br />一个全局变量能被申明在选择器和构造器（比如mixin）外，其他的变量就是当前作用域变量。<br />任何嵌套的代码块都可以访问封闭变量（如JavaScript）。<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562643459623-6ac49512-eb53-4c0c-abaf-595db2d836b6.png#align=left&display=inline&height=277&originHeight=277&originWidth=780&size=0&status=done&width=780)](http://p0.qhimg.com/t018daff8e304548675.png)<br />([View large version](http://p0.qhimg.com/t0142128dbd574e0452.png))<br />这意味着在Sass中变量的作用域完全依赖代码的嵌套结构。<br />然而CSS自定义属性完全和其他的CSS属性一样使用级联方式默认继承。<br />当然你也不能在CSS中定义一个在选择器外的属于全局的自定义属性变量，因为这不是有效的CSS。自定义属性的全局作用域实际上就是`:root`的作用域，这里面定义的属性就是全局的。<br />让我们用已知的语法知识和Sass的例子来创建一个使用原生的CSS自定义属性的例子，首先是HTML：
```
global
<div class="enclosing">
  enclosing
  <div class="closure">
    closure
  </div>
</div>
```
然后是CSS:
```
:root {
  --globalVar: 10px;
}
.enclosing {
  --enclosingVar: 20px;
}
.enclosing .closure {
  --closureVar: 30px;
  font-size: calc(var(--closureVar) + var(--enclosingVar) + var(--globalVar));
  /* 60px for now */
}
```
在CODEPEN中查看代码 [css-custom-properties-time-to-start-using 1](http://codepen.io/malyw/pen/MJmebz/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).
<a name="i7hP5"></a>
#### 对自定义属性的更改将立即应用于所有实例
到目前为止我们还没有看出他和Sass变量有什么区别。然而让我们重新给变量赋值：<br />在Sass中，是无效的：
```
.closure {
  $closureVar: 30px; // local variable
  font-size: $closureVar +$enclosingVar+ $globalVar;
  // 60px, $closureVar: 30px is used
  $closureVar: 50px; // local variable
}
```
在CODEPEN中查看代码 [css-custom-properties-time-to-start-using 3](http://codepen.io/malyw/pen/bgWerv/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).<br />但是在CSS中计算的值改变了。因为`font-size`的值因为`--closureVar`值得改变重新计算了：
```
.enclosing .closure {
  --closureVar: 30px;
  font-size: calc(var(--closureVar) + var(--enclosingVar) + var(--globalVar));
  /* 80px for now, --closureVar: 50px is used */
  --closureVar: 50px;
}
```
在CODEPEN中查看代码 [css-custom-properties-time-to-start-using 2](http://codepen.io/malyw/pen/WRjxOy/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).<br />这是第一个非常大的区别：如果你对自定义属性重新赋值，浏览器会重新计算**所有的变量**和`calc()`表达式。
<a name="Ifzc8"></a>
#### 预处理器不能识别DOM结构
假如我们想在除了`class`是`highlighted`的`div`上使用默认的`font-size`<br />下面是 HTML代码：
```
<div class="default">
  default
</div>
<div class="default highlighted">
  default highlighted
</div>
```
让我们使用CSS自定义属性：
```
.highlighted {
  --highlighted-size: 30px;
}
.default {
  --default-size: 10px;
  /* Use default-size, except when highlighted-size is provided. */
  font-size: var(--highlighted-size, var(--default-size));
}
```
因为第二个`div`元素使用了`highlighted`类，在`highlighted`类上的属性就提供给这个元素了。<br />在这里就意味着，`--hightlighted-size: 30px`被提供了。是的font-size的属性被重新赋值了。<br />一切都是这么直截了当的运行：<br />在CODEOPEN上查看代码 [css-custom-properties-time-to-start-using 4](http://codepen.io/malyw/pen/ggWMvG/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).<br />接下来让我们尝试使用Sass来实现同样的例子：
```
.highlighted {
  $highlighted-size: 30px;
}
.default {
  $default-size: 10px;
  /* Use default-size, except when highlighted-size is provided. */
  @if variable-exists(highlighted-size) {
    font-size: $highlighted-size;
  }
  @else {
    font-size: $default-size;
  }
}
```
结果显示他们都使用默认字体大小：<br />在CODEOPEN上查看代码 [css-custom-properties-time-to-start-using 5](http://codepen.io/malyw/pen/PWmzQO/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).<br />这是因为所有的Sass的计算和进程都发生在编译过程中，所以理所当然的他不知道DOM结构，所以依赖代码结构。<br />如你所见自定义属性在变量作用域和通常的css级联样式上具有优势。并且能够识别DOM结构。和普通的CSS属性使用相同的语法规则。<br />第二个例外是CSS自定义属性能**动态的识别DOM结构**
<a name="gGEvQ"></a>
### CSS关键字和`all`属性
CSS自定义属性遵守与常规CSS自定义属性相同的规则。这意味着您可以为其分配任何常见的CSS关键字：

- `inherit`

此CSS关键字应用元素的父对象的值。

- `initial`

这将应用CSS规范中定义的初始值（空值，或在某些CSS自定义属性的情况下）。

- `unset`

在自定义属性中，如果属性是继承的，则应用继承的值，如果属性是初始化的值，则引用初始化值。

- `revert`

这会将该属性重置为用户代理样式表建立的默认值（在CSS自定义属性的情况下为空值）。<br />以下是例子：
```
.common-values{
  --border: inherit;
  --bgcolor: initial;
  --padding: unset;
  --animation: revert;
}
```
我们来看另外一个例子。假设你想构建一个组件，并且想要确保没有其他样式或自定义属性被无意中应用（在这种情况下，通常会使用模块化的CSS解决方案）。<br />现在还有另一种方法：使用[`all`CSS属性](https://developer.mozilla.org/en/docs/Web/CSS/all)。这个简写将重置所有CSS属性。<br />与CSS关键字一起，我们可以执行以下操作：
```
.my-wonderful-clean-component{
  all: initial;
}
```
这会为我们的组件重置所有的样式：<br />不幸的是，`all`关键字[不会重置自定义属性](https://drafts.csswg.org/css-variables/#defining-variables)。[关于是否添加 `--` 前缀](https://github.com/w3c/webcomponents/issues/300#issuecomment-144551648)，这将重置所有CSS自定义属性，正在进行讨论。<br />所以在将来，一个完整的重置会是这样的：
```
.my-wonderful-clean-component{
  --: initial; /* reset all CSS custom properties */
  all: initial; /* reset all other CSS styles */
}
```
<a name="1AJWa"></a>
### CSS自定义属性用例
有许多自定义属性使用的方式，在这里我会展示他们中最有趣的部分。
<a name="2w1B7"></a>
#### 模拟不存在的CSS规则
这些CSS变量的名称是自定义属性，那为什么我们不能用它来模拟不存在的CSS属性？<br />有很多比如`translateX/Y/Z`,`background-repeat-x/y`(仍然不能跨浏览器兼容)，`box-shadow-color`。<br />让我们试着模拟最后一个属性。在这个例子里当`hover`的时候我们改变`box-shadow`的颜色。我们只想遵循DRY规则（不要重复你自己），所以我们只是改变它的颜色，而不是在：hover部分重复box-shadow的整个值。（变量的改变会重新计算`var()`和`calc()`）
```
.test {
  --box-shadow-color: yellow;
  box-shadow: 0 0 30px var(--box-shadow-color);
}
.test:hover {
  --box-shadow-color: orange;
  /* Instead of: box-shadow: 0 0 30px orange; */
}
```
在CODEOPEN上查看代码 [Emulating “box-shadow-color” CSS property using CSS Custom Properties](http://codepen.io/malyw/pen/KzZXRq/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).
<a name="7vXh1"></a>
#### 颜色主题
自定义属性有一个最常用的用例就是应用程序中的颜色主题。自定义属性就是用来解决这类问题的。所以，让我们为一个组件提供一个简单的颜色主题（应用程序可以遵循相同的步骤）。<br />这是button组件的[代码](https://codepen.io/malyw/pen/XpRjNK)：
```
.btn {
  background-image: linear-gradient(to bottom, #3498db, #2980b9);
  text-shadow: 1px 1px 3px #777;
  box-shadow: 0px 1px 3px #777;
  border-radius: 28px;
  color: #ffffff;
  padding: 10px 20px 10px 20px;
}
```
我们假设要反转颜色主题。<br />第一步是将所有颜色变量扩展到CSS自定义属性并重写我们的组件。[重写后的代码](https://codepen.io/malyw/pen/EZmgmZ)：
```
.btn {
  --shadow-color: #777;
  --gradient-from-color: #3498db;
  --gradient-to-color: #2980b9;
  --color: #ffffff;
  background-image: linear-gradient(
    to bottom,
    var(--gradient-from-color),
    var(--gradient-to-color)
  );
  text-shadow: 1px 1px 3px var(--shadow-color);
  box-shadow: 0px 1px 3px var(--shadow-color);
  border-radius: 28px;
  color: var(--color);
  padding: 10px 20px 10px 20px;
}
```
这有我们需要的一切。使用它，我们可以将颜色变量重写为反转值，并在需要时应用它们。例如，我们可以添加全局`inverted`类（例如，body元素），并在应用颜色时更改颜色：
```
body.inverted .btn{
  --shadow-color: #888888;
  --gradient-from-color: #CB6724;
  --gradient-to-color: #D67F46;
  --color: #000000;
}
```
以下是一个演示，您可以在其中单击一个按钮来添加和删除全局类：[demo](http://codepen.io/malyw/pen/dNWpRd)<br />在CODEOPEN中查看代码 [css-custom-properties-time-to-start-using 9](http://codepen.io/malyw/pen/dNWpRd/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).<br />如果不重复代码，在CSS预处理器中无法实现此行为。使用预处理器，您将始终需要覆盖实际的值和规则，这往往会导致额外的CSS。<br />使用CSS自定义属性，解决方案可以尽可能的干净，复制黏贴是可以避免的。因为只需要对变量进行重新赋值。
<a name="wqHD0"></a>
### 在JavaScript中使用自定义属性
以前，要将数据从CSS发送到JavaScript，我们经常不得不采取[技巧](https://blog.hospodarets.com/passing_data_from_sass_to_js)，通过CSS输出中的纯JSON编写CSS值，然后从JavaScript读取它。<br />现在，我们可以轻松地使用JavaScript中的CSS变量进行交互，使用众所周知的`.getPropertyValue()`和`.setProperty()`方法读取和写入它们，这些方法用于通常的CSS属性:
```
/**
* Gives a CSS custom property value applied at the element
* element {Element}
* varName {String} without '--'
*
* For example:
* readCssVar(document.querySelector('.box'), 'color');
*/
function readCssVar(element, varName){
  const elementStyles = getComputedStyle(element);
  return elementStyles.getPropertyValue(`--${varName}`).trim();
}
/**
* Writes a CSS custom property value at the element
* element {Element}
* varName {String} without '--'
*
* For example:
* readCssVar(document.querySelector('.box'), 'color', 'white');
*/
function writeCssVar(element, varName, value){
  return element.style.setProperty(`--${varName}`, value);
}
```
假设我们有一系列的媒体查询值
```
.breakpoints-data {
  --phone: 480px;
  --tablet: 800px;
}
```
因为我们只想在JavaScript中重用它们 - 例如，在[Window.matchMedia()](https://developer.mozilla.org/en/docs/Web/API/Window/matchMedia)中，我们可以轻松地从CSS中获取它们
```
const breakpointsData = document.querySelector('.breakpoints-data');
// GET
const phoneBreakpoint = getComputedStyle(breakpointsData)
  .getPropertyValue('--phone');
```
为了展示如何从JavaScript分配自定义属性，我创建了一个交互式3D CSS 立方体demo，以响应用户操作。<br />这不是很难我们只需要添加一个简单的背景，然后放置五个立方体面与transform属性的相关值：translateZ（），translateY（），rotateX（）和rotateY（）。<br />为了提供正确的视角，我向页面添加了以下内容：
```
#world{
  --translateZ:0;
  --rotateX:65;
  --rotateY:0;
  transform-style:preserve-3d;
  transform:
    translateZ(calc(var(--translateZ) * 1px))
    rotateX(calc(var(--rotateX) * 1deg))
    rotateY(calc(var(--rotateY) * 1deg));
}
```
唯一缺少的是交互性。当鼠标移动时，演示应该更改X和Y视角（--rotateX和-rotateY），当鼠标滚动（--translateZ）时应该放大和缩小）。<br />这是JavaScript的诀窍：
```
// Events
onMouseMove(e) {
  this.worldXAngle = (.5 - (e.clientY / window.innerHeight)) * 180;
  this.worldYAngle = -(.5 - (e.clientX / window.innerWidth)) * 180;
  this.updateView();
};
onMouseWheel(e) {
  /*…*/
  this.worldZ += delta * 5;
  this.updateView();
};
// JavaScript -> CSS
updateView() {
  this.worldEl.style.setProperty('--translateZ', this.worldZ);
  this.worldEl.style.setProperty('--rotateX', this.worldXAngle);
  this.worldEl.style.setProperty('--rotateY', this.worldYAngle);
};
```
现在，当用户移动鼠标时，演示会更改视图。您可以通过移动鼠标并使用鼠标滚轮放大和缩小来检查：[demo](http://codepen.io/malyw/pen/xgdEQp)<br />在CODEOPEN中查看代码 [css-custom-properties-time-to-start-using 10](http://codepen.io/malyw/pen/xgdEQp/) by Serg Hospodarets ([@malyw](http://codepen.io/malyw)) on [CodePen](http://codepen.io/).<br />基本上，我们只是更改了CSS自定义属性的值。其他（旋转和放大和缩小）都是由CSS完成的。<br />**提示：**调整CSS自定义属性值的最简单方法之一就是在CSS生成的内容中显示其内容（在简单的情况下，例如使用字符串），以便浏览器将自动显示当前应用的值：
```
body:after {
  content: '--screen-category : 'var(--screen-category);
}
```
您可以在纯CSS[演示](https://codepen.io/malyw/pen/oBWMOY)（无HTML或JavaScript）中查看。 （调整窗口大小，查看浏览器会自动反映更改后的CSS自定义属性值。）
<a name="HC4os"></a>
### 浏览器支持
[主流浏览器](http://caniuse.com/#feat=css-variables)都支持了CSS自定义属性:<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562643460103-53244213-ae1c-4422-89b0-9de4f446e59a.png#align=left&display=inline&height=412&originHeight=412&originWidth=780&size=0&status=done&width=780)](https://www.smashingmagazine.com/wp-content/uploads/2017/04/css-variables-large-opt.png)<br />([View large version](https://www.smashingmagazine.com/wp-content/uploads/2017/04/css-variables-large-opt.png))<br />这意味着你可以自己开始使用它们。<br />如果您需要支持旧版浏览器，您可以学习语法和使用示例，并考虑并行切换或使用CSS和预处理器变量的可能方法。<br />当然，我们需要能够检测CSS和JavaScript中的支持，以便提供回退或增强功能。<br />这很容易对于CSS，您可以使用带有虚拟功能查询的@supports[条件](https://developer.mozilla.org/en/docs/Web/CSS/@supports)：
```
@supports ( (--a: 0)) {
  /* supported */
}
@supports ( not (--a: 0)) {
  /* not supported */
}
```
在JavaScript中，您可以使用与CSS.supports（）静态方法相同的虚拟自定义属性：
```
const isSupported = window.CSS &&
    window.CSS.supports && window.CSS.supports('--a', 0);
if (isSupported) {
  /* supported */
} else {
  /* not supported */
}
```
我们看到，CSS自定义属性在每个浏览器中仍然不可用。知道这一点，您可以通过检查它们是否受支持来逐步增强您的应用程序。<br />例如，您可以生成两个主要的CSS文件：一个具有CSS自定义属性，另一个没有它们，其中属性是内联的（我们将在稍后讨论一些方法）。<br />默认加载第二个。然后，如果支持自定义属性，只需检查JavaScript并切换到增强版本即可:
```
<!-- HTML -->
<link href="without-css-custom-properties.css"
    rel="stylesheet" type="text/css" media="all" />
```
```
// JavaScript
if(isSupported){
  removeCss('without-css-custom-properties.css');
  loadCss('css-custom-properties.css');
  // + conditionally apply some application enhancements
  // using the custom properties
}
```
这只是一个例子。往下看，有更好的选择。
<a name="dmx3t"></a>
### 如何开始使用它们
针对最近的一项[调查](https://ashleynolan.co.uk/blog/frontend-tooling-survey-2016-results)，Sass已经成为了开发社区中预处理器的最佳选择。<br />所以，让我们考虑开始使用CSS自定义属性或使用Sass为他们做准备的方法。<br />我们有一些观点。
<a name="CH3Up"></a>
#### 1. 手动检查代码支持
手动检查代码中自定义属性是否支持的方法的一个优点是如果它可行我们就可以直接用它（不要忘记我们已经切换到Sass）：
```
$color: red;
:root {
  --color: red;
}
.box {
  @supports ( (--a: 0)) {
    color: var(--color);
  }
  @supports ( not (--a: 0)) {
    color: $color;
  }
}
```
这种方法确实有许多缺点，其中不仅仅是代码变得复杂，而且复制和粘贴变得很难维护。
<a name="4xErL"></a>
#### 2. 使用自动转换CSS的插件
PostCSS生态系统今天提供了几十个插件。它们中的几个在生成的CSS输出中处理自定义属性（内联值），并使它们工作，假设您仅提供全局变量（即，您只声明或更改：根选择器中的CSS自定义属性），因此它们的值可以轻松内联。<br />其中一个例子就是[postcss-custom-properties](https://github.com/postcss/postcss-custom-properties)<br />这个插件提供了几个优点：它使语法工作;它与PostCSS的所有基础设施兼容;并且不需要太多的配置。<br />但是有一些缺点。该插件需要您使用CSS自定义属性，因此您没有准备项目以从Sass变量切换的路径。此外，您将无法对转换进行很多控制，因为在Sass被编译为CSS之后完成。最后，插件不提供很多调试信息。
<a name="XCJAO"></a>
#### 3. css-vars Mixin
我开始在我大多数项目里使用CSS自定义属性并且尝试了很多策略：

- 用[cssnext](http://cssnext.io/)从Sass切换到PostCSS .<br />
- 从Sass变量切换到纯CSS自定义属性<br />
- 在Sass中使用CSS变量来检测是否支持它们。<br />

通过这些经验，我开始寻找一个可以满足我的标准的解决方案：

- 它应该很容配合Sass来使用<br />
- 应该直接使用，并且语法必须尽可能接近原生的CSS自定义属性。<br />
- 将CSS输出从内联值切换到CSS变量应该很容易。<br />
- 熟悉CSS自定义属性的团队成员将能够使用该解决方案。<br />
- 应该有一种方法有使用变量的调试信息。<br />

因此，我创建了css-vars，一个Sass mixin，可以在[Github](https://github.com/malyw/css-vars)上找到。使用它，你就可以使用CSS自定义属性语法。
<a name="6hMNN"></a>
### 使用 css-vars Mixin
声明变量，使用的mixin如下：
```
$white-color: #fff;
$base-font-size: 10px;
@include css-vars((
  --main-color: #000,
  --main-bg: $white-color,
  --main-font-size: 1.5*$base-font-size,
  --padding-top: calc(2vh + 20px)
));
```
使用这些变量，用`var()`函数：
```
body {
  color: var(--main-color);
  background: var(--main-bg, #f00);
  font-size: var(--main-font-size);
  padding: var(--padding-top) 0 10px;
}
```
这为您提供了一种从一个地方（从Sass）控制所有CSS输出并开始熟悉语法的方法。此外，您可以使用mixin重用Sass变量和逻辑。<br />当您想要支持的所有浏览器都使用CSS变量时，您需要做的就是添加：
```
`$css-vars-use-native: true;`
```
而不是调整生成的CSS中的变量属性，mixin将开始注册自定义属性，并且`var()`实例将转到生成的CSS而不进行任何转换。这意味着您将完全切换到CSS自定义属性，并具有我们讨论的所有优点。<br />如果你想打开有用的调试信息，如下：
```
`$css-vars-debug-log: true;`
```
这会给你

- 当变量没有被定义却被使用的日志<br />
- 变量被重复定义的日志<br />
- 当默认值代替了未定义变量值的日志

<a name="UY5cx"></a>
### 结束语
现在你对CSS自定义属性有了更多的了解，包括语法、优势、一些有用的例子还有如何在JavaScript中进行交互<br />你需要知道如何确认他们是否被支持，他们和CSS预处理器的变量有什么区别，以及如何在浏览器支持之前开始使用原生的CSS变量。<br />这是开始使用CSS自定义属性并为浏览器支持做准备的最佳时机。<br />_(rb, vf, al, il)_

