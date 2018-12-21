---
layout:     post
title:      Differentiate a polynomial
subtitle:   20181219_5kyu_differentiate
date:       2018-12-19
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Differentiate a polynomial
#### Codewars Kata 58√
##### Description  
https://www.codewars.com/kata/566584e3309db1b17d000027/solutions/python
  
-简述：本题以字符串形式给定一个多项式和一个未知变量的值，求该多项式的微分并将具体值代入求出结果。  
  
-思路：提取多项式字符串中各项的系数和指数，转换为微分形式，求解。  
  
-难点： 
	1 如何分割字符串提取所需的数字   
	2 如何将系数和指数相对应   
	3 考虑特殊情况如一次、零次、系数为负数、第一个系数为负数等  
  
Create a function that differentiates a polynomial for a given value of x.  
Your function will receive 2 arguments: a polynomial as a string, and a point to evaluate the equation as an integer.
  
Assumptions:  
There will be a coefficient near each x, unless the coefficient equals 1 or -1.  
There will be an exponent near each x, unless the exponent equals 0 or 1.  
All exponents will be greater or equal to zero  

##### Examples:  
differenatiate("12x+2", 3) ==> returns 12  
differenatiate("x^2+3x+2", 3) ==> returns 9  

##### My solution:
	import re

	def differentiate(equation,point):
	    res = re.split(r'(\+|-)',equation)
	    res1 = res[1:]
	    res1 = [res[0]]+["".join(i).strip() for i in zip(res1[0::2],res1[1::2])]
	    if res1[0] == '':
	        res1.pop(0)
	    if '^' in res1[0]:
	        zhishuMax = res1[0][res1[0].index('^')+1:]
	        l = int(zhishuMax)+1
	    else:
	        l = len(res1)
	    lst = [0]*l
	    len_lst = len(res1)
	    for i in range(0,len_lst):
	        if 'x' not in res1[i]:
	            lst[-1] = int(res1[i])
	        else:
	            idx_x = res1[i].index('x')
	            if '^' in res1[i]:
	                idx_2 = res1[i].index('^')
	                zhishu = res1[i][idx_2+1:]
	            else:
	                zhishu = 1
	            if idx_x == 0 or (idx_x == 1 and res1[i][0] == '+'):
	                lst[l - int(zhishu) - 1] = 1
	            elif idx_x == 1 and res1[i][0] == '-':
	                lst[l - int(zhishu) - 1] = -1
	            else:
	                lst[l - int(zhishu) - 1] = int(res1[i][:idx_x])
	    sum = 0
	    for i in range(0,len(lst)):
	        if lst[i]==0:
	            pass
	        elif l-i-2>=0 and lst[i]!=0:
	            sum+=lst[i]*(l-i-1)*(point**(l-i-2))
	        else:
	            break
	    return sum

	print(differentiate('48x^6+36x^5-18x^4+x^3+76x^2+36x+1',4968))                                                                                    

##### Given solutions:
	from collections import defaultdict
	import re

	P = re.compile(r'\+?(-?\d*)(x\^?)?(\d*)')


	def differentiate(eq, x):
	    derivate = defaultdict(int)
	    for coef, var, exp in P.findall(eq):
	        exp = int(exp or var and '1' or '0')
	        coef = int(coef != '-' and coef or coef and '-1' or '1')

	        if exp: derivate[exp - 1] += exp * coef

	    return sum(coef * x ** exp for exp, coef in derivate.items())

##### Points：
1 defaultdict 初始化字典 方便后续往里面添加数据
  
2 正则表达式
\d：匹配所有十进制数字，相当于字符类[0-9]
\D：匹配所有非数字字符，相当于字符类[^0-9]
\s：匹配所有空白字符（包括制表符、换行符等），相当于字符类[\t\n\r\f\v]
\S：匹配所有非空白字符，相当于字符类[^\t\n\r\f\v]
\w：匹配所有字母数字字符，相当于字符类[a-zA-Z0-9]
\W：匹配所有非字母数字字符，相当于字符类[^a-zA-Z0-9]
  
3 正则表达式中表示重复的元字符
问号 ? ，它用于指定匹配它前面的字符0次或者1次
加号 + ，它指定匹配它前面的字符1次或者多次。
星号 * 匹配0次或者多次，所以被匹配的内容可能压根儿就不出现，但是加号 + 要求重复的字符至少出现1次。
  
最灵活的表示重复的限定符应该是{m,n}，这里的m和n都是十进制数字。这表示它前面的字符至少重复m次，最多重复n次。比如，a/{1,3}b可以匹配a/b，a//b和a///b。但是它不匹配ab，因为ab没有斜杠，也不匹配a////b，因为它有4个斜杠超过了3个。
  
4 and和or的优先级和计算规则（用于Python）
其一, 在不加括号时候, and优先级大于or
其二, x or y 的值只可能是x或y. x为真就是x, x为假就是y
第三, x and y 的值只可能是x或y. x为真就是y, x为假就是x
PS：考虑指数和系数的多种情况，熟练使用and和or的优先级和计算规则
  
5 提取字典里的value和key 
coef * x ** exp for exp, coef in derivate.items()
  
练习正则表达式  

	import re
	P = re.compile(r'\+?(-?\d*)(x\^?)?(\d*)')
	Q = re.compile(r'\+?(\d*)(m\^?)?(\d*)')
	# \d 十进制数字0-9
	# 问号 ? ，它用于指定匹配它前面的字符0次或者1次
	# 星号 * 匹配0次或者多次
	print(P.findall('48x^6+36x^5-18x^4+x^3+76x^2+36x+1'))
	print(Q.findall('2m^2+m+5'))
