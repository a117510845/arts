# arts第九周 #

> 作者：周孝文

> 创建日期：2019-7-31

## 概述

见首页README.

# algorithm
## 题目

6. [ZigZag Conversion](https://leetcode.com/problems/longest-palindromic-substring/)

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```php
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```


```php
class Solution {

    /**
     * @param String $s
     * @param Integer $numRows
     * @return String
     */
    function convert($s, $numRows) {
        $len = strlen($s);
        if($numRows == 1 || $numRows == $len){
            return $s;
        }
        $result = '';
        $step   = 2*($numRows-1);
        for($i=0;$i<$numRows;$i++){
            for($j=0;$i+$j<$len;$j+=$step){
                $result.= $s[$i+$j];
                if($i != 0 && $i != $numRows-1 && $j+$step-$i <$len ){
                    $result.=$s[$j+$step-$i];
                }
               
            }
        
        }
        return $result; 
    
    }
}
```

### Submission Detail

| **1158 / 1158** test cases passed.          | Status: Accepted             |
| ------------------------------------------- | ---------------------------- |
| Runtime: **12 ms**Memory Usage: **14.8 MB** | Submitted: **4 minutes ago** |



### 题目解析

本题是一道Medium级别的算法题，但是为什么我觉得每道算法题感觉都很难。。首先刚写这道题目的时候有些懵逼 ZigZag是什么,之后搜了一下内容才知道就是就是把字母按照给定的行数入参将字符串排列成那种类似Z字型的样子之后按照顺序将新的字符串排列出来。那么这道算法题就变成了找规律的算法题了，把原来的字符串改成123456789ABCD,之后按照2,3,4行的设定将字符串排列 ，其实可以发现第一行和最后一行他们的排列的规律还蛮容易得到的，每行之间的间隔，如果行数是n的话 ，间隔大概是2n-2,将每列的数据挤压在一起，其实每两列之间会有一条数据，那么其实规律就比较好找

程序设计主要就是一下几个思路：

1.将行数二维数组的一级循环，将每行的元素的位置作为二级循环

2.将不是第一行和最后一行的单独判断，非中间列和前一列的步长是2n-2-$i，那么中间列的当前位置就是$j+$step-$i,在循环当中自动把中间字符串累加到当中

此道算法主要考察找规律然后把规律用表达式表达出来。


# Review

## [Why won't it...](http://blog.cleancoder.com/uncle-bob/2019/07/22/WhyWontIt.html)

A few days ago I was ordering lunch at a barbecue joint in Austin, Texas. The menu described a lovely plate of three sausages, and suggested six different sausage types to choose from. I love a good sausage; and I am especially fond of Bratwurst. So when the waiter came by I told him I wanted two Brats and a Keilbasa.

The waiter nodded and proceeded to tap on his hand-held POS terminal. Over the next 60 seconds his taps grew ever more punctuated and his expression grew ever more frustrated. He started muttering words under his breath – words that I have heard so many times before: *Why won’t it let me…?*

Apparently the genius developers who wrote the software for the hand-held POS terminal had not considered that a customer would want two of the same kind of sausage. The terminal simply would not allow the waiter to add bratwurst twice.

We had a large group at the table, and the waiter had only taken half the orders at this point; but his frustration was so great that he abandoned the table and ran into the kitchen to resolve the issue. He came back a few minutes later and told me that the kitchen would do their best.

Software is supposed to make life easier. Software is supposed to ease and enable the job of users. All too often, however, software is constraining and restrictive. If you don’t do what the software expects, the software fights you and stops you. And you mutter under your breath: “Why won’t it…”

In the early days of software we were generally forgiving of this kind of thing. It was enough of a miracle that we were getting any automated help at all. So the inflexible state machines that programmers employed in those days were a small price to pay for the massive improvement we gained from the automation.

But those days are gone. Nowadays we expect software to *get out of our way*. For example the hand-held POS terminal used by a waiter should be *more* flexible, and *less* constraining than a pad of paper. That POS terminal should *not* get in the way.

Now before you try to put all this off on the UX people, remember that you are writing the code. It is your fingers on the keyboard. It is your mind engaged in the task of making the machine do what the user needs it to do. We expect the UX people to be smart. We expect that they will try to describe a system that will stay out of the users’ way. But that doesn’t mean that we should blithely and blindly implement that specification. After all, nobody knows the machine better than we do.

Remember that as a programmer you are also a stakeholder. Your reputation is on the line. You need the product to be a success. So *play* with the software. Pretend you are a user. Walk through the use cases. Invent new use cases. Try to find areas where the software inhibits or constrains those use cases.

Yes, I know, the UX people will be doing this too. Yes, I know, there will be alpha and beta trials (probably). Yes, I know, UX is not your job. But do it anyway; because your name is on that product.

因为文章比较短，所以就截图下来，文章中多次提到一个词UX,大家百度下都会知道UX就是用户体验的简写User Experience,那全篇文章就很好理解了,其实就是为了给我们说下作为一个开发者,用户体验的一些感悟，结尾也很明显将用户体验抬到了一个很高的高度，because your name is on that product. 其实的确，作为开发者，用户体验的确不应该只是产品应该关注的事，作为产品的创造者，我们的确要有责任感。

# Tip
## idea常用的几个快捷键
| 快捷键           | 功能说明             |
| ---------------- | -------------------- |
| alt+y            | 删除当前行           |
| alt+shift+↑      | 上下箭头移动当前行   |
| alt+shift+L      | 格式化代码           |
| alt+shift+insert | 面向对象的时候会用到 |



# Share
## java内存分布结构

java的内存需要划分为5个部分：任何程度都要开辟内存空间的

- 1.栈(stack) :存放的都是方法中的局部变量。  方法的运行一定要在栈当中运行 

  局部变量:方法的参数,或者是方法()内部的变量 之前所有学的都是局部变量

  作用域：一旦超出作用域,立刻从栈内存当中消失

- 2.堆(Heap):凡是new出来的东西,都在堆当中。 

  堆内存里面的东西都有一个地址值：16进制

  堆内存里面的数据，都有默认值。规则：

  如果是整数   默认为0

  如果是浮点数 默认为0.0

  如果是字符   默认为\u0000

  如果是布尔   默认为false

  如果是引用类型 默认为null

- 3.方法区(Method Area) 存储class相关信息，包含方法的信息

- 4.本地方法栈(Native  Method Stack) :与操作系统相关

- 5.寄存器（pc Register）与cpu相关

