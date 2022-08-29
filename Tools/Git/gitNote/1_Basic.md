[返回](README.md)

# Git命令

### 初始化

`git init` # 生成一个`.git`文件，默认创建主分支（`master`）

 

### 查看状态

`git status` # 查看当前文件状态

 

### 加入暂存区中

`git add`

 

### 从暂存区删除

`git rm --cached [file name]`
`git checkout -- [file name]`
`git reset HEAD [file name]`

 

### 提交

`git commit` # 提交要求添加注释

`git commit -m '[comment]'`

`git commit -am '[comment]'` # 添加并提交

`git commit -amend -m ''` # 修改上次提交信息

 

### 查看提交日志

`git log`
`git log --graph`
`git log --graph --abbrev-commit`
`git log --graph --pretty=oneline --abbrev-commit`

 

### 重命名

`git mv`

 

# 文件

### 删除

` git rm [file name] `

### 恢复

` git reset HEAD [] ` # 从暂存区恢复

` git checkout -- [] ` # 放弃更改 

-  `rm [file name] ` ` git add [file name] `

### 查看日志

Git提交的id是一个摘要值（根据sha1计算）

`-p` # 展开提交内容 差异

`-n` # 仅显示最近n次

`- -stat` # 显示简要的增改行数统计

`--pretty=oneline` 

`--pretty=format:"%h - %an, %ar : %s"` 

### 设置提交信息

对于`user.name` & `user.email`有三个地方可以设置

- `/etc/gitconfig` # 使用情况较少（电脑），可能需要手动创建

- - `git config --system`

- `~/.gitcofig`  # 常用（用户）

- - `git config --global`

- `.git/config` # 针对特定项目

- - `git config --local`

 

### 查看配置信息

`git config [option]`



### `.gitignore`

创建文件：`.gitignore`

将要忽略文件信息写入该文件中

`*.a` # 忽略全部'.a'结尾文件

`!b.a` # 不忽略

`/TODO` # 仅忽略根目录下文件

`build/` # 该目录下全部文件

`doc/*.text` # 该目录下特定文件

`/*/` # 一层目录

`/**/` # 所有目录层次

 