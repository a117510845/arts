# arts第十周 #

> 作者：周孝文

> 创建日期：2019-8-9

## 概述

见首页README.

# algorithm
## 题目

[8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

**Note:**

- Only the space character `' '` is considered as whitespace character.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

**Example 1:**

```
Input: "42"
Output: 42
```

**Example 2:**

```
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```

**Example 3:**

```
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```

**Example 4:**

```
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
```

**Example 5:**

```
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```

```php
class Solution {

    /**
     * @param String $str
     * @return Integer
     */
    function myAtoi($str) {
          if(!$str){
         return 0;
     }
     $result = 0;
     $str = trim($str);
     
     $flag = "+";
     $i = 0;
     if($str[0] == "-"){
         $flag = "-";
         $i++;
     }elseif($str[0] == "+"){
              $i++;  
     }
     
     while(strlen($str) >$i && $str[$i]>= "0"
     && $str[$i]<= "9"
     ){
         $result = $result*10 + $str[$i];
         $i++;
     }
     if($flag == "-"){
         $result = -$result;
     }
     
     if($result > (pow(2,31)-1)){
         return (pow(2,31)-1);
     }
     if($result <  (-pow(2,31))){
                return -pow(2,31);
     }
     
     return $result;
    }
}
```

### Submission Detail

| **1079 / 1079** test cases passed.         | Status: Accepted             |
| ------------------------------------------ | ---------------------------- |
| Runtime: **4 ms**Memory Usage: **14.8 MB** | Submitted: **3 minutes ago** |


```java
class Solution {
    public int myAtoi(String str) {
        str = str.trim();
            if(str == null || str.length() < 1){
            return  0;
        }


        char flag = '+';
        double result = 0;

        int i = 0;
        if(str.charAt(i) == '-'){
            flag = '-';
            i++;
        }else if(str.charAt(i) == '+'){
            i++;
        }

        while (str.length() > i  && str.charAt(i) >= '0' && str.charAt(i) <= '9'){
            //要去除最初的字符串
            result = result*10 + (str.charAt(i) - '0');
            i++;
        }

        if (flag == '-')
            result = -result;

        if(result > Integer.MAX_VALUE){
            return Integer.MAX_VALUE ;
        }else if(result < Integer.MIN_VALUE){
            return Integer.MIN_VALUE ;
        }

        return (int)result;

        
    }
}
```

### Submission Detail

| **1079 / 1079** test cases passed.         | Status: Accepted                      |
| ------------------------------------------ | ------------------------------------- |
| Runtime: **1 ms**Memory Usage: **35.8 MB** | Submitted: **1 hour, 15 minutes ago** |

### 题目解析

本题是一道Medium级别的算法题，不算难，开篇对atoi这个名词做了解释，简单的说就是把字符串转换为对应的整数，听着好像很简单，但是其实转换的要求还是蛮多，因为最近在写java所以我用了两种语言去解题，不过用php的时候其实php是有对应的函数的就是intval(),不过我试了下，感觉在超出精度范围的时候好像会出问题，而且题目本来就是考察的算法能力,解题思路就是符合下面的要求即可

所以，有必要解释一下题目的要求：

1. 首先需要丢弃字符串前面的空格；

2. 然后可能有正负号（注意只取一个，如果有多个正负号，那么说这个字符串是无法转换的，返回0。比如测试用例里就有个“+-2”）；

3. 字符串可以包含0~9以外的字符，如果遇到非数字字符，那么只取该字符之前的部分，如“-00123a66”返回为“-123”；

4. 如果超出int的范围，返回边界值（2147483647或-2147483648）。

# Review

## [Too Clean?](http://blog.cleancoder.com/uncle-bob/2018/08/13/TooClean.html)

Anyway I think there is value in the notion that code should be livable. We should not be ashamed if our code looks a little bit lived in. On the other hand, we need to be diligent about cleaning up after ourselves; and not let the mess spin out of control.

说实话,看外国的博客真的感觉特别难理解,而且还是Robert C. Martin这种大牛的博客,文章主旨提到livable code这个概念，也说到了代码就像是生活,代码中和生活一样总有混乱的地方,而某些混乱往往能给与你代码带来意想不到创造性的东西，那么结尾就想原文的结尾那种要定时的清理，将混乱的代码控制在一个合理的范围内。																																																																																			

# Tip
## ==在java语言中的不同之处


字符串常量池，程序当中直接写上的双引号字符串，就在字符串常量池中，

对于基本类型来说，==是进行数值的比较，
对于引用类型来说  ==是进行【地址值】的比较


堆内存当中有个字符串常量池

 引用类型的== 比较是地址值 ，
 双引号直接写的字符串在常量池当中，new 的不在池当中


# Share
## java中static的定位

一旦使用static修饰成员方法，那么这就成为静态方法，静态方法不属于对象，而是属于类的，

如果没有static关键词， 那么必须首先创建独享，然后通过创建对象才能使用它
如果有了static关键字，那么不要创建对象，直接就能通过类名称来使用它

无论是成员变量，还是成员方法，如果有了static 都推荐用类名称进行调用
静态变量：类名称。静态变量
静态方法类名称静态方法()

注意事项
1.静态只能直接访问静态，不能直接访问非静态
原因：因为在内存当中是先有的静态内容，后有的非静态内容，
先人不知道后人，但是后人知道先人
2.静态方法当中不能用this,
原因：this代表当前对象，通过谁调用的方法，谁就是当前对象


