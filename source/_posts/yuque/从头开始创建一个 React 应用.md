
---

title: 从头开始创建一个 React 应用

date: 2019-07-04 15:10:50 +0800

tags: []

---
作者：紫心人<br />链接：https://zhuanlan.zhihu.com/p/36137966<br />来源：知乎<br />著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

同样的是一篇学习笔记，不过更像是简单翻译+再加工。<br />并不详细介绍 React 的写法。主要内容是：如何从无到有，创建并运行起来一个 React 应用。
<a name="cbxrP"></a>
#### React 简介
一句话介绍： React 是用于构建用户界面的 JavaScript 库。针对的是 View 层。<br />![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562224255365-acf5e8ce-453c-4a2c-ac68-33eedceb9518.jpeg#align=left&display=inline&height=469&originHeight=222&originWidth=600&size=0&status=done&width=1268)<br />虽然 React 只是视图层的一个 Library，但并非开箱即用。React 使用了很多较新的语法和关键字，浏览器并不完全支持。要使用 React 就必须将这些内容做一下处理。这样才能在浏览器下运行起来我们创建的 React 应用。

---

<a name="crT4x"></a>
#### create-react-app
React 官方提供了一个脚手架用于初始化React项目，使用 [create-react-app](https://link.zhihu.com/?target=https%3A//github.com/facebook/create-react-app) 可以简化手动设置流程。 官方网站的 Tutorial  也是以此为例。
```
# 安装 create-react-app 并创建 my-app 项目
$ npm install -g create-react-app
$ create-react-app my-app
# 或者
# npm版本在5.2.0+ 可以使用 npx 命令，简洁 
$ npx create-react-app my-app
# 进入项目目录，启动项目
$ cd my-app
$ npm start
```
![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562224255693-8dc9e0fb-2c53-4efe-aa4e-242cd408e5e8.jpeg#align=left&display=inline&height=780&originHeight=443&originWidth=600&size=0&status=done&width=1056)执行命令结束后信息<br />使用 create-react-app ，你只需要执行命令之后等待安装完依赖，就可以创建一个已经配置好的 React 应用程序，并可以基于此开始你的项目开发。这对新手无疑是很友好的。<br />如果你希望在老项目中引入 React，或着探究 React 到底是怎么运行起来的。那就需要自己动手来配置了。我们使用 [Babel](https://link.zhihu.com/?target=http%3A//babeljs.io/) 和 [Webpack](https://link.zhihu.com/?target=https%3A//webpack.js.org/) 来解决这个问题。

---

**新建项目**<br />我们先使用 npm init 和 git init 来初始化一个项目，然后增加下面三个文件夹：
```
.
+-- dist
+-- public
+-- src
```
在 public 目录中，存放所有静态资源。其中需要新建一个 index.html 文件，并写入如下内容（下面的HTML内容拷贝自 React 官方文档，并做了一些非常小的修改）：
```
<!-- sourced from https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <title>React Starter</title>
  </head>
  <body>
    <div id="root"></div>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <script src="../dist/bundle.js"></script>
  </body>
</html>
```
需要注意的是上面内容的第十行（为什么没有行数。。。假装有），也就是
```
<div id="root"></div>
```
这是 React 应用通过JS插入 DOM 结构的根节点。它会在配置 React 入口文件的时候用到。<br />还有第十四行 引入了一个名为 bundle 的 js 文件。
```
<script src="../dist/bundle.js"></script>
```
这是 React 通过 webpack 打包后最终输出的文件，名字随意。不过本教程中我们使用 bundle。<br />现在我们已经配置好了 HTML 内容。接下来还有更多配置。<br />首先，为了保证我们编写的 React 代码可以编译为浏览器可执行的代码，我们需要使用 Babel做编译工作。

---

**Babel**<br />这里解释一下 Babel 起到什么作用：<br />为了更好的在模块化开发，避免模板和组件分离，减少复杂性。 React 使用 JSX 语法，将 HTML 模板直接嵌入到了 JS 代码里面，这样就做到了模板和组件关联。但是 JS 不支持这种包含 HTML 的语法，所以需要通过工具将 JSX 编译输出成 JS 代码才能使用。<br />而 Babel 就是我们使用的 编译 工具（不仅转换JSX，还有 ES6+ 语法等）<br />关于 Babel 的安装和配置可以查看我之前的一篇笔记：<br />[![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562224255320-81d7ceae-12d1-4117-9bfe-4311fb621607.jpeg#align=left&display=inline&height=120&originHeight=120&originWidth=180&size=0&status=done&width=180)](https://zhuanlan.zhihu.com/p/35888257)<br />在此处，我们需要安装：
```
$ npm install --save-dev babel-core@6.26.0 babel-cli@6.26.0 babel-preset-env@1.6.1 babel-preset-react@6.24.1
```
因为后续会用到 webpack 。所以此处安装了 babel-core。而这个包也正是主要用来转换我们 React 代码的 Babel 包。<br />然后在项目根目录下创建 .babelrc， 配置如下：
```
{
  "presets": ["env", "react"]
}
```
env 和 react 预设集分别用于转换 ES6+ 和 React 代码。<br />Babel 就这么简单带过，实际内容也不是很难，比较好理解。

---

**Webpack**<br />如果对 webpack 没有概念，需要先去了解一下。<br />一些关于 webpack 的入门内容也可以查看我的另一篇学习笔记：<br />[![](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1562224255315-0f644c5f-9b68-4f35-9783-04c451a7e8d3.jpeg#align=left&display=inline&height=120&originHeight=120&originWidth=180&size=0&status=done&width=180)](https://zhuanlan.zhihu.com/p/35896584)<br />配置 webpack。我们需要安装如下依赖包：
```
npm install --save-dev webpack@4.6.0 webpack-cli@2.0.14 webpack-dev-server@3.1.3 style-loader@0.21.0 css-loader@0.28.11 babel-loader@7.1.4
```
其中 webpack-dev-server 是为了方便开发过程，将我们的项目在未打包前运行在一个开发服务器上，并且可以配置 修改代码后重新加载页面，这样可以在浏览器中即时反馈代码的修改。<br />style-loader  css-loader  babel-loader 用于加载处理打包过程中 css 和 js 等文件。<br />其中 babel-loader 将 webpack 和之前安装的 babel 结合起来，将 JSX 语法的 js 文件转化后再打包。

安装之后在项目根目录下创建 webpack.config.js 文件，配置如下：
```
const path = require("path");
const webpack = require("webpack");
const bundlePath = path.resolve(__dirname, "dist/");
module.exports = {
  entry: "./src/index.js",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: 'babel-loader',
        options: { presets: ['env'] }
      },
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  },
  resolve: { extensions: ['*', '.js', '.jsx'] },
  output: {
    publicPath: bundlePath,
    filename: "bundle.js"
  },
  devServer: {
    contentBase: path.join(__dirname,'public'),
    port: 3000,
    publicPath: "http://localhost:3000/dist"
  },
  plugins: [ new webpack.HotModuleReplacementPlugin() ]
};
```
此处不再详解每个配置项。补充一下之前学习笔记中没有提到的内容。<br />rules 下的 exclude 字段：用来配置需要排除（不去这些目录下寻找 test 字段正则匹配的文件）的目录或文件<br />resolve 字段：指定 webpack 可以解析哪些拓展名的文件，配置后可以在 文件引入时不带拓展名。<br />devServer 字段： 配置开发服务器，指定服务在本地运行的端口、根目录、静态资源实际目录等。<br />最后 plugins 字段里，我们加入了一个 [Hot Module Replacement](https://link.zhihu.com/?target=https%3A//webpack.js.org/guides/hot-module-replacement/) 插件的实例。这个用于 热更新，避免每次代码修改后刷新页面。

两个保证 React 运行起来的工具到此就配置完成了。接下来就是 React 方面的配置。

---

**React**<br />安装 react 和  react-dom：
```
$ npm install --save react@16.3.2 react-dom@16.3.2
```
安装完成后，我们需要在  src 目录下新建一个 React 应用程序的入口文件 index.js。我们需要在这个文件中告诉 React 在哪里插入你想渲染的页面。这个文件十分简单，不过也可以做更多配置。
```
import React from "react";
import ReactDOM from "react-dom";
import App from "./App.js";
ReactDOM.render(
  <App />,
  document.getElementById("root")
);
```
ReactDOM.render是一个函数，它会告诉 React 渲染什么以及在哪里渲染它：<br />此处我们渲染了一个名 App 组件（接下来会创建这个组件）。<br />渲染的位置是 ID 为 'root' 的DOM元素。<br />还记得前面我们单独提到的 public/index.html 文件中的第十行。也就是这个 div 元素：
```
<div id="root"></div>
```
这就是 React 要渲染的位置。<br />现在我们在相同的 src 目录下创建 App.js 文件，并插入如下代码（如果你使用 create-react-app 脚手架，此部分应该很熟悉）：
```
import React, { Component} from "react"
import "./App.css"
class App extends Component{
  render(){
    return(
      <div className="App">
        <h1> Hello, World! </h1>
      </div>
    )
  }
}
export default App
```
我们看到这里使用 import 引入了一个 css 文件。我们之前使用 webpack 做了相应的配置，所以可以将 css 文件当做模块引入进来（当然也可以使用scss，相应的配置webpack就好）。接下来在 src 目录下继续创建 App.css文件，并插入如下代码：
```
.App {
  margin: 1rem;
  font-family: Arial, Helvetica, sans-serif;
}
```
最后你的目录将会是这样的：
```
.
+-- public
| +-- index.html
+-- src
| +-- App.css
| +-- App.js
| +-- index.js
+-- .babelrc
+-- package-lock.json
+-- package.json
+-- webpack.config.js
```

到此我们手动完成了整个 React 项目从无到有的创建。现在可以使用 webpack-dev-server --mode development 命令来运行这个项目。不过我建议将这个命令配置到 package.json 中，使用 npm start 命令启动项目。<br />你可能会发现 执行命令以后 dist 文件夹下并没有内容产生。那是因为 devServer 生成的文件会直接放在内存中运行，当服务关闭时，这些文件就随之消失了。<br />如果需要生成打包后的文件，可以配置一个 npm 的 build 命令为：<br />webpack --mode production<br />这样执行 npm run build 后就可以在 dist 文件夹下看到文件了。

---

**总结**<br />在我是个特别新的新手的时候，我只会使用各种框架提供的 CLI 来创建一个新的项目。一度对各种概念很是疑惑，不得其解。通过对 babel 、webpack 等工具了解、使用之后，算是对这一套东西在脑子里有了一个粗浅的系统概念。<br />整个配置过程并不复杂，不过涉及了两个工具可能会让新手疑惑。而且这些配置仅仅是支撑起 React 运行起来，还有更多深入的配置需要学习和探索。

---

**参考文章：**<br />[Creating a React App… From Scratch —— Jedai Saboteur](https://link.zhihu.com/?target=https%3A//blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658)<br />[Tutorial —— React](https://link.zhihu.com/?target=https%3A//reactjs.org/tutorial/tutorial.html)

<a name="R7agM"></a>
#### [Create React App 中文文档](https://s0facebook0github0io.icopy.site/create-react-app/docs/getting-started)

