<div class="entry-content">

要用<strong>string.h</strong>头
<pre><code>char *strcpy(char *s1,char *s2)</code></pre>
s1必须是字符数组名或者指向字符数组元素的指针，s2是字符串（即字符数组名，字符串指针，字符串常量）。

功能：字符串s2复制到s1中，从s1指针指向的位置开始依次存储字符串2，函数返回为s1的指针。
<pre><code>char c[11]="0123456789";</code>
<code>strcpy(c,"HangZhou");//c为HangZhou</code>
<code>strcpy(c+4,"China");//c为HangChina</code></pre>
<pre><code>char *strcat(char *s1,char *s2)</code></pre>
s1必须是字符数组名或者指向字符数组元素的指针，s2是字符串（即字符数组名，字符串指针，字符串常量）。
功能：字符串s2复制到s1后，函数返回为s1的指针。
<pre><code>char c[18]="HangZhou";</code>
<code>strcat(c,"China");//c为HangZhouChina</code></pre>
<pre><code>int strcmp(char *s1,char *s2)</code></pre>
s1，s2是字符串（即字符数组名，字符串指针，字符串常量）。
功能：比较s1，s2两个字符串的大小。函数返回值0则两字符串相等；返回为1则字符串s1&gt;s2;返回值为-1则字符串s1&lt;s2。
<pre><code>strcmp("abc","abc");//返回0</code>
<code>strcmp("abc","abcd");//返回-1</code>
<code>strcmp("abc","bbc");//返回0</code></pre>
<pre><code>unsigned int strlen(char *s1)</code></pre>
s1是字符串（即字符数组名，字符串指针，字符串常量）。
功能：计算字符串中字符的个数（不计'\0')
<pre><code>strlen("China");//返回5</code>
<code>stelen("ab\110\\cd\'\\ne");//返回10</code></pre>
</div>
<footer class="entry-meta"></footer>&nbsp;
