# arts第五周 #

> 作者：周孝文

> 创建日期：2019-5-17

## 概述

见首页README.

# algorithm
## 题目

2. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

solution：

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */
class Solution {

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function addTwoNumbers($l1 , $l2) {
        
         
    $node=new ListNode($this->res + $l1->val + $l2->val);
        if($this->res=intval($node->val >9)){
            $node->val -=10;
        }
    $node->next=(!$this->res && is_null($l1->next) && is_null($l2->next) )?null:$this->addTwoNumbers($l1->next,$l2->next);
        return $node;
        
    }
}
```

### Submission Detail

| **1563 / 1563** test cases passed.          | Status: Accepted             |
| ------------------------------------------- | ---------------------------- |
| Runtime: **20 ms**Memory Usage: **14.9 MB** | Submitted: **2 minutes ago** |

总结： 这是一道对链表结构的加法题，看着感觉很简单，但是其实对于phper来说，数据结构可以说是一个很大的盲点，因为我们经常处理的可能就是对象，数组，队列可能也只是在中间件中用到，但是其实我们只要去了解其实还是很简单的，比如链表有这他自己的特点就是,他有两个要素一个是当前节点的值value还有一个就是就是一个下个节点的指向next,在链表的尾部next一般等于null，整个逻辑其实蛮简单就是通过函数内的递归不断取子节点直到取到null，有一个要注意的点就是其实当时值大于10的时候我们不能去取超过10的值所以要做进位的处理。


# Review

### Maps

## [The Cloud Is Just Someone Else's Computer](https://blog.codinghorror.com/the-cloud-is-just-someone-elses-computer/)

If you'd also like to embark upon this project, you can get [the same Partaker B18 box I did for $490 from Amazon](https://www.amazon.com/Partaker-Coffee-Graphics-Barebone-System/dp/B07L4KJXWL?tag=codihorr-20), or [$460 direct from China via AliExpress](https://www.aliexpress.com/item/Partaker-B18-DDR4-Coffee-Lake-8th-Gen-Mini-PC-Intel-Core-i7-8750H-32GB-RAM-Intel/32948461273.html). Add memory and drive to taste, build it up, then check out [endoffice.com](https://endoffice.com/) who I can enthusiastically recommend for colocation, or the colocation provider of your choice.

文章路径如小标题，博主我不是很认识，是通过知乎进去正好看到博主对云服务器的选择写了一篇文章，所以无聊看了，虽然是说云服务器，但是大体内容是介绍自己买物理机作为服务器的一些性能和价格的选择，就如结尾说的如果你只是想在自己的小空间做博客或者个人站或者是管理自己的资源的话,自己买物理机就可以而且苹果的牌子还蛮好的，如果需要复杂度比较高，而且流量大，的业务还是需要云服务器的。

# Tip
## php 空数组的json数据转换
之前在对接java接口的时候，接口总是调不通，但是沟通下其实接口是没什么大问题的，那么我就从主要的入参出发通过，不同的入参去调用接口，发现果然是是入参的问题

![flow](/source/json.png)


如图，可以看出对于空数组和非空数组其实转换出的格式时不一样的，我以为空数组转换为json格式时{},但是实际打印出的是数组，那么对于在java对接的场景如果你返回数组肯定是有问题的。

# Share
这次分享想了想，感觉分享这个东西写着写着到后期会黔驴技穷啊，不管他先来一个最近特别喜欢的一种写法简单上传验证的写法，是基于tp5.0，这范围比较窄，希望能帮到大家。

```php
          $result = $this->validate(
                ['file' => $file],
                ['file'=>'fileSize:40000000|fileExt:xls,xlsx'],
                ['file.fileSize' => '上传文件过大', 'file.fileExt' => '上传文件后缀不正确']
            );
```

文件大小和格式的验证简单两行代码搞定配合捕捉错误进行过程控制.



