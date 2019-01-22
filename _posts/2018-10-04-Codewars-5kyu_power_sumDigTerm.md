---
layout:     post
title:      Numbers that are a power of their sum of digits
subtitle:   20181004_Codewars_power_sumDigTerm
date:       2018-10-04
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Numbers that are a power of their sum of digits
#### Codewars Kata 26√
##### Description
https://www.codewars.com/kata/55f4e56315a375c1ed000159  

-简述：8 + 1 = 9 and 9^2 = 81, 512 = 5 + 1 + 2 = 8 and 8^3 = 512 找出第n个有该特性的数字。  
-思路：给定底数和指数的范围，求出一系列符合该特性的数字，然后根据要求找到第n个。  
-难点：无  

The number 81 has a special property, a certain power of the sum of its digits is equal to 81 (nine squared). Eighty one (81), is the first number in having this property (not considering numbers of one digit). The next one, is 512. Let's see both cases with the details

8 + 1 = 9 and 9^2 = 81

512 = 5 + 1 + 2 = 8 and 8^3 = 512

We need to make a function, power_sumDigTerm(), that receives a number n and may output the n-th term of this sequence of numbers. The cases we presented above means that

power_sumDigTerm(1) == 81

power_sumDigTerm(2) == 512


##### My solution
    def power_sumDigTerm(n):
        m = [0]
        for a in range(2,99):
            for b in range(2,42):
                cc = a**b
                i2 = str(cc)
                c = [int(i2[i]) for i in range(0, len(i2))]
                sum1 = sum(c)
                if a == sum1:
                    m.append(cc)
        return sorted(m)[n]
    print(power_sumDigTerm(6))

##### Given solutions
    series = [0]
    for a in range(2, 99):
        for b in range(2, 42):
            c = a**b
            if a == sum(map(int, str(c))):
                series.append(c)
    power_sumDigTerm = sorted(series)
    print(power_sumDigTerm[6])
  
##### Points  
1 sum(map(int, str(c)))用法很巧妙，比我的拆分数字方法方便多了。