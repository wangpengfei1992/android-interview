# Git扩展记录

## Git log

查看提交记录

查看后输入q退出

## Stash

使用场景：某一天你正在 feature 分支开发新需求，突然产品经理跑过来说线上有bug，必须马上修复。而此时你的功能开发到一半，于是你急忙想切到 master 分支，然后你就会看到报错

相关命令：

```
# 保存当前未commit的代码
git stash

# 恢复最近一次的stash
git stash apply

# 保存当前未commit的代码并添加备注
git stash save "备注的内容"

# 删除stash的所有记录
git stash clear

# 应用最近一次的stash，随后删除该记录
git stash pop

# 删除最近的一次stash
git stash drop

# 列出stash的所有记录
git stash list

```

如：

```
$ git stash list
stash@{0}: WIP on ...
stash@{1}: WIP on ...
stash@{2}: On ...
```

应用第二条记录：

```
$ git stash apply stash@{1}
```

## reset --soft

一般我们在使用 reset 命令时，`git reset --hard`会被提及的比较多，它能让 commit 记录强制回溯到某一个节点。而`git reset --soft`的作用正如其名，`--soft`(柔软的) 除了回溯节点外，还会保留节点的修改内容。

### 应用场景

应用场景1：有时候手滑不小心把不该提交的内容 commit 了，这时想改回来，只能再 commit 一次，又多一条“黑历史”。

应用场景2：规范些的团队，一般对于 commit 的内容要求职责明确，颗粒度要细，便于后续出现问题排查。本来属于两块不同功能的修改，一起 commit 上去，这种就属于不规范。这次恰好又手滑了，一次性 commit 上去。



```
# 恢复最近一次 commit
git reset --soft HEAD^
```

对于已经 push 的 commit，也可以使用该命令，不过再次 push 时，由于远程分支和本地分支有差异，需要强制推送`git push -f`来覆盖被 reset 的 commit。

**注意**，在`reset --soft`指定 commit 号时，会将该 commit 到最近一次 commit 的所有修改内容全部恢复，而不是只针对该 commit。





## cherry-pick



## revert



## reflog



## 资料：

https://mp.weixin.qq.com/s/aNwkDr_9hR7wvYJHp_qvVQ