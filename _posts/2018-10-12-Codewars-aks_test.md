---
layout:     post
title:      Simple AKS Primality Test
subtitle:   20181012_Codewars_aks_test
date:       2018-10-12
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Simple AKS Primality Test
#### Codewars Kata 33√
##### Description  
 https://www.codewars.com/kata/5416d02d932c1df3a3000492/solutions/python  

-简述：本题给定一个整数p，判断(x − 1)^p − (x^p − 1)的分解式是否能被p整除。   
-思路：判断多项式的结果能否被p整除，取x的值为某个范围内。  
-难点：1 time out  
  
The AKS algorithm for testing whether a number is prime is a polynomial-time test based on the following theorem:

A number p is prime if and only if all the coefficients of the polynomial expansion of (x − 1)^p − (x^p − 1) are divisible by p.

For example, trying p = 3:

 (x − 1)^3 − (x^3 − 1) = (x^3 − 3x^2 + 3x − 1) − (x^3 − 1) = − 3x^2 + 3x 
And all the coefficients are divisible by 3, so 3 is prime.

Your task is to code the test function, wich will be given an integer and should return true or false based on the above theorem. You should efficiently calculate every coefficient one by one and stop when a coefficient is not divisible by p to avoid pointless calculations. The easiest way to calculate coefficients is to take advantage of binomial coefficients: http://en.wikipedia.org/wiki/Binomial_coefficient and pascal triangle: http://en.wikipedia.org/wiki/Pascal%27s_triangle .

You should also take advantage of the symmetry of binomial coefficients. You can look at these kata: http://www.codewars.com/kata/pascals-triangle and http://www.codewars.com/kata/pascals-triangle-number-2

The kata here only use the simple theorem. The general AKS test is way more complex. The simple approach is a good exercie but impractical. The general AKS test will be the subject of another kata as it is one of the best performing primality test algorithms.

The main problem of this algorithm is the big numbers emerging from binomial coefficients in the polynomial expansion. As usual Javascript reach its limit on big integer very fast. (This simple algorithm is far less performing than a trivial algorithm here). You can compare the results with those of this kata: http://www.codewars.com/kata/lucas-lehmer-test-for-mersenne-primes Here, javascript can barely treat numbers bigger than 50, python can treat M13 but not M17.

##### My solution  
    def aks_test(p):
        for x in range(0,10):
            m = (x-1)**p-(x**p-1)
            if m%p:
                return False
        return p>1  
  
##### Given solutions  
    def aks_test(p):
        coeff = 1
        for i in xrange(p // 2):
            coeff = coeff * (p - i) / (i + 1)
            if coeff % p:
                return False
        return p > 1
  
---  
    import math

    def aks_test(p):
        if p == 1:
            return False
        for comb in combinations(p):
            if comb % p != 0:
                return False            
        return True

      # generator returns list of coefficients in first-half of polynomial expansion
      # (second-half of expansion will be duplicates)
    def combinations(n):
        i = 0
        c = 1
        for i in range(n / 2):
            c *= (n - i)
            c /= i + 1
            yield c  

##### Points:
1 整除是'//'
  
2 可以直接返回return p>1进行判断，很巧妙
  
3 用系数的方法会减少遍历次数
  