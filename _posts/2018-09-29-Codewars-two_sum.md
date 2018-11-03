---
layout:     post
title:      Two Sum
subtitle:   20180929_Codewars_two_sum
date:       2018-09-29
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Two Sum
#### Codewars Kata 21√
##### Description
Write a function that takes an array of numbers (integers for the tests) and a target number. It should find two different items in the array that, when added together, give the target value. The indices of these items should then be returned in an array like so: [index1, index2].

For the purposes of this kata, some tests may have multiple answers; any valid solutions will be accepted.

The input will always be valid (numbers will be an array of length 2 or greater, and all of the items will be numbers; target will always be the sum of two different items from that array).

Based on: http://oj.leetcode.com/problems/two-sum/

##### My solution  
    def two_sum(a, b): # 时间复杂度n^2
        for i in range(0,len(a)): 
            x = a[i]
            y = b - x
            for j in range(1,len(a)):
                if y == a[j]:
                    return [i,j]
                else:
                    j+=1
            i+=1
  
##### Given solutions  
    def two_sum(nums, target): # 时间复杂度n
        d = {} 
        for i, num in enumerate(nums): 
            diff = target - num
            if diff in d:
                return [d[diff], i]
            d[num] = i # 若不相等则将该数字存入dict  

  
↓↓↓改进后，若存在多对数字，则输出所有符合条件的数字对。↓↓↓  
  
    def two_sum(nums, target):
        d = {}
        sums = []
        for i, num in enumerate(nums):
            diff = target - num
            if diff in d:
                sums.append([diff, num])
            d[num] = i
        return sums

> 参考：https://coderbyte.com/algorithm/two-sum-problem  
  
    # our two sum function which will return  
    # all pairs in the list that sum up to S  
    def twoSum(arr, S):  
        sums = []  
        hashTable = {}  
        # check each element in array  
        for i in range(0, len(arr)):  
          # calculate S minus current element  
            sumMinusElement = S - arr[i]  
            # check if this number exists in hash table  
            # if so then we found a pair of numbers that sum to S  
            if sumMinusElement in hashTable:  
                sums.append([arr[i], sumMinusElement])  
              # add the current number to the hash table  
            hashTable[arr[i]] = arr[i]  
        # return all pairs of integers that sum to S  
        return sums  
    print(twoSum([3, 5, 2, -4, 8, 11], 7))  
