# arts第一周 #

> 作者：周孝文

> 创建日期：2019-4-6

## 概述

见首页README.

# algorithm
## 题目

1.[Two Sum](https://leetcode.com/problems/two-sum/)

Given an array of integers, return indices of the two numbers such that 
they add up to a specific target.

You may assume that each input would have exactly one solution, and you may
not use the same element twice.

solution：

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        if(is_array($nums) && count($nums)>0){
            foreach($nums as $key=> $v){
                $bcsub = $target - $v;
                if(in_array($bcsub,$nums)){
                    $hit = array_keys($nums,$bcsub);
                    if($hit[0] != $key){
                          return [$key,$hit[0]];
                    }
                }
            }
        }
    }
}
```
Submission Detail :

29 / 29 test cases passed.
Status: Accepted
Runtime: 144 ms
Memory Usage: 15.6 MB
Submitted: 1 month ago

总结： 本人喜欢打怪升级，所以一向喜欢从简单到难得过程。所以也是从easy
难度开始，上一题其实就是通过目标值找到数据中相应键值，没什么好说通过循环减法
进行比对之后收集查找,不多bb下一个。


# Review

Another short example is once.Do; once.Do(setup) reads well and would not be
improved by writing once.DoOrWaitUntilDone(setup). Long names don't automatically 
make things more readable. A helpful doc comment can often be more valuable than an 
extra long name.

本段摘自go语言的一篇入门级的使用手册 [Effective Go](https://docs.huihoo.com/go/golang.org/doc/effective_go.html)

为什么要摘这段拿出来分享呢，因为在工作中发现很多人对于方法，类，变量的命名写的很长
而且还有很多人认为写的长有益于了解，看了这句话我对之前的命名逻辑持保留意见，至于这句
话什么意思，我希望大家能自己去理解。

# Tip
## 通过查找进程的方法找到某个进程的目录文件位置
如图 

![flow](/source/ps.png)

# Share
## 引言

之前为了省钱所以不想开微博买服务器买域名，讲道理github真是个好东西，但是之前创建
私有库的时候要github通过开放私钥给你push到库内的嘛，我呢开了n个库，之后当前一个私钥
不能用很多次，之后吧各种找解决方法，如下

#参考

[git-ssh-key](https://blog.csdn.net/hustpzb/article/details/8230454)

#结语

好了，第一周ending
