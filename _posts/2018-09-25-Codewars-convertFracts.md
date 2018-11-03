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

    def gcd(a, b):
        while b:
            a, b = b, a % b
        return a

    def lcm(a, b):
        return a * b // gcd(a, b)

    def convertFracts(lst):
        denoms = [i[1] for i in lst] # denominator分母
        nums = [i[0] for i in lst] # numerator分子
        lsttt = denoms + nums # [4, 6, 8, 2, 2, 2]
        _gcd = reduce(gcd,lsttt) # 2
        denoms2 = [i[1]//_gcd for i in lst] # 化简后的分母
        nums2 = [i[0]//_gcd for i in lst] # 化简后的分子
        _lcm = reduce(lcm,denoms2) # lcm是函数
        multi = [_lcm//i for i in denoms2]
        return [[i*m,_lcm] for i,m in zip(nums2,multi)]

    a = [[2,4], [2, 6], [2, 8]] 
    print(convertFracts(a))  
 
** 1、求最大公约数的方法：辗转相除法，也叫欧几里得算法 **  
  
** 2、reduce函数：对参数序列中元素进行累积。reduce(function, iterable[, initializer]) **  
  
** 3、根据题目描述 当输入为”2,4,2,6,2,8”时，输出依然为"6 12 4 12 3 12”，测试符合要求。  **
