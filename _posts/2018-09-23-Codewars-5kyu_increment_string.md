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
Link: [increment_string](https://www.codewars.com/kata/54a91a4883a7de5d7800009c)    
  
-简述：本题给定一个字符串，若以数字结尾，则将该数字加1，若不以数字结尾，则在字符串最后加上'1'。  
-思路：我的方法是提取数字之后再提取最后一个数字单独加1求解，given solution的解法是数字整体加1，运用zfill()函数使字符串长度固定，避免str转int的过程中数字前面的0丢失。  
-难点：无  
  
Your job is to write a function which increments a string, to create a new string. If the string already ends with a number, the number should be incremented by 1. If the string does not end with a number the number 1 should be appended to the new string.

##### Examples
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
            s = s.split(lst)[0] # 从右向左找最后一个数，取除最后一个数以外的前面部分
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

##### Points
1 rstrip()方法语法：str.rstrip([chars])  
参数 chars -- 指定删除的字符（默认为空格）  
返回值 返回删除 string 字符串末尾的指定字符后生成的新字符串。  
   
2 zfill()方法语法：str.zfill(width)  
参数 width -- 指定字符串的长度。原字符串右对齐，前面填充0。  
返回值 返回指定长度的字符串。  