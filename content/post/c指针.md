+++
title= "c指针"
categories= ["code"]
tags= ["c","指针"]
date= "2016-03-06 16:45:07"
+++

<div class="entry-content">

scanf函数还是要地址，不要弄混了
scanf("%d",*(p+i)+j);//错误的是*(*(p+i)+j)

指向指针的指针
<pre> int a=3,*pi,**ppi;
 pi=&amp;a;
 ppi=&amp;pi;
 printf("a=%d\n",a);//a的值，即数字3
 printf("a-address:  %x\n",pi);pi的值，即a的地址
 printf("pi-address:  %x\n",ppi);ppi的值，即pi的地址
 printf("ppi-address:  %x\n",&amp;ppi);ppi的地址</pre>
<pre>int main(){
	char *p[6]={"Singapore","Zambia","China","Mexico","Canada","Romania"};
	char **q;
	int i;
	for(i=0;i&lt;6;i++){
            printf("%10s,  %c",p[i],*p[i]);
            q=p+i;
            printf("%10s,  %c",*q,**q);
        }
      return 0;
  }
</pre>
数组名p是指针的指针，指向元素p[0],元素p[0]指向一个字符串，

语句q=p+i;使q指向数组p[i],*q就是p[i]元素，是某个字符串的地址，

**q就是*p[i]元素，是字符串的第一个字符。

</div>
&nbsp;
