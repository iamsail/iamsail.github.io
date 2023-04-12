---
title: Shell grep
date: 2019-12-07 15:20:18
tags: Shell
---

### ** Preface **

`grep`用了很久，不过以前我用得一直很浅显，就是简单的`grep xxx`。本文对其他用法做下记录
*****************

##### ** 或操作 **

找出文件（filename）中包含123或者包含abc的行
`-E `将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则表达式。
```
grep -E '123|abc' filename 
```

*****************

##### ** 与操作 **
显示既匹配 pattern1 又匹配 pattern2 的行。
```
grep pattern1 files | grep pattern2 
```
*****************

##### ** 在多个文件中查找 **
```
grep "match_pattern" file_1 file_2 file_3 ...
```

*****************

##### ** 标记匹配颜色 --color=auto 选项：**
```
grep "match_pattern" file_name --color=auto
```
*****************

##### ** 搜索多个文件并查找匹配文本在哪些文件中 **
```
grep -l "text" file1 file2 file3...
```

*****************

##### ** 在多级目录中对文本进行递归搜索 **
```
# .表示当前目录。
grep "text" . -r -n
```

*****************

##### ** grep静默输出 **

```
#不会输出任何信息，如果命令运行成功返回0，失败则返回非0值。一般用于条件测试。
grep -q "test" filename
```

*****************

##### ** 在grep搜索结果中包括或者排除指定文件 **
```
#只在目录中所有的.php和.html文件中递归搜索字符"main()"
grep "main()" . -r --include *.{php,html}

#在搜索结果中排除所有README文件
grep "main()" . -r --exclude "README"

#在搜索结果中排除filelist文件列表里的文件
grep "main()" . -r --exclude-from filelist
```
*****************

##### ** 打印出匹配文本之前或者之后的行 **
```
#显示匹配某个结果之后的3行，使用 -A 选项：
seq 10 | grep "5" -A 3
5
6
7
8

#显示匹配某个结果之前的3行，使用 -B 选项：
seq 10 | grep "5" -B 3
2
3
4
5

#显示匹配某个结果的前三行和后三行，使用 -C 选项：
seq 10 | grep "5" -C 3
2
3
4
5
6
7
8

#如果匹配结果有多个，会用“--”作为各匹配结果之间的分隔符：
echo -e "a\nb\nc\na\nb\nc" | grep a -A 1
a
b
--
a
b
```
*****************

##### ** 只显示全字符合的列 **
只匹配整个单词，而不是字符串的一部分（如匹配‘magic’，而不是‘magical’），
```
grep -w pattern files  
```

*****************

#### ** 综合使用场景 **
```
#包含java不包含grep的进程
ps -ef |grep java|grep -v grep 
```

*****************
### ** 参考链接 **

- [Linux: grep多个关键字“与”和“或”](https://blog.csdn.net/mmbbz/article/details/51035401)
- [grep多条件与或查找 多文件查找](https://my.oschina.net/2shui/blog/882875)
- [grep命令](https://man.linuxde.net/grep)
