
---

title: Git

date: 2019-06-12 11:29:49 +0800

tags: []

---
<a name="zvFd0"></a>
#### [git查看命令地址](https://www.runoob.com/git/git-commit-history.html)

不了解GitHub,可以看 [https://github.com/xirong/my-git/blob/master/how-to-use-github.md](https://github.com/xirong/my-git/blob/master/how-to-use-github.md)

作为一名开发者，GitHub上面有很多东西值得关注学习，可是刚刚接触GitHub，怎样一步步学习使用GitHub？怎样更高效的利用GitHub？ 在这里搜集整理网络上面的资料，汇总成这么一篇repo 《GitHub使用指南》，供大家一起学习。 ![](https://cdn.nlark.com/yuque/0/2019/png/263301/1560851863515-0c037e73-537f-470a-931e-8bc2e0a0a8e1.png#align=left&display=inline&height=20&originHeight=64&originWidth=64&size=0&status=done&width=20)

- [GitHub 入门使用教程-图文并茂](http://developer.51cto.com/art/201407/446249_all.htm) 很简洁的说明如何使用，看图即可明白。
- [GitHub help](https://help.github.com/) Sometimes you just need a little help. 中文翻译版在此[GitHub 帮助文档](https://github.com/waylau/github-help)。
- [GitHub 之 fork 简介指南](https://linux.cn/article-4292-1.html) 帮你理解清楚什么是fork，fork 的工作流有哪些。
- [GitHub-cheat-sheet](https://github.com/tiimgreen/github-cheat-sheet) 关于使用 git 和 GitHub 的一些技巧汇总，中文版在此[GitHub秘籍](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.zh-cn.md)
- [The GitHub Blog](https://github.com/blog) GitHub 官方博客，关注最新动态。
- [How to Build a GitHub](http://zachholman.com/talk/how-to-build-a-github/) GitHub一名早期员工介绍GitHub的历史，5年108名员工无人离职。
- [阳志平：如何高效利用GitHub](http://www.yangzhiping.com/tech/github.html) 介绍的挺全，以及一些用法，如怎样利用GitHub来学习、演讲找工作等。
- [GitHub 支持的 emoji表情 emoji-cheat-sheet](http://www.emoji-cheat-sheet.com/) ✌️ 👏 感觉不好找到需要的表情？试试[Emoji Searcher](http://emoji.muan.co/)
-  [GitHub guides](https://guides.github.com/) 从`Contributing to Open Source on GitHub`、`Hello World`、`Forking Projects`、`Be Social`、`Making Your Code Citable`、`Mastering Issues`、`Mastering Markdown`、`Mastering Wikis`、`Getting Started with GitHub Pages` 等9个方面图文详细讲解每一步如何使用，以及能做哪些功能。
- [fork-me-on-GitHub](https://github.com/blog/273-github-ribbons) 个人博客、技术博客等如果需要添加GitHub 的彩带，可以使用此方法。
- [蒋鑫-GotGitHub](https://github.com/xirong/my-git/blob/master/GotGitHub.md) 《Git权威指南》的作者，对GitHub有很深的了解。（由于首页打开太慢，放到了本文目录中，下面的文章既是）

<a name="uzK6R"></a>
# GitHub Skills

- [Using Git blame to trace changes in a file](https://help.github.com/articles/using-git-blame-to-trace-changes-in-a-file/) 如果你想看某一个文件中每一行是谁修改的，为什么修改？那么尽情的使用 `blame` 按钮，发现文件的历史。
- [GitHub 搜索技巧](https://help.github.com/categories/search/)
- [Closing issues via commit messages - 通过提交信息关闭Issues](https://help.github.com/articles/closing-issues-via-commit-messages/)
- [Update your forked code from original repository - 如何更新自己 Fork 的代码](https://github.com/ysc/APDPlat/wiki/%E5%A6%82%E4%BD%95%E6%9B%B4%E6%96%B0%E8%87%AA%E5%B7%B1Fork%E7%9A%84%E4%BB%A3%E7%A0%81)

更多关于 GitHub 的内容请查看：[GitHubHelp](https://help.github.com/) 查找需要的信息。<br />
<br />原文地址：[http://www.worldhello.net/gotgithub/index.html](http://www.worldhello.net/gotgithub/index.html)<br />

- [git - Retrieve the commit log for a specific line in a file? - Stack Overflow](http://stackoverflow.com/questions/8435343/retrieve-the-commit-log-for-a-specific-line-in-a-file)<br />
- [Git - git-blame Documentation](https://git-scm.com/docs/git-blame)<br />
- [Git Book 中文版 - 查找问题的利器 - Git Blame](http://gitbook.liuhui998.com/5_5.html)<br />
- [每一行代码都有记录—如何用git一步步探索项目的历史 - Alexia(minmin) - 博客园](http://www.cnblogs.com/lanxuezaipiao/p/3552805.html)<br />
<a name="pBKAZ"></a>
# [Git & Gitlab 使用指南](https://zhuanlan.zhihu.com/p/36062308)


<a name="niBDX"></a>
# 一、Git 有什么奇技淫巧？

- 如何以光速查看一行代码的提交记录
- 在保存所有的文件的情况下，删除所有的commit记录：
1. 检出

```bash
git checkout --orphan latest_branch
```

2. 添加所有文件夹

```bash
git add -A
```

3. 评论消息改动

```bash
git commit -am "just come and commit"
```

4. 删除分支

```bash
git branch -D master
```

5. 将现有分支设置为master

```bash
git branch -m master
```

6. push

```bash
git push -f origin master
```

7. 在尝试过所有命令都不能把你从深渊里挽救出来的时候, **git reflog 也许能起作用。**
7. 比如撤销一次 rebase（rebase 可是会直接修改历史的，一定要了解原理后再使用） [Undoing a git rebase](https://link.zhihu.com/?target=http%3A//stackoverflow.com/questions/134882/undoing-a-git-rebase)
7. 每次 merge 完总是出现很多 .orig 文件，使用 git clean -f 干掉所有 untracked files
7. rebase 一个 diverged 分支一直要解决冲突很痛苦，可以尝试在自己的分支先 squash 一下，git rebase -i，然后再 rebase 主干，解决一次冲突就 ok 了
7. 本地有很多其实早就被删除的远程分支，可以用 git remote prune origin 全部清除掉，这样再 checkout 别的分支时就清晰多了.
7. <br />
```bash
git bisect
```
有没有过写了一天的代码，checkin无数，结果突然发现之前没注意的地方break的时候？<br />这个时候要在茫茫commits里寻找那个错误的commit是多么的痛苦啊。`git-bisect`就是大救星！<br />git-bisect本质上就是一个二分法，用起来也很简单：

```bash
git bisect start        #start
git bisect bad          #current branch is bad
git bisect good <SHA-1> #some old commit that is good
```
然后只要不停的告诉git当前commit是不是好的，

```bash
git bisect good
```
or

```bash
git bisect bad
```
就能找到罪魁祸首了！

<a name="Vj5BS"></a>
# 二、Git log常见用法
<a name="MH8hS"></a>
# 三、[git checkout 命令详解](https://www.cnblogs.com/kuyuecs/p/7111749.html)
<a name="us3H7"></a>
# 四、[git重要的三个命令stash, checkout, reset的一些总结](https://www.cnblogs.com/shih/p/6826743.html)


1. 正常的情形，修改工作区的文件然后add，commit，我使用git一般的流程是：git status ——> git stash save "message..."——> git pull --> git stash pop ——> git add . 或 git add filename ——> git commit -m 'message...' ——> git push 其中 . 表示所有的文件。
1. 只需要撤销工作区的文件修改，即用暂存区的文件覆盖工作区中的文件

git checkout -- filename

3. 当修改的文件已经add到暂存区，需要撤销这次添加，即撤销上一次git add filename 操作：

git reset -- filename / git reset HEAD filename<br />      撤销暂存区内所有的文件改动:<br />git reset / git reset HEAD

4. 当对上次提交不满意，可以让HEAD指针回退，而暂存区和工作区可以不用动

git reset --soft HEAD^

5. 如果让工作区不改变，而暂存区和引用（HEAD指针）回退一次

git reset --mixed HEAD^

6. 当需要彻底撤销最近的提交，HEAD指针、暂存区、工作区都回到上次的提交状态，自上一次以来的提交全部丢失

git reset --hard HEAD^
<a name="UItOW"></a>
#### git stash 用于保存和恢复工作进度。  

  - git stash 保存当前的工作进度。会分别对暂存区和工作区的状态进行保存。
  - git stash list 显示进度列表。此命令显然暗示了git stash 可以多次保存工作进度，并用在恢复时候选择。
  - git stash drop [] 删除一个存储的进度。默认删除最新的进度。
  - git stash clear 删除所有存储的进度。
  - git stash pop [--index] [] 
    - --index 参数：不仅恢复工作区，还恢复暂存区
    - <stash> 指定恢复某一个具体进度。如果没有这个参数，默认恢复最新进度
    -  如：以下命令恢复编号为0的进度的工作区和暂存区 
```bash
# git stash pop --index stash@{0}
```

    1. 如果不使用任何参数，会恢复最新保存的工作进度，并将恢复的工作进度从存储的工作进度列表中清除。
    1. 如果提供<stash>参数（来自git stash list显示的列表），则从该<stash>中恢复。恢复完毕也将从进度列表中删除<stash>。
    1. 选项--index除了恢复工作区的文件外，还尝试恢复暂存区。这也就是为什么恢复进度的时候显示的状态和保存进度前的略有不同。
  - git stash [save [--patch] [-k|--[no]keep-index] [-q|--quiet] []]
    - 这条命令实际上是git stash命令的完整版。
      - save，即如果需要在保存工作进度的时候使 用指定的说明，必须使用如下格式： git stash save “message...”
      - 使用参数--patch会显示工作区和HEAD的差异，通过对差异文件的编辑决定在进度中 最终要保存的工作区的内容，通过编辑差异文件可以在进度中排除无关内容。
      - 使用-k或者--keep-index参数，在保存进度后不会将暂存区重置。默认会将暂存区和工 作区强制重置。
  - git stash apply [--index] [] 除了不删除恢复的进度之外，其余和git stash pop 命令一样。
<a name="Pv5K4"></a>
#### 检出命令git checkout是git最常用的命令之一，同时也是一个很危险的命令，因为这条命令会重写工作区。
<br />检出命令的用法如下：<br />用法一：git checkout [-q] [] [--] ...<br />用法二：git checkout []<br />用法三：git checkout [-m] [[-b]--orphan] ] []

注：<br /><1> 为了避免路径和引用（或者提交ID）同名而发生冲突，可以在前用两个连续的短线（短号）--作为分隔。<br /><2> 在用法一中，

  1. 省略commit：用暂存区的文件覆盖工作区的文件。
  1. 加上commit：用指定提交中的文件覆盖暂存区和工作区中的文件。

<3>在用法二中，会改变HEAD头指针

  1.  加上<branch>：因为只有HEAD切换到一个分支才可以对提交进行跟踪，否则仍然会进入“分离头指针”的状态。在“分离头指针”状态下的提交不能被引用关联到，从而可能丢失。

所以用法二（加上）最主要的作用就是切换到某分支。<br />(2）省略：则相当于对工作区进行状态检查。<br /><4>在用法三中，主要是创建和切换到新的分支（），新的分支从指定的提交开始创建。新分支和我们熟悉的master分支没有什么实质的不同，都是在refs/heads命名空间下的引用。
<a name="9qzYM"></a>
#### 下图所示的版本库模型图描述了git checkout实际完成的操作。
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560848425192-6876ce8a-b4b0-4c9a-b11a-03de3e0712f6.png#align=left&display=inline&height=208&name=image.png&originHeight=232&originWidth=558&size=125896&status=done&width=500)<br />使用：

- git checkout branch  检出branch分支。要完成图中的三个步骤，更新HEAD以指向branch分支，以及用branch 指向的树更新暂存区和工作区。
- git checkout / git checkout HEAD 汇总显示工作区、暂存区与HEAD的差异。
- git checkout -- filename  用暂存区中filename文件来覆盖工作区中的filename文件。相当于撤销自上次执行git add filename以来（如果执行过）的本地修改。
- git checkout -- . / git checkout . 这条命令最危险！会撤销所有本地的修改（相对于暂存区）。相当于用暂存区的所有文件直接覆盖本地文件，不给用户任何确认的机会！

<a name="hRBoD"></a>
#### git reset是Git最常用的命令之一，也是最危险最容易误用的命令。
<br />用法一：git reset [-q] [] [--] ...<br />用法二：git reset [--soft --mixed | --hard | --merge | --keep] [-q] []<br />注：<br />（1）第一种用法（包含了路径的用法）不会重置引用，更不会改变工作区，而是用指定提交状态()下的文件()替换掉暂存区中的文件。<br />例如：git reset HEAD <br />　　相当于取消之前执行的git add 命令时改变的暂存区。<br />（2）第二种用法（不使用路径的用法）则会重置引用。根据不同的选项，可以对暂存区或工作区进行重置。<br />参照下面的版本库模型图，可以看不同的参数对第二种重置语法的影响。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560848637491-a9185e5f-057d-402d-ac41-3657e63fb235.png#align=left&display=inline&height=238&name=image.png&originHeight=265&originWidth=557&size=130160&status=done&width=500)<br />命令格式：git reset [--soft | --mixed | --hard] []<br />（1）使用参数--soft，如 git reset --soft <br />　　会执行上图中的操作①。即只更改引用的指向，不改变暂存区和工作区。<br />（2）使用参数--mixed或者不使用参数（默认为--mixed），如 git reset <br />　　会执行上图中的操作①和②。即更改引用的指向及重置暂存区，但是不改变工作区。<br />（3）使用参数--hard，如git reset --hard <br />　　会执行上图中的全部动作①、②、③，（理解为此时工作区、暂存区、commit都相同）即：<br />　　　　①替换引用的指向。引用指向新的提交ID。<br />　　　　②替换暂存区。替换后，暂存区的内容和引用指向的目录树一致。<br />　　　　③替换工作区。替换后，工作区的内容变得和暂存区一致，也和HEAD所指向的目录树内容相同。<br />注： 引用即HEAD指针<br />
<br />使用：<br />git reset / git reset HEAD<br />仅用HEAD指向的目录树重置暂存区，工作区不会受到影响，相当于将之前用git add命令更新到暂存区的内容撤出暂存区。引用也未改变，因为引用重置到HEAD相当于没有重置。<br />git reset -- filename / git reset HEAD filename<br />仅将文件filename 的改动撤出暂存区，暂存区中其他文件不改变。相当于命令git add filename 的反射操作。<br />git reset --soft HEAD^<br />工作区和暂存区不改变，但是引用向前回退一次。当对最新的提交说明或者提交的更改不满意时，撤销最新的提交以便重新提交。<br />之前提到过修补提交命令git commit --amend，用于对最新的提交进行重新提交以修补错误的提交说明或者错误的提交文件。修补提交命令实际上相当于执行了下面两条命令。（注：文件.git/COMMIT_EDITMSG保存了上次的提交日志）<br />　　git reset --soft HEAD^<br />　　git commit -e -F .git/COMMIT_EDITMSG<br />git reset HEAD^ / git reset --mixed HEAD^<br />工作区不改变，但是暂存区会回退到上一次提交之前，引用也会回退一次。<br />git reset --hard HEAD^<br />彻底撤销最近的提交。引用回退到前一次，而且工作区和暂存区都会回退到上一次提交的状态。自上一次以来的提交全部丢失。<br />

<a name="PRbqH"></a>
# 五、如何以光速查看一行代码的提交记录
<a name="J5CN5"></a>
## 怎么查是谁写的？
<a name="HNCKd"></a>
## 命令行工具 git blame

```bash
git blame -L 99,99 package.json 
```
即使把这个命令设置为快捷方式，一行一行的查询也是非常耗费精力的，那么有没有一眼可以看到的方式呢？那就是直接在 GitHub 上查。

