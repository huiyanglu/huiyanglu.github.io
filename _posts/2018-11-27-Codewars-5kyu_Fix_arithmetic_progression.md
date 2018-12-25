---
layout:     post
title:      Fix arithmetic progression
subtitle:   20181127_Codewars_5kyu_Fix_arithmetic_progression
date:       2018-11-27
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Fix arithmetic progression
#### Codewars Kata 53√
##### Description
https://www.codewars.com/kata/5b77b030f0aa5c9114000024/solutions/python

Description:   
-简述：本题给定一个长度大于2的数列，转换list中的数字使其+1或-1或不变，使列表变成顺序数列，相邻数字的差值固定，如果无法做到，就返回-1，若可以，返回最少的改变次数。  
-思路：前两个数分别+1/-1/不变，判断若后面每两个数之间的差都等于前两个数的差，则后面的数分别需要如何加减变化，当每个数的变化范围都在1之内，成立，遍历得到所有符合条件的变化，求变化次数总和的最小值。  

In this Kata, we define an arithmetic progression as a series of integers in which the differences
between adjacent numbers are the same.
  
You will be given an array of ints of length > 2 and your task will be to convert it into an arithmetic progression by the following rule:
  
For each element there are exactly three options: an element can be decreased by 1, an element can be increased by 1 or it can be left unchanged.
  
Return the minimum number of changes needed to convert the array to an arithmetic progression. If not possible, return -1.
  
##### Examples:  
solve([1,1,3,5,6,5]) == 4 because [1,1,3,5,6,5] can be changed to [1,2,3,4,5,6] by making 4 changes.  
solve([2,1,2]) == 1 because it can be changed to [2,2,2]  
solve([1,2,3]) == 0  because it is already a progression, and no changes are needed.  
solve([1,1,10) == -1 because it's impossible.  
solve([5,6,5,3,1,1]) == 4. It becomes [6,5,4,3,2,1]  
  

##### My solution
    def solve(arr):
        rst = []
        for x0 in (arr[0],arr[0]-1,arr[0]+1):
            for x1 in (arr[1],arr[1]-1,arr[1]+1):
                delta = x1 - x0 # 前两个数之差
                diff = [x0 != arr[0]] + [abs(x0 + i*delta - arr[i]) for i in range(1,len(arr))] 
    	# 根据x0和delta,arr[i]应该为多少,和arr[i]的实际值比较差值应<=1
                if all(each_dif <= 1 for each_dif in diff):
                    rst.append(sum(diff))
        return min(rst) if rst else -1

    print(solve([24,21,14,10]))
  
##### Points  
1 any()和all()用法  
any(x)判断x对象是否为空对象，如果都为空、0、false，则返回false，如果不都为空、0、false，则返回true  
all(x)如果all(x)参数x对象的所有元素不为0、''、False或者x为空对象，则返回True，否则返回False  
  
ps: 今天太累了参考了given solution才做出来，脑子都不转了… 看书的时候不许吃麦丽素！！！
