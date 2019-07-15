
---

title: RxJS

date: 2019-07-04 09:30:11 +0800

tags: []

---
[官网](http://reactivex.io/)<br />github地址：[https://github.com/ReactiveX/rxjs](https://github.com/ReactiveX/rxjs)
<a name="hjQZP"></a>
# 异步复杂度要到什么程度才需要用到Rxjs？
给大家介绍一个很直观的网站，用动画的方式演示了大部分Rxjs的Operator的执行过程，以及功能相似的Operator之间的比较。<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562203964640-67f1c25c-d7c0-45df-bb9b-8be787157fb6.png#align=left&display=inline&height=84&name=image.png&originHeight=232&originWidth=828&size=85482&status=done&width=300)](https://reactive.how/)<br />[https://reactive.how/](https://reactive.how/)<br />RxJS至于event,就像以前Jquery至于dom，lodash/underscore至于data。现在Jquery和lodash/underscore可以完全ES6+代替了。

用具体的实现例子去实现 RxJS, 原文地址 [An Animated Intro to RxJS | CSS-Tricks](https://link.zhihu.com/?target=https%3A//css-tricks.com/animated-intro-rxjs/%23article-header-id-3)

hi 我也是初学者 来分享一点自己的心得<br />1. 从【能解决什么问题】开始学习rx到底是解决什么问题，是怎么解决得更好等等，来建立对rx的基本认识<br />途径: 百度，google，stackoverflow搜索<br />2. 从【一个简单可运行的demo】开始学习rx基本用法<br />途径-1: Hello RxJS系列（分享自知乎网）<br />[知乎专栏](https://zhuanlan.zhihu.com/p/23331432)<br />作者<br />[@太狼](//www.zhihu.com/people/f169ccd8ba80a296455c2c0798ec343e)

途径-2: githun搜索rx demo<br />3. 【官网】开始学习rx 基本几大概念，api和用法等。最好每个api都动手做一做，下面分享的第二个网站有每个api的效果图。(我有些是边翻译边看哈哈)<br />分享-1: rx5.x官网<br />[http://reactivex.io/rxjs/manual/overview.html](https://link.zhihu.com/?target=http%3A//reactivex.io/rxjs/manual/overview.html)<br />分享-2: api效果图网<br />[RxJS - Javascript library for functional reactive programming.](https://link.zhihu.com/?target=http%3A//xgrommx.github.io/rx-book/content/observable/observable_instance_methods/flatmaplatest.html)<br />4. 【进阶】学习更多实际用途与基本原理<br />途径：angular2表单监控，angular2 http等<br />5. 【实战】开始用rxjs动手做个完整项目或者在根据项目情况中考虑加入rx<br />完



<a name="ekvTt"></a>
# 构建流式应用—RxJS详解
[原文地址](https://github.com/joeyguo/blog/issues/11)<br />最近在 Alloyteam Conf 2016 分享了《使用RxJS构建流式前端应用》，会后在线上线下跟大家交流时发现对于 RxJS 的态度呈现出两大类:有用过的都表达了 RxJS 带来的优雅编码体验，未用过的则反馈太难入门。所以，这里将结合自己对 RxJS 理解，通过 RxJS 的实现原理、基础实现及实例来一步步分析，提供 RxJS 较为全面的指引，感受下使用 RxJS 编码是怎样的体验。
<a name="TtDFo"></a>
# 目录

- 常规方式实现搜索功能
- RxJS · 流 Stream
- RxJS 实现原理简析
  - 观察者模式
  - 迭代器模式
  - RxJS 的观察者 + 迭代器模式
- RxJS 基础实现
  - Observable
  - Observer
- RxJS · Operators
  - Operators ·入门
  - 一系列的 Operators 操作
- 使用 RxJS 一步步实现搜索功能
- 总结

---

<a name="8MSM0"></a>
# 常规方式实现搜索
做一个搜索功能在前端开发中其实并不陌生，一般的实现方式是：监听文本框的输入事件，将输入内容发送到后台，最终将后台返回的数据进行处理并展示成搜索结果。<br /><input id="text"></input><br /><script><br />    var text = document.querySelector('#text');<br />    text.addEventListener('keyup', (e) =>{<br />        var searchText = e.target.value;<br />        // 发送输入内容到后台<br />        $.ajax({<br />            url: `search.qq.com/${searchText}`,<br />            success: data => {<br />              // 拿到后台返回数据，并展示搜索结果<br />              render(data);<br />            }<br />        });<br />    });<br /></script><br />上面代码实现我们要的功能，但存在两个较大的问题：

1. 多余的请求<br />当想搜索“爱迪生”时，输入框可能会存在三种情况，“爱”、“爱迪”、“爱迪生”。而这三种情况将会发起 3 次请求，存在 2 次多余的请求。<br />
1. 已无用的请求仍然执行<br />一开始搜了“爱迪生”，然后马上改搜索“达尔文”。结果后台返回了“爱迪生”的搜索结果，执行渲染逻辑后结果框展示了“爱迪生”的结果，而不是当前正在搜索的“达尔文”，这是不正确的。<br />

**减少多余请求数**，可以用 setTimeout 函数节流的方式来处理，核心代码如下<br /><input id="text"></input><br /><script><br />    var text = document.querySelector('#text'),<br />        timer = null;<br />    text.addEventListener('keyup', (e) =>{<br />        // 在 250 毫秒内进行其他输入，则清除上一个定时器<br />        clearTimeout(timer);<br />        // 定时器，在 250 毫秒后触发<br />        timer = setTimeout(() => {<br />            console.log('发起请求..');<br />        },250)<br />    })<br /></script><br />**已无用的请求仍然执行**的解决方式，可以在发起请求前声明一个当前搜索的状态变量，后台将搜索的内容及结果一起返回，前端判断返回数据与当前搜索是否一致，一致才走到渲染逻辑。最终代码为<br /><input id="text"></input><br /><script><br />    var text = document.querySelector('#text'),<br />        timer = null,<br />        currentSearch = '';

    text.addEventListener('keyup', (e) =>{<br />        clearTimeout(timer)<br />        timer = setTimeout(() => {<br />            // 声明一个当前所搜的状态变量<br />            currentSearch ＝ '书'; 

            var searchText = e.target.value;<br />            $.ajax({<br />                url: `search.qq.com/${searchText}`,<br />                success: data => {<br />                    // 判断后台返回的标志与我们存的当前搜索变量是否一致<br />                    if (data.search === currentSearch) {<br />                        // 渲染展示<br />                        render(data);<br />                    } else {<br />                        // ..<br />                    }<br />                }           <br />            });<br />        },250)<br />    })<br /></script><br />上面代码基本满足需求，但代码开始显得乱糟糟。我们来使用 RxJS 实现上面代码功能，如下<br />var text = document.querySelector('#text');<br />var inputStream = Rx.Observable.fromEvent(text, 'keyup')<br />                    .debounceTime(250)<br />                    .pluck('target', 'value')<br />                    .switchMap(url => Http.get(url))<br />                    .subscribe(data => render(data));<br />可以明显看出，**基于 RxJS 的实现，代码十分简洁！**
<a name="zLFnv"></a>
# RxJS · 流 Stream
RxJS 是 Reactive Extensions for JavaScript 的缩写，起源于 Reactive Extensions，是一个基于可观测数据流在异步编程应用中的库。RxJS 是 Reactive Extensions 在 JavaScript 上的实现，而其他语言也有相应的实现，如 RxJava、RxAndroid、RxSwift 等。学习 RxJS，我们需要从可观测数据流(Streams)说起，它是 Rx 中一个重要的数据类型。<br />**流**是在时间流逝的过程中产生的一系列事件。它具有时间与事件响应的概念。<br />![c.gif](https://cdn.nlark.com/yuque/0/2019/gif/263301/1562224751759-68a17e33-91ff-4f22-8f0a-3506139c4f40.gif#align=left&display=inline&height=281&name=c.gif&originHeight=281&originWidth=500&size=1348260&status=done&width=500)<br />下雨天时，雨滴随时间推移逐渐产生，下落时对水面产生了水波纹的影响，这跟 Rx 中的流是很类似的。而在 Web 中，雨滴可能就是一系列的鼠标点击、键盘点击产生的事件或数据集合等等。
<a name="RwwLZ"></a>
# RxJS 基础实现原理简析
对流的概念有一定理解后，我们来讲讲 RxJS 是怎么围绕着流的概念来实现的，讲讲 RxJS 的基础实现原理。RxJS 是基于观察者模式和迭代器模式以函数式编程思维来实现的。
<a name="UydvK"></a>
## 观察者模式
观察者模式在 Web 中最常见的应该是 DOM 事件的监听和触发。

- **订阅**：通过 addEventListener 订阅 document.body 的 click 事件。
- **发布**：当 body 节点被点击时，body 节点便会向订阅者发布这个消息。

document.body.addEventListener('click', function listener(e) {<br />    console.log(e);<br />},false);

document.body.click(); // 模拟用户点击<br />将上述例子抽象模型，并对应通用的观察者模型<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562224636723-3c7075b7-336a-40ca-b0d8-d9380825d5cd.png#align=left&display=inline&height=423&originHeight=423&originWidth=915&size=0&status=done&width=915)](https://cloud.githubusercontent.com/assets/10385585/19889545/58dababe-a070-11e6-8e54-be78121f9ba1.png)
<a name="o8XKV"></a>
## 迭代器模式
迭代器模式可以用 JavaScript 提供了 Iterable Protocol 可迭代协议来表示。Iterable Protocol 不是具体的变量类型，而是一种可实现协议。JavaScript 中像 Array、Set 等都属于内置的可迭代类型，可以通过 iterator 方法来获取一个迭代对象，调用迭代对象的 next 方法将获取一个元素对象，如下示例。<br />var iterable = [1, 2];

var iterator = iterable[Symbol.iterator]();

iterator.next(); // => { value: "1", done: false}<br />iterator.next(); // => { value: "2", done: false}

iterator.next(); // => { value: undefined, done: true}<br />元素对象中：value 表示返回值，done 表示是否已经到达最后。<br />遍历迭代器可以使用下面做法。<br />var iterable = [1, 2];<br />var iterator = iterable[Symbol.iterator]();

while(true) {<br />    let result;<br />    try {<br />        result = iterator.next();  // <= 获取下一个值<br />    } catch (err) {<br />        handleError(err);  // <= 错误处理<br />    }<br />    if (result.done) {<br />        handleCompleted();  // <= 无更多值（已完成）<br />        break;<br />    }<br />    doSomething(result.value);<br />}<br />主要对应三种情况：

- 获取下一个值<br />调用 next 可以将元素一个个地返回，这样就支持了返回多次值。<br />
- 无更多值(已完成)<br />当无更多值时，next 返回元素中 done 为 true。<br />
- 错误处理<br />当 next 方法执行时报错，则会抛出 error 事件，所以可以用 try catch 包裹 next 方法处理可能出现的错误。<br />
<a name="r8Owr"></a>
## RxJS 的观察者 + 迭代器模式
RxJS 中含有两个基本概念：Observables 与 Observer。Observables 作为被观察者，是一个值或事件的流集合；而 Observer 则作为观察者，根据 Observables 进行处理。<br />Observables 与 Observer 之间的订阅发布关系(观察者模式) 如下：

- **订阅**：Observer 通过 Observable 提供的 subscribe() 方法订阅 Observable。
- **发布**：Observable 通过回调 next 方法向 Observer 发布事件。

下面为 Observable 与 Observer 的伪代码<br />// Observer<br />var Observer = {<br />    next(value) {<br />        alert(`收到${value}`);<br />    }<br />};

// Observable<br />function Observable (Observer) {<br />    setTimeout(()=>{<br />        Observer.next('A');<br />    },1000)<br />}

// subscribe<br />Observable(Observer);<br />上面实际也是观察者模式的表现，那么迭代器模式在 RxJS 中如何体现呢？<br />在 RxJS 中，Observer 除了有 next 方法来接收 Observable 的事件外，还可以提供了另外的两个方法：error() 和 complete()，与迭代器模式一一对应。<br />var Observer = {<br />    next(value) { /* 处理值*/ },<br />    error(error) { /* 处理异常 */ },<br />    complete() { /* 处理已完成态 */ }<br />};<br />结合迭代器 Iterator 进行理解：

- **next()**<br />Observer 提供一个 next 方法来接收 Observable 流，是一种 push 形式；而 Iterator 是通过调用 iterator.next() 来拿到值，是一种 pull 的形式。<br />
- **complete()**<br />当不再有新的值发出时，将触发 Observer 的 complete 方法；而在 Iterator 中，则需要在 next 的返回结果中，当返回元素 done 为 true 时，则表示 complete。<br />
- **error()**<br />当在处理事件中出现异常报错时，Observer 提供 error 方法来接收错误进行统一处理；Iterator 则需要进行 try catch 包裹来处理可能出现的错误。<br />

下面是 Observable 与 Observer 实现观察者 + 迭代器模式的伪代码，数据的逐渐传递传递与影响其实就是流的表现。<br />// Observer<br />var Observer = {<br />    next(value) {<br />        alert(`收到${value}`);<br />    },<br />    error(error) {<br />        alert(`收到${error}`);<br />    },<br />    complete() {<br />        alert("complete");<br />    },<br />};

// Observable<br />function Observable (Observer) {<br />    [1,2,3].map(item=>{<br />        Observer.next(item);<br />    });

    Observer.complete();<br />    // Observer.error("error message");<br />}

// subscribe<br />Observable(Observer);
<a name="QC1vM"></a>
# RxJS 基础实现
有了上面的概念及伪代码，那么在 RxJS 中是怎么创建 Observable 与 Observer 的呢?
<a name="YZPbn"></a>
### 创建 Observable
RxJS 提供 create 的方法来自定义创建一个 Observable，可以使用 next 来发出流。<br />var Observable = Rx.Observable.create(observer => {<br />    observer.next(2);<br />    observer.complete();<br />    return  () => console.log('disposed');<br />});
<a name="9zN6u"></a>
### 创建 Observer
Observer 可以声明 next、err、complete 方法来处理流的不同状态。<br />var Observer = Rx.Observer.create(<br />    x => console.log('Next:', x),<br />    err => console.log('Error:', err),<br />    () => console.log('Completed')<br />);<br />最后将 Observable 与 Observer 通过 subscribe 订阅结合起来。<br />var subscription = Observable.subscribe(Observer);<br />RxJS 中流是可以被取消的，调用 subscribe 将返回一个 subscription，可以通过调用 subscription.unsubscribe() 将流进行取消，让流不再产生。<br />看了起来挺复杂的？换一个实现形式：<br />// @Observables 创建一个 Observables<br />var streamA = Rx.Observable.of(2);

// @Observer streamA$.subscribe(Observer)<br />streamA.subscribe(v => console.log(v));<br />将上面代码改用链式写法，代码变得十分简洁：<br />Rx.Observable.of(2).subscribe(v => console.log(v));
<a name="1jiUR"></a>
# RxJS · Operators 操作
<a name="DmlXg"></a>
## Operators 操作·入门
Rx.Observable.of(2).subscribe(v => console.log(v));<br />上面代码相当于创建了一个流(2)，最终打印出2。那么如果想将打印结果翻倍，变成4，应该怎么处理呢？<br />**方案一?**： 改变事件源，让 Observable 值 X 2<br />Rx.Observable.of(2 * 2 /* <= */).subscribe(v => console.log(v));<br />**方案二?**： 改变响应方式，让 Observer 处理 X 2<br />Rx.Observable.of(2).subscribe(v => console.log(v * 2 /* <= */));<br />**优雅方案**： RxJS 提供了优雅的处理方式，可以在事件源(Observable)与响应者(Observer)之间增加操作流的方法。<br />Rx.Observable.of(2)<br />             .map(v => v * 2) /* <= */<br />             .subscribe(v => console.log(v));<br />map 操作跟数组操作的作用是一致的，不同的这里是将流进行改变，然后将新的流传出去。在 RxJS 中，把这类操作流的方式称之为 Operators(操作)。RxJS提供了一系列 Operators，像map、reduce、filter 等等。操作流将产生新流，从而保持流的不可变性，这也是 RxJS 中函数式编程的一点体现。关于函数式编程，这里暂不多讲，可以看看另外一篇文章 [《谈谈函数式编程》](https://github.com/joeyguo/blog/issues/10)<br />到这里，我们知道了，流从产生到最终处理，可能经过的一些操作。即 RxJS 中 Observable 将经过一系列 Operators 操作后，到达 Observer。<br />Operator1   Operator2<br />Observable ----|-----------|-------> Observer
<a name="cvj5t"></a>
## 一系列的 Operators 操作
RxJS 提供了非常多的操作，像下面这些。<br />Aggregate,All,Amb,ambArray,ambWith,AssertEqual,averageFloat,averageInteger,averageLong,blocking,blockingFirst,blockingForEach,blockingSubscribe,Buffer,bufferWithCount,bufferWithTime,bufferWithTimeOrCount,byLine,cache,cacheWithInitialCapacity,case,Cast,Catch,catchError,catchException,collect,concatWith,Connect,connect_forever,cons,Contains,doAction,doAfterTerminate,doOnComplete,doOnCompleted,doOnDispose,doOnEach,doOnError,doOnLifecycle,doOnNext,doOnRequest,dropUntil,dropWhile,ElementAt,ElementAtOrDefault,emptyObservable,fromNodeCallback,fromPromise,fromPublisher,fromRunnable,Generate,generateWithAbsoluteTime,generateWithRelativeTime,Interval,intervalRange,into,latest (Rx.rb version of Switch),length,mapTo,mapWithIndex,Materialize,Max,MaxBy,mergeArray,mergeArrayDelayError,mergeWith,Min,MinBy,multicastWithSelector,nest,Never,Next,Next (BlockingObservable version),partition,product,retryWhen,Return,returnElement,returnValue,runAsync,safeSubscribe,take_with_time,takeFirst,TakeLast,takeLastBuffer,takeLastBufferWithTime,windowed,withFilter,withLatestFrom,zipIterable,zipWith,zipWithIndex<br />关于每一个操作的含义，可以查看[官网](http://reactivex.io/documentation/operators.html)进行了解。operators 具有静态（static）方法和实例（ instance）方法，下面使用 Rx.Observable.xx 和 Rx.Observable.prototype.xx 来简单区分，举几个例子。<br />**Rx.Observable.of**<br />of 可以将普通数据转换成流式数据 Observable。如上面的 Rx.Observable.of(2)。<br />**Rx.Observable.fromEvent**<br />除了数值外，RxJS 还提供了关于事件的操作，fromEvent 可以用来监听事件。当事件触发时，将事件 event 转成可流动的 Observable 进行传输。下面示例表示：监听文本框的 keyup 事件，触发 keyup 可以产生一系列的 event Observable。<br />var text = document.querySelector('#text');<br />Rx.Observable.fromEvent(text, 'keyup')<br />             .subscribe(e => console.log(e));<br />**Rx.Observable.prototype.map**<br />map 方法跟我们平常使用的方式是一样的，不同的只是这里是将流进行改变，然后将新的流传出去。上面示例已有涉及，这里不再多讲。<br />Rx.Observable.of(2)<br />             .map(v => 10 * v)<br />             .subscribe(v => console.log(v));<br />Rx 提供了许多的操作，为了更好的理解各个操作的作用，我们可以通过一个可视化的工具 [marbles 图](http://rxmarbles.com/) 来辅助理解。如 map 方法对应的 marbles 图如下<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562224637404-cb22087f-9fda-4234-a8bd-8a211fd52991.png#align=left&display=inline&height=428&originHeight=428&originWidth=1098&size=0&status=done&width=1098)](https://cloud.githubusercontent.com/assets/10385585/19889586/9af9d4ca-a070-11e6-8582-8dbdcfcef520.png)<br />箭头可以理解为时间轴，上面的数据经过中间的操作，转变成下面的模样。<br />**Rx.Observable.prototype.mergeMap**<br />mergeMap 也是 RxJS 中常用的接口，我们来结合 marbles 图(flatMap(alias))来理解它<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562224637493-53b74d3b-8131-49cf-9894-601e4b0fcb9e.png#align=left&display=inline&height=494&originHeight=494&originWidth=1064&size=0&status=done&width=1064)](https://cloud.githubusercontent.com/assets/10385585/19889614/cb4bed20-a070-11e6-9de0-7f04d8de53cc.png)<br />上面的数据流中，产生了新的分支流(流中流)，mergeMap 的作用则是将分支流调整回主干上，最终分支上的数据流都经过主干的其他操作，其实也是将流中流进行扁平化。<br />**Rx.Observable.prototype.switchMap**<br />switchMap 与 mergeMap 都是将分支流疏通到主干上，而不同的地方在于 switchMap 只会保留最后的流，而取消抛弃之前的流。<br />除了上面提到的 marbles，也可以 ASCII 字符的方式来绘制可视化图表，下面将结合 Map、mergeMap 和 switchMap 进行对比来理解。
```
@Map             @mergeMap            @switchMap
                         ↗  ↗                 ↗  ↗
-A------B-->           a2 b2                a2 b2  
-2A-----2B->          /  /                 /  /  
                    /  /                 /  /
                  a1 b1                a1 b1
                 /  /                 /  /
                -A-B----------->     -A-B---------->
                --a1-b1-a2-b2-->     --a1-b1---b2-->
```
mergeMap 和 switchMap 中，A 和 B 是主干上产生的流，a1、a2 为 A 在分支上产生，b1、b2 为 B 在分支上产生，可看到，最终将归并到主干上。switchMap 只保留最后的流，所以将 A 的 a2 抛弃掉。<br />**Rx.Observable.prototype.debounceTime**<br />debounceTime 操作可以操作一个时间戳 TIMES，表示经过 TIMES 毫秒后，没有流入新值，那么才将值转入下一个操作。<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562224636984-6bc3f28f-4f3d-44a6-a530-11498638ea33.png#align=left&display=inline&height=421&originHeight=421&originWidth=1089&size=0&status=done&width=1089)](https://cloud.githubusercontent.com/assets/10385585/19889647/f6ce3aac-a070-11e6-8a35-b04f05afbe36.png)<br />RxJS 中的操作符是满足我们以前的开发思维的，像 map、reduce 这些。另外，无论是 marbles 图还是用 ASCII 字符图这些可视化的方式，都对 RxJS 的学习和理解有非常大的帮助。
<a name="dg75Y"></a>
# 使用 RxJS 一步步实现搜索示例
RxJS 提供许多创建流或操作流的接口，应用这些接口，我们来一步步将搜索的示例进行 Rx 化。<br />使用 RxJS 提供的 fromEvent 接口来监听我们输入框的 keyup 事件，触发 keyup 将产生 Observable。<br />var text = document.querySelector('#text');<br />Rx.Observable.fromEvent(text, 'keyup')<br />             .subscribe(e => console.log(e));<br />这里我们并不想输出事件，而想拿到文本输入值，请求搜索，最终渲染出结果。涉及到两个新的 Operators 操作，简单理解一下：

- **Rx.Observable.prototype.pluck('target', 'value')**<br />将输入的 event，输出成 event.target.value。<br />
- **Rx.Observable.prototype.mergeMap()**<br />将请求搜索结果输出回给 Observer 上进行渲染。<br />

var text = document.querySelector('#text');<br />Rx.Observable.fromEvent(text, 'keyup')<br />             .pluck('target', 'value') // <--<br />             .mergeMap(url => Http.get(url)) // <--<br />             .subscribe(data => render(data))<br />上面代码实现了简单搜索呈现，但同样存在一开始提及的两个问题。那么如何减少请求数，以及取消已无用的请求呢？我们来了解 RxJS 提供的其他 Operators 操作，来解决上述问题。

- **Rx.Observable.prototype.debounceTime(TIMES)**<br />表示经过 TIMES 毫秒后，没有流入新值，那么才将值转入下一个环节。这个与前面使用 setTimeout 来实现函数节流的方式有一致效果。<br />
- **Rx.Observable.prototype.switchMap()**<br />使用 switchMap 替换 mergeMap，将能取消上一个已无用的请求，只保留最后的请求结果流，这样就确保处理展示的是最后的搜索的结果。<br />

最终实现如下，与一开始的实现进行对比，可以明显看出 RxJS 让代码变得十分简洁。<br />var text = document.querySelector('#text');<br />Rx.Observable.fromEvent(text, 'keyup')<br />             .debounceTime(250) // <- throttling behaviour<br />             .pluck('target', 'value')<br />             .switchMap(url => Http.get(url)) // <- Kill the previous requests<br />             .subscribe(data => render(data))
<a name="9lqho"></a>
# 总结
本篇作为 RxJS 入门篇到这里就结束，关于 RxJS 中的其他方面内容，后续再拎出来进一步分析学习。<br />RxJS 作为一个库，可以与众多框架结合使用，但并不是每一种场合都需要使用到 RxJS。复杂的数据来源，异步多的情况下才能更好凸显 RxJS 作用，这一块可以看看民工叔写的[《流动的数据——使用 RxJS 构造复杂单页应用的数据逻辑》](https://github.com/xufei/blog/issues/38) 相信会有更好的理解。<br />附:<br />RxJS(JavaScript) [https://github.com/Reactive-Extensions/RxJS](https://github.com/Reactive-Extensions/RxJS)<br />RxJS(TypeScript ) [https://github.com/ReactiveX/rxjs](https://github.com/ReactiveX/rxjs)<br />[查看更多文章 >>](https://github.com/joeyguo/blog)<br />[https://github.com/joeyguo/blog](https://github.com/joeyguo/blog)

