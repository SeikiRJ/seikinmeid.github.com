---
layout: post
title: [转]Linux全文搜索工具
category: learning
description: 使用grep来进行全目录全文搜索
---

如果要搜索整个linux系统里，那个文本里写了 jdk1.4.0

则以root登录，然后 执行 `grep   jdk1.4.0   /   -r`

-------------------------------------------------------------------------------

Linux grep命令

##用`grep`搜索文本文件

如果您要在几个文本文件中查找一字符串，可以使用`grep`命令。`grep`在文本中搜索指定的字符串。

假设您正在`/usr/src/linux/Documentation`目录下搜索带字符串`magic`的文件：

`$ grep magic /usr/src/linux/Documentation/*`

sysrq.txt:* How do I enable the magic SysRQ key?

sysrq.txt:* How do I use the magic SysRQ key?

其中文件‘sysrp.txt’包含该字符串，讨论的是 SysRQ 的功能。

默认情况下，`grep`只搜索当前目录。如果此目录下有许多子目录，`grep`会以如下形式列出：

grep: sound: Is a directory

这可能会使`grep`的输出难于阅读。这里有两种解决的办法：

明确要求搜索子目录：`grep -r`

或忽略子目录：`grep -d skip`

当然，如果预料到有许多输出，您可以通过 管道 将其转到‘less’上阅读：

`$ grep magic /usr/src/linux/Documentation/* | less`

这样，您就可以更方便地阅读。

有一点要注意，您必需提供一个文件过滤方式（搜索全部文件的话用 *）。如果您忘了，`grep`会一直等着，直到该程序被中断。如果您遇到了这样的情况，按 ，然后再试。

命令行参数：

`grep -i pattern files` ：不区分大小写地搜索。默认情况区分大小写，

`grep -l pattern files` ：只列出匹配的文件名，

`grep -L pattern files` ：列出不匹配的文件名，

`grep -w pattern files` ：只匹配整个单词，而不是字符串的一部分（如匹配‘magic’，而不是‘magical’），

linux下全目录全文搜索强大工具grep - 做人如果没有梦想，那跟咸鱼有什么区别？ - 勤奋的傻小子的博客grep -C number pattern files ：匹配的上下文分别显示[number]行，

`grep pattern1 | pattern2 files` ：显示匹配 pattern1 或 pattern2 的行，

`grep pattern1 files | grep pattern2` ：显示既匹配 pattern1 又匹配 pattern2 的行。

这里还有些用于搜索的特殊符号：

\< 和 \> 分别标注单词的开始与结尾。

例如：

###grep '\'

`grep '\' `只匹配‘man’，而不是‘Batman’或‘manic’等其他的字符串。

'^'：指匹配的字符串在行首，'$'：指匹配的字符串在行尾，如果您不习惯命令行参数，可以试试图形界面的`grep`，如 reXgrep 。这个软件提供 AND、OR、NOT 等语法，还有漂亮的按钮 。如果您只是需要更清楚的输出，不妨试试 fungrep 。

结合find和grep来搜索多个目录中的文件内容。

`# find / -name "*.txt" -print`

/ :find 命令从目录/开始搜索并搜索所有源于它的子目录

-name :指明搜索的名字或名字模式,查找所有以.txt结尾的文件

-print :表明find命令应输出其搜索到的和标准相匹配的文件名

`# find -name "*.txt" -print -exec grep test {} \;`

grep test {} \; :-exec参数的一部分.每次找到和-name参数中指定的条件相匹配的文件时,用来搜索单词test的grep命令将被执行。

{} :参数告诉find命令每次执行-exec部分的命令时插入匹配文件的完整路径和文件名。

\; :表示find每次找到一个匹配文件时其所执行的-exec部分的命令结束。

也可以将-print去掉。

最最最强大之处在此，全目录全文搜索，可以进入子目录在所有文件中搜索字符串，看官 请看：

`grep -lr 'string' /etc/`

这个命令就可以搞定。搜索etc下面的文件，包含所有目录下的文件。这样就搞定了。

-i，乎略大小写
-l，找出含有这个字符串的文件
-r，不放过子目录

还学了一招查日志

`tail -F /var/log/qmail/current|tai64nlocal|grep --line-buffered 'to remote'`

来源:http://jinsedeme0881.blog.163.com/blog/static/473543222010102693058237/
