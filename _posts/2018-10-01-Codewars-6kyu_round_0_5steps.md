---
layout:     post
title:      Round by 0.5 steps
subtitle:   20181001_Codewars_round_0.5steps
date:       2018-10-01
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Round by 0.5 steps
#### Codewars Kata 23√
##### Description
Link: https://www.codewars.com/kata/51f1342c76b586046800002a  
  
-简述：本题要求设计一个函数使得小数以0.5为步长进行四舍五入。  
-思路：具体分类讨论小数的范围和对应的四舍五入的值(笨方法)。将该数字翻倍，按照原本的四舍五入规则进行处理，然后再除以2（聪明方法）  
-难点：无  
  
Round any given number to the closest 0.5 step

I.E.

solution(4.2) = 4
solution(4.3) = 4.5
solution(4.6) = 4.5
solution(4.8) = 5
Round up if number is as close to previous and next 0.5 steps.

solution(4.75) == 5

##### My solution
    def solution(a):
        b = int(a)
        c = a - b
        if c<0.25:
            return b
        elif c>0.25 and c<0.75:
            return b+0.5
        elif c > 0.75:
            return b+1
        else:
            return a+0.25

##### Given solutions
    def solution(n):
        return round(2 * n) / 2

##### Points  
1 round() 方法返回浮点数x的四舍五入值。  
x -- 数字表达式。  
n -- 表示从小数点位数，其中 x 需要四舍五入，默认值为 0。  