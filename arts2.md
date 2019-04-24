# arts第二周 #

> 作者：周孝文

> 创建日期：2019-4-15

## 概述

见首页README.

# algorithm
## 题目

1.[Reverse Integer](https://leetcode.com/problems/reverse-integer/)

Given a 32-bit signed integer, reverse digits of an integer.

solution：

```php
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function reverse($x) {
        if(!is_int($x)){
            return 0;
        }
        if(abs($x) <= 9){
         return $x;
        }
        $absRes =  abs($x);
        $remainder = 0;
        $res = 0;
        while($absRes > 9){
            $remainder = $absRes%10;
            $absRes = ($absRes-$remainder)/10; //每次要初始化的位数上的值
            $res =  $res*10 + $remainder;
        };
        $res = $res*10 + $absRes;
           if($res < -pow(2,31) || $res > (pow(2,31)-1)){
            return 0;
        }
        if($x>0){
            return rtrim($res,0);
        }else{
            return '-'.rtrim($res,0);
        }
    }
}
```
Submission Detail :

**1032 / 1032** test cases passed.

Status: Accepted

Runtime: **12 ms**

Memory Usage: **16.5 MB**

Submitted: **1 month, 1 week ago**

总结： 本人喜欢打怪升级，所以一向喜欢从简单到难得过程。所以也是从easy
难度开始，上一题其实就是对32位有符号整数进行位置转换,解题思路就主要是递归,还有一个注意点就是对32位整数要注意数据溢出的判断。


# Review

The control structures of Go are related to those of C but differ in important ways. There is no `do` or `while` loop, only a slightly generalized `for`; `switch` is more flexible; `if` and`switch` accept an optional initialization statement like that of `for`; `break` and `continue` statements take an optional label to identify what to break or continue; and there are new control structures including a type switch and a multiway communications multiplexer, `select`. The syntax is also slightly different: there are no parentheses and the bodies must always be brace-delimited.

本段摘自go语言的一篇入门级的使用手册 [Effective Go](https://docs.huihoo.com/go/golang.org/doc/effective_go.html)

其实很多人喜欢放上一些自己看到的文献，我喜欢放一些语言的特性因为这样可以促进自己更快的了解这个语言，每个语言都是自己的特别之处，把他特别的标出来能让自己特殊记忆，上面的内容主要是说对于循环结构与c语言结构体的区别，因为我是php嘛，我时常使用foreach循环，但是到了golang这里就变成了for range循环很实用

# Tip
## thinkPHP框架的对于C层中一些代码结构的见解

如图 

![flow](/source/ps2.png)

# Share
## 引言

之前很少接触过打开文件，加载文件类的需求，对于php文件加载的机制也仅限于require和include，对于绝对路径和相对于路径的相关函数使用还是比较拙劣的，下面是自己最近笔记中记录的函数

```php
echo __FILE__ ; // 取得当前文件的绝对地址，结果：D:\www\test.php

echo dirname(__FILE__); // 取得当前文件所在的绝对目录，结果：D:\www\

echo dirname(dirname(__FILE__)); //取得当前文件的上一层目录名，结果：D:\
```

说实话，之前看arts群里介绍说使用typora很好用强烈建议，用了之后才发现真的太好了

