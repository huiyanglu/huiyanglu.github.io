---
layout:     post
title:      Mystery Function
subtitle:   20181112_Codewars_4kyu_mystery
date:       2018-11-12
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Mystery Function
#### Codewars Kata 50√
##### Description
https://www.codewars.com/kata/56b2abae51646a143400001d/solutions/python

The mystery function is defined over the non-negative integers. The more common name of this function is concealed in order to not tempt you to search the Web for help in solving this kata, which most definitely would be a very dishonorable thing to do.

Assume num has n bits. Then mystery(num) is the number whose binary representation is the num'th entry in the table T(n), where T(n) is defined recursively as follows:

T(1) = ['0', '1']
T(n + 1) is obtained by taking two copies of T(n), reversing the second copy, prepending each entry of the first copy with '0' and each entry of the reversed copy with '1', and then concatenating the two. For example:

T(2) = ['00', '01', '11', '10']
and

T(3) = ['000', '001', '011', '010', '110', '111', '101', '100']
mystery(6) is the 6'th entry in T(3)(with indexing starting at 0), i.e., '101' interpreted as a binary number. So, mystery(6) returns 5.

Your mission is to implement the functionmystery, where the argument may have up to 63 bits. Note that T(63) is far too large to compute and store, so you'll have to find an alternative way of implementing mystery. You are also asked to implement mystery_inv (JS mysteryInv), the inverse of mystery. Finally, you are asked to implement a function name_of_mystery (JS nameOfMystery), which shall return the name that mystery is more commonly known as. After passing all tests you are free to learn more about this function on Wikipedia or other place.

Hint: If you don't know the name of mystery, remember there is information in passing as well as failing a test.

##### My wrong answer
    def mystery(num):
        n = len(bin(num))-2
        a1 = [0,1]
        for i in range(1,n):
            ar = list(reversed(a1))
            a21 = ['0'+str(j) for j in a1]
            a22 = ['1'+str(j) for j in ar]
            a1 = a21+a22
            if len(a1)==2**n:
                return int(a1[num],2)
            else:
                i+=1

    def mystery_inv(num):
        n = len(bin(num))-2
        a1 = [0, 1]
        for i in range(1,n):
            ar = list(reversed(a1))
            a21 = ['0'+str(j) for j in a1]
            a22 = ['1'+str(j) for j in ar]
            a1 = a21+a22
            if len(a1)==2**n:
                return a1.index(bin(num)[2:])
            else:
                i+=1
ps:错误原因 超时了。。是笨方法- -

##### Given solution
    def mystery(n):
        rst = n ^ (n >> 1)
        return rst

    def mystery_inv(n):
        mask = n >> 1
        while mask != 0:
            n = n ^ mask
            mask = mask >> 1
        return n

    def name_of_mystery():
        return "Gray code"

    print(mystery_inv(5))

Tips:
'>>1' 右移一个单位
'^' 表示异或