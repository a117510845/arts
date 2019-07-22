# arts第八周 #

> 作者：周孝文

> 创建日期：2019-7-18

## 概述

见首页README.

# algorithm
## 题目

5. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```php
Input: "cbbd"
Output: "bb"
```

```php
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function longestPalindrome($s) {
    if(strlen($s)<2){
            return $s;
        }
        $dp=[];
        $left=$right=$len=0;
        for($i=0;$i<strlen($s);$i++){
            $dp[$i][$i]=1;
            for($j=0;$j<$i;++$j){
                $dp[$j][$i]=($s[$i]==$s[$j] && ($i-$j <2 || $dp[$j+1][$i-1]));
                if($dp[$j][$i] && $len < $i-$j+1){
                    $len=$i-$j+1;
                    $left=$j;
                    $right=$i;
                }
                
            }
        }
        return substr($s,$left,$right-$left+1);
    }
}
```

### Submission Detail

| **103 / 103** test cases passed.              | Status: Accepted                      |
| --------------------------------------------- | ------------------------------------- |
| Runtime: **1596 ms**Memory Usage: **36.5 MB** | Submitted: **1 hour, 14 minutes ago** |

### 题目解析

虽然是一道Medium难度的题目,但是涉及的动态规划的算法着实让我研究了很久，虽然研究了很久但是还是有很多不理解的地方,首先我描述下这道题目,在给定的字符串中找出回文字符串，首先让人想到的暴力破解的方式，但是很明显在长字符串的情况下，程序直接超时了,那么在程序的角度来看，当前的程序设计肯定是有问题或者冗余，仔细回想下暴力破解的程序运行轨迹，其实程序是是从每个字符开始计算然后对字符串进行反转对比,很明显对于字符串的反转和从每个字符串开始循环的过程是很耗时而且消耗性能的,所以超时的结果也是显而易见的。

那么就需要一种高效的算法来解决寻找回文字符串，看过动态规划算法的人应该都知道，它常用的几种模型,当前的回文字符串正好符合其区间模型的算法,因为我也是因为这道算法题才去了解动态规划算法，而且看了一下午对于其几种经典模型也是一知半解,需要长期的联系巩固 ，在很多动态规划的转移方程都是通过先写递归加记忆法从而推导出公式，我利用动态规范解题的思路比较简单，就是通过逐条的递归通过当前节点状态的判断决定是否进行到下一个节点，如代码所示以把[i,j]作为回文串的区间,$dp二维数组相当于一个节点的状态，通过划定通过当前节点的条件保存当前回文串区间，最后截取。


# Review

## [Classes vs. Data Structures](http://blog.cleancoder.com/uncle-bob/2019/06/16/ObjectsAndDataStructures.html/)

- Classes make functions visible while keeping data implied. Data structures make data visible while keeping functions implied.
- Classes make it easy to add types but hard to add functions. Data structures make it easy to add functions but hard to add types.
- Data Structures expose callers to recompilation and redeployment. Classes isolate callers from recompilation and redeployment.

这篇文章的作者是《代码整洁之道》的作者，所以看过clean code的人应该对Robert C. Martin比较熟悉,我是听过有这本书，但是没看过，整篇文章看着断句蛮简单的,但是内容十分晦涩,就像题目主要围绕类和数据结构为主题开展的一问一答的形式的讨论，因为本人英文不是很好，所以是变对照翻译变看的，之前其实看过中文版的关于DI,IOC是对照代码的描述，但是这种纯文字描述，我全文翻译去看,理解起来也感觉很难懂，有句话就是好的文章要多读几遍，所以多读读吧，本文前一段主要说类和数据对象的定义和区别还有两者之间的关联的，还有在代码中二者使用场景各种变换，最后用类和数据结构的三种不同的方式存在描述做了结尾，博主把类和数据结构的关系描述的很细致,我是觉得蛮适合大家去推敲的,特别是在写底层代码的时候。

# Tip
## 接口调用中json格式转换的问题
最近在对接接口时候,鉴于数据接口的安全问题,数据加密是一件比较重要的事情,那么在接口对接过程中加密验签就是必不可少的了，但是有个问题就是，对于有特殊字符串的转义过程中，json_encode都会加\做处理，那结果是就是在json_encode 和json_decode的转义过程中字段内的数据会多增加\这个字符,很明显有有问题，在第二个入参上其实是可以选择自己不同的要求，比如不要求转码，有的不要转中文，具体需求看你的选择,以下是文档路径。

https://www.php.net/manual/en/function.json-encode.php

# Share
## java数据类型的基本问题

举个例子比如

int i = 1.5; // 错误

int i = 60000000000000000000000000L//错误

突然给出上述两个错误看着有些突兀，下面我就从java的数据类型角度叙述下,

Java 的两大数据类型:

- 内置数据类型
- 引用数据类型

## 内置数据类型

Java语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

具体哪些我就不说了，但是数据类型自动转换之间是有原则的，并不是说等比如数据范围小的值往数据范围大的值转换 如 int类型数据 往long类型数据转换 那没什么问题 ，但是long类型的值 往 int类型的值转换的话 就会造成数据溢出，你将double的值转换成int类型的就会造成精度的丢失，比如本来值是3.4就会转换成3

