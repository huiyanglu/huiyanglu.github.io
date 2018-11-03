---
layout:     post
title:      String incrementer
subtitle:   20180923_Codewars_increment_string
date:       2018-09-23
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# String incrementer
#### Codewars Kata 15√
##### Description
Your job is to write a function which increments a string, to create a new string. If the string already ends with a number, the number should be incremented by 1. If the string does not end with a number the number 1 should be appended to the new string.

Examples:
foo -> foo1
foobar23 -> foobar24
foo0042 -> foo0043
foo9 -> foo10
foo099 -> foo100

Attention: If the number has leading zeros the amount of digits should be considered.

##### My solution  
    import re

    def increment_string(s):
        number = re.findall(r'\d+', s) # 找到所有数字
        if number:
            lst = number[-1]
            s = s.rsplit(lst, 1)[0] # 从右向左找最后一个数，取除最后一个数以外的前面部分
            number = str(int(lst) + 1) # 先把最后一个数转为数字，加1，再转为字符串（过程中lst的位数会变化）
            return s + '0' * (len(lst) - len(number)) + number # 转换中少掉的0要补上
        else:
            return s + '1'  
  
##### Given solutions
    def increment_string(strng):
        head = strng.rstrip('0123456789')
        tail = strng[len(head):]
        if tail == "": return strng+"1"
        return head + str(int(tail) + 1).zfill(len(tail))
  
---  
    import re

    def increment_string(input):
        match = re.search("(\d*)$", input)
        if match:
            number = match.group(0)
            if number is not "":
                return input[:-len(number)] + str(int(number) + 1).zfill(len(number))
        return input + "1"
