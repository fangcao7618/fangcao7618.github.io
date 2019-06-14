
---

title: markdown

date: 2019-06-14 16:57:03 +0800

tags: []

---
<a name="9c70b61e"></a>
# 欢迎使用 Cmd Markdown 编辑阅读器

<a name="c1812f49"></a>
## 学习网站：https://www.zybuluo.com/mdeditor、[https://markdown-here.com/](https://markdown-here.com/)
<a name="HaRaX"></a>
## 安装chrome插件：chrome-extension://elifhakcjgalahccnjkneoccemfahfoa/common/options.html可以编辑markdown

我们理解您需要更便捷更高效的工具记录思想，整理笔记、知识，并将其中承载的价值传播给他人，**Cmd Markdown** 是我们给出的答案 —— 我们为记录思想和分享知识提供更专业的工具。 您可以使用 Cmd Markdown：

> - 整理知识，学习笔记
> - 发布日记，杂文，所见所想
> - 撰写发布技术文稿（代码支持）
> - 撰写发布学术论文（LaTeX 公式支持）<br />
![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560502630664-88fa6097-c712-46cf-a203-976fe09ab167.png#align=left&display=inline&height=256&originHeight=256&originWidth=256&size=0&status=done&width=256)<br />
除了您现在看到的这个 Cmd Markdown 在线版本，您还可以前往以下网址下载：


<a name="396affc8"></a>
### [Windows/Mac/Linux 全平台客户端](https://www.zybuluo.com/cmd/)

> 请保留此份 Cmd Markdown 的欢迎稿兼使用说明，如需撰写新稿件，点击顶部工具栏右侧的  **新文稿** 或者使用快捷键 `Ctrl+Alt+N`。


---

<a name="7a88e6d6"></a>
## 什么是 Markdown

Markdown 是一种方便记忆、书写的纯文本标记语言，用户可以使用这些标记符号以最小的输入代价生成极富表现力的文档：譬如您正在阅读的这份文档。它使用简单的符号标记不同的标题，分割不同的段落，**粗体** 或者 _斜体_ 某些文字，更棒的是，它还可以

<a name="68f67455"></a>
### 1. 制作一份待办事宜 [Todo 列表](https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown#13-%E5%BE%85%E5%8A%9E%E4%BA%8B%E5%AE%9C-todo-%E5%88%97%E8%A1%A8)

- [ ] 支持以 PDF 格式导出文稿
- [ ] 改进 Cmd 渲染算法，使用局部渲染技术提高渲染效率
- [x] 新增 Todo 列表功能
- [x] 修复 LaTex 公式渲染问题
- [x] 新增 LaTex 公式编号功能

<a name="f925c277"></a>
### 2. 书写一个质能守恒公式[[1]](#fn1)

$$E=mc^2$$

<a name="fe52e1c5"></a>
### 3. 高亮一段代码[[2]](#fn2)

```python
@requires_authorization
class SomeClass:
    pass
if __name__ == '__main__':
    # A comment
    print 'hello world'
```

<a name="4edb0e5f"></a>
### 4. 高效绘制 [流程图](https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown#7-%E6%B5%81%E7%A8%8B%E5%9B%BE)


![](https://cdn.nlark.com/yuque/__mermaid_v3/bfdd8f6fee101b983d67b093ee95b5a0.svg#code=graph%20TD%3B%0A%20%20%20%20A--%3EB%3B%0A%20%20%20%20A--%3EC%3B%0A%20%20%20%20B--%3ED%3B%0A%20%20%20%20C--%3ED%3B&id=658db4fe&type=mermaid)
<a name="30c642fc"></a>
### 5. 高效绘制 [序列图](https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown#8-%E5%BA%8F%E5%88%97%E5%9B%BE)

```seq
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

<a name="69188c06"></a>
### 6. 高效绘制 [甘特图](https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown#9-%E7%94%98%E7%89%B9%E5%9B%BE)

```gantt
title 项目开发流程
    section 项目确定
        需求分析       :a1, 2016-06-22, 3d
        可行性报告     :after a1, 5d
        概念验证       : 5d
    section 项目实施
        概要设计      :2016-07-05  , 5d
        详细设计      :2016-07-08, 10d
        编码          :2016-07-15, 10d
        测试          :2016-07-22, 5d
    section 发布验收
        发布: 2d
        验收: 3d
```

<a name="b2983356"></a>
### 7. 绘制表格
| 项目 | 价格 | 数量 |
| --- | ---: | :---: |
| 计算机 | $1600 | 5 |
| 手机 | $12 | 12 |
| 管线 | $1 | 234 |


<a name="e0ff62ae"></a>
### 8. 更详细语法说明

<a name="15e3da28"></a>
## 想要查看更详细的语法说明，可以参考我们准备的 [Cmd Markdown 简明语法手册][1]，进阶用户可以参考 [Cmd Markdown 高阶语法手册][2] 了解更多高级功能。
<a name="uTy9t"></a>
## 总而言之，不同于其它 _所见即所得_ 的编辑器：你只需使用键盘专注于书写文本内容，就可以生成印刷级的排版格式，省却在键盘和工具栏之间来回切换，调整内容和格式的麻烦。**Markdown 在流畅的书写和印刷级的阅读体验之间找到了平衡。** 目前它已经成为世界上最大的技术分享网站 GitHub 和 技术问答网站 StackOverFlow 的御用书写格式。

<a name="4837aa10"></a>
## 什么是 Cmd Markdown

您可以使用很多工具书写 Markdown，但是 Cmd Markdown 是这个星球上我们已知的、最好的 Markdown 工具——没有之一 ：）因为深信文字的力量，所以我们和你一样，对流畅书写，分享思想和知识，以及阅读体验有极致的追求，我们把对于这些诉求的回应整合在 Cmd Markdown，并且一次，两次，三次，乃至无数次地提升这个工具的体验，最终将它演化成一个 **编辑/发布/阅读** Markdown 的在线平台——您可以在任何地方，任何系统/设备上管理这里的文字。

<a name="95ce40a0"></a>
### 1. 实时同步预览

我们将 Cmd Markdown 的主界面一分为二，左边为**编辑区**，右边为**预览区**，在编辑区的操作会实时地渲染到预览区方便查看最终的版面效果，并且如果你在其中一个区拖动滚动条，我们有一个巧妙的算法把另一个区的滚动条同步到等价的位置，超酷！

<a name="54e7d7e1"></a>
### 2. 编辑工具栏

也许您还是一个 Markdown 语法的新手，在您完全熟悉它之前，我们在 **编辑区** 的顶部放置了一个如下图所示的工具栏，您可以使用鼠标在工具栏上调整格式，不过我们仍旧鼓励你使用键盘标记格式，提高书写的流畅度。<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560502630655-cd90fcda-e646-41ef-9b9a-e47789a3846f.png#align=left&display=inline&height=47&originHeight=47&originWidth=573&size=0&status=done&width=573)

<a name="9694f0a6"></a>
### 3. 编辑模式

完全心无旁骛的方式编辑文字：点击 **编辑工具栏** 最右侧的拉伸按钮或者按下 `Ctrl + M`，将 Cmd Markdown 切换到独立的编辑模式，这是一个极度简洁的写作环境，所有可能会引起分心的元素都已经被挪除，超清爽！

<a name="393136fb"></a>
### 4. 实时的云端文稿

为了保障数据安全，Cmd Markdown 会将您每一次击键的内容保存至云端，同时在 **编辑工具栏** 的最右侧提示 `已保存` 的字样。无需担心浏览器崩溃，机器掉电或者地震，海啸——在编辑的过程中随时关闭浏览器或者机器，下一次回到 Cmd Markdown 的时候继续写作。

<a name="a23a965a"></a>
### 5. 离线模式

在网络环境不稳定的情况下记录文字一样很安全！在您写作的时候，如果电脑突然失去网络连接，Cmd Markdown 会智能切换至离线模式，将您后续键入的文字保存在本地，直到网络恢复再将他们传送至云端，即使在网络恢复前关闭浏览器或者电脑，一样没有问题，等到下次开启 Cmd Markdown 的时候，她会提醒您将离线保存的文字传送至云端。简而言之，我们尽最大的努力保障您文字的安全。

<a name="378f014a"></a>
### 6. 管理工具栏

为了便于管理您的文稿，在 **预览区** 的顶部放置了如下所示的 **管理工具栏**：<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560502630661-418e5498-f2fd-4741-a416-f2448a9a61eb.jpeg#align=left&display=inline&height=49&originHeight=49&originWidth=367&size=0&status=done&width=367)<br />通过管理工具栏可以：<br />发布：将当前的文稿生成固定链接，在网络上发布，分享<br />新建：开始撰写一篇新的文稿<br />删除：删除当前的文稿<br />导出：将当前的文稿转化为 Markdown 文本或者 Html 格式，并导出到本地<br />列表：所有新增和过往的文稿都可以在这里查看、操作<br />模式：切换 普通/Vim/Emacs 编辑模式

<a name="73bca1b9"></a>
### 7. 阅读工具栏

![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560502630681-ef4e363b-c4b2-438e-9e53-138449886927.jpeg#align=left&display=inline&height=34&originHeight=34&originWidth=206&size=0&status=done&width=206)<br />通过 **预览区** 右上角的 **阅读工具栏**，可以查看当前文稿的目录并增强阅读体验。<br />工具栏上的五个图标依次为：<br />目录：快速导航当前文稿的目录结构以跳转到感兴趣的段落<br />视图：互换左边编辑区和右边预览区的位置<br />主题：内置了黑白两种模式的主题，试试 **黑色主题**，超炫！<br />阅读：心无旁骛的阅读模式提供超一流的阅读体验<br />全屏：简洁，简洁，再简洁，一个完全沉浸式的写作和阅读环境

<a name="581faef4"></a>
### 8. 阅读模式

在 **阅读工具栏** 点击  或者按下 `Ctrl+Alt+M` 随即进入独立的阅读模式界面，我们在版面渲染上的每一个细节：字体，字号，行间距，前背景色都倾注了大量的时间，努力提升阅读的体验和品质。

<a name="6da09d4c"></a>
### 9. 标签、分类和搜索

在编辑区任意行首位置输入以下格式的文字可以标签当前文档：<br />标签： 未分类<br />标签以后的文稿在【文件列表】（Ctrl+Alt+F）里会按照标签分类，用户可以同时使用键盘或者鼠标浏览查看，或者在【文件列表】的搜索文本框内搜索标题关键字过滤文稿，如下图所示：<br />![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560502630687-58af457e-6640-45a3-935b-a482a32a7829.png#align=left&display=inline&height=329&originHeight=329&originWidth=649&size=0&status=done&width=649)

<a name="703a7af6"></a>
### 10. 文稿发布和分享

<a name="869e89a6"></a>
## 在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击  (Ctrl+Alt+P) 发布这份文档给好友吧！

再一次感谢您花费时间阅读这份欢迎稿，点击  (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！<br />作者 [@ghosert][3]<br />2016 年 07月 07日

```javascript
// All the code you will ever need
var hw = "Hello World!"
alert(hw);
```

My math is so rusty that I barely remember the _quadratic equation_:<br />$-b \pm \sqrt{b^2 - 4ac} \over 2a$

---


1. 支持 **LaTeX** 编辑显示支持，例如：$\sum_{i=1}^n a_i=0$， 访问 [MathJax][4] 参考更多使用方法。 [↩︎](#fnref1)
1. 代码高亮功能支持包括 Java, Python, JavaScript 在内的，**四十一**种主流编程语言。<br />
[1]: [https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown](https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown)<br />
[2]: https://www.zybuluo.com/mdeditor?url=https://www.zybuluo.com/static/editor/md-help.markdown#cmd-markdown-高阶语法手册<br />
[3]: [http://weibo.com/ghosert](http://weibo.com/ghosert)<br />
[4]: [http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)<br />
| Name  | Lunch order | Spicy  | Owes |<br />
| ----- | ----------- | ------ | ---: |<br />
| Joan  | saag paneer | medium |  $11 |<br />
| Sally | vindaloo    | mild   |  $14 |<br />
| Erin  | lamb madras | HOT    |   $5 |<br />
There are **multiple syntax highlighting themes** to choose from. Here's one of them: [↩︎](#fnref2)

