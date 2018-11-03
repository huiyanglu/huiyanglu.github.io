---
layout:     post
title:      Maximum subarray sum
subtitle:   20181009_Codewars_maxSequence
date:       2018-10-09
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Maximum subarray sum
#### Codewars Kata 31√
##### Description
The maximum sum subarray problem consists in finding the maximum sum of a contiguous subsequence in an array or list of integers:

maxSequence([-2, 1, -3, 4, -1, 2, 1, -5, 4])
should be 6: [4, -1, 2, 1]

Easy case is when the list is made up of only positive numbers and the maximum sum is the sum of the whole array. If the list is made up of only negative numbers, return 0 instead.

Empty list is considered to have zero greatest sum. Note that the empty list or array is also a valid sublist/subarray.

##### My solution
    def maxSequence(arr):
        if arr == []:
            return 0
        else:
            a = []
            for i in range(0,len(arr)):
                for j in range(0,len(arr)):
                    sum2 = sum(arr[i:j+1])
                    a.append(sum2)
            return max(a)

    print(maxSequence([-2, 1, -3, 4, -1, 2, 1, -5, 4]))

##### Given solutions  
    def maxSequence(arr):
        max,curr=0,0
        for x in arr:
            curr+=x
            if curr<0:curr=0
            if curr>max:max=curr
        return max
  
---  
    def maxSequence(arr):
      lowest = ans = total = 0
      for i in arr:
        total += i
        lowest = min(lowest, total)
        ans = max(ans, total - lowest)
      return ans
  
---  
    def maxSequence(arr):
        maxl = 0
        maxg = 0
        for n in arr:
            maxl = max(0, maxl + n)
            maxg = max(maxg, maxl)
        return maxg
