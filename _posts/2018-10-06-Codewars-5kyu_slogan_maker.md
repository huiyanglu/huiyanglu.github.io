---
layout:     post
title:      All Star Code Challenge # 19
subtitle:   20181006_Codewars_slogan_maker
date:       2018-10-06
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# All Star Code Challenge # 19
#### Codewars Kata 28√
##### Description
Link: https://www.codewars.com/kata/5865a407b359c45982000036  
  
-简述：本题给定一些单词组成的列表（可能有重复），输出单词的不同排列顺序，去掉重复的单词。  
-思路：去重，用排列组合的函数  
-难点：无  
  
You work for an ad agency and your boss, Bob, loves a catchy slogan. He's always jumbling together "buzz" words until he gets one he likes. You're looking to impress Boss Bob with a function that can do his job for him.

Create a function called sloganMaker() that accepts an array of string "buzz" words. The function returns an array of all possible UNIQUE string permutations of the buzz words (concatonated and separated by spaces).

Your boss is not very bright, so anticipate him using the same "buzz" word more than once, by accident. The function should ignore these duplicate string inputs.

sloganMaker(["super", "hot", "guacamole"]);
//[ 'super hot guacamole',
//  'super guacamole hot',
//  'hot super guacamole',
//  'hot guacamole super',
//  'guacamole super hot',
//  'guacamole hot super' ]

sloganMaker(["cool", "pizza", "cool"]); // => [ 'cool pizza', 'pizza cool' ]
Note:
There should be NO duplicate strings in the output array The input array MAY contain duplicate strings, which should STILL result in an output array with all unique strings An empty string is valid input
The order of the permutations in the output array does not matter

##### My solution
    import itertools

    def slogan_maker(a):
        a2 = list(set(a))
        a2.sort(key=a.index) # 字符串去重后按原顺序排列
        x = []
        result = list(itertools.permutations(a2, len(a2))) # 字符串排列组合考虑顺序
        for i in range(0,len(result)):
            x.append(' '.join(result[i]))
        return x        

##### Given solutions
from itertools import permutations

def slogan_maker(arr):
    return list(map(' '.join, permutations(dict(zip(arr, range(len(arr)))))))

##### Points
1  

    import itertools  
    itertools.permutations()  
---
    from itertools import permutations  
    permutations()  
导入模块/导入模块中的具体函数 两种方式   

2 zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。  
![zip&dict](https://ws3.sinaimg.cn/large/006tNc79ly1fzeowzrsntj30c205m3z2.jpg)
  
3 map()是 Python 内置的高阶函数，它接收一个函数 f 和一个 list，并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。  
