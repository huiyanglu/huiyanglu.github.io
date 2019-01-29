---
layout:     post
title:      Common Denominators
subtitle:   20180925_Codewars_convertFracts
date:       2018-09-25
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Common Denominators
#### Codewars Kata 17√
##### Description
Link: [convertFracts](https://www.codewars.com/kata/54d7660d2daf68c619000d95)   
  
-简述：本题以列表形式给定一些分数的分子和分母组合值，要求将各分数转换为分母相等的形式。  
-思路：求出所有分母的最小公倍数。  
-难点：1 模块导入和列表推导式表达。  
  
You will have a list of rationals in the form
 { {numer_1, denom_1} , ... {numer_n, denom_n} }
or
 [ [numer_1, denom_1] , ... [numer_n, denom_n] ]
or
 [ (numer_1, denom_1) , ... (numer_n, denom_n) ]
where all numbers are positive ints.

You have to produce a result in the form
 (N_1, D) ... (N_n, D)
or
 [ [N_1, D] ... [N_n, D] ]
or
 [ (N_1', D) , ... (N_n, D) ]
or
{ {N_1, D} ... {N_n, D} }
depending on the language (See Example tests)
in which D is as small as possible and
 N_1/D == numer_1/denom_1 ... N_n/D == numer_n,/denom_n.

##### Example:
convertFracs [(1, 2), (1, 3), (1, 4)] should be [(6, 12), (4, 12), (3, 12)]

**Note for Bash**  
input is a string, e.g "2,4,2,6,2,8"
output is then "6 12 4 12 3 12"

##### My solution  
    from functools import reduce
    from math import gcd

    def get_lcm(lst):
        return reduce(lambda a,b: a * b // gcd(a, b),lst)

    def convertFracts(lst):
        my_gcd = reduce(gcd,[i[0]+i[1] for i in lst])
        my_lcm = get_lcm([i[1]//my_gcd for i in lst])
        return [[i[0]*my_lcm//i[1],my_lcm] for i in lst]

    a = [[2,4], [2, 6], [2, 8]]
    print(convertFracts(a))

    # 根据题目描述 当输入为”2,4,2,6,2,8”时，输出依然为"6 12 4 12 3 12”，测试符合要求。 

##### Given solutions:
    from fractions import gcd

    def get_lcm(lst):
      return reduce(lambda x, y : x*y/gcd(x,y), lst)

    def convertFracts(lst):
      lcm = get_lcm([ y for x, y in lst])
         return [ [x*lcm/y, lcm] for x, y in lst]

##### Points:
1 求最大公约数的方法：辗转相除法，也叫欧几里得算法。  
   
2 reduce函数：对参数序列中元素进行累积。reduce(function, iterable[, initializer])    
  
3 根据题目描述 当输入为”2,4,2,6,2,8”时，输出依然为"6 12 4 12 3 12”，测试符合要求。    
  
4 gcd函数原来是从fractions模块导入，现在变为从math模块导入。  
