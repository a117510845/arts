# arts第十一周 #

> 作者：周孝文

> 创建日期：2019-9-17

## 概述

见首页README.

# algorithm
## 题目

[10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the **entire** input string (not partial).

**Note:**

- `s` could be empty and contains only lowercase letters `a-z`.
- `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

**Example 1:**

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

**Example 2:**

```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

**Example 3:**

```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

**Example 4:**

```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
```

**Example 5:**

```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

```php
class Solution {
 /**
     * @param String $s
     * @param String $p
     * @return Boolean
     */
    function isMatch($s, $p) {
    

        //s和p均''时，认为匹配
        $dp[0][0] = true;
        //s不为'',p为'',dp[1...s.length][0] = false;

        //s为空,p为*时候的预处理
        for($j=1;$j<=strlen($p);$j++){
            if($p[$j-1] == "*"){
                $dp[0][$j] = isset($dp[0][$j-2])?$dp[0][$j-2]:false;
            }
        }

        //若s不为空，p也不为空的判断
        for($i=1;$i<=strlen($s);$i++){
            for($j=1;$j<=strlen($p);$j++){
                //若两个字符串当前的char相同
                if(($s[$i-1] == $p[$j-1] )|| $p[$j-1] == '.'){
                    $dp[$i][$j] = isset($dp[$i-1][$j-1])?$dp[$i-1][$j-1]:false;
                //若两个字符串当前的char不同
                }else{
                    if($p[$j-1] == '*'){
                        //下面要开始比较在*之前出现字符的几种状态
                        //首先是第一种出现0次
                        $dp[$i][$j] = isset($dp[$i][$j-2])?$dp[$i][$j-2]:false;
                        //如果出现1次或者很多次
                        if($p[$j-2]== '.' ||  ($p[$j-2] == $s[$i-1])){
                            $dp[$i][$j] = ($dp[$i-1][$j] || $dp[$i][$j]);
                        }
                    }
                }
            }
        }
        
        return $dp[strlen($s)][strlen($p)];
    }
}
```

### Submission Detail

| **447 / 447** test cases passed.            | Status: Accepted                        |
| ------------------------------------------- | --------------------------------------- |
| Runtime: **16 ms**Memory Usage: **14.7 MB** | Submitted: **15 hours, 53 minutes ago** |


### 题目解析

本题是一道Hard级别的算法题,刚开始看到.*的时候我首先的想法是正则匹配,看到英文叙述之后发现的确，.代表匹配一个简单字符，\*代表在它之前的字符,可以出现0,1次或者多次,很明显可以理解为按照实例写符合实例的正则匹配规则就是程序的主体,根据实例我第一想法是根据s,p进行递归验证,方法是没有问题,但是感觉不够灵活,估计空间和时间复杂度也很高,像这种递进式的演算问题,我又想到了一种算法叫动态规划，相比简单粗暴的递归,动态规划更容易理解，并且效率更高一点,代码中把逻辑分成了几个阶段的注释，可以参考下。

# Review

## [The *True* Corruption of Agile](http://blog.cleancoder.com/uncle-bob/2014/03/28/The-Corruption-of-Agile.html)

文章比较多,待增加中																																																																																			

# Tip
## 简述java.util.Properties集合

properties 类表示了一个持久的属性值，Properties可保存在流中或从流中加载
properties 集合是唯一和IO流相结合的集合
    可以使用properties结合中的方法store把集合中的临时数据，持久化写入到硬盘中
    存储，可以使用properties集合中的方法load把硬盘中保存的文件(键值对)，读取到
    集合中使用

属性列表中每个键及其对应值都是一个字符串
    properties集合是一个双列集合，key和value默认都是字符串


# Share
## Lambda表达式的数据格式:

  有三部分组成：
      a.一些参数
      b.一个箭头
      c.一段代码
  格式:
    (参数列表) ->  (一些重写方法的代码)
解释说明格式：
    ():接口中抽象方法的参数列表，没有参数,就空着;有参数就写出参数，多个参数使用逗号隔开
    ->;传递的意思，把参数传给方法体
    {}:重写接口中的抽象方法的方法体

lambda的使用前提
接口中有且仅有一个抽象方法。
必须有上下文推断



