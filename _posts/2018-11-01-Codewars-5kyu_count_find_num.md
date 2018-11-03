---
layout:     post
title:      Generating Numbers From Prime Factors I
subtitle:   20181101_Codewars_5kyu_count_find_num
date:       2018-11-01
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Generating Numbers From Prime Factors I
#### Codewars Kata 43√
##### Description

Given a list of prime factors, primesL, and an integer, limit, try to generate in order, all the numbers less than the value of limit, that have all and only the prime factors of primesL

Example
primesL = [2, 5, 7]
limit = 500  
  
List of Numbers Under 500          Prime Factorization  
___________________________________________________________
           70                         [2, 5, 7]  
          140                         [2, 2, 5, 7]  
          280                         [2, 2, 2, 5, 7]  
          350                         [2, 5, 5, 7]  
          490                         [2, 5, 7, 7]  
  
There are 5 of these numbers under 500 and the largest one is 490.

##### Task
For this kata you have to create the function count_find_num(), that accepts two arguments: primesL and limit, and returns the amount of numbers that fulfill the requirements, and the largest number under limit.
  
The example given above will be:  

    primesL = [2, 5, 7]
    limit = 500
    count_find_num(primesL, val) == [5, 490]
  
If no numbers can be generated under limit then return an empty list:  

    primesL = [2, 3, 47]
    limit = 200
    find_nums(primesL, limit) == []
  
The result should consider the limit as inclusive:  

    primesL = [2, 3, 47]
    limit = 282
    find_nums(primesL, limit) == [1, 282]
  
Features of the random tests:  
  
number of tests = 200
2 <= length_primesL <= 6 // length of the given prime factors array
5000 <= limit <= 1e17
2 <= prime <= 499  // for every prime in primesL


##### My solution  
    import itertools
    from functools import reduce

    def count_find_num(primesL,limit):
        prod_base = reduce(lambda x,y:x*y,primesL)
        rst = [1]+[i for i in primesL]
        count = 0
        for num in range(2,25):
            each_comb = [i for i in itertools.combinations_with_replacement(primesL, num)]
            for j in range(0,len(each_comb)):
                changetoint = [int(i) for i in each_comb[j]]
                prod_each_comb = reduce(lambda x,y:x*y,changetoint)
                rst.append(prod_each_comb)
        sorted_prod_lst = sorted(rst)
        for num2 in range(0,len(sorted_prod_lst)):
            final_rst = sorted_prod_lst[num2]*prod_base
            if final_rst<=limit:
                count+=1
            elif limit<prod_base:
                return []
            else:
                return [count,prod_base*(sorted_prod_lst[count-1])]

    print(count_find_num([2, 181, 277, 449],183207235273926))



##### Given solution
    def count_find_num(primes, limit):
        base = eval( '*'.join( map(str, primes) ) )
        
        if base > limit:
            return []
        
        results = [base]
        
        for p in primes:
            for num in results:
                num *= p
                while num not in results and num <= limit:
                    results += [num]
                    num *= p
        
        return [ len(results), max(results) ]
  
ps: 我的方法用时太长，虽然没有timed out，遍历的范围不能确定，solution的方法用了while就很巧妙了！是依次重复加一个数直到超出再换下一个，和我的思路不一样，这个方法更简便。  
  