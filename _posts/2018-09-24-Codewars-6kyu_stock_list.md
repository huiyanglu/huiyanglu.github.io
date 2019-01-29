---
layout:     post
title:      Help the bookseller !
subtitle:   20180924_Codewars_stock_list
date:       2018-09-24
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Help the bookseller !
#### Codewars Kata 16√
##### Description  
Link: [stock_list](https://www.codewars.com/kata/help-the-bookseller/python)  
  
A bookseller has lots of books classified in 26 categories labeled A, B, ... Z. Each book has a code c of 3, 4, 5 or more capitals letters. The 1st letter of a code is the capital letter of the book category. In the bookseller's stocklist each code c is followed by a space and by a positive integer n (int n >= 0) which indicates the quantity of books of this code in stock.

For example an extract of one of the stocklists could be:
L = {"ABART 20", "CDXEF 50", "BKWRK 25", "BTSQZ 89", "DRTYM 60"}.
or
L = ["ABART 20", "CDXEF 50", "BKWRK 25", "BTSQZ 89", "DRTYM 60"] or ....
You will be given a stocklist (e.g. : L) and a list of categories in capital letters e.g :

  M = {"A", "B", "C", "W"}
or
  M = ["A", "B", "C", "W"] or ...
and your task is to find all the books of L with codes belonging to each category of M and to sum their quantity according to each category.

For the lists L and M of example you have to return the string (in Haskell/Clojure a list of pairs):

  (A : 20) - (B : 114) - (C : 50) - (W : 0)
where A, B, C, W are the categories, 20 is the sum of the unique book of category A, 114 the sum corresponding to "BKWRK" and "BTSQZ", 50 corresponding to "CDXEF" and 0 to category 'W' since there are no code beginning with W.

If L or M are empty return string is "" (Clojure should return an empty array instead).

Note:
In the result codes and their values are in the same order as in M.

##### My solution
    def stock_list(listOfArt, listOfCat):
        if listOfArt == [] or listOfCat == []:
            return ''
        rst1 = []
        for i in listOfCat:
            cnt = 0
            for j in listOfArt:
                if i == j[0]:
                    j2 = j.split(' ')
                    cnt += int(j2[-1])
            rst1.append('({} : {})'.format(i,cnt))
        return ' - '.join(rst1[i] for i in range(len(rst1)))

    b = ["ABAR 200", "CDXE 500", "BKWR 250", "BTSQ 890", "DRTY 600"]
    c = ["A", "B"]
    print(stock_list(b, c))

##### Given solutions
    from collections import Counter

    def stock_list(listOfArt, listOfCat):
        if not listOfArt:
            return ''
        codePos = listOfArt[0].index(' ') + 1
        cnt = Counter()
        for s in listOfArt:
            cnt[s[0]] += int(s[codePos:])
        return ' - '.join('({} : {})'.format(cat, cnt[cat]) for cat in listOfCat)

---
    def stock_list(stocklist, categories):
        if not stocklist or not categories:
            return ""
        return " - ".join(
            "({} : {})".format(
                category,
                sum(int(item.split()[1]) for item in stocklist if item[0] == category))
            for category in categories)

##### Points  
1 Counter类的目的是用来跟踪值出现的次数。  