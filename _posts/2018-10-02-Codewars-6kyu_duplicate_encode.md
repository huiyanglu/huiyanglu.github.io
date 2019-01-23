---
layout:     post
title:      Duplicate Encoder
subtitle:   20181002_Codewars_duplicate_encode
date:       2018-10-02
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Duplicate Encoder
#### Codewars Kata 24√
##### Description
Link: https://www.codewars.com/kata/54b42f9314d9229fd6000d9c  
  
-简述：本题给定一个字符串，若字符串中的字符只出现过一次，则用'('代替，若出现过不止一次，则用')'代替。  
-思路：计数，判断是否出现过超过一次，分情况替代。  
-难点：如何更简便地写代码  
  
The goal of this exercise is to convert a string to a new string where each character in the new string is '(' if that character appears only once in the original string, or ')' if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.

Examples:

"din" => "((("

"recede" => "()()()"

"Success" => ")())())"

"(( @" => "))(("


Notes:

Assertion messages may be unclear about what they display in some languages. If you read "...It Should encode XXX", the "XXX" is actually the expected result, not the input! (these languages are locked so that's not possible to correct it).

##### My solution
    from collections import Counter
    import re

    def duplicate_encode(n):
        nn = n.lower()
        dct = dict(Counter(nn))
        del_1 = dict((key,value)for key,value in dct.items()if value!=1)
        b = [i for i in del_1.keys()]
        nn.split(',')
        a = []
        for i in range(0, len(nn)):
            if nn[i] in b:
                num = re.sub(r'\D', ")", nn[i])
            else:
                num = re.sub(r'[0-9a-zA-Z\s\_\@\(\)\*\:\!\'\"]', "(", nn[i])
            a.append(num)
            i += 1
        return ''.join(a)

##### Given solutions
    def duplicate_encode(word):
        return "".join(["(" if word.lower().count(c) == 1 else ")" for c in word.lower()])

---
    from collections import Counter

    def duplicate_encode(word):
        word = word.lower()
        counter = Counter(word)
        return ''.join(('(' if counter[c] == 1 else ')') for c in word)

---
	# This solution is O(n) instead of O(n^2) like the methods that use .count()
	# because .count() is O(n) and it's being used within an O(n) method.
	# The space complexiety is increased with this method.
    import collections
    def duplicate_encode(word):
        new_string = ''
        word = word.lower()
        # more info on defaultdict and when to use it here:
        # http://stackoverflow.com/questions/991350/counting-repeated-characters-in-a-string-in-python
        d = collections.defaultdict(int)
        for c in word:
            d[c] += 1
        for c in word:
            new_string = new_string + ('(' if d[c] == 1 else ')')
        return new_string

##### Points
1 ''.join(('(' if counter[c] == 1 else ')') for c in word) 非常简便的方法
  
2 最后一个答案的时间复杂度为O(n)，前面几个答案的时间复杂度为O(n^2)，因为.count()的复杂度为O(n)，for的复杂度也为O(n)；若不使用count()，用字典和for循环，复杂度更低。