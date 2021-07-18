### 高亮

`:syntax on `

##### 颜色不匹配

- `Vimeditor`有两组语法颜色。一种是在背景较亮时使用，另一种是在背景较暗时使用。当vim启动时，它会尝试将`“background”`选项设置为亮的还是暗的。

- 当前使用背景

`:set background?` 

- 设置

`:set background=light `

##### 显示为黑白

- UNIX系统上使用的`xterm`程序受到影响。将终端类型设置为颜色版本。在`Linux`上是`xterm-color`，在`Solaris`上是`xtermc`。

 `shell`

`if ($term == xterm) set term = xterm-color`

##### 颜色测试

`:edit $VIMRUNTIME/syntax/colortest.vim `

`:source %`

### 提交文件类型

- 使用文件的扩展名来确定文件类型。例如，以. C或.h结尾的文件被认为是C文件。如果您正在编辑一个名为settings.inc的C

`:set filetype=c`

`:help new-filetype` # 自动启动这设置



### 设置缩进

- 默认缩进为8个，正常缩进应该为4个

`:set shiftwidth=4`

- 自动缩进设置

`cindent`  # C风格缩进（C/C++/Java） 

`smartindent ` #  对每一行的缩进量与前一行相同，左花括号({)，则添加额外的缩进，右花括号(})，则删除缩进。对于`“cinwords”`选项指定的任何关键字，还会添加额外的缩进，以“#”开头的行会得到特殊处理。如果一行以“#”开头，所有缩进都将被删除。

`autoindent`  # 设置与前一行缩进对齐，结构化语言(如Pascal、Perl和Python)

 `:set cindent` # 当您键入诸如if (x)之类的内容时，下一行将自动缩进一个额外的级别

- `<C-D>`

  - 改变缩进‘}’前移

- 格式修正

  - `=`

  - `=%` # % 匹配{}

  - 段落缩进

  ` \>% `

  ` \>i{`

  这个右移命令(>)将选中的文本右移一个shift宽度。在本例中，接下来的选择命令是i{，它是“inner{}块”命令。



### 查找定位

`[CTRL-I`, `]CTRL-I` # 在当前文件中搜索光标下的单词和由#include指令引入的任何单词

 

`gd`, `gD ` # 搜索本地变量，全局变量

`]CTRL-D`,` [CTRL-D`  #  跳到宏定义

`]d`,` [d`,` ]D`,` [D`  #  显示宏定义

 

`%` # 匹配跳转

{} 、/*---*/ 、#if，#else，#endif



### 标签

vim可以识别C/C++函数的定义，因此可以生成名为tags的内容文件表

Linux中可以使用`ctags *.c `[^1]生成

vim中：`:tag function`

`:tags `展示标签列表

`:stag  tag`  #  split + tag

CTRL-W]  #  分割当前窗口并跳到上面窗口中光标下的标记



 CTRL-]    #  找到函数即是是在另一个文件里面

 CTRL-T   #   执行前面的标记。count参数，指示需要返回多少标记



#### vim查找其他`ctags`文件

`:tag /write`

`:tag /^read`

`:tag /DoFile\|do_file\|Do_File `or `:tag /[Dd]o_\=[Ff]ile`  #   当不确定文件名，可以使用多个猜想

`:tselect{name}`  #  列出可能符合选项



### 显示非可见字符

`:set list`

- 默认情况下，Vim不会显示`space,tabs,newlines,trailing`使用该命令显示非可见字符

`:set nolist`

`:set list!`

- 切换显示或隐藏不可见字符



##### 可视模式下排序

- 进入可视模式
- 选取要排序的行
- `!sort`



##### 快速修复模式

`quickfix`将编译过程中产生的错误信息保存到文件中，然后vim利用这些信息跳转到源文件的对应位置

-   显示详细错误信息

`:cc `

- 跳到上一个错误

`:cp   `

- 跳到下一个错误

`:cn`   

- 打开`quickfix`窗口

`:cw`  

- 打开`quickfix`窗口，可以在后面添加窗口高度参数，如10行：` :copen 10`

`:cope(n) `

- 关闭`quickfix`窗口

`:ccl(ose) `

- 查看全部信息

  `:clist`



##### 运行`make`程序

`:make`



##### `errorfile`定义了用于`:clist`命令和`-q`命令行选项的默认文件名

`:set errorfile=error.list`



##### 搜索给定的字符（`grep`）

`grep`命令的作用类似于`:make`。它运行外部程序`grep`并捕获输出

- `grep -w [变量] [file_name] `
  - `-w`  
    - 只查找完整单词



### `autocommand`

根据不同文件打开不同选项

`:autocommand`











[^1]:需要事先安装`ctags`,大部分系统自带