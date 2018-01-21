+++
title= "make 帮助编译"
categories= ["电脑"]
tags= ["gcc.make","编译"]
date= "2016-03-06 16:49:17"
+++

<pre>#this is a make file
hello.out:max.o min.o main.c
        gcc max.o min.o main.c -o hello.out
max.o:max.c
        gcc -c max.c
min.o:min.c
        gcc -c min.c</pre>
<div>Make在linux和unix中非常重要；
Make工具可以将大型的的开发项目分成若干个模块；
Make工具很清晰和很快捷的整理源文件；
Make内部也是用的gcc；源码有好多源文件，如果每次修改都编译会很繁琐，make会比gcc简单
约定一个Makefile，每次修改代码都把makefile重新修改一遍
以#开头的是注释
main:max.o min.o main.c
（tab=6个空格必须用tab）gcc max.o min.o main.c -o main
max.o:max.c
gcc -c max.c
min.o:min.c //生成依赖
gcc -c min-c

</div>
