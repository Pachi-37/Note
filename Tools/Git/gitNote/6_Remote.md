[返回](README.md)

### `Git GUI`(不推荐)

`gitk`

- `tcl`可能不兼容

`git gui`

`github desktop`



### 别名

`git config --global alias.br branch`



### `Git refspec`

本地分支与远程分支对应关系

在缺省的情况之下会被`git remote add`命令自动生成，并获取远端`refs/heads`下面所有引用写入本地`refs/remote/origin`

`git log origin/master`

`git log remote/origin/master`

`git log refs/remote/origin/master`  

-  最终命令



### 远程创建分支并关联本地分支

`git push --set-upstream origin [branch]`

`git push --set-upstream origin [local_branch]:[remote_branch]`

### 将远程分支拉取到本地

`git checkout -b [branch_name] origin/[branch_name]`

`git checkout --track origin/[branch_name]`

- `git checkout [branch_name]`
- `git push -u origin [branch_name]`

##### 删除分支

`git psuh origin <space>:dest `

`git push origin --delete dest`



##### `git push`完整写法

`git push origin src:dest`



##### `git pull`完整写法

`git pull origin src:dest`



`HEAD`

- `HEAD`指向当前分支，该文件内部不包含SHA-1
- `reflog`记录对`HEAD`操作
- `sysmbolic-ref`实现对`HEAD`文件修改
  - 读取
    - `git sysmbolic-ref HEAD`
  - 切换分支
    - `git sysmbolic-ref HEAD refs/heads/master`



##### `ORIG_HEAD`

远程`HEAD`分支SHA-1的值



##### `FETCH_HEAD`

- `commit id`
- `commit message`



### 远程标签

`git push origin [tag_name]`

`git push origin --tags`

`git push origin refs/tags/v1.0/:refs/tags/v1.0`

删除标签

`git push origin :refs/tags/v1.0`

`git push origin --delete tag [tag ]`



#### 远端拉取代码到分支

`git fetch origin master:refs/remotes/origin/mymaster`