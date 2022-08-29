[返回](README.md)

### `checkout`

`git checkout -- [file]` 

- 丢弃修改，使之与上一次缓存区中内容保持一致

- 使用`git add`命令之后这个命令不会改变文件

`git reset HEAD [name]` 

-  将之前添加到暂存的内容移除到工作区



切换到另一个分支最新的提交点

 

切换到之前版本

`git checkout [commit id]` 

-  进入游离状态[^1]，不属于任何分支（匿名分支）

`git branch [name] [commit id]` #

- 创建新的分支来保存这个状态



### 临时更改分支

`git stash` 

-  将当前分支上的修改临时保存

`git stash list`
`git stash save [commit]`

 

`git stash pop` 

-  取出最新的缓存，并删除

`git stash apply` 

-  不删除之前——`git stash drop stash@{0}手动删除

`git stash apply stash@{[num]}`

 

 

`git branch -m [name] [name]` # 分支改名

 

 

 

[^1]:HEAD指针游离：不指向branch提交时时则会在一个detached状态利: 我们可以很方便地在历史版本之间互相切换，比如需要回到某次提交，直接 checkout 对应的 commit id 或者 tag 名即可。弊：在这个基础上的提交会新开一个匿名分支且提交是无法可见保存的，一旦切到别的分支，游离状态以后的提交就不可追溯了。