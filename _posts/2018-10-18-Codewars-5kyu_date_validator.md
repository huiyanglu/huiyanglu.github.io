---
layout:     post
title:      Regex for Gregorian date validation
subtitle:   20181018_Codewars_5kyu_date_validator
date:       2018-10-18
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Regex for Gregorian date validation
#### Codewars Kata 38√
##### Description
  
https://www.codewars.com/kata/5ab23a9c1cec39668c000055/solutions/python  

-简述：本题给定日期的格式，要求写出日期的常规表达方法dd.mm.yyyy  
-思路：运用正则表达式，考虑各个月份的日期变化。  
-难点：1 leap year闰年的特殊情况特殊表达  

Your task is to write regular expression that validates gregorian date in format "DD.MM.YYYY"

Correct date examples:

"23.12.2008"
"01.08.1994"
Incorrect examples:

"12.23.2008"
"01-Aug-1994"
" 01.08.1994"
  
Notes:

-maximum length of validator is 400 characters to avoid hardcoding. (shortest solution to date is 170 characters)  
-validator should process leap days (February, 29) correctly.  
-the date is Gregorian, it's important to determine if year is leap: https://en.wikipedia.org/wiki/Gregorian_calendar  

##### Given solution
    date_validator = r'^(29\.02\.(\d\d(0[48]|[2468][048]|[13579][26])|(0[48]|[2468][048]|[13579][26])00)|(31\.(0[13578]|1[02])|(29|30)\.(0[13-9]|1[0-2])|(0[1-9]|1\d|2[0-8])\.(0[1-9]|1[0-2]))\.(\d{3}[1-9]|\d\d[1-9]\d|\d[1-9]\d\d\[1-9]\d{3}))$'

---
    date_validator = (
        '((('
        '(0[1-9]|1\d|2[0-8])\.(0[1-9]|1[012])|'    # 01-28 of any month
        '(29|30)\.(0[13-9]|1[012])|'               # 29-30 of months, except February
        '(31\.(0[13578]|1[02])))\.'                # 31 of long months
        '([1-9]\d{3}|\d{3}[1-9]))|'                # any year, except 0000
        '(29\.02\.('                               # leap day
        '\d\d([2468][048]|[13579][26]|0[48])|'     # leap years (mod 4)   
        '([2468][048]|[13579][26]|0[48])00'        # leap years (mod 400)
        ')))$' )

##### Points
1 
![avatar](https://ws3.sinaimg.cn/large/006tNc79gy1fz4akmu5noj319r0u0e81.jpg)
![avatar](https://ws4.sinaimg.cn/large/006tNc79gy1fz4akox019j31ga0u0qth.jpg)

2 Gregorian calendar  
Every year that is exactly divisible by four is a leap year, except for years that are exactly divisible by 100, but these centurial years are leap years if they are exactly divisible by 400. For example, the years 1700, 1800, and 1900 are not leap years, but the year 2000 is.  
闰年：能被4或400整除且不能被100整除的年份（0001-9999）  

3  
![avatar](https://ws2.sinaimg.cn/large/006tNc79gy1fz4amx3o1bj30k60g30v8.jpg)
![avatar](https://ws2.sinaimg.cn/large/006tNc79gy1fz4amzhdyhj30k507pdgs.jpg)
