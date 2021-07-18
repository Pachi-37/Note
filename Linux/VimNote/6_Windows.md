# 窗口操作

### 打开一个新窗口

`:split` # 打开其他窗口

`:split [file name]` # 在其他窗口打开文件

`:[num] split` # 加数字指定窗口大小

 

 

`:new`

` :sview `



### 切换窗口

`CTRL-Ww `

 `CTRL-W【mov】`



### 退出窗口

`:q`

`ZZ`

### 窗口加命令

`:split+command` 

### 窗口大小改变

`CTRL-W-`

`CTRL-W+`

`CTRL-W=`

`CTRL-W_`

命令使当前窗口计数行数很高。如果没有指定计数，则将窗口增加到最大大小	



## 缓冲区

缓冲区来描述正在编辑的文件。实际上，缓冲区是您所编辑的文件的副本。

在屏幕上的有，不在没有

### 三种状态

`Active` # 屏幕显示

`Hidden` # 被使用但是不显示

`Inactive` # 不被使用



### 隐藏缓冲区

不想使得窗口分割

 

改变屏幕分配比例，使得一个窗口尽量占满

关闭一个（丢失操作）

 

使用隐藏命令

` :hide `



### 缓冲区命令 & 显示

`:buffers` # 显示缓冲列表

 

`- `# 不使用 

`h` # 隐藏 

`%` # 当前 

`# `# 交换的 

`+` # 被更改



### 使用缓存区

`:buffer number `

`:buffer file`

 

`:sbuffer number`

 

`:bnext Go to the next buffer. `

`:count bnext Go to the next buffer count times. `

`count sbnext Shorthand for :split followed by :count bnext. `

`:count bprevious Go to previous buffer. If a count is specified, go to the count previous buffer. `

`:count sbprevious Shorthand for :split and :count bprevious. `

`:count bNext Alias for :bprevious.`

`:count sbNext Alias for :sbprevious. `

`:blast Go to the last buffer in the list. `

`:sblast Shorthand for :split and :blast. `

``:brewind Go to the first buffer in the list. `

`:sbrewind Shorthand for :split and :rewind. `

`:bmodified count Go to count modified buffer on the list. `

`:sbmodified count Shorthand for :split and :bmodified.`