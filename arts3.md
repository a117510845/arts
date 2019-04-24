# arts第三周 #

> 作者：周孝文

> 创建日期：2019-4-24

## 概述

见首页README.

# algorithm
## 题目

28.[Implement strStr()](https://leetcode.com/problems/implement-strstr/)

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

solution：

```php
class Solution {

    /**
     * @param String $haystack
     * @param String $needle
     * @return Integer
     */
    function strStr($haystack, $needle) {
        if(!$needle){
           return 0;
        }
        if(($result = strpos($haystack,$needle)) === false){
            return -1;
        }else{
            return $result;
        }
    }
}
```
### Submission Detail

| **74 / 74** test cases passed.             | Status: Accepted              |
| ------------------------------------------ | ----------------------------- |
| Runtime: **8 ms**Memory Usage: **14.9 MB** | Submitted: **31 minutes ago** |

总结： 本人喜欢打怪升级，所以一向喜欢从简单到难得过程。所以也是从easy
难度开始，上一题其实就是对目标字符串进行特定字符串查找，查找出特定字符串在目标字符串中出现的位置，考察点比较基础，需要注意的是要考虑一些特殊情况比如空字符串。


# Review

### Maps

Maps are a convenient and powerful built-in data structure that associate values of one type (the *key*) with values of another type (the *element* or *value*). The key can be of any type for which the equality operator is defined, such as integers, floating point and complex numbers, strings, pointers, interfaces (as long as the dynamic type supports equality), structs and arrays. Slices cannot be used as map keys, because equality is not defined on them. Like slices, maps hold references to an underlying data structure. If you pass a map to a function that changes the contents of the map, the changes will be visible in the caller.

Maps can be constructed using the usual composite literal syntax with colon-separated key-value pairs, so it's easy to build them during initialization.

本段摘自go语言的一篇入门级的使用手册 [Effective Go](https://docs.huihoo.com/go/golang.org/doc/effective_go.html)

这段内容主要是说明go语言中一个重要的关键词map的定义,golang有两种比较重要的数据结构,一个是slice还有一个是map,其实map的使用类似hash,而slice底层是数组，二者看似有对数组的操作，但是map比slice要更灵活对键值的设置选择性更多，特别是对于key，value组合的映射关系可以很明确，如果大家想深入了解欢迎去我贴的路径去看

# Tip
## thinkPHP5框架的新特性validate验证器

## 验证场景

| 版本  | 新增功能                                   |
| :---- | :----------------------------------------- |
| 5.0.4 | 增加`hasScene`方法用于检查是否存在验证场景 |

可以在定义验证规则的时候定义场景，并且验证不同场景的数据，例如：

```
$rule = [
    'name'  => 'require|max:25',
    'age'   => 'number|between:1,120',
    'email' => 'email',
];
$msg = [
    'name.require' => '名称必须',
    'name.max'     => '名称最多不能超过25个字符',
    'age.number'   => '年龄必须是数字',
    'age.between'  => '年龄只能在1-120之间',
    'email'        => '邮箱格式错误',
];
$data = [
    'name'  => 'thinkphp',
    'age'   => 10,
    'email' => 'thinkphp@qq.com',
];
$validate = new Validate($rule);
$validate->scene('edit', ['name', 'age']);
$result = $validate->scene('edit')->check($data);
```

表示验证edit场景（该场景定义只需要验证name和age字段）。

如果使用了验证器，可以直接在类里面定义场景，例如：

```
namespace app\index\validate;

use think\Validate;

class User extends Validate
{
    protected $rule =   [
        'name'  => 'require|max:25',
        'age'   => 'number|between:1,120',
        'email' => 'email',    
    ];
    
    protected $message  =   [
        'name.require' => '名称必须',
        'name.max'     => '名称最多不能超过25个字符',
        'age.number'   => '年龄必须是数字',
        'age.between'  => '年龄只能在1-120之间',
        'email'        => '邮箱格式错误',    
    ];
    
    protected $scene = [
        'edit'  =>  ['name','age'],
    ];
    
}
```

然后再需要验证的地方直接使用 scene 方法验证

```
$data = [
    'name'  => 'thinkphp',
    'age'   => 10,
    'email' => 'thinkphp@qq.com',
];

$validate = new \app\index\validate\User($rule);
$result = $validate->scene('edit')->check($data);
```

可以在定义场景的时候对某些字段的规则重新设置，例如：

```
namespace app\index\validate;

use think\Validate;

class User extends Validate
{
    protected $rule =   [
        'name'  => 'require|max:25',
        'age'   => 'number|between:1,120',
        'email' => 'email',    
    ];
    
    protected $message  =   [
        'name.require' => '名称必须',
        'name.max'     => '名称最多不能超过25个字符',
        'age.number'   => '年龄必须是数字',
        'age.between'  => '年龄只能在1-120之间',
        'email'        => '邮箱格式错误',    
    ];
    
    protected $scene = [
        'edit'  =>  ['name','age'=>'require|number|between:1,120'],
    ];
    
}
```

可以对场景设置一个回调方法，用于动态设置要验证的字段，例如：

```php
$rule = [
    'name'  => 'require|max:25',
    'age'   => 'number|between:1,120',
    'email' => 'email',
];
$msg = [
    'name.require' => '名称必须',
    'name.max'     => '名称最多不能超过25个字符',
    'age.number'   => '年龄必须是数字',
    'age.between'  => '年龄只能在1-120之间',
    'email'        => '邮箱格式错误',
];
$data = [
    'name'  => 'thinkphp',
    'age'   => 10,
    'email' => 'thinkphp@qq.com',
];
$validate = new Validate($rule);
$validate->scene('edit', function($key,$data){
    return 'email'==$key && isset($data['id'])? true : false;
});
$result = $validate->scene('edit')->check($data);
```

以上主要介绍了通过构造Validate文件配置相应的类进行规则，场景等相关配置，想了解更多不如多动手

# Share
## 引言

之前写代码总是喜欢把逻辑代码和展示层的内容写在一起,其实正常的业务开发是无关痛痒，但是当业务逻辑变的繁杂多样，多重分层的时候，一个c层的控制器实在是太多了，所以在这种痛点的基础上我想寻求一个合理的优雅的解决方案，那么AOP思想(面向切面编程)隆重登场。

```php
先说一个Spring是什么吧，大家都是它是一个框架，但框架这个词对新手有点抽象，以致于越解释越模糊，不过它确实是个框架的，但那是从功能的角度来定义的，从本质意义上来讲，Spring是一个库，一个Java库，所以我个人觉得应该这样回答Spring是什么：Spring是一个库，它的功能是提供了一个软件框架，这个框架目的是使软件之间的逻辑更加清晰，配置更灵活，实现这个目的的手段使用AOP和IoC，而AOP和IoC是一种思想，是一种什么样的思想呢，等下细说，先说AOP在Java里是利用反射机制实现（你也可以认为是动态代理，不过动态代理也是反射机制实现的，所以还是先不要管动态代理，我们这里化繁为简，不让它干扰咱们对AOP的理解），如何使用AOP呢，很简单滴，等下介绍。
下面先说AOP是什么样的思想，我们一步一步慢慢来，先看一下传统程序的流程，比如银行系统会有一个取款流程

我们可以把方框里的流程合为一个，另外系统还会有一个查询余额流程，我们先把这两个流程放到一起：

有没有发现，这个两者有一个相同的验证流程，我们先把它们圈起来再说下一步：

有没有想过可以把这个验证用户的代码是提取出来，不放到主流程里去呢，这就是AOP的作用了，有了AOP，你写代码时不要把这个验证用户步骤写进去，即完全不考虑验证用户，你写完之后，在另我一个地方，写好验证用户的代码，然后告诉Spring你要把这段代码加到哪几个地方，Spring就会帮你加过去，而不要你自己Copy过去，这里还是两个地方，如果你有多个控制流呢，这个写代码的方法可以大大减少你的时间，不过AOP的目的不是这样，这只是一个“副作用”，真正目的是，你写代码的时候，事先只需考虑主流程，而不用考虑那些不重要的流程，懂C的都知道，良好的风格要求在函数起始处验证参数，如果在C上可以用AOP，就可以先不管校验参数的问题，事后使用AOP就可以隔山打牛的给所有函数一次性加入校验代码，而你只需要写一次校验代码。不知道C的没关系，举一个通用的例子，经常在debug的时候要打log吧，你也可以写好主要代码之后，把打log的代码写到另一个单独的地方，然后命令AOP把你的代码加过去，注意AOP不会把代码加到源文件里，但是它会正确的影响最终的机器代码。
现在大概明白了AOP了吗，我们来理一下头绪，上面那个方框像不像个平面，你可以把它当块板子，这块板子插入一些控制流程，这块板子就可以当成是AOP中的一个切面。所以AOP的本质是在一系列纵向的控制流程中，把那些相同的子流程提取成一个横向的面，这句话应该好理解吧，我们把纵向流程画成一条直线，然把相同的部分以绿色突出，如下图左，而AOP相当于把相同的地方连一条横线，如下图右，这个图没画好，大家明白意思就行。

    

这个验证用户这个子流程就成了一个条线，也可以理解成一个切面，aspect的意思我认为是方面，你用什么实物去类比，只要你能理解都可以。这里的切面只插了两三个流程，如果其它流程也需要这个子流程，也可以插到其它地方去。
```

总结下我的想法 其实aop思想就是设计模式中的代理模式,实现也是蛮简单的,在php的语言看来在项目代码中拆分出一个代理文件夹专门放对应c层的代理类，作为业务逻辑堆放，最近在用tp，tp3.2的event类正好契合的了aop的思想。

