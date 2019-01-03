---
layout:     post
title:      Prime number decompositions
subtitle:   20181107_Codewars_5kyu_getAllPrimeFactors3
date:       2018-11-07
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Prime number decompositions
#### Codewars Kata 47√
##### Description
https://www.codewars.com/kata/53c93982689f84e321000d62/solutions/python

-简述：本题给定一个数字，要求设计三个函数，分别求该数字的全部质因数、质因数以及其幂数、各质因数的乘积数组。  
-思路：求出所有质因数，再按照要求的输出格式进行输出  
-难点：1 避免time out的情况 2 避免步骤重复繁琐  

You have to code a function getAllPrimeFactors which take an integer as parameter and return an array containing its prime decomposition by ascending factors, if a factors appears multiple time in the decomposition it should appear as many time in the array.

Exemple: getAllPrimeFactors(100) returns [2,2,5,5] in this order.

This decomposition may not be the most practical.

You should also write getUniquePrimeFactorsWithCount, a function which will return an array containing two arrays: one with prime numbers appearing in the decomposition and the other containing their respective power.

Exemple: getUniquePrimeFactorsWithCount(100) returns [[2,5],[2,2]]

You should also write getUniquePrimeFactorsWithProducts an array containing the prime factors to their respective powers.

Exemple: getUniquePrimeFactorsWithProducts(100) returns [4,25]

Errors, if:

n is not a number
n not an integer
n is negative or 0
The three functions should respectively return [], [[],[]] and [].

Edge cases:

if n=0, the function should respectively return [], [[],[]] and [].  
if n=1, the function should respectively return [1], [[1],[1]], [1].  
if n=2, the function should respectively return [2], [[2],[1]], [2].  
The result for n=2 is normal. The result for n=1 is arbitrary and has been chosen to return a usefull result. The result for n=0 is also arbitrary but can not be chosen to be both usefull and intuitive. ([[0],[0]] would be meaningfull but wont work for general use of decomposition, [[0],[1]] would work but is not intuitive.)

##### My solution
    import collections

    def getAllPrimeFactors(n):
        dec = []
        i = 2
        if str(n).isdigit():
            if n == 1:
                return [1]
            else:
                while n > 1:
                    while n % i == 0:
                        n /= i
                        dec.append(i)
                    i += 1
                return dec
        else:
            return []

    def getUniquePrimeFactorsWithCount(n):
        c = collections.Counter(getAllPrimeFactors(n))
        lst1 = []
        lst2 = []
        for key,value in c.items():
            lst1.append(key)
            lst2.append(value)
        return [lst1,lst2]

    def getUniquePrimeFactorsWithProducts(n):
        c = getUniquePrimeFactorsWithCount(n)
        return [c[0][i]**c[1][i] for i in range(0,len(c[0]))]

    print(getUniquePrimeFactorsWithProducts(100))
  
##### Given solutions
    import math
    import collections

    def getAllPrimeFactors(n):
      numberToDecompose = n
      if (not isinstance(numberToDecompose,(int,long)) or numberToDecompose<=0):    return []
      answer = ([1] if (numberToDecompose==1) else  [])
      for possibleFactor in range (2,numberToDecompose+1):
          while (numberToDecompose % possibleFactor == 0):
             answer.extend([possibleFactor])
             numberToDecompose = numberToDecompose / possibleFactor
      answer = sorted(answer)
      return answer

    def getUniquePrimeFactorsWithProducts(n):
      ch= getUniquePrimeFactorsWithCount(n)
      x= [a**b for (a,b) in zip (ch[0], ch[1])]
      return x
      
    def getUniquePrimeFactorsWithCount(n):
        c = collections.Counter (getAllPrimeFactors(n))
        d=  [a for  (a,_) in c.items()]
        e = [b for  (_,b) in c.items()]
        return [d,e]

##### Points
1 collections.Counter 计数 生成字典形式  
或者Counter()直接计数  
  
2 报错TypeError: 'builtin_function_or_method' object is not subscriptable  
错误原因：括号用错了 append后面应该是()  
---