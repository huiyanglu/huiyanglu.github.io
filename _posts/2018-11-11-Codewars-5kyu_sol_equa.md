---
layout:     post
title:      Diophantine Equation
subtitle:   20181111_Codewars_5kyu_sol_equa
date:       2018-11-11
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Diophantine Equation
#### Codewars Kata 49√
##### Description
https://www.codewars.com/kata/554f76dca89983cc400000bb
  
-简述：给定一个整数n，找到所有满足x^2-4y^2=n的整数x和y  
-思路：  
1 找取值范围的极值，当y=0时，x取最大值为根号n  
2 x^2 - 4 * y^2 = (x - 2y) * (x + 2y)  

https://en.wikipedia.org/wiki/Diophantine_equation
In mathematics, a Diophantine equation is a polynomial equation, usually with two or more unknowns, such that only the integer solutions are sought or studied.

In this kata we want to find all integers x, y (x >= 0, y >= 0) solutions of a diophantine equation of the form:

x2 - 4 * y2 = n
(where the unknowns are x and y, and n is a given positive number) in decreasing order of the positive xi.

If there is no solution return [] or "[]" or "". (See "RUN SAMPLE TESTS" for examples of returns).

Examples:
solEquaStr(90005) --> "[[45003, 22501], [9003, 4499], [981, 467], [309, 37]]"
solEquaStr(90002) --> "[]"
Hint:
x2 - 4 * y2 = (x - 2*y) * (x + 2*y)
"""

##### Given solution
    import math

    def sol_equa(n):
        rst = []
        for i in range(1,int(math.sqrt(n))+1):
            if n % i != 0:
                continue
            j = n//i
            x = (i+j)//2
            y = (j-i)//4
            if x>=0 and y>=0 and (i==x-2*y) and (j ==x+2*y):
                rst.append([x,y])
        return rst

    print(sol_equa(16))

##### Given solution
    def sol_equa(n):
        return [[(n/i + i)/2,(n/i - i)/4] for i in range(1, int(n ** 0.5) + 1)
        if n % i == 0 and (n/i + i) % 2 ==0 and (n/i - i) % 4 ==0]

##### Points  
1 找到遍历的最小范围，使运行时间尽可能短

