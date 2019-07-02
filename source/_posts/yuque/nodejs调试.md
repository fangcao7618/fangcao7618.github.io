
---

title: nodejs调试

date: 2019-07-01 13:52:03 +0800

tags: []

---
<a name="96CYy"></a>
## 使用Inspector调试Node.js程序
<a name="JSqkk"></a>
### Inspector介绍
[http://nodejs.cn/api/inspector.html](http://nodejs.cn/api/inspector.html)

<a name="cF5x1"></a>
#### 使用Inspector调试Node.js的优势

- 可查看当前上下文的变量
- 可观察当前函数调用堆栈
- 不侵入代码
- 可在暂停状态下执行指定代码

```bash
mkdir node-debug
code node-debug
```

在mac中使用vscode的命令code以及使用命令行在vscode中打开文件夹<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561961439209-1b583b4a-022d-4928-a242-ac1b96729f13.png#align=left&display=inline&height=1280&name=image.png&originHeight=1280&originWidth=2128&size=196618&status=done&width=2128)<br />使用command + shift + p，并输入shell，选择Shell Command:Install ‘code’ command in PATH,如上图。<br />完成后，即可使用vscode的命令行 code.

如何用code命令打开文件夹<br />1.在新窗口中打开文件夹<br />cd到需要打开的文件夹下，然后使用code -n .<br />上面指令中的-n 表示new window<br />2.在原窗口中打开文件夹<br />cd到需要打开的目录下，使用code -r .<br />上面指令中的-r表示 reuse window<br />至于code的其它命令，可以使用code -h查看和学习。

```javascript
let v = 0;
function a(v) {
    let v2 = 100;
    v += v2;
}

function b() {
    a(v);
}

b();
```
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561960411904-39c8aab0-81c9-4f96-894c-4320c7cd7da5.png#align=left&display=inline&height=840&name=image.png&originHeight=840&originWidth=1027&size=114066&status=done&width=1027)

devtoolsFrontendUrl用于谷歌浏览器调试
<a name="Ln2Wr"></a>
#### Inspector的构成以及原理

- WebSockets服务（监听命令）
- Inspector协议 http://nodejs.cn/api/inspector.html
- HTTP服务（获取元信息）

![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561960440489-085a007c-305a-496b-a097-ec6232c392ec.png#align=left&display=inline&height=178&originHeight=337&originWidth=1410&status=done&width=746)
<a name="2plGR"></a>
### 
<a name="y2IzT"></a>
### 激活调试

- 如何激活调试
```bash
node --inspect app.js
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561962037538-fe23efab-7739-4c10-8435-a25dea19a948.png#align=left&display=inline&height=120&name=image.png&originHeight=120&originWidth=1262&size=156048&status=done&width=1262)

因为代码执行完了，所以没有下文了

我们接下来弄一个可以一直看的

那用express弄一个<br />[http://www.expressjs.com.cn/](http://www.expressjs.com.cn/)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561963088962-0d608ff7-45cd-4728-9bdc-39ff99ac23ff.png#align=left&display=inline&height=277&name=image.png&originHeight=277&originWidth=779&size=49042&status=done&width=779)<br />例子有了

```bash
node app.js
```
关闭指定的端口号：<br />lsof -i:端口号   <br />kill -9 6422<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561963620480-431f2075-9b18-4612-8a2e-b412da7d3004.png#align=left&display=inline&height=132&name=image.png&originHeight=132&originWidth=1178&size=154915&status=done&width=1178)
<a name="CUlwA"></a>
### 为什么node --inspect app.js 不能激活
**![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561963935485-312e4533-0802-4980-a438-7163cdf9ef0a.png#align=left&display=inline&height=239&name=image.png&originHeight=239&originWidth=796&size=31706&status=done&width=796)**<br />**<br />这样设置后就好了

- 激活调试后会发生什么
1. Node进程通过WebSockets监听调试信息
1. 启动一个HTTP服务，提供元信息

- 如何调试没有激活的Node.js程序？

在Linux和OSX上，可以监听到SIGUSR1发送的调试信息
<a name="X50BX"></a>
### 调试客户端
Chrome DevTools

- 访问chrome://inspect 点击配置按钮，确保Host和Port对应

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561965211085-98690bea-fa37-494e-9aca-41f15d35f4af.png#align=left&display=inline&height=361&name=image.png&originHeight=361&originWidth=600&size=54217&status=done&width=600)

- 访问元信息中的devtoolsFrontendUrl

![](https://cdn.nlark.com/yuque/0/2019/png/263301/1561960440489-085a007c-305a-496b-a097-ec6232c392ec.png#align=left&display=inline&height=178&originHeight=337&originWidth=1410&status=done&width=746)

- 点击绿色小图标

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561969129902-f872fe7e-0d8a-42f8-be4a-51e54ae00c8d.png#align=left&display=inline&height=238&name=image.png&originHeight=238&originWidth=753&size=31699&status=done&width=753)


<a name="xC68e"></a>
#### 调试客户端-Chrome devtools
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561969171621-b86ba10b-bc50-4a86-af5d-04a1f874cac5.png#align=left&display=inline&height=1136&name=image.png&originHeight=1136&originWidth=2006&size=972107&status=done&width=2006)
<a name="7twRI"></a>
#### 调试客户端-vscode

- 启动方式：按F5

这种方式适合简单的场景

- 配置launch.json or “打开自动附加”

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561970135254-1a0b5ac4-d2a4-4760-8830-2ece8ec21dbc.png#align=left&display=inline&height=209&name=image.png&originHeight=209&originWidth=670&size=42124&status=done&width=670)<br />添加参数<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561970309681-5147d3a3-45ff-47c7-9820-4b1586dfc3ea.png#align=left&display=inline&height=116&name=image.png&originHeight=116&originWidth=690&size=24843&status=done&width=690)<br />后面在配置文件里面可以配置成<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561970331172-ee464930-554e-4f91-afbf-968abb2238a6.png#align=left&display=inline&height=368&name=image.png&originHeight=368&originWidth=634&size=47155&status=done&width=634)<br />点击调试面板，两处任意一个都行，都可以开启调试<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561970390347-aba6f60a-ecee-4499-aed1-5711b408e1ad.png#align=left&display=inline&height=1080&name=image.png&originHeight=1080&originWidth=590&size=75989&status=done&width=590)<br />添加配置<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561970810528-f896c0e1-da5d-4ea7-8efd-4e8938cd411f.png#align=left&display=inline&height=126&name=image.png&originHeight=126&originWidth=351&size=6887&status=done&width=351)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1561970780178-e458f5c2-7328-4e10-a13e-b3eddb003825.png#align=left&display=inline&height=184&name=image.png&originHeight=184&originWidth=766&size=18358&status=done&width=766)可以启动多个服务

- 调试动作
- 数据展现
- Log Point
- RERL
<a name="Fl1wc"></a>
### 命令行参数介绍
带领大家解读[官网文档](http://nodejs.cn/api/cli.html)，并通过实际案例介绍；<br />[debugger调试器](http://nodejs.cn/api/debugger.html)

