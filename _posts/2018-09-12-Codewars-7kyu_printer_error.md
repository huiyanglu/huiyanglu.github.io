---
layout:     post
title:      Printer error
subtitle:   20180912_Codewars_printer_error
date:       2018-09-12
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Printer error
#### Codewars Kata 4√
##### Description  
Link: [printer_error](https://www.codewars.com/kata/546f922b54af40e1e90001da)  
   
-简述：本题假设一个打印机的错误检查，若打印内容不在字母a-m内，则报错，输出错误次数。  
-思路：运用正则找出所有异常数字  
-难点：无  
   
In a factory a printer prints labels for boxes. For one kind of boxes the printer has to use colors which, for the sake of simplicity, are named with letters from a to m.
The colors used by the printer are recorded in a control string. For example a "good" control string would be aaabbbbhaijjjm meaning that the printer used three times color a, four times color b, one time color h then one time color a...
Sometimes there are problems: lack of colors, technical malfunction and a "bad" control string is produced e.g. aaaxbbbbyyhwawiwjjjwwm.
You have to write a function printer_error which given a string will output the error rate of the printer as a string representing a rational whose numerator is the number of errors and the denominator the length of the control string. Don't reduce this fraction to a simpler expression.
The string has a length greater or equal to one and contains only letters from ato z.

##### Examples:
s="aaabbbbhaijjjm"
error_printer(s) => "0/14”

s="aaaxbbbbyyhwawiwjjjwwm"
error_printer(s) => "8/22"

##### My solution:
    import re
    def printer_error(s):
        # your code
        m = str(len(re.findall(r'[n-z]',s)))
        q = str(len(s))# 总长度 要加str!
        return m+'/‘+q # str字符串可以用+连接

    s="aammmxyzz"
    x = printer_error(s)
    print(x)   

##### Given solutions:
    from re import sub
    def printer_error(s):
        return "{}/{}".format(len(sub("[a-m]",'',s)),len(s))
---
    def printer_error(s):
        errors = 0
        count = len(s)
        for i in s:
            if i > "m":
                errors += 1
        return str(errors) + "/" + str(count)

##### Points  
1 可以直接用if i > "m":表达m之后的字母  
  