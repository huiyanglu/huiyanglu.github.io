---
layout:     post
title:      Domain name validator
subtitle:   20181211_5kyu_validate
date:       2018-12-11
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Domain name validator
#### Codewars Kata 56√
##### Description  

-简述：本题用于验证域名是否符合规则。规则包括：
	1 域名可能包含子域（level），以.点分割 
	2 域名包括top level在内不能超过127个level 
	3 域名不能超过253个字符 
	4 level名必须由小写和大写字母、数字、-（减号）组成。
	5 level名不能以减号开头或结尾 
	6 level不能超过63字符 
	7 top level不能全是数字
-思路：运用正则表达式
-难点：1 需要同时设定多个限定要求
Description:
In this kata you have to create a domain name validator mostly compliant with RFC 1035, RFC 1123, and RFC 2181

For purposes of this kata, following rules apply:
	⁃	Domain name may contain subdomains (levels), hierarchically separated by . (period) character
	⁃	Domain name must not contain more than 127 levels, including top level (TLD)
	⁃	Domain name must not be longer than 253 characters (RFC specifies 255, but 2 characters are reserved for trailing dot and null character for root level)
	⁃	Level names must be composed out of lowercase and uppercase ASCII letters, digits and - (minus sign) character
	⁃	Level names must not start or end with - (minus sign) character
	⁃	Level names must not be longer than 63 characters
	⁃	Top level (TLD) must not be fully numerical

Additionally, in this kata domain name must contain at least one subdomain (level) apart from TLD.

Top level validation must be naive - ie. TLDs nonexistent in IANA register are still considered valid as long as they adhere to the rules given above.

The validation function accepts string with the full domain name and returns boolean value indicating whether the domain name is valid or not.
Examples:
validate('codewars') == False 没有level
validate('g.co') == True
validate('codewars.com') == True
validate('CODEWARS.COM') == True
validate('sub.codewars.com') == True
validate('codewars.com-') == False 不能以-结尾
validate('.codewars.com') == False 不能以点开头
validate('example@codewars.com') == False 不能包含@
validate('127.0.0.1') == False 不能全为数字

##### My solution:
import re

def differentiate(equation,point):
                                                                             
##### Given solutions:
import re

def validate(domain):
    return re.match('''
        (?=^.{,253}$)          # max. length 253 chars
        (?!^.+\.\d+$)          # TLD is not fully numerical
        (?=^[^-.].+[^-.]$)     # doesn't start/end with '-' or '.'
        (?!^.+(\.-|-\.).+$)    # levels don't start/end with '-'
        (?:[a-z\d-]            # uses only allowed chars
        {1,63}(\.|$))          # max. level length 63 chars
        {2,127}                # max. 127 levels
        ''', domain, re.X | re.I)

print(validate('codewars.com'))

##### Points
1

练习正则表达式：
import re

P = re.compile(r'\+?(-?\d*)(x\^?)?(\d*)')
Q = re.compile(r'\+?(\d*)(m\^?)?(\d*)')
# \d 十进制数字0-9
# 问号 ? ，它用于指定匹配它前面的字符0次或者1次
# 星号 * 匹配0次或者多次

print(P.findall('48x^6+36x^5-18x^4+x^3+76x^2+36x+1'))
print(Q.findall('2m^2+m+5'))

Link: https://www.codewars.com/kata/domain-name-validator/solutions?show-solutions=1