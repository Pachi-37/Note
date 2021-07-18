[返回](README.md)

# 分支

### 创建分支

`git branch new_branch`

### 切换分支

`git checkout new_branch`

### 创建分支并切换

`git checkout -b new_branch`

### 删除 & 合并

`git branch -d new_branch` # 删除分支

`git merge new_branch` # 合并分支

### 分支消息查看

`git branch -v` # 当前分支最后一次提交信息

##### 分支的本质

分支本质是单链表，每一个节点为快照

第二次提交指向第一次提交（`commit`链，`parent`（`commit id`））

##### HEAD

`HEAD`指向当前分支，`master`指向提交分支，创建其他分支`dev`新建指针（指向`master`）

#####  Fast forward

`master`分支直接跳转

##### 合并冲突

分支产生分歧，自动合并产生错误，需要手动解决

解决冲突之后使用`git add`告诉 git 冲突解决，`git commit`

### 分支控制 & 版本回退

如果可能，合并分支时Git会使用`fastforward`模式

该模式之下，删除分支时会丢失分支信息：
 直接使用分支提交信息信息合并

合并分支时

`git merge --no-ff new_branch` # 触发一次新的提交

### 版本回退

每次提交是一次快照，恢复快照

返回到上一个版本

`git reset --hard HEAD^`
`git reset --hard HEAD~1`
`git reset --hard commit_id`

返回某一个版本

`git relog` # 操作日志