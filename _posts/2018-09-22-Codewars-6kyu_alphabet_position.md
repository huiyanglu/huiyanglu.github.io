---
layout:     post
title:      Replace With Alphabet Position
subtitle:   20180922_Codewars_alphabet_position
date:       2018-09-22
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Replace With Alphabet Position
#### Codewars Kata 14√
##### Description
Link: [alphabet_position](https://www.codewars.com/kata/546f922b54af40e1e90001da) 
  
-简述：本题给定一个英文句子的字符串，要求把字母转换成数字，a对应1，b对应2，以此类推。  
-思路：遍历每个字母转换为数字。  
-难点：无  
  
In this kata you are required to, given a string, replace every letter with its position in the alphabet.

If anything in the text isn't a letter, ignore it and don't return it.
a being 1, b being 2, etc.

As an example:
	alphabet_position("The sunset sets at twelve o' clock.")    
    
Should return "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11" as a string.
  
##### My solution  
    def alphabet_position(text):
        lst = []
        court = 0
        txt = text.lower()
        for i in range(0,len(text)):
            if txt[i].isalpha():
                b = ord(txt[i])-96
                lst.append(b)
                i+=1
            else:
                i+=1
        return ' '.join(str(x) for x in lst) 
      # 注意返回的形式（如何不以数组形式返回）
  
##### Given solutions  
    def alphabet_position(text):
        return ' '.join(str(ord(c) - 96) for c in text.lower() if c.isalpha())

##### Improved solutions:
    def alphabet_position(text):
        return ' '.join([str(ord(i)-96) for i in text.lower() if i.isalpha()])

##### Points
1 ord()函数以一个字符（长度为1的字符串）作为参数，返回对应的 ASCII 数值，或者 Unicode 数值。
  
2 given solution的表达式是我的答案的列表推导式，很方便，可以多用。
  