---
layout:     post
title:      Simple fraction to mixed number converter
subtitle:   20180927_Codewars_mixed_fraction
date:       2018-09-27
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Simple fraction to mixed number converter
#### Codewars Kata 19√
##### Description
Link: https://www.codewars.com/kata/556b85b433fb5e899200003f  
  
-简述：本题旨在设计一个函数，将假分数转换为带分数的形式。  
-思路：考虑多种正负数的情况，先求出带分数前面的数字。  
-难点：1 如何简化代码  
  
Task
Given a string representing a simple fraction x/y, your function must return a string representing the corresponding mixed fraction in the following format:

[sign]a b/c

where a is integer part and b/c is irreducible proper fraction. There must be exactly one space between a and b/c. Provide [sign] only if negative (and non zero) and only at the beginning of the number (both integer part and fractional part must be provided absolute).

If the x/y equals the integer part, return integer part only. If integer part is zero, return the irreducible proper fraction only. In both of these cases, the resulting string must not contain any spaces.

Division by zero should raise an error (preferably, the standard zero division error of your language).

Value ranges
-10 000 000 < x < 10 000 000
-10 000 000 < y < 10 000 000

Examples
Input: 42/9, expected result: 4 2/3.
Input: 6/3, expedted result: 2.
Input: 4/6, expected result: 2/3.
Input: 0/18891, expected result: 0.
Input: -10/7, expected result: -1 3/7.
Inputs 0/0 or 3/0 must raise a zero division error.

Note
Make sure not to modify the input of your function in-place, it is a bad practice.

##### My solution
    def gcd(a, b):
        while b:
            a, b = b, a % b
        return a

    def mixed_fraction(s):
        m = s.split('/')
        a = int(m[0])
        b = int(m[1])
        if (a >=0 and b>0) or (a<0 and b<0):
            c = a // b
        elif (a<0 and b>0) or (a>0 and b<0):
            c = a//b+1
        elif a==0:
            c = 0
        d = a - c * b
        e = gcd(d, b)
        r2 = abs(b // e)
        if d == 0:
            return '%d' %(c)
        elif d !=0 and c == 0:
            r1 = d // e
            if r2 == 1:
                return '%d' % (r1)
            else:
                return '%d/%d' % (r1, r2)
        else:
            r1 = abs(d // e)
            if r2 == 1:
                c = c-r1
                return '%d' % (c)
            else:
                return '%d %d/%d' % (c, r1, r2)

##### Given solutions
    from fractions import gcd

    def mixed_fraction(s):
        x, y = map(int, s.split('/'))
        signx = x/abs(x) if x else 1
        signy = y/abs(y) if y else 1
        sign = signx * signy
        x, y = map(abs, (x, y))
        a, b = divmod(x, y)
        g = gcd(b, y)
        b, c = b/g, y/g
        result = (str(a) * bool(a) +
                   ' ' * bool(a) * bool(b) +
                   (str(b) + '/' + str(c)) * bool(b))
        if not result:
            return '0'
        if sign < 0:
            result = '-' + result
        return result

---
    from fractions import Fraction

    def mixed_fraction(s):
        f = Fraction(*map(int, s.split('/')))
        if f.denominator == 1: return str(f.numerator)
        n = abs(f.numerator) / f.denominator * (1 if f.numerator > 0 else -1)
        f = abs(f - n) if n else f - n
        return "{} {}".format(n, f) if n else str(f)

##### Points
1 divmod(a,b)方法返回的是a//b（商）以及a%b(余数)，返回结果类型为tuple
  
2 bool() 函数用于将给定参数转换为布尔类型，如果没有参数，返回 False。
bool 是 int 的子类。
  
3 Fraction分数类，能够自动约分，Fraction.numerator和Fraction.denominator 分子和分母
  
4 from fractions import gcd在fractions库中，快速找到两个数的最大公约数
  