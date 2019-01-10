---
layout:     post
title:      Largest rectangle in background
subtitle:   20181029_Codewars_5kyu_largest_rect
date:       2018-10-29
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Largest rectangle in background
#### Codewars Kata 42√
##### Description
Largest Rectangle in Background
Imagine a photo taken to be used in an advertisement. The background on the left of the motive is whitish and you want to write some text on that background. So you scan the photo with a high resolution scanner and, for each line, count the number of pixels from the left that are sufficiently white and suitable for being written on. Your job is to find the area of the largest text box you can place on those pixels.

Example: In the figure below, the whitish background pixels of the scanned photo are represented by asterisks.

	*********************************
	*********
	*******
	******
	******
	******
	**************
	**************
	**************
	***************
	*********************
  
If you count the pixels on each line from the left you get the list (or array, depending on which language you are using) [33, 9, 7, 6, 6, 6, 14, 14, 14, 15, 21]. The largest reactangle that you can place on these pixels has an area of 70, and is represented by the dots in the figure below.
  
	*********************************
	*********
	*******
	******
	******
	******
	..............
	..............
	..............
	..............*
	..............*******
  
Write a function that, given a list of the number whitish pixels on each line in the background, returns the area of the largest rectangle that fits on that background.
  
##### Given solutions  
    def largest_rect(histogram):
        histogram.append(0)
        stack = [-1] # s是h1的index的序列
        result = 0
        for i in range(0,len(histogram)):
            while histogram[i] < histogram[stack[-1]]: # s序列的最后一位对应的h1里的数
                h = histogram[stack.pop()] # []里是去掉的那个数
                w = i - stack[-1] - 1 # 符合要求的数字有几个
                result = max(result, h * w)
            stack.append(i)
        histogram.pop()
        return result

    print(largest_rect([3,4,5,4,3,4,5]))
  
---  
    def largest_rect(h):
        st=[]; m=0; i=0
        while i<len(h):
            if len(st)==0 or h[st[-1]]<=h[i]: st.append(i); i+=1
            else: l=st.pop(); m=max(m, h[l]*(i if len(st)==0 else i-st[-1]-1))
        while len(st)>0: l=st.pop(); m=max(m, h[l]*(i if len(st)==0 else i-st[-1]-1))
        return m
  
---  
    def largest_rect(h):
      r,s,i,l=0,[],0,len(h)
      while i<l:
        if not s or h[s[-1]]<=h[i]: s.append(i); i+=1
        else:  t=s.pop(); a=i-s[-1]-1 if s else i; a*=h[t]; r=r if r>a else a
      while s: t=s.pop(); a=i-s[-1]-1 if s else i; a*=h[t]; r=r if r>a else a
      return r
    
  ps: 今天的好难…思路就想好久好久…看答案都看不懂_(:з」∠)_
