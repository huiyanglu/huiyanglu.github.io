---
layout:     post
title:      Extract the domain name from a URL
subtitle:   20181015_Codewars_domain_name
date:       2018-10-15
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Extract the domain name from a URL
#### Codewars Kata 35√
##### Description
Description:
https://www.codewars.com/kata/514a024011ea4fb54200004b

-简述：本题给定一个网址，要求提取其中的网页名部分（即.com之前的部分）  
-思路：以不同的分隔符来分割字符串提取  
-难点：1 考虑多种网址的情况  
  
Write a function that when given a URL as a string, parses out just the domain name and returns it as a string. For example:

domain_name("http://github.com/carbonfive/raygun") == "github" 
domain_name("http://www.zombie-bites.com") == "zombie-bites"
domain_name("https://www.cnet.com") == "cnet"

##### My solution
    def domain_name(url):
        return url.split('//')[-1].split('www.')[-1].split('.')[0]
    	# 取//后面
    	# www.后面的关键词
    	# 以 ' . '分割

##### Given solution
    def domain_name_01(self, url):
        url = url.split('/')
        return url[0 if len(url) == 1 else 2].split('.')[-2]

    def domain_name_02(self, url):
        return url.split('//')[-1].split('/')[0].split('.')[-2]

    def domain_name_03(self, url):
        result = re.search(r"(//)?((?P<domain>\w+)\.)+", url)
        return result.group('domain') if result else None

    def domain_name_04(self, url):
        result = re.search(r"(//)?(\w+\.)?(?P<domain>\w+)\.", url)
        return result.group('domain') if result else None
  
##### Points
1 串联分割split用法
  
ps:回头再做这题就觉得超简单了ㄟ( ▔, ▔ )ㄏ