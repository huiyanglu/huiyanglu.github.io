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
