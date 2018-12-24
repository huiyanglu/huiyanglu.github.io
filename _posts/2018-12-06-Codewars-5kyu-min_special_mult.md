---
layout:     post
title:      Find The Minimum Number Divisible by Integers of an Array II
subtitle:   20181206_5kyu_min_special_mult
date:       2018-12-06
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Find The Minimum Number Divisible by Integers of an Array II
#### Codewars Kata 55√
##### Description  
https://www.codewars.com/kata/56f1b3c94d0c330e4a000e95/solutions/python
  
-简述：本题给定一列数，设计一个函数求出该列数的最小公倍数。若该列表中存在数字以外的项，则输出所有invalid项。  
-思路：判断列表中每一项是不是数字，若不是则输出，若全为数字则求最小公倍数。  
-难点：1 考虑数字的特殊情况如'-012'等，这种也是数字。  

Given a certain array of integers, create a function that may give the minimum number that may be divisible for all the numbers of the array.
  
This will be a harder version of Find The Minimum Number Divisible by integers of an array I
  
This is an example that shows how many times, a brute force algorithm cannot give a fast solution. We need the help of maths, in this case of number theory.
  
We need to apply the prime factorization of a number:
  
Think in doing the prime factorization of the product of all the different values of the array and think how to obtain from it the minimum number that is divisible by all the values of the array.
  
See the same cases as the previous part:
  
min_special_mult([2, 3 ,4 ,5, 6, 7]) == 420
The array may have integers that occurs more than once:
  
min_special_mult([18, 22, 4, 3, 21, 6, 3]) == 2772  
The array should have all its elements integer values. If the function finds an invalid entry (or invalid entries) like strings of the alphabet or symbols will not do the calculation and will compute and register them, outputting a message in singular or plural, depending on the number of invalid entries.
  
min_special_mult([16, 15, 23, 'a', '&', '12']) == "There are 2 invalid entries: ['a', '&']"
  
min_special_mult([16, 15, 23, 'a', '&', '12', 'a']) == "There are 3 invalid entries: ['a', '&', 'a']"
  
min_special_mult([16, 15, 23, 'a', '12']) == "There is 1 invalid entry: a"  
If the string is a valid number, the function will convert it as an integer.
  
min_special_mult([16, 15, 23, '12']) == 5520

min_special_mult([16, 15, 23, '012']) == 5520  
All the None elements of the array will be ignored:  

min_special_mult([18, 22, 4, , None, 3, 21, 6, 3]) == 2772  
If the array has a negative number, the function will convert to a positive one.  
  
min_special_mult([18, 22, 4, , None, 3, -21, 6, 3]) == 2772  
  
min_special_mult([16, 15, 23, '-012']) == 5520  
The test for this part will be more challenging having arrays up to 5000 elements and up to 800 different values.  
  
A simple brute force algorithm will not be able to pass the tests. Enjoy it!  

##### My solution
    from functools import reduce

    def gcd(a, b):
        while b:
            a, b = b, a % b
        return a

    def lcm(a, b):
        return a * b // gcd(a, b)

    def min_special_mult(alist):
        invalid_lst = []
        for i in alist:
            str_i = i
            if str(i)[0]=='-':
                str_i = int(str(i)[1:])
            if isinstance(str_i,str) and not str(str_i).isdigit() and i!=None:
                invalid_lst.append(i)
        if invalid_lst==[]:
            lst2 = [abs(int(i)) for i in alist if i is not None]
            return reduce(lcm,lst2)
        elif len(invalid_lst)==1:
            return 'There is {} invalid entry: {}'.format(str(len(invalid_lst)),str(invalid_lst[0]))
        else:
            return 'There are {} invalid entries: {}'.format(str(len(invalid_lst)), str(invalid_lst))

    print(min_special_mult([16, 15, 23,None,'a','b', '-012']))

##### Given solutions
    def min_special_mult(a):
        gcd=lambda a,b:gcd(b,a%b) if b else a
        lcm=lambda a,b:a*b/gcd(a,b)
        try:
            return reduce(lcm,[abs(int(e)) for e in a if e],1)
        except:
            def isint(n):
                try:int(str(n),base=10)
                except ValueError:return False
                return True
            s=[e for e in a if e and not isint(e)]
            if len(s)>1:w,x,y,z='are',len(s),'ies',s
            else:w,x,y,z='is',1,'y',s[0]
            return "There {} {} invalid entr{}: {}".format(w,x,y,z)

---
    from fractions import gcd

    def lcm(x, y):
        return x // gcd(x, y) * y

    def min_special_mult(arr):
        xs = []
        invalid_entries = []
        for y in arr:
            if y is None:
                continue
            if isinstance(y, basestring):
                try:
                    y = int(y)
                except ValueError:
                    pass
            if not isinstance(y, (int, long)):
                invalid_entries.append(y)
                continue
            xs.append(abs(y))
        if invalid_entries:
            if len(invalid_entries) == 1:
                return 'There is 1 invalid entry: {}'.format(invalid_entries[0])
            else:
                return 'There are {} invalid entries: {}'.format(
                    len(invalid_entries), invalid_entries)
        return reduce(lcm, xs)

##### Points   
1 Python3中math里面有个模块gcd直接求最小公倍数
  
2 使用reduce函数时需要from functools import reduce  
reduce() 函数语法：  

    reduce(function, iterable[, initializer])

function -- 函数，有两个参数，可为lambda自定义的函数  
iterable -- 可迭代对象  
initializer -- 可选，初始参数  
  
3 None不算invalid情况，在全数字的情况中将None去掉再求  
