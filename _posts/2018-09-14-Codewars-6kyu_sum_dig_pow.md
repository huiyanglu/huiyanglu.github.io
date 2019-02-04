---
layout:     post
title:      Take a Number And Sum Its Digits Raised To The Consecutive Powers And ....¡Eureka!!
subtitle:   20180914_Codewars_sum_dig_pow
date:       2018-09-14
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Take a Number And Sum Its Digits Raised To The Consecutive Powers And ....¡Eureka!!
#### Codewars Kata 6√
##### Description
Link: [sum_dig_pow](https://www.codewars.com/kata/5626b561280a42ecc50000d1)  
  
-简述：本题假设一种数字特性，如89 = 8^1 + 9^2，135 = 1^1 + 3^2 + 5^3，给定一个数字范围，求出该范围内所有符合该特性的数字。   
-思路：遍历该范围内所有数字，判断是否符合要求，若符合则输出。  
-难点：无   
  
The number 89 is the first integer with more than one digit that fulfills the property partially introduced in the title of this kata. What's the use of saying "Eureka"? Because this sum gives the same number.

In effect: 89 = 8^1 + 9^2

The next number in having this property is 135.

See this property again: 135 = 1^1 + 3^2 + 5^3

We need a function to collect these numbers, that may receive two integers a, b that defines the range \[a, b] (inclusive) and outputs a list of the sorted numbers in the range that fulfills the property described above.

Let's see some cases:
sum_dig_pow(1, 10) == [1, 2, 3, 4, 5, 6, 7, 8, 9]
sum_dig_pow(1, 100) == [1, 2, 3, 4, 5, 6, 7, 8, 9, 89]
If there are no numbers of this kind in the range [a, b] the function should output an empty list.

sum_dig_pow(90, 100) == [] 

##### My solution:
    def ans(num):
        return sum([int(j)**(int(i)+1) for i,j in enumerate(str(num))])

    def sum_dig_pow(a,b):
        return [ans(each) for each in range(a,b+1) if ans(each)==each]

    print(sum_dig_pow(80,100))        

##### Given solution:
    def filter_func(a):
        return sum(int(d) ** (i+1) for i, d in enumerate(str(a))) == a

    def sum_dig_pow(a, b):
        return filter(filter_func, range(a, b+1))

##### Points
1  filter() 函数用于过滤序列，过滤掉不符合条件的元素，返回一个迭代器对象，如果要转换为列表，可以使用 list() 来转换。  
---
该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判，然后返回 True 或 False，最后将返回 True 的元素放到新列表中。
  
语法 filter(function, iterable)
  
参数  
function -- 判断函数。  
iterable -- 可迭代对象。  