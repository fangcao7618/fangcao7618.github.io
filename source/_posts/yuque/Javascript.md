
---

title: Javascript

date: 2019-06-14 10:25:59 +0800

tags: []

---
<a name="RGsMd"></a>
## querySelectorAll getElementsBy 区别？
> <a name="bd16e43f"></a>
#### 浏览器兼容

querySelectorAll 已被 IE 8+、FF 3.5+、Safari 3.1+、Chrome 和 Opera 10+ 良好支持 。getElementsBy 系列，以最迟添加到规范中的 getElementsByClassName 为例，IE 9+、FF 3 +、Safari 3.1+、Chrome 和 Opera 9+ 都已经支持该方法了。
> <a name="f82513a1"></a>
#### 接收参数

querySelectorAll 方法接收的参数是一个 CSS 选择符。而 getElementsBy 系列接收的参数只能是单一的 className、tagName 和 name。
```javascript
var c1 = document.querySelectorAll('.b1 .c')
var c2 = document.getElementsByClassName('c')
var c3 = document.getElementsByClassName('b2')[0].getElementsByClassName('c')
```

> <a name="ddc6e94b"></a>
#### 返回值

大部分人都知道，querySelectorAll 返回的是一个 Static Node List，而 getElementsBy 系列的返回的是一个 Live Node List。
```html
<ul>
  <li></ul>
  <li></ul>
  <li></ul>
  <li></ul>
  <li></ul>
</ul>
<script>
// Demo 1
var ul = document.querySelectorAll('ul')[0],
    lis = ul.querySelectorAll("li");
for(var i = 0; i < 5 ; i++){
    ul.appendChild(document.createElement("li"));
}
console.log(lis) //5
// Demo 2
var ul = document.getElementsByTagName('ul')[0],
    lis = ul.getElementsByTagName("li");
for(var i = 0; i < 5 ; i++){
    ul.appendChild(document.createElement("li"));
}
console.log(lis) //5+2
</script>
```
Demo 1 中的 lis 是一个静态的 Node List，是一个 li 集合的快照，对文档的任何操作都不会对其产生影响。<br />Demo 2 中的 lis 是一个动态的 Node List， 每一次调用 lis 都会重新对文档进行查询，导致无限循环的问题。<br />但为什么要这样设计呢？ 其实，在 W3C 规范中对 querySelectorAll 方法有明确规定<br />

> The NodeList object returned by the querySelectorAll() method must be static ([DOM], section 8).

那什么是 NodeList 呢？
> The NodeList interface provides the abstraction of an ordered collection of nodes, without defining or constraining how this collection is implemented. NodeList objects in the DOM are live.

所以，NodeList 本质上是一个动态的 Node 集合，只是规范中对 querySelectorAll 有明确要求，规定其必须返回一个静态的 NodeList 对象。

```javascript
document.querySelectorAll('a').toString() // return "[object NodeList]"
document.getElementsByTagName('a').toString() // return "[object HTMLCollection]"
```
这里又多了一个 HTMLCollection 对象出来，那 HTMLCollection 又是什么？

实际上，HTMLCollection 和 NodeList 十分相似，都是一个动态的元素集合，每次访问都需要重新对文档进行查询。两者的本质上差别在于，HTMLCollection 是属于 Document Object Model HTML 规范，而 NodeList 属于 Document Object Model Core 规范。这样说有点难理解，看看下面的例子会比较好理解

```javascript
var ul = document.getElementsByTagName('ul')[0],
  lis1 = ul.childNodes,
  lis2 = ul.children
console.log(lis1.toString(), lis1.length) // "[object NodeList]" 11
console.log(lis2.toString(), lis2.length) // "[object HTMLCollection]" 4
```
NodeList 对象会包含文档中的所有节点，如 Element、Text 和 Comment 等。HTMLCollection 对象只会包含文档中的 Element 节点。另外，HTMLCollection 对象比 NodeList 对象 多提供了一个 namedItem 方法。所以在现代浏览器中，querySelectorAll 的返回值是一个静态的 NodeList 对象，而 getElementsBy 系列的返回值实际上是一个 HTMLCollection 对象 。

[参照文章](https://www.zhihu.com/question/24702250)
<a name="I4tMa"></a>
## NodeList 和 HTMLCollection 之间的关系？

<br />历史上的 DOM 集合接口。主要不同在于 `HTMLCollection`是元素集合而 NodeList 是节点集合（即可以包含元素，也可以包含文本节点）。所以 `node.childNodes` 返回 `NodeList`，而 `node.children` 和 `node.getElementsByXXX` 返回 `HTMLCollection` 。<br />唯一要注意的是 `querySelectorAll` 返回的虽然是 `NodeList` ，但是实际上是元素集合，并且是静态的（其他接口返回的 `HTMLCollection` 和 `NodeList` 都是 live 的）。<br />Both interfaces are collections of DOM nodes. They differ in the methods they provide and in the type of nodes they can contain. While a NodeList can contain any node type, an HTMLCollection is supposed to only contain Element nodes. An HTMLCollection provides the same methods as a NodeList and additionally a method called namedItem.<br />Collections are always used when access has to be provided to multiple nodes, e.g. most selector methods (such as getElementsByTagName) return multiple nodes or getting a reference to all children (element.childNodes).<br />

<a name="Rx8bI"></a>
## ["1", "2", "3"].map(parseInt) 坑
第一反应都觉得结果会是 `[1,2,3]`<br />但实际结果却是 `[1, NaN, NaN]`<br />这是为什么呢？主要是 `map` 这个方法在调用 `callback`函数时，会给它传递三个参数:

- 当前正在遍历的元素
- 元素索引
- 原数组本身

也是就是说如上代码其实等同于

```javascript
['1', '2', '3'].map((i, index, array) => parseInt(i, index, array))
```
这样就直观的解释了上面的答案是怎么产生得了。因为 `parseInt` 会接受两个参数：参数和进制数。

```javascript
// 实际代码运算等于如下
parseInt('1', 0) // 1
parseInt('2', 1) // NaN
parseInt('3', 2) // NaN
```
所以为了避免这个坑，平时写 `map` 还是不要偷懒了，完整的写法才更直观并且更容易维护。

```javascript
['1', '2', '3'].map(str => parseInt(str))
```
<a name="Qu4B3"></a>
## 
<a name="RXhM8"></a>
## 省略参数引发的 bug
省略参数是 es6 之后提供的一个很好用也非常常用的功能。但还是有一些细节值得注意，不然一不小心就会出现 bug。

```javascript
function test(num = 1) {
  console.log(num)
}

test() // (num is set to 1)
test(undefined) // (num is set to 1 too)

test('') // (num is set to '')
test(null) // (num is set to null)
test(false) // (num is set to false)
```
如上面 demo 所示，只有参数没传或者是 `undefined` 是才会生效，其它情况默认参数并不会起作用。<br />所以有的时候你传入了`''`空字符串是不行的，还需要自己手动判断一下。<br />str = str || defalutString

另外，一个容易忽略的地方是，参数默认值不是传值的，而是每次都重新计算默认值表达式的值。也就是说，参数默认值是惰性求值的。

```javascript
let x = 99
function foo(p = x + 1) {
  console.log(p)
}

foo() // 100

x = 100
foo() // 101
```
上面代码中，参数 p 的默认值是 x + 1。这时，每次调用函数 foo，都会重新计算 x + 1，而不是默认 p 等于 100。

<a name="vPi0o"></a>
## 多余逗号引发的错误
刚入前端的时候看错误日志，`ie` 的错误日志特别多，一直没找到原因，后来发现是 JSON 最后一组键值后多逗号。

```javascript
// 所有浏览器都正常
var json_normal = {
  id: 1,
  name: "John"
};

// ie 报错，其它游览器正常
var json_error = {
  id: 1,
  name: "John",
};
```
好在现在有了 `eslint` 或者 `preitter`这种工具，这种错误很少会再发生了。

<a name="Awisc"></a>
## js 中的逗号

```javascript
if (((a = 1), a++, a)) {
  console.log(a)
}
```
很多人一下子可能会一脸懵逼。<br />但看一下 [MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/if...else) 就很清楚了<br />

> 逗号操作符 对它的每个操作数求值（从左到右），并返回最后一个操作数的值。


举个例子<br />`var a=(1+1,2+2,3+3);` 结果就是 6。 `3+3`<br />
<br />但在函数中，比如比 `Math.max(x,y,z)`。这里的逗号就是分隔函数参数。<br />还有声明变量时，`var a=1,b=2,c=3`。这里的逗号也是起分隔的作用。<br />再举一个例子大家应该就理解了

```javascript
alert(2 * 5, 2 * 4)
//输出10而不是8  函数接收第一个参数,也说明逗号级别比较低
console.log(2 * 5, 2 * 4) // 10,8

alert((2 * 5, 2 * 4))
// 输出8 ()是返回了,相当于隐藏了return 所以返回最右边操作数的值
console.log((2 * 5, 2 * 4));//8
```

<br />其实最常见的运用场景就是平时经常的`for`循坏

```javascript
for (var i = 0, j = 9; i <= 9; i++, j--) {console.log(i,j)}
```

<a name="gFEmn"></a>
## document.documentElement 与 document.body 区别

<br />在前端开发中，我们经常需要获取网页中滚动条滚过的长度，获取该值的方式一般通过`scrollTop`属性，如：`document.body.scrollTop`，或者`document.documentElement.scrollTop`，这两者都是经常用来获取文档滚动条滚过长度值的方式，他们又有什么区别呢？

之前一直没注意，只到有一天发现了一个 bug:document.body.scrollTop 拿到的值一直是 0。<br />
<br />在这个之前我们先来了解一下 是干嘛的？为什么每个页面都需要加上这段声明。

> doctype 声明不属于 HTML 标签，它是一条指令，告诉浏览器编写页面所用的标记的版本。 这个声明的目的是防止浏览器在渲染文档时，切换到我们称为“[怪异模式(兼容模式)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)”的渲染模式。`<!DOCTYPE html>` 能确保浏览器按照最佳的相关规范进行渲染，而不是使用一个不符合规范的渲染模式。


`document.documentElement` 与 `document.body`

- document 代表的是整个文档(对于一个网页来说包括整个网页结构)
- document.documentElement 是整个文档节点树的根节点，在网页中即 html 标签
- document.body 是整个文档 DOM 节点树里的 body 节点，网页中即为 body 标签元素

但在标准模式下`document.body.scrollTop`是无效的。

> 从 Chrome 61 开始，标准模式中 document.scrollingElement 已被修正为 document.documentElement。换句话说，这个版本开始标准模式中 document.body.scrollTop 始终都等于 0。


所以这里建议使用兼容写法：

```javascript
const scrollTop = Math.max(
  window.pageYOffset,
  document.documentElement.scrollTop,
  document.body.scrollTop
)
```
或者

```javascript
function getBodyScrollTop() {
  const el =
    document.documentElement || document.scrollingElement || document.body
  return el.scrollTop
}
```
**每当这时候我就有一些怀念`jQuery`了**。
<a name="sort"></a>
## sort

```javascript
var array = [3, 7, 2, 8, 2, 782, 7, 29, 1, 3, 0, 34]
array.sort()
// => [0, 1, 2, 2, 29, 3, 3, 34, 7, 7, 782, 8]
```
默认情况下，`sort`是按照`Unicode code points`排序的，换而言之，先回比较首个字符的 code point，若相同的情况下依次位数比下去。

所以很多时候我们需要自定义 sort 的规则。最常见的操作：

```javascript
const array = [3, 7, 2, 8, 2, 782, 7, 29, 1, 3, 0, 34]
array.sort((pre, next) => pre - next)
// => [0, 1, 2, 2, 3, 3, 7, 7, 8, 29, 34, 782]
```

其实它的规则很简单，你想让 next 和 pre 换位子就返回一个>0的值，其它情况位置不变，即返回<=0的值。
<a name="codepointat-vs-charcodeat"></a>
## codePointAt vs charCodeAt
JavaScript 允许采用`\uxxxx`形式表示一个字符，其中`xxxx`表示字符的 Unicode 码点。<br />但是，这种表示法只限于码点在\u0000~\uFFFF 之间的字符。超出这个范围的字符，必须用两个双字节的形式表示。

```javascript
'\uD842\uDFB7'
// "𠮷"
```

JavaScript 内部，字符以 UTF-16 的格式储存，每个字符固定为 2 个字节。对于那些需要 4 个字节储存的字符（Unicode 码点大于 0xFFFF 的字符），JavaScript 会认为它们是两个字符。

```javascript
var s = '𠮷'

s.length // 2
s.charAt(0) // ''
s.charAt(1) // ''
s.charCodeAt(0) // 55362
s.charCodeAt(1) // 57271
```
所以 ES6 提供了 codePointAt 方法，能够正确处理 4 个字节储存的字符，返回一个字符的码点。

```javascript
'𠮷'.codePointAt() //134071
```
总之，codePointAt 方法会正确返回 32 位的 UTF-16 字符的码点。对于那些两个字节储存的常规字符，它的返回结果与 charCodeAt 方法相同。

<a name="rTZKa"></a>
## switch 作用域
其实我们经常会忽略一个点，switch case 是共用一个作用域的。<br />比如如下代码就会抛出重复定义的错误：

```javascript
switch (x) {
  case 0:
    let foo
    break

  case 1:
    let foo // 重复定义引起TypeError
    break
}
// Uncaught SyntaxError: Identifier 'foo' has already been declared
```
解决方案也很简单，我们给每一个 case 加上一个 bracket 就可以了：

```javascript
switch (x) {
  case 0: {
    let foo
    break
  }

  case 1: {
    let foo // 重复定义引起TypeError
    break
  }
}
```
<a name="LciUL"></a>
## div 如何监听 keydown 事件
之前有一个人问我，为什么他监听了一个 div 的 keydown 事件，为什么没有用？ 我看了一下代码发现的确没有写错？但为什么就不触发呢？<br />后来查阅了一下文档
> Focused element processing the key event, root element if no suitable input element focused

发现只有能被 focus 的元素才能出发键盘事件，所以 div 也就不能触发 keydown 事件了。<br />那怎么才能让 div 支持呢？<br />答案是 `tabindex` [mdn](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/tabindex)。它表示元素是可聚焦的，并且可以通过键盘导航来访问到该元素。<br />这样一来我们就能愉快的使用`keydown`事件了.
<a name="lqKfa"></a>
## try catch 的 finally 坑
try...catch 的 finally 可能很多人都没有使用过，它其实和 promise 中的 finally 很类似。 见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/try...catch)。<br />它无论是否有异常它都会执行。 常见的操作就是 将关闭弹窗或者 loading

```javascript
var fn = function() {
  try {
    console.log('ok')
    return 'ok'
  } catch {
    console.log('error')
    return 'error'
  } finally {
    console.log('finally')
    return 'finally'
  }
}
fn()
// ok finally "finally"
```
我们发现最终输出了`finally`。因为这个语句只会有一个 return，finally 中的 return 覆盖了之前的定义。而且 return 会被放在最后执行。[详情见](https://stackoverflow.com/questions/3837994/why-does-a-return-in-finally-override-try)。

```javascript
var fn = function() {
  var res=''
  try {
    res='ok'
  } catch {
    res='error'
  } finally {
    return res
  }
}
fn() //"ok"
```
不过最好还是和 promise 中的 finally 一样，在里面做一些没有副作用的事情。免得发生一些 bug。
<a name="8eG9o"></a>
## atob 方法解码中文字符
由于一些网络通讯协议的限制,你必须使用 window.btoa() 方法对原数据进行编码后，才能进行发送。接收方使用相当于 window.atob() 的方法对接受到的 base64 数据进行解码,得到原数据。

```javascript
window.btoa('foo')
// "Zm9v"

window.atob('Zm9v')
// "foo"
```
atob 这个方法名称乍一看，很奇怪，不知道这个单词什么意思。我们可以理解为 A to B，也就是从 A 到 B。<br />atob 表示 Base64 字符 to 普通字符，也就是 Base64 解码。<br />当你在 Chrome console 中执行 `window.btoa('中文')`会发下会报错。
> `Uncaught DOMException: Failed to execute 'btoa' on 'Window': The string to be encoded contains characters outside of the Latin1 range.`

这时候我们可以借助 `encodeURIComponent` 和 `decodeURIComponent` 转义非中文字符。

```javascript
window.btoa(encodeURIComponent('中文'))
// ('JUU0JUI4JUFEJUU2JTk2JTg3')

decodeURIComponent(window.atob('JUU0JUI4JUFEJUU2JTk2JTg3'))
// "中文"
```
<a name="97hNP"></a>
## Safari 下 Date 的坑
在 使用 Date 相关 api 的时候要牢记一个坑，就是 Safari 对一些时间格式是不支持的。比如：
```javascript
Date.parse('2018-10-16 12:00:00')
// 1539662400000 -- 在Chrome 下
// NaN -- 在Safari下
```
问题就出在 Safari 对于这个格式 YYYY-MM-DD HH:MM:SS 无法解析，Safari 要求 Date.parse()或 Date()转换日期的字符串需要满足 RFC2822 或 ISO 8601 定义的格式。不过我们可以将其转化为 YYYY/MM/DD HH:MM:SS

```javascript
Date.parse(new Date('2018-10-16 12:00:00'.replace(/-/g, '/'))) 
```
相关[stackoverflow](https://stackoverflow.com/questions/4310953/invalid-date-in-safari)<br />

<a name="fd465dc3"></a>
## new Date 在 safari 的坑
`new Date('2019-06-04 00:00:00')`在除了 Safari 的浏览器都能正常运行。 问题就出在 Safari 对于这个格式 `YYYY-MM-DD HH:MM:SS` 无法解析，所以我们需要做的是将其转化为 `YYYY/MM/DD HH:MM:SS`
```javascript
+new Date('2019-06-04 00:00:00'.replace(/-/g, '/'))
```
<a name="Tsg1B"></a>
## e.target 与 e.currentTarget 的区别
有一次在面试的时候问了事件委托的题目，面试人说了一个 currentTarget，突然发现`target`和`currentTarget`的区别我好像有些忘记了，太多相似的 api 和属性了。

首先我们来看一下 MDN 上对它们的解释

- target：一个触发事件的对象的引用， 当事件处理程序在事件的冒泡或捕获阶段被调用时。
- currentTarget： 当事件遍历 DOM 时，标识事件的当前目标。它总是引用事件处理程序附加到的元素，而不是 event.target，event.target 标识事件发生的元素。

可能还是很抽象 ，这里提供一个在线[demo](https://jsbin.com/xekebepaqi/edit?html,js,console,output)。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
<ul>
  <li>hello 1</li>
  <li>hello 2</li>
  <li>hello 3</li>
  <li>hello 4</li>
</ul>
</body>
</html>
<script>
const ul = document.querySelectorAll('ul')[0]
ul.addEventListener('click', function(e) {
  let oLi1 = e.target
  let oLi2 = e.currentTarget
  console.log(oLi1.tagName); //  被点击的li
  console.log(oLi2.tagName); // ul
  console.log(oLi1 === oLi2); // false
});
</script>
```
也就是说，currentTarget 始终是监听事件者，而 target 是事件的真正发出者。
<a name="CFzhD"></a>
## 函数变量必填校验
这里分享一个平时写 ES6 的时候一个小技巧。如何简单的校验并强制在使用这个函数时必须传参数。

```javascript
const isRequired = () => {
  throw new Error('Missing parameter')
}

const foo = (something = isRequired()) => {
  console.log(something)
  return something
}
foo(123)
foo() // Error:Missing parameter
```
<a name="3pXxV"></a>
## 前端错误处理
错误处理对于任何前端来说都是必不可少的。任何人写代码都避免不了会有 bug，而且很多 bug 也不是测试用例能完全覆盖的，如果我们没有一个完整的错误处理和错误收集的系统，我们都无法知道我们有 bug，不仅如此，很多 bug 也不一定是前端的问题，比如某个接口返回的数据格式不对了或者少字段了，亦或是在某个特定的浏览器型号上才有的问题等等。而且有了错误处理和收集，我们也才能更好的通过错误栈来还原这个问题。<br />

<a name="MQRyh"></a>
### 有哪些错误需要处理

- JS 语法错误、代码异常
- 请求错误
- 静态资源加载异常
- Promise 异常
- 页面崩溃和卡顿
<a name="try-catch"></a>
### Try Catch
try-catch 只能捕获到同步的运行时错误，对语法和异步错误却无能为力，捕获不到。 1.同步运行时错误：

1. 同步错误

```javascript
try {
  let name = 'foo'
  console.log(nam)
} catch (e) {
  console.log('捕获到异常：', e)
}
```

> 捕获到异常： 'ReferenceError: nam is not defined at <anonymous>:3:15'

2. 语法错误

```javascript
try {
  let name = 'foo
  console.log(nam)
} catch (e) {
  console.log('捕获到异常：', e)
}
```

> Uncaught SyntaxError: Unexpected identifier

3. 异步错误

```javascript
try {
  setTimeout(() => {
    undefined.map(v => v)
  }, 1000)
} catch (e) {
  console.log('捕获到异常：', e)
}
```
> 每次的数都不一样，运行一次就加1
> Uncaught TypeError: Cannot read property 'map' of undefined

<a name="window-onerror"></a>
### window.onerror
当 JS 运行时错误发生时，window 会触发一个 ErrorEvent 接口的 error 事件，并执行 window.onerror()。

```javascript
/**
 * @param {String}  message    错误信息
 * @param {String}  source    出错文件
 * @param {Number}  lineno    行号
 * @param {Number}  colno    列号
 * @param {Object}  error  Error对象（对象）
 */
window.onerror = function(message, source, lineno, colno, error) {
  console.log('捕获到异常：', { message, source, lineno, colno, error })
}
```
不同域名下的 js 报错不能被 全局的 window.onerror 监听到，我们需要给相关的 js 文件上加上 Access-Control-Allow-Origin:*的 response header，并且引用相关的 js 文件时加上 crossorigin 属性。相关[文章](https://www.jianshu.com/p/315ffe6797b8)

在实际的使用过程中，onerror 主要是来捕获预料之外的错误，而 try-catch 则是用来在可预见情况下监控特定的错误，两者结合使用更加高效。

<a name="window-addeventlistener"></a>
### window.addEventListener
当一项资源（如图片或脚本）加载失败，加载资源的元素会触发一个 Event 接口的 error 事件，并执行该元素上的 onerror() 处理函数。这些 error 事件不会向上冒泡到 window ，不过（至少在 Firefox 中）能被单一的 window.addEventListener 捕获。

```javascript
<img src="./foo.png">
<scritp>
window.addEventListener('error', (error) => {
    console.log('捕获到异常：', error);
}, true)
</script>
```
<a name="promise-catch"></a>
### Promise Catch
没有写 catch 的 Promise 中抛出的错误无法被 onerror 或 try-catch 捕获到，所以我们务必要在 Promise 中不要忘记写 catch 处理抛出的异常。<br />或者可以全局增加一个对 unhandledrejection 的监听，用来全局监听 Uncaught Promise Error。使用方式：

```javascript
window.addEventListener('unhandledrejection', function(e) {
  console.log(e)
})
```

当然你如果使用如 axios 这种库的话，错误处理完全可以放在它的请求实例里面做。更加的灵活。

<a name="vue-errorhandler"></a>
### VUE errorHandler
```javascript
Vue.config.errorHandler = (err, vm, info) => {
  console.error('通过vue errorHandler捕获的错误')
  console.error(err)
  console.error(vm)
  console.error(info)
}
```
<a name="1hVlk"></a>
### React 异常捕获
```javascript
componentDidCatch(error, info) {
    console.log(error, info);
}
```

<a name="UkWSW"></a>
### 崩溃和卡顿
[相关文章](https://zhuanlan.zhihu.com/p/40273861) [实践总结】优雅的处理 vue 项目异常](https://juejin.im/post/5cf72029f265da1b5f264334)

<a name="4LEXG"></a>
## insertBefore 坑

<br />Node.insertBefore()很多人都用过， 它在参考节点之前插入一个节点作为一个指定父节点的子节点。
> var insertedNode = parentNode.insertBefore(newNode, referenceNode);

但看文档还有一句补充说明：
> 如果 referenceElement 为 null 则 newElement 将被插入到子节点的末尾。如果 newElement 已经在 DOM 树中，newElement 首先会从 DOM 树中移除。

这就很坑了，如下面的例子：
```javascript
<div id="parentElement">
  <span id="bar">bar</span>
  <span id='foo'>foo</span>
</div>
<script>
var foo = document.getElementById("foo")
var bar = document.getElementById("bar")
var parentDiv = document.getElementById("parentElement")
parentDiv.insertBefore(foo, bar)
</script>
```
原本以为结果是 `foo` `bar` `foo`，但实际结果是`foo` `bar`。<br />因为根据文档，当你 insertBefore 的是一个已存在的值时，会移动它而不是拷贝它重新插入。贼坑！！！<br />如果使用 ES6 的话可以使用 `before`
```javascript
var foo = document.getElementById('foo')
var bar = document.getElementById('bar')
bar.before(foo)
```
<a name="d41d8cd9"></a>
## 
<a name="O5Plg"></a>
## 为什么前端监控要用 GIF 打点
目前主流的前端监控数据上报都是采用 GIF 的上报方式，(百度统计/友盟/谷歌统计）都是这样实现的。但为什么一定要使用 GIF 呢？不能发 post 请求或者通过 script 标签的形式么？<br />当然你也可以使用一些黑科技的方式上报，用纯 css 来实现。但这种方案并没有什么特别的好处。<br />

```css
.track-xx:active:after {
  content: url(track.php?xxxx=foo);
}
```
<a name="d41d8cd9-1"></a>
### 
<a name="5caCe"></a>
### 主要原因

- 没有跨域问题<br />
- 不会阻塞页面加载，影响用户体验<br />
- 在所有图片中体积最小，相较 BMP/PNG，可以节约 41%/35%的网络资源<br />

详情见 [为什么前端监控要用 GIF 打点](https://mp.weixin.qq.com/s/v6R2w26qZkEilXY0mPUBCw)
<a name="a653042e"></a>
### 使用方式
但建议不要按如下方法使用
```javascript
new Image().src = 'https://foo.com/bar.gif?t=xxxx&b=1'
```
这段代码的问题是这个 new Image()是一个没有引用的临时变量，随时可能被浏览器的垃圾回收机制回收。如果这个图片的 HTTP 请求尚未建立，那么在被回收时这个请求就会被取消，导致打点并没有真正发出。如果打点所在的页面比较复杂，浏览器垃圾回收机制可能会被频繁触发，那么这种方式打点的丢失率可能会高达 10%以上。

解决方法很简单，将这个图片赋值给一个全局变量即可，例如：
```javascript
const img = new Image()
const key = +new Date() //加一个时间戳，防止图片被浏览器缓存了，不再发送请求  "+"转换时间戳
window[t] = img
img.onload = img.onerror = img.onabort = function() {
  // img标签加载完成、错误或终止时，解除事件绑定，销毁相关对象
  img.onload = img.onerror = img.onabort = null
  window[key] = null
  img = null
}
img.src = `${url}?t=key`
```
<a name="d41d8cd9-2"></a>
### 
<a name="VkXKl"></a>
### 其它方案
Beacon API

- 在空闲的时候异步发送统计，不影响页面诸如 JS、CSS Animation 等执行
- 即使页面在 unload 状态下，也会异步发送统计，不影响页面过渡/跳转到下跳页
- 能够被客户端优化发送，尤其在 Mobile 环境下，可以将 Beacon 请求合并到其他请求上，一同处理



<a name="object-create-null-vs"></a>
## Object.create(null) vs {}
查看 vue 的源码 或者一些开源项目的源码，发现不少地方都是使用 `Object.create(null)`来创建一个空对象的。<br />当使用语句 const obj = {}; 创建对象时，它其实并不是一个真的`空对象`，它从 Object.prototype 上继承了一些方法：

- hasOwnProperty
- isPrototypeOf
- propertyIsEnumerable
- toString/toLocaleString
- valueOf

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560496421757-4fdbc517-a05f-420c-81b4-52b37d79d591.png#align=left&display=inline&height=301&name=image.png&originHeight=315&originWidth=419&size=41364&status=done&width=400)


![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560496470556-3b7706ae-8953-40a0-bfeb-39fb28de3e1e.png#align=left&display=inline&height=159&name=image.png&originHeight=130&originWidth=328&size=9324&status=done&width=400)

如果使用 `Object.create(null)` 创建的对象，在没有继承任何东西。

**所以说是不是 `Object.create(null)` 是更好的创建一个空对象的方案呢？**<br />这就要看从 Object 上继承的那些方法我们是不是有用到了。

<a name="hasownproperty"></a>
### hasOwnProperty
判断一个对象属性中是否具有指定的属性，返回 `true` or `false`。

<a name="2LMgx"></a>
### valueOf
valueOf 很少直接使用。在隐式转换类型时，JavaScript 引擎会调用 valueOf 方法，强制把对象转换成原始值<br />

<a name="8b378531"></a>
### toString、isPrototypeOf 和 propertyIsEnumerable
这几个方法直接使用的情况较少，但自己的代码中不用并不表示别人写的代码不会调用。比如，有些框架可能会调用 toString 方法来判断结果是否为 [object Object]。<br />

<a name="54bbba80"></a>
### 结论
因此，我们可以得出结论：当创建的对象只在当前执行环境中使用并且不会用到任何从 Object.prototype 上继承来的方法，也不会将该对象作为其他对象的原型的时候，那么可以使用 Object.create(null)。比如，构造一个字典对象的时候。<br />不过相对而言 `const obj={}`在浏览器中的执行速度是会比`Object.create(null)`快的，具体可点击链接[test](https://jsperf.com/object-create-null-vs-literal/2)。不过你一般代码中这些性能差距完全是可以忽略不计的。

<a name="async-await-with-foreach"></a>
## async/await with forEach()
之前在工作中遇到了一个需求，实现一个简单的请求队列，大概意思就是这个页面有一个 list，我需要按 list 顺序依次发请求，多数据做一些操作，每次等前一个请求成功之后，再执行下一个，全部执行完毕之后，显示已完成。<br />这不就是用 `async/await`就可以实现了。于是写了如下代码：
```javascript
const waitFor = ms => new Promise(r => setTimeout(r, ms));
[1, 2, 3].forEach(async num => {
  await waitFor(1000)
  console.log(num)
})
console.log('Done')
```
What？为什么`await`没有生效，直接就输出了`1,2,3`？谷歌搜索了一下，发现原来是`forEach`的锅。 我们简单来看一下 `forEach`的实现原理：
```javascript
Array.prototype.forEach = function(callback) {
  // this represents our array
  for (let index = 0; index < this.length; index++) {
    // We call the callback for each entry
    callback(this[index], index, this)
  }
}
```
我们可以看到它只是 for 循环的一个简单封装，而且在内部它只是简单做了一个回调，根本就不会`wait`。其实一些其它的数组方式比如`map`、`reduce`等等也是不支持的，因为 Array 的迭代方法就支持不支持参数函数返回 promise 的异步用法，有兴趣的可以自行了解。<br />那我们直接用 `for`循环不就好了
```javascript
async function test() {
  for (let index = 0; index < [1, 2, 3].length; index++) {
    await waitFor(1000)
    console.log(index)
  }
  console.log('done')
}
```
或者 `for-of`更为简单
```javascript
async function test() {
  for (let i of [1, 2, 3]) {
    await waitFor(1000)
    console.log(i)
  }
  console.log('done')
}
```

<a name="09ccd519"></a>
## 获取元素宽度
说真的，我觉得前端麻烦的地方就是 API 太多了，我只是想获取一个元素的宽度居然有`getBoundingClientRect().width`

<a name="7de30023"></a>
## 我使用 Async/Await 而不使用 Promises 的六个理由
本文主要来自于 [6 Reasons Why JavaScript’s Async/Await Blows Promises Away](https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9)，在 medium 上，需要翻墙阅读。<br />之前我很长一段时间内都是使用 promise 的，但遇到一些复杂业务的时候，发现还是写起来会很不爽，代码阅读性也有所欠缺。<br />

1. 简洁

对比 Promise，我们不需要书写.then，不需要新建一个匿名函数处理响应，也不需要再把数据赋值给一个我们其实并不需要的变量

2. a

但 Async/Await 也不是没有缺点的，很多人经常会错用它。比如我一个组件创建的的时候会异步向服务器发送三个请求，`a`、`b、c`。 很多人会这么写
```javascript
async function mount() {
  const resultA = await fetch('A')
  const resultB = await fetch('B')
  const resultC = await fetch('C')
  render(resultA, resultB, resultC)
}
```
虽然上面的这段写法相对于 promise 简洁了不少，但效率来说是不合格的。因为这个请求是异步的，毫无联系的，所有没必要顺序请求，他们三个明显可以异步并发的去请求。要想实现真正的异步，还是需要依赖 Promise.all 封装一层：
```javascript
async function mount() {
  const result = await Promise.all(
    fetch('a.json'),
    fetch('b.json'),
    fetch('c.json')
  )
  render(...result)
}
```

未完待续...

