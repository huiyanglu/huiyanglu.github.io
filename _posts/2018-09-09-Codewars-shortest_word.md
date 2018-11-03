---
layout:     post
title:      Shortest word
subtitle:   20180909_Codewars_Shortest_word
date:       2018-09-09
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---

# Shortest word
#### Codewars Kata 1 √
##### Description:
Simple, given a string of words, return the length of the shortest word(s).
String will never be empty and you do not need to account for different data types.

##### My solution:
	s = input("Input the words:")
	l_split = s.split(' ')
	shortest = 100
	for word in l_split:
		if len(word)<shortest:
       			shortest = len(word)
	print(shortest)
 

##### Given solutions:  
	def find_short(s):   
		return min(len(x) for x in s.split())  
  
>split()  
>语法：str.split(str="", num=string.count(str)).  
>参数：  
>str -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。  
>num -- 分割次数。  
  
	def find_short(s):   
		return min(map(len, s.split(' ')))  
  
>map() 
>语法：map(function, iterable, ...)  
>参数：  
>function -- 函数  
>iterable -- 一个或多个序列  
  
	def find_short(s):   
		return len(min(s.split(' '), key=len))  
  
 **今日Tips：Markdown换行要在末尾加至少两个空格**
