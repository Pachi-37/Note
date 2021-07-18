### 缩写

使用短单词，vim自动展开为长单词

`:abbreviate ad advertisement`

- 查看缩写列表

`abbreviate`



### 映射键

将一组命令绑定到一组键

`map [键] [命令]`



##### 修改退格`t_kb`和删除键`t_kD`

- 交换退格，删除键

`:fixdel `

- 选择退格键在插入模式下的作用
- 允许跨越缩进

`backspace=indent`

- 允许跨行 

`:set backspace=eol `

- 允许在插入开始时退格

`:set backspace=start `

`set backspace=indent,eol,start`



### 配置文件

将命令写入一个文件

`:mkvimrc file`

读取

`:source file`

初始化文件

`:version`



##### `.vimrc`

```bash
#  开启高亮
:syntax on

:autocmd FileType *      set formatoptions=tcql 
\ nocindent comments& 
:autocmd FileType c,cpp  set formatoptions=croql 
\ cindent comments=sr:/*,mb:*,ex:*/,:// 

#  缩进
:set autoindent 
:set autowrite 

#  缩写 
:ab #d #define 
:ab #i #include 
:ab #b /**************************************** 
:ab #e <Space>****************************************/ :ab #l /*--------------------------------------------*/ :ab #j Jack Benny Show

#  缩进尺寸
:set shiftwidth=4 

#  开启高亮搜索
:set hlsearch 
:set incsearch

:set textwidth=70 
```

