---
layout:     post
title:      Write out numbers
subtitle:   20181113_Codewars_5kyu_number2words
date:       2018-11-13
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Write out numbers
#### Codewars Kata 51√
##### Description
https://www.codewars.com/kata/52724507b149fa120600031d/solutions/python

-简述：本题给定一个数字，要求讲其转换为文字形式表达。  
-思路：分情况讨论，数字过大时需要调用函数自身更为简便  

Create a function that transforms any positive number to a string representing the number in words. The function should work for all numbers between 0 and 999999.

Examples
number2words(0)  ==>  "zero"
number2words(1)  ==>  "one"
number2words(9)  ==>  "nine"
number2words(10)  ==>  "ten"
number2words(17)  ==>  "seventeen"
number2words(20)  ==>  "twenty"
number2words(21)  ==>  "twenty-one"
number2words(45)  ==>  "forty-five"
number2words(80)  ==>  "eighty"
number2words(99)  ==>  "ninety-nine"
number2words(100)  ==>  "one hundred"
number2words(301)  ==>  "three hundred one"
number2words(799)  ==>  "seven hundred ninety-nine"
number2words(800)  ==>  "eight hundred"
number2words(950)  ==>  "nine hundred fifty"
number2words(1000)  ==>  "one thousand"
number2words(1002)  ==>  "one thousand two"
number2words(3051)  ==>  "three thousand fifty-one"
number2words(7200)  ==>  "seven thousand two hundred"
number2words(7219)  ==>  "seven thousand two hundred nineteen"
number2words(8330)  ==>  "eight thousand three hundred thirty"
number2words(99999)  ==>  "ninety-nine thousand nine hundred ninety-nine"
number2words(888888)  ==>  "eight hundred eighty-eight thousand eight hundred eighty-eight"
  
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
        elif n<1000000:
            return number2words(n//1000) + ' thousand' + (' '+ number2words(n%1000) if n%1000>0 else '')

    print(number2words(869043))
  
##### Given solution
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
            return decades[n//10-1] + ('' if n % 10 == 0 else '-' + digits[n % 10])
        elif n<1000:
            return number2words(n//100) + ' hundred' + (' ' + number2words(n % 100) if n % 100 > 0 else '')
        elif n<1000000:
            return number2words(n // 1000) + " thousand" + (' ' + number2words(n % 1000) if n % 1000 > 0 else '')

    print(number2words(869043))

##### Points  
1 不加and，调用函数自身  
  
2 如何提取数字的各位数字  
  
ps: 用到了函数迭代