---
layout:     post
title:      Sum without highest and lowest number
subtitle:   20180913_Codewars_sum_array
date:       2018-09-13
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Sum without highest and lowest number
#### Codewars Kata 5√
##### Description  
Link: [sum_array](https://www.codewars.com/kata/576b93db1129fcf2200001e6)    
   
-简述：本题给定一列数字，要求去掉其最大值和最小值后求和。  
-思路：求最大最小值，去掉，求和。  
-难点：无  
   
Sum all the numbers of the array (in F# and Haskell you get a list) except the highest and the lowest element (the value, not the index!).
(The highest/lowest element is respectively only one element at each edge, even if there are more than one with the same value!)
   
##### Example:
{ 6, 2, 1, 8, 10 } => 16
{ 1, 1, 11, 2, 3 } => 6

##### Test:
Test.describe("Basic tests")
Test.it("None or Empty")
Test.assert_equals(sum_array(None), 0)
Test.assert_equals(sum_array([]), 0)

Test.it("Only one Element")
Test.assert_equals(sum_array([3]), 0)
Test.assert_equals(sum_array([-3]), 0)

Test.it("Only two Element")
Test.assert_equals(sum_array([ 3, 5]), 0)
Test.assert_equals(sum_array([-3, -5]), 0)

Test.it("Real Tests")
Test.assert_equals(sum_array([6, 2, 1, 8, 10]), 16)
Test.assert_equals(sum_array([6, 0, 1, 10, 10]), 17)
Test.assert_equals(sum_array([-6, -20, -1, -10, -12]), -28)
Test.assert_equals(sum_array([-6, 20, -1, 10, -12]), 3)

##### My solution:
def sum_array(arr):
    if arr==None or len(arr)<3:
        return 0
    else:
        arr.remove(min(arr))
        arr.remove(max(arr))
        return sum(arr)

##### Given solutions:
def sum_array(arr):
    if arr == None or len(arr) < 3: # 可以用or连接两个条件
        return 0
    return sum(arr) - max(arr) - min(arr)

def sum_array(arr):
    return sum(sorted(arr)[1:-1]) if arr and len(arr) > 1 else 0

##### Points
1 答案的方法更加巧妙  