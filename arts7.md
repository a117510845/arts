# arts第七周 #

> 作者：周孝文

> 创建日期：2019-6-3

## 概述

见首页README.

# algorithm
## 题目

4. [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume **nums1** and **nums2** cannot be both empty.

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```php
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```



```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLongestSubstring($s) {
        $arr = array_merge($nums1,$nums2);
        sort($arr);
        $resultVal = 0;
        if(is_array($arr) && count($arr)>0){
            $length = count($arr);
            if($length%2==0){
                $resultVal = ($arr[floor($length/2)-1] + $arr[floor($length/2)])/2;
            }else{
                $resultVal =   $arr[floor($length/2)];
            }
        }

        return $resultVal;
    }
}
```

### Submission Detail

| **2084 / 2084** test cases passed.          | Status: Accepted            |
| ------------------------------------------- | --------------------------- |
| Runtime: **40 ms**Memory Usage: **15.1 MB** | Submitted: **1 minute ago** |

### 题目解析

这道算法题属于hard级别的题目，从我的解题实例中其实并没有特别复杂是因为我其实没有在意题目中以复杂度O(log (m+n))的思路来解题，因为本人对于时间复杂度和空间复杂度的方面的内容比较欠缺，所以暂时以当前认为最简单的代码完成算法解题，后续我会考虑根据二分法，分治法等其他方法来解题，我当前的解题思路很简单就会归并排序然后获取值。


# Review

### Maps

## [An Exercise Program for the Fat Web?](https://blog.codinghorror.com/an-exercise-program-for-the-fat-web/)

>With the latest Chrome crackdown on ad blockers, now is the time, and I'm impressed how simple and easy [Pi-Hole](https://pi-hole.net/) is to run. Just find a quiet place to plug it in, spend an hour configuring it, and promptly proceed to forget about it forever as you enjoy a lifetime subscription to *a glorious web ad instant weight loss program across every single device on your network with (almost) zero effort!*
>
>Finally, an exercise program I can believe in.

这篇文章作者是一名知名的程序员，是谁呢，我也不知道，但是最近比较喜欢看他对于业内一些东西的见解，这篇文章其实是作者对当前网络环境中出现的一种广告泛滥导致一些乱象的叙述，随着各种垃圾广告的暴露，相应的浏览器层面的广告拦截器也应运而生，但是实际上广告拦截器也不过是互联网公司的盈利手端，最后作为给我们介绍一个路由设备可以通过dns，dhcp在源头上拦截广告的泛滥，让网络真正的瘦身。

# Tip
## java中的异常类型
![flow](/source/throw.png)

# Share
因为我是学php出生的，所以在数据的处理方面特别依赖数据，但是自从学了java之后我发现其实java不是怎么用数组直接进行数据。

--因为java的数组是固定长度的，集合长度可变 

--数组只能通过下标访问元素,类型固定,而有的集合可以通过任意类型查找所映射的具体对象

那么java喜欢使用的几个处理的数据的类型是什么就是list和set，具体怎么用，大家自己去看看吧



