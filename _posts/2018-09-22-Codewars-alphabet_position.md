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
