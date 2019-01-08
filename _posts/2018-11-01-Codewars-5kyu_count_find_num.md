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
https://www.codewars.com/kata/58f9f9f58b33d1b9cf00019d

-简述：本题给定一个质数因子列表和一个整数作为限定范围，求出所有小于该整数且质因数仅为列表中数字的数，输出数字的个数和最大的一个。  
-思路：将质因数列表相乘，不断叠加直到乘积大于限定数停止。  
-难点：1 如何缩短运行时间，减少遍历次数。  
  
Given a list of prime factors, primesL, and an integer, limit, try to generate in order, all the numbers less than the value of limit, that have all and only the prime factors of primesL.  
  
##### Examples
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
  
#####Improved solution:
**（数字大时的运行时间依然不如given solution）**
    from functools import reduce

    def count_find_num(primesL,limit):
        base = reduce(lambda x, y: x * y, primesL)
        rst1 = [base]
        if base>limit:
            return []
        for each in primesL:
            for num in rst1:
                num = num * each
                if num > limit:# 如果排列后的rst1的num已经大于limit了，就不继续往下遍历直接退出循环进入下一项了
                    break
                else:
                    while num not in rst1 and num<=limit:
                        rst1 = sorted(rst1+[num])#加入列表的数字是未排序的，及时排序可以减少遍历次数
                        num*=each
        return [len(rst1),max(rst1)]
  
##### Points:  
1 列表中所有数字相乘：  

    reduce(lambda x, y: x * y, primesL)
  
2 加入列表的数字是未排序的，及时排序可以减少遍历次数。如果排列后的rst1的num已经大于limit了，就不继续往下遍历直接退出循环进入下一项了
  
3 经过对程序运行时间的多次测试，尽管加入判断条件能够减少遍历次数，但由于用到了sorted排序，从另一方面增加了运行时间，因此当数字很大遍历次数很多时，其实每次都要排序是对时间的浪费，因此不可取。
  
4 运行时间检测方法
    import time
    start_CPU2 = time.clock()
    ...
    end_CPU2 = time.clock()
    print("Given solution: %f CPU seconds" % (end_CPU2 - start_CPU2))
  
5 eval() 函数用来执行一个字符串表达式，并返回表达式的值。  
通过比较eval()和lambda函数的运行时间，可以发现使用eval的程序运行时间更短。
  
ps: 我的方法用时太长，虽然没有timed out，遍历的范围不能确定，solution的方法用了while就很巧妙了！是依次重复加一个数直到超出再换下一个，和我的思路不一样，这个方法更简便。  
  