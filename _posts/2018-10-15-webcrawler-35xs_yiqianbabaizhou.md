---
layout:     post
title:      Python爬虫之爬取小说《一千八百昼》
subtitle:  20181015_webcrawler_35xs_yiqianbabaizhou
date:       2018-10-15
author:     Huiyang_Lu
header-img: img/post-bg-cute1.jpg
catalog: true
tags:
    - Python
    - WebCrawler
---
# Python爬虫之爬取小说《一千八百昼》
#### 每章节单独存为一个TXT文件
##### Description  
  
**爬虫原因** ：在微博被安利了蟹总的这篇公路文，网页版广告太多。
  
**过程中遇到的问题** ：   
  
1、汉字出现乱码   
原因：部分网站charset为gbk  
解决方法：换成charset为utf-8的盗版小说网站   
（嗯…其实还没有彻底解决…因为gbk还不会转码）  
    
2、只能爬取一个章节  
原因及解决方法：chapter_list需要通过找关键词来获取逗号相隔的list    
    
3、chapter_url的网址可能需要补充完整，否则无法打开    
  
##### My solution  
    
      # 爬去小说《一千八百昼》，作者：蟹总
      # 网站：https://www.35xs.com/book/276274/
      # charset = utf-8

    import requests
    import os
    import time
    from bs4 import BeautifulSoup

    headers = {
        'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.84 Safari/537.36'
    }

    # 获取小说各个章节的名字和url
    def getChapterInfo(novel_url):
        chapter_html = requests.get(novel_url, headers=headers).text
        soup = BeautifulSoup(chapter_html,'lxml')
        soup2 = soup.find('ul',{'class':'mulu_list'})
        chapter_list = soup2.find_all('li') # 先找到'li'
        chapter_all_dict = {}
        for each in chapter_list:
            import re
            chapter_each = {}
            chapter_each['title'] = each.find('a').get_text()
            chapter_each['chapter_url'] = 'http://www.35xs.com'+each.find('a')['href']
            chapter_num = int(re.findall('\d+',each.get_text())[0])
            chapter_all_dict[chapter_num] = chapter_each # 记录到所有的章节的字典中保存，返回字典
        return chapter_all_dict

    # 获取小说章节内容，写入文本
    def getChapterContent(each_chapter_dict):
        content_html = requests.get(each_chapter_dict['chapter_url'],headers=headers).text
        soup = BeautifulSoup(content_html,'lxml')
        content_tag = soup.find('div',{'class':'bookreadercontent'})
        p_tag = content_tag.find_all('p')
        print('正在保存的章节-->'+ each_chapter_dict['title'])
        for each in p_tag: # 正文内容
            paragraph = each.get_text().strip() # 去掉首尾字符
            with open(each_chapter_dict['title']+r'.txt','a',encoding = 'utf8')as f:
                f.write(''+ paragraph + '\n\n')
                f.close()

    if __name__ == '__main__':
        start = time.clock() # 程序运行起始时间
        novel_url = 'https://www.35xs.com/book/276274/'
        novel_info = getChapterInfo(novel_url)
        dir_name = '保存的小说路径'
        if not os.path.exists(dir_name):
            os.mkdir(dir_name)
        os.chdir(dir_name)
        for each in novel_info:
            getChapterContent(novel_info[each])
        end = time.clock() # 记录程序结束时间
        print('保存结束，共保存 %d 章，花费时间：%f s'%(len(novel_info),(end-start)))
