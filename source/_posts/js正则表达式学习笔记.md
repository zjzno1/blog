title: js正则表达式学习笔记
date: 2016-08-22 10:40:42
tags:
- js
- 正则
---
#### 正则表达式中的特殊字符

\ 转义 
^ 匹配一个或一行的开头
$ 匹配一个或一行的结尾
\* 匹配前面元字符0次或多次
\+ 匹配前面元字符1次或多次
? 匹配前面元字符0次或1次
x|y 匹配x或y
. 表示匹配字符串中出现的第一个非换行符字符
{n} 精确匹配元字符n次
{n,} 匹配元字符n次或以上
{n,m} 匹配n-m次
[xyz] 字符集，匹配这个字符集中的任意一个字符
[^xyz] 不匹配这个字符集中的任意一个字符
[\b] 匹配一个退格符 
\b 匹配一个单词的边界 
\B 匹配一个单词的非边界 
\cX 这儿，X是一个控制符，/\cM/匹配Ctrl-M 
\d 匹配一个字数字符，/\d/ = /[0-9]/ 
\D 匹配一个非字数字符，/\D/ = /[^0-9]/ 
\n 匹配一个换行符 
\r 匹配一个回车符 
\s 匹配一个空白字符，包括\n,\r,\f,\t,\v等 
\S 匹配一个非空白字符，等于/[^\n\f\r\t\v]/ 
\t 匹配一个制表符 
\v 匹配一个重直制表符 
\w 匹配一个可以组成单词的字符，包括字母大小写、数字、下划线，如[\w]匹配"$5.98"中的5，等于[a-zA-Z0-9] 
\W 匹配一个不可以组成单词的字符，如[\W]匹配"$5.98"中的$，等于[^a-zA-Z0-9]

##### 注：(1) javascript默认是贪婪匹配，也就是说匹配重复字符是尽可能多地匹配，而且允许后续的正则表达式继续匹配。而进行非贪婪匹配，只需要在待匹配的字符后面跟随一个问号即可：“??”、“+?”、“*?”、“{1,5}?”。比如：/a+/可以匹配一个或多个连续的字母a。当使用“aaa”作为匹配字符串时，/a+/会匹配它的三个字母。但是/a+?/会尽可能少的匹配，只能匹配第一个哦~
(2)当要匹配连字符-时，在[]中请把它放在第一位，以防解释为范围。

#### 正则表达式中/i,/g,/ig,/gi,/m的区别和含义

/i (忽略大小写)
/g (全文查找出现的所有匹配字符)
/m (多行查找)
/gi(全文查找、忽略大小写)
/ig(全文查找、忽略大小写)
