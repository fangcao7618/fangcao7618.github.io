
---

title: npm 基本用法和实用技巧

date: 2019-07-01 18:04:29 +0800

tags: []

---
- [基本用法](https://github.com/theicebear/npm-basic-usage#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)
  - [安装与升级](https://github.com/theicebear/npm-basic-usage#%E5%AE%89%E8%A3%85%E4%B8%8E%E5%8D%87%E7%BA%A7)
    - [安装](https://github.com/theicebear/npm-basic-usage#%E5%AE%89%E8%A3%85)
    - [升级](https://github.com/theicebear/npm-basic-usage#%E5%8D%87%E7%BA%A7)
    - [安装指定版本的 npm](https://github.com/theicebear/npm-basic-usage#%E5%AE%89%E8%A3%85%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC%E7%9A%84-npm)
  - [常用命令](https://github.com/theicebear/npm-basic-usage#%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
    - [npm install](https://github.com/theicebear/npm-basic-usage#npm-install)
    - [npm uninstall](https://github.com/theicebear/npm-basic-usage#npm-uninstall)
    - [npm update](https://github.com/theicebear/npm-basic-usage#npm-update)
    - [npm ls](https://github.com/theicebear/npm-basic-usage#npm-ls)
    - [npm adduser](https://github.com/theicebear/npm-basic-usage#npm-adduser)
    - [npm init](https://github.com/theicebear/npm-basic-usage#npm-init)
    - [npm publish](https://github.com/theicebear/npm-basic-usage#npm-publish)
    - [npm unpublish](https://github.com/theicebear/npm-basic-usage#npm-unpublish)
    - [npm deprecate](https://github.com/theicebear/npm-basic-usage#npm-deprecate)
    - [npm dist-tag](https://github.com/theicebear/npm-basic-usage#npm-dist-tag)
    - [npm view](https://github.com/theicebear/npm-basic-usage#npm-view)
    - [npm link](https://github.com/theicebear/npm-basic-usage#npm-link)
    - [npm conifg](https://github.com/theicebear/npm-basic-usage#npm-conifg)
- [工作原理](https://github.com/theicebear/npm-basic-usage#%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)
- [实用技巧](https://github.com/theicebear/npm-basic-usage#%E5%AE%9E%E7%94%A8%E6%8A%80%E5%B7%A7)
  - [pacakge.json](https://github.com/theicebear/npm-basic-usage#pacakgejson)
    - [dependencies](https://github.com/theicebear/npm-basic-usage#dependencies)
    - [optionalDependencies](https://github.com/theicebear/npm-basic-usage#optionaldependencies)
    - [peerDependencies](https://github.com/theicebear/npm-basic-usage#peerdependencies)
    - [bundledDependencies](https://github.com/theicebear/npm-basic-usage#bundleddependencies)
    - [bin](https://github.com/theicebear/npm-basic-usage#bin)
    - [config](https://github.com/theicebear/npm-basic-usage#config)
  - [.npmrc](https://github.com/theicebear/npm-basic-usage#npmrc)
  - [.npmignore](https://github.com/theicebear/npm-basic-usage#npmignore)
  - [scripts](https://github.com/theicebear/npm-basic-usage#scripts)
  - [shrinkwrap](https://github.com/theicebear/npm-basic-usage#shrinkwrap)
  - [cache](https://github.com/theicebear/npm-basic-usage#cache)
<a name="OUQEc"></a>
## [](https://github.com/theicebear/npm-basic-usage#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)基本用法
<a name="VACUH"></a>
### [](https://github.com/theicebear/npm-basic-usage#%E5%AE%89%E8%A3%85%E4%B8%8E%E5%8D%87%E7%BA%A7)安装与升级
<a name="nCnNQ"></a>
#### [](https://github.com/theicebear/npm-basic-usage#%E5%AE%89%E8%A3%85)安装
安装 Node.js 时会自动安装 npm。
```
nvm install 4
```
<a name="h5MEU"></a>
#### [](https://github.com/theicebear/npm-basic-usage#%E5%8D%87%E7%BA%A7)升级
```
npm install npm -g
```
<a name="mETJn"></a>
#### [](https://github.com/theicebear/npm-basic-usage#%E5%AE%89%E8%A3%85%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC%E7%9A%84-npm)安装指定版本的 npm
```
npm install npm@2 -g
```
<a name="PCoEJ"></a>
### [](https://github.com/theicebear/npm-basic-usage#%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)常用命令
<a name="1ZOm6"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-install)npm install

1. 根据 `package.json` 文件安装依赖。
```
npm install
```

1. 安装指定的依赖包。
```
npm install [<@scope>/]<pkg>
```
> 如果当前目录中存在 `package.json` 文件，则安装满足文件中版本规则的最高版本；否则安装最新版本依赖包。

1. 安装指定版本的依赖包。
```
npm install [<@scope>/]<pkg>@<tag>
npm install [<@scope>/]<pkg>@<version>
npm install [<@scope>/]<pkg>@<version range>
```

1. 从本地位置安装依赖。
```
npm install <folder>
npm install <tarball file>
```
> 可以用 `npm pack` 生成 `<tarball file>`

1. 从网络位置安装依赖。
```
npm install <tarball url>
npm install <git:// url>
npm install <github username>/<github project>
```

1. 常用参数：
  - `-g, --global`：安装全局依赖，如果没有指定依赖包名，则将当前目录中的包安装至全局<br />
  - `-S, --save`：安装依赖的同时将该依赖写入 `dependencies`<br />
  - `-D, --save-dev`：安装依赖的同时将该依赖写入 `devDependencies`<br />
  - `-O, --save-optional`：安装依赖的同时将该依赖写入 `optionalDependencies`<br />
  - `-E, --save-exact`：写入 `package.json` 时带有确切版本号<br />
  - `--no-optional`：不安装 optional dependencies，可继承<br />
  - `--only={dev[elopment]|prod[uction]}`：无视 `NODE_ENV`，只安装 `devDependencies` 或仅安装除了 `devDependencies` 之外的依赖项<br />
  - `--dry-run`：走一遍安装的过程并报告结果，但实际上没有安装任何依赖<br />
2. 别名：`i`<br />
<a name="7R8Cr"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-uninstall)npm uninstall

1. 删除一个指定的依赖包，并且完全移除为了该包而安装的任何文件
```
npm uninstall [<@scope>/]<pkg>[@<version>]... [-S|--save|-D|--save-dev|-O|--save-optional]
```

1. 常用参数：与 `npm install` 类似<br />
1. 别名：`remove`、`rm`、`r`、`un`、`unlink`<br />
<a name="tKZWE"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-update)npm update

1. 升级所有依赖包至版本规则允许的最新版本，并安装缺失的依赖包
```
npm update [<pkg>...]
```

1. 常用参数：
  - `-g`：升级全局依赖包
  - `--dev`：同时升级在 `devDependencies` 中的依赖包
  - `--depth Infinity`：从 `npm@2.6.1` 起 `npm update` 默认仅升级顶层依赖，使用该参数升级所有依赖包
  - `--save`：升级依赖包，同时记录升级后的版本
2. 别名：`up`、`upgrade`<br />
<a name="53moF"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-ls)npm ls

1. 以树形结构打印依赖包及其版本
```
npm ls [[<@scope>/]<pkg> ...]
```

1. 常用参数：
  - `--json`：以 JSON 格式输出
  - `--long`：输出额外信息
  - `--global`：输出全局依赖信息
  - `--depth <int>`：输出依赖树的最大深度
  - `--prod[uction]`：仅输出 `dependencies` 中的依赖
  - `--dev`：仅输出 `devDependencies` 中的依赖
2. 别名：`list`、`la`、`ll`<br />
<a name="6WLpO"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-adduser)npm adduser
登录 npm
```
npm adduser
```
<a name="0adne"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-init)npm init

1. 提问，然后产生一个 `package.json` 文件
```
npm init [-f|--force|-y|--yes]
```

1. 常用参数：
  - `-f, --force, -y, --yes`：使用默认的答案，不再提问
  - `--scope <scope>`：指定新模块的 scope，例如 `mtfe`
<a name="bH3VH"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-publish)npm publish

1. 发布一个新的包，或一个包的新版本
```
npm publish [<tarball>|<folder>] [--tag <tag>] [--access <public|restricted>]
```
> 如果没有 tarball 或 folder 被指定，则使用当前目录

1. 常用参数：
  - `--tag <tag>`：给被发布的包注册指定的 tag，如果没有该参数，则默认使用 `latest`
<a name="VBJ8m"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-unpublish)npm unpublish
取消发布一个包，或一个包的某些版本
```
npm unpublish [<@scope>/]<pkg>[@<version>]
```
<a name="v5tIs"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-deprecate)npm deprecate
弃用一个包，或一个包的某些版本，尝试安装这些弃用包的用户将会收到警告
```
npm deprecate <pkg>[@<version>] <message>
```
<a name="uBrUi"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-dist-tag)npm dist-tag

1. 给一个包的某个版本注册 tag
```
npm dist-tag add <pkg>@<version> [<tag>]
```

1. 移除一个 tag
```
npm dist-tag rm <pkg> <tag>
```

1. 显示指定包的所有 tag
```
npm dist-tag ls [<pkg>]
```
<a name="iraAO"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-view)npm view

1. 显示一个包的详细信息
```
npm view [<@scope>/]<name>[@<version>] [<field>[.<subfield>]...]
```
> `<field>` 和 `<subfield>` 表示输出信息中的字段

1. 别名：`info`、`show`、`v`<br />
<a name="aTxTO"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-link)npm link
将一个本地目录中的模块符号链接至一个项目的依赖中，实现上述功能需要两步：

1. 在模块目录中执行下面的命令，创建一个从全局依赖指向当前目录的符号链接
```
npm link
```
```
/usr/local/Cellar/nvm/0.25.4/versions/node/v4.4.4/lib/node_modules/handgrip
-> /Users/Dylan/handgrip
```

1. 在其他目录中执行下面的命令，创建一个从局部依赖指向全局依赖的符号链接
```
npm link [<@scope>/]<pkg>[@<version>]
```
> `[<@scope>/]<pkg>[@<version>]` 所表示已经执行了第一步的模块，或其所包含的版本

```
# npm link handgrip
/Users/Dylan/koalition-boilerplate/node_modules/handgrip
-> /usr/local/Cellar/nvm/0.25.4/versions/node/v4.4.4/lib/node_modules/handgrip
-> /Users/Dylan/handgrip
```
由于依赖通过符号链接的方式组织，在模块目录中的修改可以立即在其他目录中生效。
<a name="AO1sx"></a>
#### [](https://github.com/theicebear/npm-basic-usage#npm-conifg)npm conifg

1. 设置一个配置项
```
npm config set <key> <value> [-g|--global]
npm set <key> <value> [-g|--global]
```

1. 如果配置项的值阙如，将采用默认值 `true`。
1. 读取一个配置项
```
npm config get <key>
npm get <key>
```

1. 删除一个配置项
```
npm config delete key
```

1. 列出所有的配置
```
npm config list
```

1. 在编辑器中打开配置文件
```
npm config edit
```

1. 使用 `--global` 来打开全局配置文件。
<a name="gAGTg"></a>
## [](https://github.com/theicebear/npm-basic-usage#%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)工作原理
> 下面的内容基本上翻译了 [npm v3 Dependency Resolution](https://docs.npmjs.com/how-npm-works/npm3)、[npm3 Duplication and Deduplication](https://docs.npmjs.com/how-npm-works/npm3-dupe)、[npm3 Non-determinism](https://docs.npmjs.com/how-npm-works/npm3-nondet) 这三篇文章

npm v3 依赖解析的主要思想：尽可能地减少间接依赖安装目录的深度，最理想的情况是与直接依赖安装在同一目录下，通过这种方式来减少依赖目录的嵌套，缓解整个依赖目录层次过深的问题。（因为 Windows 中文件路径的长度不能大于 260 个字符。）<br />🌰：<br />假如我们有模块 A，模块 A 依赖了模块 B。

然后我们创建了已依赖模块 A 的应用 App。<br />在执行 `npm install` 的时候，npm v3 会把模块 A 及其依赖模块 B 都安装在 `/node_modules` 目录中。（npm v2 则会把模块 B 会嵌套在模块 A 中。）

此时，我们的应用 App 又需要依赖模块 C，而模块 C 依赖了另一个版本的模块 B。

然而，由于模块 B v1.0 已经被安装在了顶层依赖目录中，模块 B v2.0 就无法安装到同一位置了。这种情况下，npm v3 将会默认采用 npm v2 的行为，将这个新的模块 B 嵌套在依赖它的模块中，也就是说，把模块 B v2.0 安装到模块 C 中。

在控制台打印出依赖树和目录树。

---

_如果再安装一个依赖模块 B v1.0 或 v2.0 会怎么样呢？_<br />此时，我们的应用 App 又需要依赖模块 D，而模块 D 与模块 C 一样，依赖了模块 B v2.0。

由于模块 B v1.0 已经被安装在了顶层依赖目录中，模块 B v2.0 就无法安装到同一位置了。因此，尽管模块 C 中已经有了一份拷贝，模块 B v2.0 还是被安装到了模块 D 中（否则就 requrie 不到了）。

如果一个间接依赖被两个以上的包所依赖，且不能安装在顶层依赖目录中，那么这个间接依赖会被复制一份，并嵌套在直接依赖的目录中。<br />相反地，如果一个间接依赖被两个以上的包所依赖，且被安装在顶层依赖目录中，那么这个依赖就不会被复制，而被依赖它的包所共享。<br />🌰，我们又加了一个依赖模块 E，模块 E 与模块 A 一样，依赖了模块 B v1.0。

由于模块 B v1.0 已经安装再来顶层依赖目录中，所以不需要复制并嵌套该模块，直接安装模块 E，然后模块 E 就可以与模块 A 共享模块 B v1.0 了。

在控制台打印出依赖树和目录树。

---

_如果我们把模块 A 升级至 v2.0，模块 A v2.0 不再依赖模块 B v1.0，而是依赖模块 B v2.0，这会怎么样呢？_<br />执行 `npm install mod-a@2`，npm v3 将做以下事情：

1. 移除模块 A v1.0
1. 安装模块 A v2.0
1. 保留模块 B v1.0，因为模块 E 仍旧依赖它
1. 由于模块 B v1.0 还在顶层依赖目录中，模块 B v2.0 被嵌套安装在模块 A v2.0 中

在控制台打印出依赖树和目录树。

最后，我们吧模块 E 升级至 v2.0，模块 E v2.0 同样不再依赖模块 B v1.0，而是依赖模块 B v2.0。

npm v3 将做以下事情：

1. 移除模块 E v1.0
1. 安装模块 E v2.0
1. 由于没有模块依赖模块 B v1.0，移除该模块
1. 由于顶层依赖目录中没有模块 B，在该目录中安装模块 B v2.0

在控制台打印出依赖树和目录树。

现在，模块 B v2.0 几乎出现在了每一个依赖目录中，这显然不够简洁，我们可以执行：
```
npm dedupe
```
这条命令可以仅保留顶层依赖目录中的模块 B v2.0，而移除其他次级目录中的拷贝。<br />在控制台打印出目录树。

---

我们让 App 回到刚才的一个状态：

在这个🌰中，我们的应用有以下 `package.json` 文件：<br />{<br />  "name": "example3",<br />  "version": "1.0.0",<br />  "description": "",<br />  "main": "index.js",<br />  "scripts": {<br />    "test": "echo \"Error: no test specified\" && exit 1"<br />  },<br />  "keywords": [],<br />  "author": "",<br />  "license": "ISC",<br />  "dependencies": {<br />    "mod-a": "^1.0.0",<br />    "mod-c": "^1.0.0",<br />    "mod-d": "^1.0.0",<br />    "mod-e": "^1.0.0"<br />  }<br />}<br />如果此时运行 `npm install`，控制台会输出以下结果：

然后，我们再次把模块 A 升级到 v2.0，模块 A v2.0 不在依赖模块 B v1.0，而是依赖模块 B v2.0：
```
npm install mod-a@2 --save
```
控制台输出：

此时，我们的依赖目录看起来是这样的：

而且我们得到了一个新的 `package.json`：<br />{<br />  "name": "example3",<br />  "version": "1.0.0",<br />  "description": "",<br />  "main": "index.js",<br />  "scripts": {<br />    "test": "echo \"Error: no test specified\" && exit 1"<br />  },<br />  "keywords": [],<br />  "author": "",<br />  "license": "ISC",<br />  "dependencies": {<br />    "mod-a": "^2.0.0",<br />    "mod-c": "^1.0.0",<br />    "mod-d": "^1.0.0",<br />    "mod-e": "^1.0.0"<br />  }<br />}<br />接着，我们运行：
```
npm install
```
控制台输出：

依赖目录变成了：

---

**总结：**

1. 依赖目录的结构取决于依赖安装的顺序

1. `npm install` （不带参数）安装出的依赖目录结构是稳定的，因为 `package.json` 中依赖的排列顺序总是字典序<br />
1. npm v3 需要尽可能的减少间接依赖安装目录的深度，于是不得不从树根至树叶一级一级遍历下来，寻找可用的最远祖先节点，严重延长了依赖的安装时间<br />
<a name="K9KJm"></a>
## [](https://github.com/theicebear/npm-basic-usage#%E5%AE%9E%E7%94%A8%E6%8A%80%E5%B7%A7)实用技巧
<a name="nSXev"></a>
### [](https://github.com/theicebear/npm-basic-usage#pacakgejson)pacakge.json
<a name="5DMsW"></a>
#### [](https://github.com/theicebear/npm-basic-usage#dependencies)dependencies
版本号的写法：

- `version`: 必须匹配确切的版本号
- `>version`、`>=version`、`<version`、`<=version`
- `~version`：如果 minor 级的版本被确定的话，允许 patch 级的版本变化；否则允许 minor 级版本变化
  - `~1.2.3` := `>=1.2.3 <1.3.0`
  - `~1.2` := `>=1.2.0 <1.3.0`
  - `~1` := `>=1.0.0 <2.0.0`
  - `~0.2.3` := `>=0.2.3 <0.3.0`
  - `~0` := `>=0.0.0 <1.0.0`
  - `~1.2.3-beta.2` := `>=1.2.3-beta.2 <1.3.0`
- `^version`：允许版本号中不修改最左非零位及其前缀的所有版本号更高的变化
  - `^1.2.3` := `>=1.2.3 <2.0.0`
  - `^0.2.3` := `>=0.2.3 <0.3.0`
  - `^0.0.3` := `>=0.0.3 <0.0.4`
  - `^1.2.3-beta.2` := `>=1.2.3-beta.2 <2.0.0`
  - `^0.0.3-beta` := `>=0.0.3-beta <0.0.4`
  - `^1.2.x` := `>=1.2.0 <2.0.0`
  - `^0.0.x` := `>=0.0.0 <0.1.0`
  - `^0.0` := `>=0.0.0 <0.1.0`
  - `^1.x` := `>=1.0.0 <2.0.0`
- `1.2.x`：`1.2.0`、`1.2.1` 等，不包括 `1.3.0`
- `*` 或空：任何版本
- `version1 - version2`：`>=version1 <=version2`
- `range1 || range2`
- `tag`：指定 tag
- `file:...`：本地路径
- `http://...`、`git...`：网络路径
  - `git://github.com/user/project.git#commit-ish`
  - `git+ssh://user@hostname:project.git#commit-ish`
  - `git+ssh://user@hostname/project.git#commit-ish`
  - `git+http://user@hostname/project/blah.git#commit-ish`
  - `git+https://user@hostname/project/blah.git#commit-ish`
- `user/repo#commit-ish`：GitHub 仓库
<a name="AJ3R4"></a>
#### [](https://github.com/theicebear/npm-basic-usage#optionaldependencies)optionalDependencies
`optionalDependencies` 中的依赖安装失败时，npm 不会停止整个安装过程。<br />模块本身应当处理由于依赖安装失败导致依赖缺失的问题，🌰如：<br />try {<br />  var foo = require('foo')<br />  var fooVersion = require('foo/package.json').version<br />} catch (er) {<br />  foo = null<br />}<br />if ( notGoodFooVersion(fooVersion) ) {<br />  foo = null<br />}

// .. then later in your program ..

if (foo) {<br />  foo.doFooThings()<br />}
<a name="Tp343"></a>
#### [](https://github.com/theicebear/npm-basic-usage#peerdependencies)peerDependencies
`peerDependencies` 表示当前模块**适配**其他某些模块，也就是只有当那些指定的模块被安装时，当前模块才会被安装。<br />🌰如：<br />{<br />  "name": "tea-latte",<br />  "version": "1.3.5",<br />  "peerDependencies": {<br />    "tea": "2.x"<br />  }<br />}<br />表示确保模块 tea-latte 只能同模块 tea 2.x 一起安装。
> 如果 `peerDependencies` 中的模块没有被明确依赖的话，npm v2 会自动安装这些模块，但 npm v3 不会再安装这些模块，而是输出一个警告。

<a name="eljYH"></a>
#### [](https://github.com/theicebear/npm-basic-usage#bundleddependencies)bundledDependencies
`bundledDependencies` 表示在当前模块打包或发布时，需要被置于模块内部的依赖。<br />使用的时机：

1. 使用的依赖不是来自于 npm，或者修改了这个依赖
1. 使用开发者自己的项目作为依赖
1. 希望在模块中包含一些文件
<a name="zfgGA"></a>
#### [](https://github.com/theicebear/npm-basic-usage#bin)bin
将可执行的文件安装到 PATH 中。可能安装到的位置有：
```
# global:
/usr/local/opt/nvm/versions/node/v4.4.4/bin/
/usr/local/bin/
# local:
./node_modules/.bin/
```
🌰：<br />{ "bin" : { "myapp" : "./cli.js" } }<br />当安装这个模块时，npm 会创建一个指向 `cli.js` 的符号链接。<br />{ "name": "my-program",<br />  "version": "1.2.5",<br />  "bin": "./path/to/program" }<br />上面的写法等价于：<br />{ "name": "my-program",<br />  "version": "1.2.5",<br />  "bin" : { "my-program" : "./path/to/program" } }
<a name="FozEp"></a>
#### [](https://github.com/theicebear/npm-basic-usage#config)config
`package.json` 文件中的 `config` 字段可以用来设置模块脚本中可以用到的配置参数。<br />🌰，如果一个模块有：<br />{ "name" : "foo",<br />  "config" : { "port" : "8080" } }<br />那么在模块脚本（如 `start`）中就可以通过 `process.env.npm_package_config_port`，访问到这个配置。<br />这个配置也可以被命令 `npm config set foo:port 8001` 覆盖。
<a name="IkhZh"></a>
### [](https://github.com/theicebear/npm-basic-usage#npmrc).npmrc
配置文件有：

- 项目配置文件（/path/to/my/project/.npmrc）
- 用户配置文件（~/.npmrc）
- 全局配置文件（/path/to/node/etc/npmrc）
- 内置配置文件（/path/to/npm/npmrc）

环境变量用法：
```
prefix = ${HOME}/.npm-packages
```
数组用法：
```
key[] = "first value"
key[] = "second value"
```
> 项目配置文件和用户配置文件的权限必须设置为只能被当前用户读写（0600），否则该配置文件会被 npm 忽略

可以通过 `npm config` 命令来管理配置文件。<br />常用配置项：

- `cache`：npm 本地缓存目录，默认 `~/.npm`
- `cache-max`：保持缓存项目且不向 registry 检查的最长时间，单位秒，默认 `Infinity`，缓存中的数据不会自动删除除非执行 `npm cache clean` 命令
- `cache-min`：保持缓存项目且不向 registry 检查的最短时间，单位秒，默认 `10`，可以置为 `999999` 等以尽量延长缓存生效时间
- `depth`：`npm ls` 等命令中的默认深度，默认 `Infinity`
- `editor`：npm 默认使用的编辑器
- `engine-strict`：如果置为 `true`，npm 将会拒绝安装不符合当前 Node.js 版本的模块
- `force`：强力执行一些命令
  - 生命周期脚本执行失败不再阻塞安装过程
  - 发布会覆盖已经发布的版本
  - 访问 registry 时会跳过缓存
- `global`：全局模式
- `globalconfig`：全局配置文件的路径
- `global-style`：以安装全局依赖的方式安装局部依赖，只有直接依赖会被放在顶层依赖目录中
- `https-proxy`：代理
- `if-present`：如果置为 `true`，`npm run-script` 就不会在脚本找不到时报错
- `ignore-scripts`：如果置为 `true`，npm 就不会运行 `package.json` 定义的脚本
- `init-module`：指定 `npm init` 命令运行的模块
- `init-author-name`：`npm init` 使用的默认作者名
- `init-author-email`：`npm init` 使用的默认作者邮箱
- `init-author-url`：`npm init` 使用的默认作者 URL
- `init-license`：`npm init` 使用的默认许可证
- `init-version`：`npm init` 使用的默认版本号
- `json`：`npm ls` 等命令输出 JSON 格式的数据
- `link`：如果置为 `true`，如果全局依赖中有合适的包，安装局部依赖时将会直接链接到这个全局依赖的包；如果全局依赖中没有该包的任何版本，则全局安装这个包，并链接到局部依赖中；其他情况则在局部依赖中安装该包
- `long`：`npm ls` 和 `npm search` 显示额外信息
- `message`：`npm version` 写在 git 提交中的信息，`%s` 将被替换为版本号
- `npat`：安装时运行测试
- `onload-script`：指定一个在 npm 加载时 `require()` 的包，编程使用 npm 时可能会有用
- `only`：与命令中的 `--only` 效果类似
- `optional`：如果置为 `false`，则不安装 `optionalDependencies` 中的依赖
- `prefix`：指定安装全局依赖的路径
- `production`：如果置为 `true`，则开启生产模式，`npm install` 将不安装开发依赖，声明周期脚本运行时自动设置 `NODE_ENV="production"`
- `registry`：指定 npm registry 的 URL
- `rollback`：移除安装失败的模块
- `save`：与命令中的 `--save` 效果类似
- `scope`：与命令中的 `--scope` 效果类似
- `shrinkwrap`：如果置为 `false`，安装时忽略 `npm-shrinkwrap.json`
- `progress`：如果置为 `false`，不显示进度条
- `loglevel`：设置输出日志的 level，置为 `silly` 可以显示全部日志
<a name="BE5hK"></a>
### [](https://github.com/theicebear/npm-basic-usage#npmignore).npmignore
当模块目录中存在 `.gitignore` 但没有 `.npmignore` 时，npm 将会忽略 `.gitignore` 中的文件。如果目录中存在 `.npmignore`，npm 将会根据 `.npmignore` 忽略文件。<br />默认被 npm 忽略，不需要添加到 `.npmignore` 中的文件：

- `.*.swp`
- `._*`
- `.DS_Store`
- `.git`
- `.hg`
- `.npmrc`
- `.lock-wscript`
- `.svn`
- `.wafpickle-*`
- `config.gypi`
- `CVS`
- `npm-debug.log`

除了 bundled dependencies 外，node_modules 中的所有文件也会被忽略。<br />下面的文件即使添加到 `.npmignore` 中的文件也不会被忽略：

- `package.json`
- `README`（及其变体）
- `CHANGELOG`（及其变体）
- `LICENSE`、`LICENCE`
<a name="ZwkeS"></a>
### [](https://github.com/theicebear/npm-basic-usage#scripts)scripts
npm 支持的生命周期脚本有：

- `prepublish`: 发布模块之前执行，也在不带任何参数的局部 `npm install` 之前执行
- `publish`、`postpublish`: 发布模块之后执行
- `preinstall`: 安装该模块之前执行
- `install`、`postinstall`: 安装该模块之后执行
- `preuninstall`、`uninstall`: 移除该模块之前执行
- `postuninstall`: 移除该模块之后执行
- `preversion`、`version`: 修改模块版本号之前执行
- `postversion`: 修改模块版本号之后执行
- `pretest`、`test`、`posttest`: 在 `test` 命令的前后执行
- `prestop`、`stop`、`poststop`: 在 `stop` 命令的前后执行
- `prestart`、`start`、`poststart`: 在 `start` 命令的前后执行.
- `prerestart`、`restart`、`postrestart`: 在 `restart` 命令的前后执行，如果 `restart` 脚本没有提供，`restart` 命令将会执行 `stop` 脚本再执行 `start` 脚本

对于自定义名称的脚本，可以通过 `npm run-script <pkg> <stage>` 来执行，匹配名称的 _pre_ 和 _post_ 命令同样也会执行。
<a name="aEYq5"></a>
### [](https://github.com/theicebear/npm-basic-usage#shrinkwrap)shrinkwrap
`npm shrinkwrap` 可以用来锁定依赖的版本号。<br />一个使用的🌰：

1. 我们有模块 A：

{<br />  "name": "A",<br />  "version": "0.0.1",<br />  "dependencies": {<br />    "B": "<0.1.0"<br />  }<br />}

1. 模块 B：

{<br />  "name": "B",<br />  "version": "0.0.1",<br />  "dependencies": {<br />    "C": "<0.1.0"<br />  }<br />}

1. 和模块 C：

{<br />  "name": "C",<br />  "version": "0.0.1"<br />}

1. 这三个模块都只有 0.0.1 这一个版本。此时运行 `npm install A`，将会得到：
```
A@0.0.1
`-- B@0.0.1
    `-- C@0.0.1
```

1. 如果模块 B 发布了 0.0.2 版本，此时运行`npm install A`，将会得到：
```
A@0.0.1
`-- B@0.0.2
    `-- C@0.0.1
```

1. 但是模块 A 的作者希望安装原来的版本，那么他可以运行：
```
npm shrinkwrap
```

1. 然后在项目目录下得到了一个`npm-shrinkwrap.json`文件：

{<br />  "name": "A",<br />  "version": "0.0.1",<br />  "dependencies": {<br />    "B": {<br />      "version": "0.0.1",<br />      "from": "B@<0.1.0",<br />      "resolved": "https://registry.npmjs.org/B/-/B-0.0.1.tgz",<br />      "dependencies": {<br />        "C": {<br />          "version": "0.0.1",<br />          "from": "C@<0.1.0",<br />          "resolved": "https://registry.npmjs.org/C/-/C-0.0.1.tgz"<br />        }<br />      }<br />    }<br />  }<br />}

1. `npm shrinkwrap`命令根据当前目录中的 node_modules 目录锁定了依赖版本号，此时再运行`npm install`，该命令的行为将变为：
  1. 重新构造 `npm-shrinkwrap.json` 中描述的依赖树，如果一个依赖项中的 `resolved` 字段可用，则使用该字段获取依赖，否则使用 `version` 字段来获取依赖
  1. 以普通的方式安装 `npm-shrinkwrap.json` 中缺失的依赖

---

添加或升级依赖包的方法：

- 添加或升级一个依赖包
```
npm install --save <pkg>
```

- 升级所有依赖包
```
npm install --no-shrinkwrap
```
注意事项：

1. 如果 node_modules 目录中的依赖比 `package.json` 中定义的多或者少，`npm shrinkwrap` 命令将会失败
1. `npm shrinkwrap` 命令不锁定 `devDependencies` 中依赖的版本，即 `npm-shrinkwrap.json` 中不包含开发依赖；如果希望锁定开发依赖的版本，则需要在运行命令时加上 `--dev` 参数
1. shrinkwrap 不会继承，即执行过程中不会访问依赖的 `npm-shrinkwrap.json` 文件；但是，依赖中如果有 `npm-shrinkwrap.json` 文件，在安装该依赖的时就会按照这个文件来安装相关的模块到 node_modules 目录中，如果没有 `npm-shrinkwrap.json` 文件，开发者需要在使用 shrinkwrap 前自行确认 node_modules 目录中的依赖都是有效的；shrinkwrap 总是据当前目录中的 node_modules 目录中的内容锁定依赖版本号
<a name="FFYiN"></a>
### [](https://github.com/theicebear/npm-basic-usage#cache)cache
npm 将数据缓存在 `npm config get cache` 命令指定的路径中。<br />当局部安装一个模块时，npm 会执行以下步骤：

1. 检查缓存中的模块信息文件（.cache.json，包括 ETag 等信息）是否存在并在免检时间内
1. 如果存在合适的缓存信息文件且没有超过免检时间，执行步骤 6
1. 获取该模块的最新信息文件，然后计算出合适的模块版本号
1. 如果缓存中有该版本号的模块，则执行步骤 6
1. 下载该版本号的模块，并将其载入缓存中
1. 取缓存中的文件，并将其安装至目标路径中

`npm cache` 命令的用法：

1. 向缓存中添加指定的模块：
```
npm cache add <tarball file>
npm cache add <folder>
npm cache add <tarball url>
npm cache add <name>@<version>
```

1. 显示缓存中的数据：
```
npm cache ls [<path>]
```

1. 清空缓存：
```
npm cache clean [<path>]
```
npm 缓存的改进方案：

1. [local-npm](https://github.com/nolanlawson/local-npm)：一个本地 npm 镜像，但是仅缓存已经安装过的模块，没有网络时自动回退到本地<br />
1. [npm_lazy](https://github.com/mixu/npm_lazy)

转自：[https://github.com/theicebear/npm-basic-usage](https://github.com/theicebear/npm-basic-usage)

