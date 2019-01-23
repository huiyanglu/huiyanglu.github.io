---
layout:     post
title:      Consecutive k-Primes
subtitle:   20181005_Codewars_consec_kprimes
date:       2018-10-05
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Consecutive k-Primes
#### Codewars Kata 27√
##### Description
Link: https://www.codewars.com/kata/573182c405d14db0da00064e  
  
-简述：一个拥有k个质因数的自然数被称作k-prime，本题给定k值和一列数，求出该列数字中有多少相邻两个数都为k-prime的组合  
-思路：通过函数求出每个数字的质因数个数，算出符合条件的数字个数  
-难点：1 减少遍历次数  
  
A natural number is called k-prime if it has exactly k prime factors, counted with multiplicity. A natural number is thus prime if and only if it is 1-prime.

Examples:
k = 2 -> 4, 6, 9, 10, 14, 15, 21, 22, …
k = 3 -> 8, 12, 18, 20, 27, 28, 30, …
k = 5 -> 32, 48, 72, 80, 108, 112, …
	# Task: Given an integer k and a list arr of positive integers the function consec_kprimes (or its variants in other languages) returns how many times in the sequence arr numbers come up twice in a row with exactly k prime factors?

Examples:

arr = [10005, 10030, 10026, 10008, 10016, 10028, 10004]
consec_kprimes(4, arr) => 3 because 10005 and 10030 are consecutive 4-primes, 10030 and 10026 too as well as 10028 and 10004 but 10008 and 10016 are 6-primes.

consec_kprimes(4, [10175, 10185, 10180, 10197]) => 3 because 10175-10185 and 10185- 10180 and 10180-10197 are all consecutive 4-primes.

##### My solution
    def factoring(n):
        primefac = []
        d = 2
        while d <= n**0.5:
            while (n % d) == 0:
                primefac.append(d)
                n //= d
            d += 1
        if n > 1:
            primefac.append(n)
        return len(primefac)

    def consec_kprimes(k, arr):
        count = 0
        for i in range(0, len(arr)-1):
            b = factoring(arr[i])
            b2 = factoring(arr[i+1])
            if b == k and b2 == k:
                count+=1
        return count     

##### Given solutions
    def count_factors(n):
        t, d, q, m = 2, 5, 2 + n % 2, int(n ** .5)
        while q <= m and n % q:
            t, d, q = 6-t, d+t, d
        return q <= m and 1 + count_factors(n // q) or n > 1

    def consec_kprimes(k, arr):
        factors = list(map(count_factors, arr))
        return sum(left == k == right for left, right in zip(factors, factors[1:]))

##### Points
1 答案的list(map())和zip()函数用的太巧妙了 真是灵活运用  