# arts第六周 #

> 作者：周孝文

> 创建日期：2019-5-27

## 概述

见首页README.

# algorithm
## 题目

3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

**Example 2:**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```php
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLongestSubstring($s) {
        $max = 0;
        $current = '';
        for($i=0;$i<strlen($s);$i++){
            if(strpos($current,$s[$i]) !== false){
                $current = substr($current,strpos($current,$s[$i])+1);
            }
            $current.= $s[$i];
            $len = strlen($current);
            $max     = max($max,$len);
        }
        return $max;
    }
}
```

### Submission Detail

| **987 / 987** test cases passed.            | Status: Accepted             |
| ------------------------------------------- | ---------------------------- |
| Runtime: **20 ms**Memory Usage: **14.9 MB** | Submitted: **2 minutes ago** |

### 题目解析

这里遍历整个字符串，定义一个变量用来存储字符串，定义一个变量存储最大的长度，只要出现重复了，说明此时就是从头到当前字母无重复的最大长度，我们需要把开始计算位置移至它的下一个位置即可。每次保存最大连续长度，直至遍历结束


# Review

### Maps

## [What does Stack Overflow want to be when it grows up?](https://blog.codinghorror.com/what-does-stack-overflow-want-to-be-when-it-grows-up/)

>**Stack Overflow is you.**
>
>This is the scary part, the great leap of faith that Stack Overflow is predicated on: trusting your fellow programmers. The programmers who choose to participate in Stack Overflow are the “secret sauce” that makes it work. You are the reason I continue to believe in developer community as the greatest source of learning and growth. You are the reason I continue to get so many positive emails and testimonials about Stack Overflow. I can’t take credit for that. But you can.
>
>I learned the collective power of my fellow programmers long ago writing on Coding Horror. The community is far, far smarter than I will ever be. All I can ask — all any of us can ask — is to help each other along the path.
>
>And if your fellow programmers decide to recognize you for that, then I say you’ve well and truly earned it.

上面是一篇优秀程序员的博客的内容，为什么说优秀呢，根据这篇文章发现博主是stack-overflow的创始人，整篇文章讲述了他对堆栈溢出这个平台的想法，历程和感悟，也正如结尾说的无论做什么，我们都在一起吗，也希望大家能好好的利用这个平台提升自己的技能水平。

# Tip
## java中的包的概念定义
例如：音乐类-myClassMusic

-music

com.imooc.music.MyClassMusic

-movie

com.imooc.movie.MyClassMovie

3.系统中的包

java.(功能).(类)

java.lang.(类)包含java语言基础的类

java.util.(类) 包含java语言中各种工具类

java.io.(类)  包含输入，输出相关功能的类

# Share
最近一直在自学java,那么写程序就像战斗一样肯定要一把趁手的武器，我选择idea，讲到idea我感觉没什么好像我之前用的phpstorm没什么区别，但是真的去写代码的时候还有看别人写项目的视频的时候发现真的别人一键生成的代码，我还傻兮兮的一行一行的敲，下面就是我觉得比较实用的几个小功能。

### alt + enter 代码小助手

1.实现接口

2.单词拼写

3.导包

### shift + F6 批量变量重构

### Refactor 的extract 的提取操作

特别是alt+enter真的各种实用，简直就像一个万能钥匙



