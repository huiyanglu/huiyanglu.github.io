---
layout:     post
title:      Shuffle It Up
subtitle:   20181017_Codewars_all_permuted
date:       2018-10-17
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Shuffle It Up
#### Codewars Kata 37√
##### Description
https://www.codewars.com/kata/shuffle-it-up/pytho
   
-简述：本题给定一列数字的长度，要求重新排列该列数，使得每个数字都不在其原来的位置上，求共有多少种不同排列方法。  
-思路：原方法：遍历所有排列可能，找出不符合情况的排列，但该方法用时太久。该问题有专门的数学计算公式，较为简便。  
-难点：无  

We have an array of unique elements. A special kind of permutation is the one that has all of its elements in a different position than the original.
  
Let's see how many of these permutations may be generated from an array of four elements. We put the original array with square brackets and the wanted permutations with parentheses.
  
arr = [1, 2, 3, 4]  
      (2, 1, 4, 3)  
      (2, 3, 4, 1)  
      (2, 4, 1, 3)  
      (3, 1, 4, 2)  
      (3, 4, 1, 2)  
      (3, 4, 2, 1)  
      (4, 1, 2, 3)  
      (4, 3, 1, 2)  
      (4, 3, 2, 1)  
      _____________  
      
A total of 9 permutations with all their elements in different positions than arr.  
The task for this kata would be to create a code to count all these permutations for an array of certain length.
  
Features of the random tests:
  
l = length of the array
10 ≤ l ≤ 5000
  

##### My solution  
    def all_permuted(n):
        a,b = 0, 1
        for i in range(1,n):
            a,b = b, (i+1)*(a+b)
        return a

    print(all_permuted(4))

##### Given solutions  
    from itertools import islice

    def A000166():
        # https://oeis.org/A000166
        a, b, n = 1, 0, 1
        while True:
            yield a
            a, b = b, n * (a + b)
            n += 1

    all_permuted = dict(enumerate(islice(A000166(), 5000))).get
  
---  
    def f(n):
        # by working through sizes 1-9 found an iterative relationship
        # f(1) = 0
        # f(n) = n*f(n-1) + (1 if n is even else -1)
        if (n==0):
            return 1
        else:
            return n*f(n-1)+(1 if n%2==0 else -1)

    def all_permuted(array_length):
        return f(array_length)
 
##### Points  
1   
> https://baike.baidu.com/item/%E9%94%99%E4%BD%8D%E9%87%8D%E6%8E%92/9967097?fr=aladdin  
> 错位重排是指一种比较难理解的复杂数学模型，是伯努利和欧拉在错装信封时发现的，因此又称伯努利-欧拉装错信封问题。  
> 表述为：编号是1、2、…、n的n封信，装入编号为1、2、…、n的n个信封，要求每封信和信封的编号不同，问有多少种装法？  
> 对这类问题有个固定的递推公式，记n封信的错位重排数为Dn，则D1=0，D2=1，Dn=（n-1）（Dn-2+Dn-1） 此处n-2、n-1为下标。n>2  
> 我们只需记住Dn的前几项：D1=0，D2=1，D3=2，D4=9，D5=44。  
> 递推公式：（N-1）*（A+B）=C （A是第一项，B是第二项，C是第三项，N是项数）  

2 思路：
a = 0, b = 1, i=1   
a = 1, b=(1+1)*(0+1)=2, i=2  
a = 2, b = (2+1)*(1+2)=9, i=3  
a = 9, b = (3+1)*(2+9)=44, i=4  
a = 44, b = (4+1)*(9+44)  
...  