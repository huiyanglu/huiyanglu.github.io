---
layout:     post
title:      Break the Caesar!
subtitle:   20181016_Codewars_break_caesar
date:       2018-10-16
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Break the Caesar!
#### Codewars Kata 36√
##### Description
https://www.codewars.com/kata/598e045b8c13926d8c0000e8  
  
-简述：本题旨在破解凯撒密码的加密方法，将各字母在字母表中同时移动一定数量的位置使其加密，求破解该密码的方法。  
-思路：分别测试将每个字母往回移动1-26次，句中单词的个数，求出最大个数。  
-难点：1 生成凯撒密码的方法。  
  
The Caesar cipher is a notorious (and notoriously simple) algorithm for encrypting a message: each letter is shifted a certain constant number of places in the alphabet. For example, applying a shift of 5 to the string "Hello, world!" yields "Mjqqt, btwqi!", which is jibberish.

In this kata, your task is to decrypt Caesar-encrypted messages using nothing but your wits, your computer, and a set of the 1000 (plus a few) most common words in English in lowercase (made available to you as a preloaded variable named WORDS, which you may use in your code as if you had defined it yourself).

Given a message, your function must return the most likely shift value as an integer.

A few hints:  
Be wary of punctuation
Shift values may not be higher than 25

##### My solution  
abc = 'abcdefghijklmnopqrstuvwxyz'

def caesar(s, k):
    trans = str.maketrans(abc, abc[k:] + abc[:k])
    return s.translate(trans)

def break_caesar(message):
    message = ''.join(c if c.isalpha() else ' ' for c in message).lower()
    hits = []
    for k in range(26):
        dec = caesar(message, -k)
        cnt = 0
        for word in dec.split():
            if word in WORDS:
                cnt += 1
        hits.append(cnt)

    return hits.index(max(hits))

	# 自己运行判断单词 可用enchant
	# import enchant
	# d = enchant.Dict("en_US")
	# d.check("Hello")
	# True/False

##### Given solution
abc = 'abcdefghijklmnopqrstuvwxyz'

def break_caesar(message):
    caesar = lambda s, key: s.translate(str.maketrans(abc, abc[key:] + abc[:key]))
    message = ''.join(c if c.isalpha() else ' ' for c in message).lower()    
    hits = [ sum(w in WORDS for w in caesar(message, -key).split()) for key in range(26) ]
    return hits.index(max(hits))

##### Points
1 maketrans()方法语法：  
str.maketrans(intab, outtab)  
参数  
intab -- 字符串中要替代的字符组成的字符串。  
outtab -- 相应的映射字符的字符串。  
返回值  
返回字符串转换后生成的新字符串。  
注：两个字符串的长度必须相同，为一一对应的关系。    
  
2   
![translate](https://ws1.sinaimg.cn/large/006tNc79gy1fz6j9qukimj30f308zt9p.jpg)
  
3 自己运行判断单词 可用enchant  
    import enchant
    d = enchant.Dict("en_US")
    d.check("Hello")
    True/False