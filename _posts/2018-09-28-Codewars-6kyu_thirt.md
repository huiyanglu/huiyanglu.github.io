---
layout:     post
title:      A Rule of Divisibility by 13
subtitle:   20180928_Codewars_thirt
date:       2018-09-28
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# A Rule of Divisibility by 13
#### Codewars Kata 20√
##### Description
Link: [thirt](https://www.codewars.com/kata/564057bc348c7200bd0000ff)   
  
-简述：本题给定10的次方数被13整除的余数列表1, 10, 9, 12, 3, 4，是一个循环数列，求任意多位数被13整除的remainder。  
-思路：各位数字和余数列表分别相乘，若相加结果等于该数字，则为remainder，若不等则继续调用函数。  
-难点：1 如何使代码最简化  
  
When you divide the successive powers of 10 by 13 you get the following remainders of the integer divisions:

1, 10, 9, 12, 3, 4.

Then the whole pattern repeats.

Hence the following method: Multiply the right most digit of the number with the left most number in the sequence shown above, the second right most digit to the second left most digit of the number in the sequence. The cycle goes on and you sum all these products. Repeat this process until the sequence of sums is stationary.

...........................................................................

Example: What is the remainder when 1234567 is divided by 13?

7×1 + 6×10 + 5×9 + 4×12 + 3×3 + 2×4 + 1×1 = 178

We repeat the process with 178:

8x1 + 7x10 + 1x9 = 87

and again with 87:

7x1 + 8x10 = 87

...........................................................................

From now on the sequence is stationary and the remainder of 1234567 by 13 is the same as the remainder of 87 by 13: 9

Call thirt the function which processes this sequence of operations on an integer n (>=0). thirt will return the stationary number.

thirt(1234567) calculates 178, then 87, then 87 and returns 87.

thirt(321) calculates 48, 48 and returns 48


##### My solution
    import itertools as it

    def thirt(n):
        pattern = it.cycle([1, 10, 9, 12, 3, 4])
        l1 = [int(i) for i in str(n)]
        l1.reverse()
        prod_sum = sum([a * b for a, b in zip(l1, pattern)])
        if n == prod_sum:
            return prod_sum
        return thirt(prod_sum)

    print(thirt(1234567)) 

##### Given solutions
    array = [1, 10, 9, 12, 3, 4]

    def thirt(n):
        total = sum([int(c) * array[i % 6] for i, c in enumerate(reversed(str(n)))])
        if n == total:
            return total
        return thirt(total)
---
    import itertools as it

    def thirt(n):
        if n < 100: return n
        
        pattern = it.cycle([1, 10, 9, 12, 3, 4])
        
        return thirt(sum(d*n for d,n in zip(map(int, str(n)[::-1]), pattern)))

##### Points  
1 循环数列 pattern = it.cycle([1, 10, 9, 12, 3, 4])  
  
2 数列反向用str(n)[::-1] 更方便  