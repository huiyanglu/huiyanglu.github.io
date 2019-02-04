---
layout:     post
title:      Rot13
subtitle:   20180918_Codewars_rot13
date:       2018-09-18
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Rot13
#### Codewars Kata 10√
##### Description
Link: [rot13](https://www.codewars.com/kata/530e15517bc88ac656000716)  
  
-简述：本题给定一个单词，要求将每个字母在字母表中向前或向后移动13位，返回移动后的单词。  
-思路：正则筛选替换  
-难点：无  
  
ROT13 is a simple letter substitution cipher that replaces a letter with the letter 13 letters after it in the alphabet. ROT13 is an example of the Caesar cipher.

Create a function that takes a string and returns the string ciphered with Rot13. If there are numbers or special characters included in the string, they should be returned as they are. Only letters from the latin/english alphabet should be shifted, like in the original Rot13 "implementation".

Please note that using "encode" in Python is considered cheating.

> ROT-13 编码是一种每一个字母被另一个字母代替的方法。这个代替字母是由原来的字母向前移动 13 个字母而得到的。数字和非字母字符保持不变。

##### My solution:
    # -*- coding:utf-8 -*-
    import re
    import string

    regex = re.compile('[a-z]{1}', re.IGNORECASE)

    def replace(match):
        upletters = string.ascii_uppercase  # 大写
        lowletters = string.ascii_lowercase  # 小写

        word = match.group(0)
        if word in lowletters:
            return lowletters[lowletters.index(word[0])+13 if lowletters.index(word[0])<13 else lowletters.index(word[0])-13]
        else:
            return upletters[
                upletters.index(word[0]) + 13 if upletters.index(word[0]) < 13 else upletters.index(word[0]) - 13]

    def rot13(s):
        return regex.sub(replace, s)

##### Given solutions:  
    import string
    from codecs import encode as _dont_use_this_
    from string import maketrans, lowercase, uppercase

    def rot13(message):
        lower = maketrans(lowercase, lowercase[13:] + lowercase[:13])
        upper = maketrans(uppercase, uppercase[13:] + uppercase[:13])
        return message.translate(lower).translate(upper)
---
    import string

    def rot13(message):
        return ''.join(chr((65 if c.isupper() else 97) + ((ord(c) - (65 if c.isupper() else 97)) + 13)%26) if c.isalpha() else c for c in message)
  
##### Points
1 **↑↑↑注意maketrans的用法**  
> maketrans()方法语法：  
> str.maketrans(intab, outtab)  
> 参数:  
> intab -- 字符串中要替代的字符组成的字符串。  
> outtab -- 相应的映射字符的字符串。  

    import string

    def rot13(message):
        return ''.join(chr((65 if c.isupper() else 97) + ((ord(c) - (65 if c.isupper() else 97)) + 13)%26) if c.isalpha() else c for c in message)
  
2 报错  
[mistake](https://ws4.sinaimg.cn/large/006tNc79gy1fzush2xcqzj30f2046js1.jpg)  
原因：https://www.python.org/dev/peps/pep-0263/  
解决方法：首行加# -*- coding:utf-8 -*-  


