1. 相对引用 
   1. ^上移一个 `main^` 相当于“`main` 的父节点”
   2. ~[数字] 上移一个数字，如果没有数字，上移一个

```
git checkout main^ // 上移到main的父节点，如果main是合并而来，上移到垂直的父节点
git checkout main^2 // 上移到第二个合并的父节点
git checkout commitId // 将HEAD指向 commitId
git checkout HEAD~^2~2 // 上移一个，找第二个父节点，上移两个
```

2. 移动分支

```
git branch -f main HEAD~3 // 将 main 分支强制指向 HEAD 的第 3 级父提交
git branch -f main commitId // 将 main 分支强制指向 commitId
```

3. 撤销变更

```
git reset HEAD~1 // 向上移动分支，原来指向的提交记录就跟从来没有提交过一样
git revert HEAD // 新增一个提交，用来撤销之前的HEAD
```

4. 整理提交记录

```
git cherry-pick <提交号>  <提交号>// 把一个或多个提交，移动到当前HEAD下面，提交不能是 HEAD 上游的提交
// cherry-pick需要知道commitID，rebase会列出备选提交记录
git rebase --interactive // 简写-i
git rebase -i HEAD~4 // 从HEAD上面第四个提交开始整理
```

5. 练习

```
你之前在 newImage 分支上进行了一次提交，然后又基于它创建了 caption 分支，然后又提交了一次。

此时你想对某个以前的提交记录进行一些小小的调整。比如设计师想修改一下 newImage 中图片的分辨率，尽管那个提交记录并不是最新的了。
我们可以通过下面的方法来克服困难：

先用 git rebase -i 将提交重新排序，然后把我们想要修改的提交记录挪到最前
然后用 git commit --amend 来进行一些小修改
接着再用 git rebase -i 来将他们调回原来的顺序
最后我们把 main 移到修改的最前端（用你自己喜欢的方法），就大功告成啦！
当然完成这个任务的方法不止上面提到的一种（我知道你在看 cherry-pick 啦），之后我们会多点关注这些技巧啦，但现在暂时只专注上面这种方法。 最后有必要说明一下目标状态中的那几个' —— 我们把这个提交移动了两次，每移动一次会产生一个 '；而 C2 上多出来的那个是我们在使用了 amend 参数提交时产生的，所以最终结果就是这样了。

也就是说，我在对比结果的时候只会对比提交树的结构，对于 ' 的数量上的不同，并不纳入对比范围内。只要你的 main 分支结构与目标结构相同，我就算你通过。


```

```
git rebase -i HEAD~2
git commit --amend
git rebase -i HEAD~2
git branch -f main HEAD
```

```
git checkout newImage
git commit --amend
git cherry-pick c3
git branch -f main HEAD
```

6. Tags

```
git tag V1 C1 // 创建V1标签，指向C1的提交id
```

7. describe

​		由于标签在代码库中起着“锚点”的作用，Git 还为此专门设计了一个命令用来**描述**离你最近的锚点（也就是标签），它就是 `git describe`！

​		Git Describe 能帮你在提交历史中移动了多次以后找到方向；当你用 `git bisect`（一个查找产生 Bug 的提交记录的指令）找到某个提交记录时，或者是当你坐在你那刚刚度假回来的同事的电脑前时， 可能会用到这个命令。

​		`git describe` 的语法是：

```
git describe <ref>
```

`<ref>` 可以是任何能被 Git 识别成提交记录的引用，如果你没有指定的话，Git 会以你目前所检出的位置（`HEAD`）。

它输出的结果是这样的：

```
<tag>_<numCommits>_g<hash>
```

`tag` 表示的是离 `ref` 最近的标签， `numCommits` 是表示这个 `ref` 与 `tag` 相差有多少个提交记录， `hash` 表示的是你所给定的 `ref` 所表示的提交记录哈希值的前几位。

当 `ref` 提交记录上有某个标签时，则只输出标签名称

```
git describe <ref> // 
```

8. 多分支 rebase

```
// 不允许用cherry-pick
// rebase会将当前分支的新提交拆下来，保存成patch，然后合并进其他分支新的commit，最后将patch接进当前分支
git rebase main // 把main分支重新整理到当前分支，当前分支的提交在后面
```

9. 偏离的工作

`git fakeTeamwork foo 3` // 模拟其他人提交的远程

```
git fetch
git rebase origin/main
git push

git fetch
git merge origin/main
git push

git pull --rebase
git push
```



10. 你应该按照流程,新建一个分支, 推送(push)这个分支并申请pull request,但是你忘记并直接提交给了main.现在你卡住并且无法推送你的更新.

    新建一个分支feature, 推送到远程服务器. 然后reset你的main分支和远程服务器保持一致, 否则下次你pull并且他人的提交和你冲突的时候就会有问题.

    ```
    git checkout -b feature
    git push
    git checkout main
    git reset o/main
    // 答案
    git reset --hard o/main
    git checkout -b feature c2
    git push origin feature
    ```

11. ```
    git reset --hard commitId // 回退，撤销到某次提交
    git push -f
    
    git revert // revert 是回滚某个 commit ，不是回滚“到”某个
    git revert -n 版本号 // 反转，撤销之前的某一版本，但是又想保留该目标版本后面的版本
    git commit -m 
    ```

12. 

show solution 命令查看答案 [git练习](https://learngitbranching.js.org/?locale=zh_CN)
