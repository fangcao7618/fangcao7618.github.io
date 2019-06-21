
---

title: vim

date: 2019-06-13 10:29:42 +0800

tags: []

---
- [Vim 有什么奇技淫巧](https://www.zhihu.com/question/27478597/answer/639544215)？
- [Vim实用插件推荐](https://zhuanlan.zhihu.com/p/24742679)
- [笨方法学Vimscript](http://learnvimscriptthehardway.stevelosh.com/)面向那些想学会如何自定义[Vim](http://www.vim.org/)编辑器的用户。
- [Mac开发配置手册](https://aaaaaashu.gitbooks.io/mac-dev-setup/content/iTerm/zsh.html)

<a name="sS8TM"></a>
## 安装[macvim](https://macvim-dev.github.io/macvim/)
mac预装了vim，但官方的 vim 在 Mac 上只有一个很不完善的，长期没人维护的 Carbon 图形用户界面。[macvim](https://link.jianshu.com?t=http://macvim-dev.github.io/macvim/) 主要是在此基础上添加了一个完整的 Cocoa 用户界面，其核心部分和 vim 同步。MacVim 采用了分离进程的方式，一个 MacVim 程序可以启动多个 vim 进程，每个显示在一个 MacVim 窗口中，这是官方的 vim 和其他平台下的 gvim 所不支持的。MacVim 还支持很多 Mac OS X 原生的界面特性，比如工具栏、滚动条、全屏显示、Mac 菜单快捷键的绑定等。

```bash
# 查看预装vim版本
vim --version

# 查看预装vim路径
where vim
```
<a name="PRnie"></a>
### 安装
有两种方式来安装macvim:

1. Github上下载[`macvim.dmg`](https://link.jianshu.com/?t=http://macvim-dev.github.io/macvim/)安装包进行安装
1. 使用[Homebrew](https://link.jianshu.com/?t=https://aaaaaashu.gitbooks.io/mac-dev-setup/content/Homebrew/index.html)安装 [https://aaaaaashu.gitbooks.io/mac-dev-setup/content/Homebrew/index.html](https://aaaaaashu.gitbooks.io/mac-dev-setup/content/Homebrew/index.html)

这也是我们所采用的方式：

```bash
brew install macvim
```

<a name="tSVd6"></a>
### 建立软链接(这步可以不走)
无论使用哪种方式进行安装，可以在MacVim.app包文件中找到mvim和vim的可执行文件，要在shell中方便的执行这些命令，可以：

1. 将可执行文件所在路径添加到环境变量`$PATH`中
1. 将可执行文件复制到环境变量`$PATH`中的某一个路径下；
1. 在`$PATH`中的某一个路径下创建该可执行文件的软/硬链接；
1. 为可执行文件设置别名，并添加到配置文件中（/.zshrc）；

这里推荐在/usr/local/bin目录下为mvim软链接的方式。同时，mac预装vim版本过低，推荐使用MacVim.app包中的vim将其替代,如果想同时保留原来预装的/usr/bin/vim中的vim，可以通过创建别名来将其“覆盖”掉。

```bash
# 将可执行文件所在路径添加到环境变量`$PATH`中，单引号内的字符会原样输出
echo 'export PATH=/usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/bin:$PATH' >> ~/.zshrc

# 或将可执行文件mvim复制到/usr/local/bin/路径下
cp /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/bin/mvim /usr/local/bin/mvim

# 或者在/usr/local/bin/路径中为mvim建立软链接
ln -s /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/bin/mvim /usr/local/bin/mvim

# 为macvim中的vim创建别名，将其添加至~/.zshrc配置文件
echo 'alias vim="/usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/MacOS/vim"' >> ~/.zshrc
# 重新加载.zshrc以使修改生效 
source ~/.zshrc
```

**安装验证**<br />终端输入vim，终端vim显示如下:<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560908646250-e3c1de5f-82ca-4a2c-878c-f6cb69cdd983.png#align=left&display=inline&height=651&name=image.png&originHeight=1302&originWidth=1918&size=1706037&status=done&width=959)<br />终端输入mvim，弹出GUIvim如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560908668483-db364b87-5124-43d2-b1b1-e7215a957a0c.png#align=left&display=inline&height=415&name=image.png&originHeight=830&originWidth=1350&size=535236&status=done&width=675)

<a name="LPTFH"></a>
## 配置文件
在vim启动过程中，首先将查找配置文件并执行其中的命令，而这些初始化文件一般有vimrc、gvimrc和exrc三种。通过`:version`命令可以查看vim的配置文件信息：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560908755893-d2bf3bf9-1029-4b52-b8ab-cfaa65be5ea6.png#align=left&display=inline&height=861&name=image.png&originHeight=1722&originWidth=1604&size=1307772&status=done&width=802)
<a name="DWN7f"></a>
#### 配置文件的位置
vim的配置文件有全局和用户两种版本，分别存放于`$VIM`和`$HOME`目录中，用户配置文件默认是没有的，必要时由用户自己在`$HOME`目录下创建。可以使用`:echo`命令查看他们的路径，使用`:e`命令进入目录：

```bash
:echo $VIM
/usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim

:echo $HOME
/Users/fangcao
```

1. vimrc是vim最常用的配置文件
1. gvim是Gvim的配置文件
1. exrc仅用于向后兼容olvi/ex；除非你使用vi-compatible模式，否则不需要关注exrc配置文件

<a name="ArVpM"></a>
#### 配置文件的加载顺序(这步也可以不用)
可以通过`:scriptname`查看各脚本的加载顺序:

```bash
1: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/vimrc
  2: ~/.vimrc
  3: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/syntax/syntax.vim
  4: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/syntax/synload.vim
  5: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/syntax/syncolor.vim
  6: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/filetype.vim
  7: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/menu.vim
  8: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/autoload/paste.vim
  9: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/runtime/ftoff.vim
 10: ~/.vim/bundle/Vundle.vim/autoload/vundle.vim    
  ......
 85: /usr/local/Cellar/macvim/8.0-133/MacVim.app/Contents/Resources/vim/gvimrc
 86: ~/.gvimrc    
  ......
```
可以看到：macvim在启动时会依次加载全局vimrc>>用户.vimrc>>全局gvimrc>>用户.gvimrc，而终端vim在启动既不加载gvimrc也不加载.gvimrc也就是说：

1. 用户配置文件中的配置会覆盖全局配置文件的配置；因此，我们可以通过创建~/.vimrc来修改vim的默认配置。
1. 对GUIvim，gvimrc会覆盖vimrc中的配置；因此，我们可以通过创建~/.vimrc使终端vim和GUIvim拥有不同的配置。此外，GUIvim支持更多扩展，有些功能在终端vim中无法使用。
<a name="4aQEt"></a>
#### 创建用户配置文件

```bash
# 切换至用户目录
cd ~
# 使用mvim创建并打开.vimrc
mvim .vimrc
```
<a name="pHcwl"></a>
#### 编辑配置文件

```bash
可以使用以下命令，新建缓冲区来编辑配置文件：
:edit $MYVIMRC
也可以使用以下命令，新建标签页来编辑配置文件：
:tabedit $MYVIMRC
```
当然也可以使用任何其他文本编辑器打开配置文件进行编辑。

<a name="OdCbo"></a>
#### 应用配置文件
修改配置文件后，需要重新启动Vim，或使用:source命令来应用新的设置：

```bash
:source $MYVIMRC
```
我们可以在配置文件中增加以下命令，在保存后自动应用配置：

```bash
autocmd bufwritepost .vimrc source $MYVIMRC
```
<a name="NWSje"></a>
## 配置文件基本配置
<a name="n05H8"></a>
### 显示中文帮助

1. 下载[vimdoc](https://link.jianshu.com/?t=https://sourceforge.net/projects/vimcdoc/?source=typ_redirect)
1. 将文件解压到~/.vim/doc，若路径不存在则自己创建
1. 打开vim执行:helptags ~/.vim/doc
1. 在~/.vimrc中进行配置：

```bash
set helplang=cn 
if version >= 603
    set helplang=cn
    set encoding=utf-8
endif
```


没有完毕<br />转自：[https://www.jianshu.com/p/923aec861af3](https://www.jianshu.com/p/923aec861af3)

