---
layout:     post
title:      English beggars
subtitle:   20180930_Codewars_beggars
date:       2018-09-30
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# English beggars
#### Codewars Kata 22√
##### Description
https://www.codewars.com/kata/59590976838112bfea0000fa  

-简述：本题给定一系列值和一些乞丐，你应该返回一个数组，其中包含每个乞丐带回家的总和，假设它们都经常循环， 第一个到最后一个。  
-思路：常规做法：循环递增；巧妙方法：values[i::n]  
-难点：无  

Born a misinterpretation of this kata, your task here is pretty simple: given an array of values and an amount of beggars, you are supposed to return an array with the sum of what each beggar brings home, assuming they all take regular turns, from the first to the last.

For example: [1,2,3,4,5] for 2 beggars will return a result of [9,6], as the first one takes [1,3,5], the second collects [2,4].

The same array with 3 beggars would have in turn have produced a better out come for the second beggar: [5,7,3], as they will respectively take [1,4], [2,5] and [3].

Also note that not all beggars have to take the same amount of "offers", meaning that the length of the array is not necessarily a multiple of n; length can be even shorter, in which case the last beggers will of course take nothing (0).

Note: in case you don't get why this kata is about English beggars, then you are not familiar on how religiously queues are taken in the kingdom ;)

##### My solution
    def beggars(a,n):
        res = [ 0 for i in range(n)]
        for j in range(0,len(a)):
            if n != 0:
                res[j%n] += a[j]
            else:
                return []
        return res

##### Given solutions
    def beggars(values, n):
        return [sum(values[i::n]) for i in range(n)]

##### Points
1 values[i::n]从i开始，间隔为n  