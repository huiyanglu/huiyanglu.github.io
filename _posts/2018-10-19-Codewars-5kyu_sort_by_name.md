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
  
Sort - one, three, two  
Hey You !  
Sort these integers for me ...  

By name ...

Do it now !

Input
Range is 0-999

There may be duplicates

The array may be empty

##### Given solutions
    S = ["", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine",
         "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"]
    TENTH = ["", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"]


    def convertToString(n):
        if not n: return "zero"
        c,t,u = map(lambda v: (n%(v*10))//v, (100,10,1))
        return " ".join(s for s in ["{} hundred".format(S[c]) * bool(c), TENTH[t], S[u+10*(t==1)]] if s)

    def sort_by_name(arr): return sorted(arr, key=convertToString)
  
---  
    def sort_by_name(arr):
        return sorted(arr, key=convert)

    def convert(a):
        if not a: return "zero"
        d = {1:'one', 2:'two', 3:'three', 4:'four', 5:'five', 6:'six', 7:'seven', 8:'eight', 9:'nine', 10:'ten', 11:'eleven', 12:'twelve', 13:'thirteen', 14:'fourteen', 15:'fifteen', 16:'sixteen', 17:'seventeen', 18:'eighteen', 19:'nineteen', 20:'twenty', 30:'thirty', 40:'forty', 50:'fifty', 60:'sixty', 70:'seventy', 80:'eighty', 90:'ninety'}
        r = []
        if a // 100: r.append("{} hundred".format(d[a // 100]))
        if a % 100:
            if a % 100 <= 20: r.append(d[a % 100])
            else:
                b = d[a % 100 // 10 * 10]
                if a % 10: b += " {}".format(d[a % 10])
                r.append(b)
        return " ".join(r)
           
   
** Tips: sort by name的意思是按照名称的英文字母顺序排列。**
