---
layout:     post
title:      Counting Duplicates
subtitle:   20180916_Codewars_duplicate_count
date:       2018-09-16
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Counting Duplicates
#### Codewars Kata 8√
##### Description  
Link: [duplicate_count](https://www.codewars.com/kata/54bf1c2cd5b56cc47f0007a1)  
  
-简述：本题给定一个字符串，求其中重复字符（次数大于1）的个数。  
-思路：直接counter求解，注意生成字典或列表的形式  
-难点：无  
  
Count the number of Duplicates
Write a function that will return the count of distinct case-insensitive alphabetic characters and numeric digits that occur more than once in the input string. The input string can be assumed to contain only alphabets (both uppercase and lowercase) and numeric digits.
  
##### Example
"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabBcde" -> 2 # 'a' occurs twice and 'b' twice (bandB)
"indivisibility" -> 1 # 'i' occurs six times
"Indivisibilities" -> 2 # 'i' occurs seven times and 's' occurs twice
"aA11" -> 2 # 'a' and '1'
"ABBA" -> 2 # 'A' and 'B' each occur twice

##### Test:
test.assert_equals(duplicate_count("abcde"), 0)
test.assert_equals(duplicate_count("abcdea"), 1)
test.assert_equals(duplicate_count("indivisibility"), 1)

##### My solution:
    from collections import Counter
    def duplicate_count(n):
        nn = n.lower()
        dct = dict(Counter(nn))
        del_1 = dict((key,value)for key,value in dct.items()if value!=1)
        return len(del_1)    

##### Given solutions:
    def duplicate_count(s):
      return len([c for c in set(s.lower()) if s.lower().count(c)>1])
---
    from collections import Counter
    def duplicate_count(text):
        return sum(1 for c, n in Counter(text.lower()).iteritems() if n > 1)

##### Points
1 Counter() （计数器）是对字典的补充，用于追踪值的出现次数。  
  
2 在Python 3.x 里面，iteritems()方法已经废除了。在3.x里用 items()替换iteritems() ，可以用于 for 来循环遍历。  
  