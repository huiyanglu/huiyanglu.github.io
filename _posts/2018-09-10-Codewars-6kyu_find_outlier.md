---
layout:     post
title:      Find The Parity Outlier
subtitle:   20180910_Codewars_find_outlier
date:       2018-09-10
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Find outlier
#### Codewars Kata 2√
##### Description
Link: [find_outlier](https://www.codewars.com/kata/5526fc09a1bbd946250002dc)  
  
-简述：本题给定一列数字，要求找出其中唯一的奇数或偶数。  
-思路：分别求奇数列和偶数列，根据数列长度求解。  
-难点：无  
  
You are given an array (which will have a length of at least 3, but could be very large) containing integers. The array is either entirely comprised of odd integers or entirely comprised of even integers except for a single integer N. Write a method that takes the array as an argument and returns this "outlier" N.

##### My solution:   
    #原方法 超麻烦 步骤太多 
    def find_outlier(integers):
        even = [ ]
        odd = [ ]
        for num in integers:
            if num % 2 == 0:
                even.append(num)
            else:
                odd.append(num)
        if len(even)>1 and len(odd)==1:
            return odd[0]
        elif len(odd)>1 and len(even)==1:
            return even[0]  
  
##### Given solutions:  
    def find_outlier(int):
        odds = [x for x in int if x%2!=0]
        evens= [x for x in int if x%2==0]
        return odds[0] if len(odds)<len(evens) else evens[0]

##### Improved solutions:
    def find_outlier(integers):
        evens = [num for num in integers if num%2==0]
        odds = [num for num in integers if num%2!=0]
        return odds[0] if len(odds)<len(evens) else evens[0]

##### Points
1 和IQ test题类似 更简单  