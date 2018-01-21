+++
title= "c语言main函数的参数"
categories= ["code"]
tags= ["c","main"]
date= "2016-03-06 16:42:33"
+++

<div class="entry-content">
<pre>int main(int argc,char *argv[])</pre>
第一个形参argc存放程序执行时的参数格式，至少是一个（这个参数就是该程序的可执行文件名），第二个形参argv为指针数组，存放指向实参的指针；
argv[0]指向第一个实参，即该程序的可执行文件名，argv[1]指向第二个实参。
<pre>#include&lt;sdio.h&gt;
   int main(int argc,char *argv[]){
   int i;
   printf("参数个数%d\n",argc);
   i=0;
   while(i&lt;argc){
     printf("第%d个参数:%s\n",i+1,argv[i]);
     i++;
   }
   return 0;
 }</pre>
</div>
&nbsp;
