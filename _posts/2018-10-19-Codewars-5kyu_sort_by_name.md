---
layout:     post
title:      Sort - one, three, two
subtitle:   20181019_Codewars_5kyu_sort_by_name
date:       2018-10-19
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Sort - one, three, two
#### Codewars Kata 39√
##### Description
  
Link:  
https://www.codewars.com/kata/56f4ff45af5b1f8cd100067d
  
-简述：本题给定一列数字，要求按照各数字的文字表达形式重新对数列进行排序（按照名称的英文字母顺序排列）  
-思路：参考将数字转换为文字的题目，运用sorted()函数，调用key直接求解  
-难点：1 sorted的key如何设置  

Sort - one, three, two  
Hey You !  
Sort these integers for me ...  

By name ...

Do it now !

Input
Range is 0-999

There may be duplicates

The array may be empty

##### My solution
    def number2words(n):
        digits = ['zero','one','two','three',
             'four','five','six','seven',
             'eight','nine','ten','eleven',
             'twelve','thirteen','fourteen',
             'fifteen','sixteen','seventeen',
             'eighteen','nineteen','twenty']
        decades = ['ten','twenty','thirty','forty',
                   'fifty','sixty','seventy','eighty',
                   'ninety']
        if n < 20:
            return digits[n]
        elif n < 100:
            return decades[n//10-1] + ('-' + digits[n % 10] if n % 10 > 0 else '')
        elif n < 1000:
            return digits[n//100] + ' hundred' + (' '+ number2words(n%100) if n%100>0 else '')

    def sort_by_name(s):
        return sorted(s,key=number2words)

    print(sort_by_name([2,4,6]))   
  
##### Given solutions
    S = ["", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine",
         "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"]
    TENTH = ["", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"]


    def convertToString(n):
        if not n: return "zero"
        c,t,u = map(lambda v: (n%(v*10))//v, (100,10,1))
        return " ".join(s for s in ["{} hundred".format(S[c]) * bool(c), TENTH[t], S[u+10*(t==1)]] if s)

    def sort_by_name(arr): return sorted(arr, key=convertToString)
  
   
##### Points
1 sorted 语法：  
sorted(iterable[, cmp[, key[, reverse]]])  
参数说明：  
iterable -- 可迭代对象。  
cmp -- 比较的函数，这个具有两个参数，参数的值都是从可迭代对象中取出，此函数必须遵守的规则为，大于则返回1，小于则返回-1，等于则返回0。  
key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。  
reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。    
=> key也可以用lambda自建函数  
  
2 sort 与 sorted 区别：  
sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。
list 的 sort 方法返回的是对已经存在的列表进行操作，无返回值.  
内建函数sorted 方法返回的是一个新的list，而不是在原来的基础上进行的操作。
  
** Tips: sort by name的意思是按照名称的英文字母顺序排列。**
