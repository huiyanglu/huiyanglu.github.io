---
layout:     post
title:      Integer triangles
subtitle:   20181008_Codewars_give_triang
date:       2018-10-08
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Integer triangles
#### Codewars Kata 30√
##### Description
Link: https://www.codewars.com/kata/55db7b239a11ac71d600009d  

-简述：本题设定一个三边长度均为整数且一个角为120度的三角形，给定三边之和的最大值，求出能够生成的所有三角形三边之长。  
-思路：已知有一个角为120度的三角形三边公式，求出各边的长度范围，遍历求解。  
-难点：1 如何准确定位各边长的长度范围，使得遍历范围最小。  
  
You have to give the number of different integer triangles with one angle of 120 degrees which perimeters are under or equal a certain value. Each side of an integer triangle is an integer value.

give_triang(max. perimeter) --------> number of integer triangles,
with sides a, b, and c integers such that:

a + b + c <= max. perimeter

See some of the following cases

give_triang(5) -----> 0 # No Integer triangles with perimeter under or equal five
give_triang(15) ----> 1 # One integer triangle of (120 degrees). It's (3, 5, 7)
give_triang(30) ----> 3 # Three triangles: (3, 5, 7), (6, 10, 14) and (7, 8, 13)
give_triang(50) ----> 5 # (3, 5, 7), (5, 16, 19), (6, 10, 14), (7, 8, 13) and (9, 15, 21) are the triangles with perim under or equal 50.

##### My solution
    def give_triang(per):
        r1 = []
        for b in range(3,per-2):
            if (2 * b > per):
                break
            for c in range(b,per-2):
                if (b + 2 * c > per):
                    break
                a = (b * b + b * c + c * c) ** 0.5
                if a+b+c<=per and a == int(a):
                    result = [b,c,a]
                    r1.append(result)
                    c+=1
            b+=1
        return len(r1)

##### Given solutions  
    from itertools import combinations
    import math

    def give_triang(per):
        x = 0
        for c in list(combinations(range(1,per//3*2),2)):
            sq = math.sqrt(c[0]**2+c[1]**2+c[0]*c[1])
            if sq.is_integer() and (sq+sum(c)) <= per:
                x += 1
        return x
  
---  
    from math import sqrt
    def give_triang(per):
        # your code here
        cnt=0
        for a in range(1,int(per/3)+1): 
            for b in range(a+1,int(per/2)+1):
                c=sqrt(a**2+b**2+a*b)
                if (c==int(c))&(a+b+c<=per): cnt+=1
        return cnt # number of integer triangles with one angle of 120 degrees
  
---  
    from fractions import gcd
    give_triang=lambda p:sum(p // (n*n + 2*m*m + 3*m*n)
        for m in range(int(p ** .5) + 1)
            for n in range(1, m)
                if (m - n) % 3 and gcd(m, n) == 1)

##### Points
1 a^2=b^2+c^2+bc，其中a所对角为120度。  
  
2 combinations(range(1,per//3*2),2) 生成2个数 不相等 相加之和的范围为1至per//3*2  
  
3 120度的两条斜边一定不会相等，因为若为等腰三角形，则底边的值=斜边*根号3，必定不是整数。  