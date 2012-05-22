---
layout: post
title: Perl正则匹配及chomp函数练习
description: Perl正则匹配及chomp函数练习。
keywords: Perl, chomp
---
昨天晚上在群里看到豆豆在讨论Perl正则匹配的问题，自己没事也跟着做了一下。因为自己看的骆驼书还没看到正则这一块，好多都不了解，所以记录一下。

<pre class="html" name="colorcode">
[root@localhost perl]#cat test
1
one one
hello
22
d
</pre>

<pre class="html" name="colorcode">
[root@localhost test]# perl -ne 'print if /\d/' test
1
22
</pre>

test是一个文件

-e:代表执行perl命令

-n:代表遍历文件的内容

\d是perl元字符,在perl中代表匹配一个数字

\d	匹配一个数字的字符,和 [0-9] 语法一样，\d代表任意数字的字符集[0-9]

\D	非数字,其他同 \d

这里有更详细的

http://www.php-oa.com/2008/12/20/power-perl.html

而这样输入就得到不想要的输出字符结果。
<pre class="html" name="colorcode">
[root@stationx perl]# perl -ne 'print if /\D/' test
1
one
hello
22
d
</pre>

北京|MOON  22:12:42
<pre class="html" name="colorcode">
22:11:40#tp#test> perl -ne 'print if /^\D+$/' test
one
hello
d
</pre>
<pre class="html" name="colorcode">
22:12:18#tp#test> perl -ne 'print if /^\d+$/' test
1
22
</pre>


\d+	匹配多个数字字符串,和 [0-9]+ 语法一样
\D+	非数字,其他同 \d+
^    配置字符串的开始
$    匹配字符串的结束


北京|豆  22:42:16
<pre class="html" name="colorcode">
[root@stationx perl]# perl -ne 'chomp($a=$_);print $_ if $a =~ /\D/' test
one
hello
d
</pre>

北京|豆  22:30:29

perl在正则匹配的时候将新行\n也算作一个字符

所以print if /\D/不对

北京|MOON<walkerxk@gmail.com>  22:31:23

所以经常要chomp

###何为chomp？

<strong>Perl chomp函数</strong>

<strong>介绍:</strong>
chomp函数通常会删除变量里包含的字符串尾部的换行符。它是chop函数的一个略微安全些的版本，因为它对没有换行符的字符串没有影响。更准确地说，它根据了解$/的当前值删除字符串终止符，而不只是最后一个字符。如果字符串后面有两个以上的换行符，chomp也仅仅删除一个。如果结尾处没有换行符，它什么也不做，直接返回零。
和chop不同，chomp返回删除的字符数量。你不能chomp一个直接量，只能处理变量。

<strong>用法:</strong>
<pre class="html" name="colorcode">
chomp VARIABLE
chomp LIST
chomp
</pre>

<strong>例子：</strong>
<pre class="perl" name="colorcode">
#!/usr/bin/perl

$string1 = "This is test";
$retval  = chomp( $string1 );

print " Choped String is : $string1\n";
print " Number of characters removed : $retval\n";

$string1 = "This is test\n";
$retval  = chomp( $string1 );

print " Choped String is : $string1\n";
print " Number of characters removed : $retval\n";
</pre>

<strong>结果如下：</strong>
<pre class="html" name="colorcode">
Choped String is : This is test
Number of characters removed : 0
Choped String is : This is test
Number of characters removed : 1
</pre>
