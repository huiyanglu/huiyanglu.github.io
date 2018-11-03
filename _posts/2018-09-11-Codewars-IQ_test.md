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
Bob is preparing to pass IQ test. The most frequent task in this test is to find out which one of the given numbers differs from the others. Bob observed that one number usually differs from the others in evenness. Help Bob — to check his answers, he needs a program that among the given numbers finds one that is different in evenness, and return a position of this number.

! Keep in mind that your task is to help Bob solve a real IQ test, which means indexes of the elements start from 1 (not 0)

##### Examples:
iq_test("2 4 7 8 10") => 3 // Third number is odd, while the rest of the numbers are even
iq_test("1 2 1 1") => 2 // Second number is even, while the rest of the numbers are odd

##### My solution  
    def iq_test(lines):
      even = []
          odd = []
         integers = lines.split(' ')
         # 分割每个数字，分别加引号，成为一个数组[]
          print(integers)
          for num in integers:
                if int(num) % 2 == 0:
                    even.append(num)
                else:
                    odd.append(num)
          if len(even)>1 and len(odd)==1:
                spec = odd[0]
                return integers.index(spec)+1
                # index生成该数字的索引，即在数列中的位置，从0开始
          elif len(odd)>1 and len(even)==1:
                spec = even[0]
                return integers.index(spec)+1
    print(iq_test('1 3 5 7 8'))  

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
