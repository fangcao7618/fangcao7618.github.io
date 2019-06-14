
---

title: Git

date: 2019-06-12 11:29:49 +0800

tags: []

---
<a name="WbKVb"></a>
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

