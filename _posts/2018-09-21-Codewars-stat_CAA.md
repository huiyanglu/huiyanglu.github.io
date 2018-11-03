---
layout:     post
title:      Statistics for an Athletic Association
subtitle:   20180921_Codewars_stat_CAA
date:       2018-09-21
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Statistics for an Athletic Association
#### Codewars Kata 13√
##### Description
You are the "computer expert" of a local Athletic Association (C.A.A.). Many teams of runners come to compete. Each time you get a string of all race results of every team who has run. For example here is a string showing the individual results of a team of 5 runners:

"01|15|59, 1|47|6, 01|17|20, 1|32|34, 2|3|17"

Each part of the string is of the form: h|m|s where h, m, s (h for hour, m for minutes, s for seconds) are positive or null integer (represented as strings) with one or two digits. There are no traps in this format.

To compare the results of the teams you are asked for giving three statistics; range, average and median.

Range : difference between the lowest and highest values. In {4, 6, 9, 3, 7} the lowest value is 3, and the highest is 9, so the range is 9 − 3 = 6.

Mean or Average : To calculate mean, add together all of the numbers in a set and then divide the sum by the total count of numbers.

Median : In statistics, the median is the number separating the higher half of a data sample from the lower half. The median of a finite list of numbers can be found by arranging all the observations from lowest value to highest value and picking the middle one (e.g., the median of {3, 3, 5, 9, 11} is 5) when there is an odd number of observations. If there is an even number of observations, then there is no single middle value; the median is then defined to be the mean of the two middle values (the median of {3, 5, 6, 9} is (5 + 6) / 2 = 5.5).

Your task is to return a string giving these 3 values. For the example given above, the string result will be

"Range: 00|47|18 Average: 01|35|15 Median: 01|32|34"of the form:
"Range: hh|mm|ss Average: hh|mm|ss Median: hh|mm|ss"
where hh, mm, ss are integers (represented by strings) with each 2 digits.

Remarks:
if a result in seconds is ab.xy... it will be given truncated as ab.
if the given string is "" you will return ""

##### My solution  
    def change(x):
        h1 = x // 3600
        m1 = (x - 3600 * h1) // 60
        s1 = x - 3600 * h1 - 60 * m1
        return h1,m1,s1

    def stat(strg):
        if strg =='': # 判断输入是否为数字
            return ''
        else:
            s = strg.split(',')
            lst = []
            sum = 0
            l = len(s)
            try:
                int('')
            except ValueError:
                pass
            for i in range(0,l):
                b1 = s[i].split('|')  # 数列的第一个数将数字分隔开
                c1 = int(b1[0]) * 3600 + int(b1[1]) * 60 + int(b1[2])
                lst.append(c1)
                sum += lst[i]
            avg = sum//l
            rge = max(lst)-min(lst)
            if l%2 == 0:
                lst.sort()
                med = (lst[l//2]+lst[l//2-1])/2
            else:
                lst.sort() # 先排序 再求中位数
                med = lst[l//2]
            avgr = change(avg)
            rger = change(rge)
            medr = change(med)
            return "Range: %02d|%02d|%02d "%rger+"Average: %02d|%02d|%02d "%avgr+"Median: %02d|%02d|%02d"%medr 
      # 注意字符串输出的格式，善用+号
      # 注意字母拼写不要出错  

##### Given solutions  
    def stat(strg):

        def get_time(s):
            '''Returns the time, in seconds, represented by s.'''
            hh, mm, ss = [int(v) for v in s.split('|')]
            return hh * 3600 + mm * 60 + ss

        def format_time(time):
            '''Returns the given time as a string in the form "hh|mm|ss".'''
            hh = time // 3600
            mm = time // 60 % 60
            ss = time % 60
            return '{hh:02d}|{mm:02d}|{ss:02d}'.format(**locals())

        def get_range(times):
            return times[-1] - times[0]

        def get_average(times):
            return sum(times) // len(times)

        def get_median(times):
            middle = len(times) >> 1
            return (times[middle] if len(times) & 1 else
                    (times[middle - 1] + times[middle]) // 2)

        if strg == '':
            return strg
        times = [get_time(s) for s in strg.split(', ')]
        times.sort()
        rng = format_time(get_range(times))
        avg = format_time(get_average(times))
        mdn = format_time(get_median(times))
        return 'Range: {rng} Average: {avg} Median: {mdn}'.format(**locals())
