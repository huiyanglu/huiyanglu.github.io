---
layout:     post
title:      The highest profit wins!
subtitle:   20180917-Codewars-Min_max
date:       2018-09-17
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---

# The highest profit wins!
#### Codewars Kata 9√
**本题考算法，不可直接调用函数**  
##### Description  
Link: [Min_max](https://www.codewars.com/kata/559590633066759614000063)  
  
-简述：本题给定一列数字，通过算法求出其最大值和最小值。    
-思路：遍历该列数字，比较大小。（不可用min和max函数，考的是循环算法）  
-难点：无  
   
##### Story
Ben has a very simple idea to make some profit: he buys something and sells it again. Of course, this wouldn't give him any profit at all if he was simply to buy and sell it at the same price. Instead, he's going to buy it for the lowest possible price and sell it at the highest.
##### Task
Write a function that returns both the minimum and maximum number of the given list/array.

##### Examples
min_max([1,2,3,4,5])   == [1,5]

min_max([2334454,5])   == [5, 2334454]

min_max([1])           == [1, 1]

##### Remarks
All arrays or lists will always have at least one element, so you don't need to check the length. Also, your function will always get an array or a list, you don't have to check for null, undefined or similar.

##### My solution
    def min_max(lst):
        min = lst[0]
        max = lst[0]
        for i in range(0,len(lst)):
            if lst[i] > max:
                max = lst[i]
            elif lst[i] < min:
                min = lst[i]
            i += 1
        return [min,max]

##### Points  
1 本题考算法，不可直接调用函数  
