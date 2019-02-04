---
layout:     post
title:      IQ test
subtitle:   20180911_Codewars_iq_test
date:       2018-09-11
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# IQ test
#### Codewars Kata 3√
##### Description
Link: [iq_test](https://www.codewars.com/kata/552c028c030765286c00007d)  
  
-简述：本题给定一列数字，要求找出其中最特殊的那一个（奇数中的偶数，偶数中的奇数）  
-思路：用列表推导，找到奇数和偶数，判断求异  
-难点：无  
  
Bob is preparing to pass IQ test. The most frequent task in this test is to find out which one of the given numbers differs from the others. Bob observed that one number usually differs from the others in evenness. Help Bob — to check his answers, he needs a program that among the given numbers finds one that is different in evenness, and return a position of this number.

! Keep in mind that your task is to help Bob solve a real IQ test, which means indexes of the elements start from 1 (not 0)

##### Examples:
iq_test("2 4 7 8 10") => 3 // Third number is odd, while the rest of the numbers are even
iq_test("1 2 1 1") => 2 // Second number is even, while the rest of the numbers are odd

##### My solution  
  def iq_test(lines):
      integers = lines.split(' ')
      even = [num for num in integers if int(num)%2==0]
      if len(even)==1:
          spec = even[0]
          return integers.index(spec)+1
          # index生成该数字的索引，即在数列中的位置，从0开始
      else:
          spec = [num for num in integers if int(num)%2!=0]
          return integers.index(spec[0])+1

##### Given solutions
    def iq_test(numbers):
          e = [int(i) % 2 == 0 for i in numbers.split()]
          return e.index(True) + 1 if e.count(True) == 1 else e.index(False) + 1  
    
    def iq_test(numbers):
          eo = [int(n)%2 for n in numbers.split()]
          return eo.index(1 if eo.count(0)>1 else 0)+1  
    
    def iq_test(numbers):
          indexEven = 0
          indexOdd = 0
          numEven = 0
          numOdd = 0
          nums = numbers.split(" ")
          for i in range(len(nums)):
                if int(nums[i])%2 == 0:
                    numEven += 1
                    indexEven = i+1
                else:
                    numOdd += 1
                    indexOdd = i+1
          if numEven == 1:
                return indexEven
          else:
                return indexOdd  

##### Points  
1 该题目要求较简单，仅考虑数字的奇偶性。  
