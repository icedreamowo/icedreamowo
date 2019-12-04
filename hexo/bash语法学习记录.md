---
title: bash语法学习记录
date: 2019-10-23 15:13:55
tags:
	-IT TECH
---

bash是什么:https://www.jianshu.com/p/b513087cd7ec
bash基础教程:https://www.runoob.com/linux/linux-shell.html
记录学习时的一些细节

bash文件可以在第一句声明 脚本解释器的位置
bash解释器的默认位置在__/bin/bash__
```bash
#! /bin/bash
```
变量不需要特别声明 只要使用未定义过的变量名即可
注意赋值时等号前后___不能___ 使用空格 否则会报错
引用变量时需要在前面加上__$__
```bash
#! /bin/bash
str="NewString"
echo $str

#>NewString
```
变量类型一般为字符串 需要整型以及整型计算时需要__let__关键字
```bash
#! /bin/bash
num=1
echo $num
let "num=$num+1"
echo $num

#>1
#>2
```
__readonly__关键字可以设置变量为只读
变量不需要__$__修饰
```bash
#! /bin/bash
num=1
readonly num
let "num=$num+1"
echo $num

#>./start.sh:行4: num: 只读变量
#>1
```
__unset__关键字可以清除变量
变量不需要__$__修饰
```bash
#! /bin/bash
num=1
unset num
echo $num

#>
#输出空行
```
但是__unset__不可以清除只读变量
```bash
#! /bin/bash
num=1
readonly num
unset num
echo $num

#>./start.sh: 第 4 行:unset: num: 无法反设定: 只读 variable
#>1
```
变量清除后可以再次使用
```bash
#! /bin/bash
num=1
unset num
echo $num
num=2
echo $num

#>
#>2
```
可以直接在字符串中引用其他字符串
这里可能会导致字符串中有歧义
如 $numSum 是指numSum变量还是num变量加上Sum字符串
可以用大括号来避免歧义
如使用 ${num}Sum 来代替$numSum 
```bash
#! /bin/bash
num="2"
str="1 + 1 eqls $num"
echo $str

#>1 + 1 eqls 2
```
### 数组操作
数组成员之间用__空格__隔开,而不是使用逗号
引用数组成员的时候需要添加大括号
```bash
#! /bin/bash
strArray=(
	1
	2
	3
	4
	"EndOfArray"
)
echo ${strArray[0]}
echo ${strArray[4]}
#${Array[index]}

#>1
#>EndOfArray
```
可以使用 __*__ 或者 __@__ 来指代数组的所有成员
注意当计算数组成员个数的时候 需要使用${#strArray[@]}而不是${#strArray}
```bash
#! /bin/bash
strArray=(
	1
	2
	3
	4
	"EndOfArray"
)
echo ${strArray[@]}
echo ${strArray[*]}

echo ${#strArray}
echo ${#strArray[@]}
echo ${#strArray[*]}

#>1 2 3 4 EndOfArray
#>1 2 3 4 EndOfArray
#>1
#>5
#>5
```