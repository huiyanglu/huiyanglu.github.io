---
layout:     post
title:      Phone Directory
subtitle:   20181105_Codewars_5kyu_phone
date:       2018-11-05
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Phone Directory
#### Codewars Kata 45√
##### Description
https://www.codewars.com/kata/566584e3309db1b17d000027/solutions/python
-简述：本题给定通讯录里的一些信息，包括人名、电话号码、地址。要求查找到所需的电话号码对应的人名和地址，考虑不止一人或未找到的情况。  
-思路：运用正则表达式，分类讨论。  
-难点：1 通讯录里的格式有些不一样的，要考虑周全。  
  
John keeps a backup of his old personal phone book as a text file. On each line of the file he can find the phone number (formated as +X-abc-def-ghij where X stands for one or two digits), the corresponding name between < and > and the address.

Unfortunately everything is mixed, things are not always in the same order, lines are cluttered with non-alpha-numeric characters.

Examples of John's phone book lines:

    "/+1-541-754-3010 156 Alphand_St. <J Steeve>\n"

    " 133, Green, Rd. <E Kustur> NY-56423 ;+1-541-914-3010!\n"

    "<Anastasia> +48-421-674-8974 Via Quirinal Roma\n"

Could you help John with a program that, given the lines of his phone book and a phone number returns a string for this number : "Phone => num, Name => name, Address => adress"

##### Examples:

s = "/+1-541-754-3010 156 Alphand_St. <J Steeve>\n 133, Green, Rd. <E Kustur> NY-56423 ;+1-541-914-3010!\n"

phone(s, "1-541-754-3010") should return "Phone => 1-541-754-3010, Name => J Steeve, Address => 156 Alphand St."

It can happen that, for a few phone numbers, there are many people for a phone number -say nb- , then

return : "Error => Too many people: nb"

or it can happen that the number nb is not in the phone book, in that case

return: "Error => Not found: nb"

You can see other examples in the test cases.

JavaScript random tests completed by @ matt c

Note
Codewars stdout doesn't print part of a string when between < and >

  
##### My solution
    import re

    def domain_name(url):
        mod_url = re.sub(r'[^A-Za-z0-9\+\-\<\>\.\']|/d+',' ',url)
        name1 = mod_url.split('<')[-1].split('>')[0]
        return 'Name => ' + name1

    def domain_phone(url):
        mod_url = re.sub(r'[^A-Za-z0-9\+\-\<\>\.\']|/d+', ' ', url)
        del_name = mod_url.split('<')[0] + mod_url.split('>')[-1]
        phone1 = del_name.split('+')[-1].split(' ')[0]
        return phone1

    def domain_address(url):
        mod_url = re.sub(r'[^A-Za-z0-9\+\-\<\>\.\']|/d+', ' ', url)
        del_name = mod_url.split('<')[0] + mod_url.split('>')[-1]
        mod_add = del_name.split('+')[0]+del_name.split('+')[-1].split(' ', 1)[-1]
        x = re.split(r'[^A-Za-z0-9\-\.\']+', mod_add.strip())
        add1 = ' '.join(x)
        return 'Address => '+add1

    def phone(strng,num):
        split_strng = re.split(r'\n', strng.strip())
        count = 0
        for each_strng in split_strng:
            each_phone = domain_phone(each_strng)
            if each_phone == num:
                count += 1
                rst_strng = each_strng
        if count>1:
            return 'Error => Too many people: ' + num
        elif count == 0:
            return 'Error => Not found: '+ num
        else:
            phone = 'Phone => '+domain_phone(rst_strng)
            name = domain_name(rst_strng)
            addr = domain_address(rst_strng)
            rst = phone+', '+name+', '+addr
            return str(rst)


##### Given solution
    from re import sub

    def phone(dir, num):
        if dir.count("+" + num) == 0:
            return "Error => Not found: " + num
        
        if dir.count("+" + num) > 1:
            return "Error => Too many people: " + num
        
        for line in dir.splitlines():#按照换行符分割，每行为一项
            if "+" + num in line:
                name = sub(".*<(.*)>.*", "\g<1>", line)
                line = sub("<" + name + ">|\+" + num, "", line)
                    #name和num用''代替，相当于删掉name和num
                address = " ".join(sub("[^a-zA-Z0-9\.-]", " ", line).split())
                    #除数字、字母、点、-以外的全部替换为' '空格
                    #split()不带参数时以空格进行分割，带参数时以该参数进行分割
                return "Phone => %s, Name => %s, Address => %s" % (num, name, address)

##### Points  
1 split()当不带参数时以空格进行分割，当代参数时，以该参数进行分割。  
  
2 \g<1>  
In addition to character escapes and backreferences as described above, \g<name> will use the substring matched by the group named name, as defined by the (?P<name>...) syntax. \g<number> uses the corresponding group number; \g<2> is therefore equivalent to \2, but isn’t ambiguous in a replacement such as \g<2>0. \20 would be interpreted as a reference to group 20, not a reference to group 2 followed by the literal character '0'. The backreference \g<0> substitutes in the entire substring matched by the RE.
https://docs.python.org/3.2/library/re.html
  
3 splitlines() 按照换行符分割，每行为一项
  
4 ‘|’代表左右表达式任意匹配一个
  
5 str.count(string) 求字符串中某个部分string出现的次数
  
ps: 正则真好用。
