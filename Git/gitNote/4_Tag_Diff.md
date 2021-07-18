[返回](README.md)

# 标签

- 标记特别的提交快照，使用 git tag 给它打上标签

- 轻量级

  ```
  git tag v1.0.1
  ```

   

  带附注的标签

  ```
  git tag -a v.1.0.2 -m 'commit'
  ```

   

  删除标签

  ```
  git tag -d [name]
  ```

   

  查看

  ```
  git tag
  ```

   

  查找(支持模糊查找)

  ```
  git tag -l 'name'
  ```



### diff 

`diff [源] 【目标】`
`diff -u [源] 【目标】`

 

`---`源文件

`+++`目标文件

`@@【-1】【+1，3】@@` # ‘-’源文件 1第一行开始 ‘+’目标文件 1：第一行开始， 3：连续3行

 

“ ”：两个文件都存在

“-”：目标文件不含

“+”：源文件不含

### git blame

文件上一次修改信息

 

```
git blame [name]
```



### git diff

比较工作区和暂存区的差别

暂存区为源文件

工作区为目标文件

 

`git diff HEAD` 

-  工作区与最新的一次提交

`git diff --cached commit_id`

 

`git diff --cached`  

-  最新的提交与暂存区