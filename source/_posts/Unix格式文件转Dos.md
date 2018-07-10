---
title: Unix格式文件转Dos
date: 2018-06-18 16:04:15
tags: note
---
#### 1.Linux和windows下文件格式不统一
> 原因：

Windows下换行使用CR...LF两个字符来表示

- 其中CR为回车（ASCII=0x0D）

- LF为换行（ASCII=0x0A）

Linux下使用LF一个字符来表示。
> 结果

在Linux下编辑或者程序生成的文件导出到windows后会出现乱码或解析出错的问题。

#### 2.Unix和DOS文件的相互转化

1. 使用Linux工具或者命令
>  dos2unix工具

>  tr命令

>  Emacs编辑器

2. 使用vim 编辑器

```
vim file

DOS转UNIX：:set fileformat=unix

UNIX转DOS：:set fileformat=dos

:wq

```

3.使用脚本语言处理

Perl Python等，也是把换行符做处理。

Python：
```
# DOS转UNIX：
Python -c “importsys; map(sys.stdout.write, (l[:-2] + ‘\n’ for l in sys.stdin.readlines()))”< dosfile.txt > unixfile.txt

# UNIX转DOS：
python -c “importsys; map(sys.stdout.write, (l[:-1] + ‘\r\n’ for l in sys.stdin.readlines()))”< dosfile.txt > unixfile.txt
```

#### 3.vim编辑器下对文件的一些操作

- 格式相互转化

  set fileformats=unix,dos

  
>   shell、python等脚本需要保存为unix格式

> 在linux下直接运行时会提示：No such file or directory
因为Linux把换行符也当成脚本解释器的一部分了。
-  查看文件格式

   set fileformat

- 设置文件末尾是否自动增加换行符

   set endofline/noendofline 
- 设置是否显示不可见字符

  set list/nolist 