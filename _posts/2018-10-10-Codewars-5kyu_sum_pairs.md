---
layout:     post
title:      Sum of Pairs
subtitle:   20181010_Codewars_sum_pairs
date:       2018-10-10
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Sum of Pairs
#### Codewars Kata 32√
##### Description
https://www.codewars.com/kata/54d81488b981293527000c8f  
  
-简述：本题给定一列数字和一个求和的值，返回数列中前两个相加的和为该数字的值。  
-思路：已知一个数，判断另一个数是否在数列中  
-难点：1 防止超时  
  
Given a list of integers and a single sum value, return the first two values (parse from the left please) in order of appearance that add up to form the sum.

sum_pairs([11, 3, 7, 5],   10)
== [3, 7]

sum_pairs([4, 3, 2, 3, 4],    6)
Entire pair is earlier, and therefore is the correct answer
== [4, 2]

sum_pairs([0, 0, -2, 3], 2)
There are no pairs of values that can be added to produce 2.
== None/nil/undefined (Based on the language)

sum_pairs([10, 5, 2, 3, 7, 5],   10)
Entire pair is earlier, and therefore is the correct answer
== [3, 7]
Negative numbers and duplicate numbers can and will appear.

NOTE: There will also be lists tested of lengths upwards of 10,000,000 elements. Be sure your code doesn't time out.

##### My solution (error)
	# 错误回答，超时了
	def sum_pairs(ints,s):
	    for i in range(0,len(ints)):
	        if s-ints[i] in ints[i+1:]:
	            return [ints[i],s-ints[i]]                                                                          

##### Given solution  
    def sum_pairs(ints, s):
        rst = set()
        for i in range(0,len(ints)):
            if s - ints[i] in rst:
                return [s - ints[i],ints[i]]
            rst.add(ints[i])
  
> set是一个无序且不重复的元素集合。
注意在创建空集合的时候只能使用s=set()，因为s={}创建的是空字典
  
##### Points
1 set()的时间复杂度是O(1)  
  
PS: 今天我的方法timed out了，看了答案才做出来。
