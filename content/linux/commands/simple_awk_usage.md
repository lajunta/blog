---
title: "Simple_awk_usage"
date: 2023-11-02T18:46:05+08:00
draft: false
---

Simple Awk Usage
===

__[Geeksforgeeks LINK](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)__

__[TecMint LINK](https://www.tecmint.com/category/awk-command/)__

awk 是一个脚本语言，用来操作数据和生成报告。它不需要编译，但允许用户使用变量，数字函数，字符函数和逻辑操作符
awk 是三个开发者的首字母 Aho, Weinberger, and Kernighan

#### 语法

```bash
awk options 'selection_criteria {action}' inputfile > outputfile
```

#### 参数

```bash
-F 分隔符
```

### 内置变量

- NR 行号
- NF  最后的栏目
- FS   输入的分隔符
- OFS 输出时的分隔符
- RS 换行符号 “\n”
- ORS 输出的换行符号

- BEGIN pattern: means that Awk will execute the action(s) specified in BEGIN once before any input lines are read.
- END pattern: means that Awk will execute the action(s) specified in END before it actually exits.

### Print first column

```bash
ps | awk `{print $1}`
```

### Print multiple columns with different seperator

```bash
awk -F ":" '{print $1 $2 $7}'  /etc/passwd
```

### add tab or other charactor between output columns

```bash
awk -F ":" '{print $1"\t"$2"\t"$7}'  /etc/passwd
```

### print last column and use pattern to filter irrelative lines
must start with  /

```bash
awk -F "/"  '{ /^\// print $NF}' /etc/shells | uniq | sort
```

### Only print from line 3 to line 6
```bash
$awk 'NR==3, NR==6 {print NR,$0}'  employee.txt  
```

### Printing lines with more than 10 characters:
```bash
awk 'length($0) >10' geeks.txt
```

### Only print satisfied line 

```bash
awk '{ if($3=="B6") print $0 }'  geeks.txt
```
