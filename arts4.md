# arts第四周 #

> 作者：周孝文

> 创建日期：2019-5-6

## 概述

见首页README.

# algorithm
## 题目

35.[Search Insert Position](https://leetcode.com/problems/search-insert-position/)

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

solution：

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function searchInsert($nums, $target) {
        $index = array_search($target,$nums);
        if( $index === 0 || $index ){
            return $index;
        }else{
            foreach($nums as $k=>$val){
                if($val >= $target){
                    return $k;
                }
            }
          return count($nums);
        }
    }
}
```

### Submission Detail

| **62 / 62** test cases passed.              | Status: Accepted             |
| ------------------------------------------- | ---------------------------- |
| Runtime: **16 ms**Memory Usage: **15.9 MB** | Submitted: **8 minutes ago** |

总结： 本人喜欢打怪升级，所以一向喜欢从简单到难得过程。所以也是从easy
难度开始，这道题其实就是对目标数组中指定的数字进行定位查找,此道题关键的php是array_search结果是获取目标数字的键值，要注意的点是0键值还有非数组内数字的情况。


# Review

### Maps

1. Hyper-focus on mastering one language instead of learning a little bit about several languages.
2. If you don’t know which language to start with, pick a general-purpose language.

Don’t stress out on which one you should choose because there are jobs for every language. What matters most is your motivation, determination, and ability to focus on learning and mastering your chosen language.

本段摘自medium.freecodecamp.org的一篇文章 

文章路径是：https://medium.freecodecamp.org/how-to-choose-which-programming-language-you-should-learn-in-2019-60abef241012

之前一直看到的是golang的技术文档，想换个口味在别人的推荐下去了freecodecamp，发现前端的文章比较多，找到了一篇我比较感兴趣的文章主要是说关于软件开发者在自己未来学习语言的抉择问题,文中对前端还有后端的语言都有罗列,可以说指出了语言的优秀之处，最后也是总结出要专注一门语言，持续学习的概念。

# Tip
## phpstudy在nginx配置root路径时的坑
首先叙述下场景因为线上系统是nginx的，所以为了配合环境的一致也好排查问题，特别换了phpstudy作为本地的开发环境，那么针对站点的配置，对自己也是有帮助的,那么在配置server的root路径时遇到了小写字母的路径不兼容的问题,那么针对此问题把小写的root路径写出来

```nginx
server {
        listen       80;
        server_name  nirms.guangjing.test ;
        root   "D:\phpstudy\PHPTutorial\WWW/nirms";
        location / {
            index  index.html index.htm index.php;
			  if (!-e $request_filename) {
			   rewrite  ^(.*)$  /index.php?s=/$1  last;
			   break;
			  }
            #autoindex  on;
        }
        location ~ \.php(.*)$ {
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_split_path_info  ^((?U).+\.php)(/?.+)$;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            fastcgi_param  PATH_INFO  $fastcgi_path_info;
            fastcgi_param  PATH_TRANSLATED  $document_root$fastcgi_path_info;
            include        fastcgi_params;
        }
}
```


root路径最后一个目录名如果用大写的话不会出现问题，但是如果是小写可以通过/解决指向不到的问题。

# Share
## 引言

想想最近好像也没有什么特别好说的东西，唯一感觉和之前不同的就是svn换git了，重拾git的我感觉又焕发了神采，svn真的是旧时代的产物了，那么贴个有用的东西给大家。

![flow](/source/git.jpg)



