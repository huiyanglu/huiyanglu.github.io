---
layout:     post
title:      Solve For X
subtitle:   20181021_Codewars_5kyu_solve_for_x
date:       2018-10-21
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Solve For X
#### Codewars Kata 40√
##### Description
Link:  
https://www.codewars.com/kata/59c2e2a36bddd2707e000079/solutions/python
  
-简述：本题给定一个方程式形式的字符串，求方程的解。  
-思路：运用eval()函数，直接求解字符串形式的方程。  
-难点：1 没有难点~  
  
You will be given an equation as a string and you will need to solve for X(https://www.mathplacementreview.com/algebra/basic-algebra.php#solve-for-a-variable)
  
and return x's value. For example:  
  
solve_for_x('x - 5 = 20') # should return 25  
solve_for_x('20 = 5 * x - 5') # should return 5  
solve_for_x('5 * x = x + 8') # should return 2  
solve_for_x('(5 - 3) * x = x + 2') # should return 2  
  
NOTES:
-All numbers will be whole numbers  
-Don't forget about the order of operations.https://www.mathplacementreview.com/algebra/basic-algebra.php#order-of-operations   
-If the random tests don't pass the first time, just run them again.  
  
##### My solution
    def solve_for_x(equation):
        for x in range(-1000,1001):
            if eval(equation.replace('=','==')):
                return x

    print(solve_for_x('2*x+1=5'))

##### Given solutions
    from itertools import count

    def solve_for_x(equation):
        return next( x for n in count(0) for x in [n, -n] if eval(equation.replace("x", str(x)).replace("=", "==")) )
  
---  
    def solve_for_x(equation):
      left_side = equation.split('=')[0];
      right_side = equation.split('=')[1];

      for x in range(-1000, 1000):
        if eval(left_side) == eval(right_side):
          return x

##### Points
1 函数next()，它通过调用其next ()方法从迭代器中检索下一个项目。  
  
2 count(0) 是所有整数的序列。  