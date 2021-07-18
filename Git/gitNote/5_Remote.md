[返回](README.md)

### 关联远程仓库

`git remote add origin `

`git push -u origin master`



##### 显示所有远程仓库

- `git remote show`
- 本地可以关联多个远程仓库
- 显示远程仓库详细信息
  - `git remote show [origin]`
  
    - ```
      Fetch URL: git@github.com:Pachi-37/mrdpachi.git
      Push  URL: git@github.com:Pachi-37/mrdpachi.git
      HEAD branch: master  #  远程克隆分支
      Remote branch:
      	master tracked  #  远程master分支被追踪
      Local branch configured for 'git pull':
          master merges with remote master
      Local ref configured for 'git push':
          master pushes to master (up to date)
      
      ```
  
      
  
  - `origin`为第一个远程仓库的别名，一般为默认



`git push`

- `matching`
  - `git config --global push.default matching`
  - 将本地分支推送到远程（远程分支存在并且同名）
- `simple`
  - `git config --global push.default simple`
  - 将当前分支推动到与之对应的远程分支（`git pull`更新当前分支的远程分支）







#### 分支要求

- `Gitflow`
  - 比较复杂 
- 基于Git分支的开发模型
  - 开发环境
    - `develop`
      - 频繁变化
  - 测试分支
    - `test`
      - 变化不是特别频繁
  - 生产发布分支
    - `master`
  - 紧急修复分支
    - `bugfix`



推荐使用SSH

关联远程仓库时使用SSH，`~/.SSH/Know_hosts`

工具(putty)

- `ssh-keygen`
- 公钥配对





### Git协作模型

- 远程协助双人模型

##### 远程分支

涉及到的分支

- `master`[local]
- `origin/master`
- `master`[remote]

查看分支

- `git branch -a`
  - 显示所有分支
- `git branch -av`
  - 分支 + 最后提交

克隆

- `git clone [address] [directory]`

冲突

- 对同一行修改，造成冲突（却决于谁先`push`）
- `git pull`
  - 获取最新仓库，准备解决冲突
  - `git fetch`
  - `git merge Origin/master`
- 修改冲突文件
- `git add`[^1]
  - 标识冲突解决

- `git commit`



[^1]:1.将未追踪的文件加入到追踪列表之中  2.已经被追踪的工作路径文件加入缓存区  3.文件冲突修改完的标识