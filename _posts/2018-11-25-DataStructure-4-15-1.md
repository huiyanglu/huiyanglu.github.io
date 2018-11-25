---
layout:     post
title:      Data Structure 4.15. Discussion Questions (1)
subtitle:   20181125_DataStructure_4-15-1
date:       2018-11-25
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Data Structure 4.15. Discussion Questions (1)
#### Call stack for the Tower of Hanoi problem
##### Description
Draw a call stack for the Tower of Hanoi problem.
Assume that you start with a stack of three disks.
要求：用堆栈解决汉诺塔问题（盘子个数为3）
缺陷：不能显示栈的内容 只能显示数目
改进：可用list模拟栈

My solution:
    from pythonds.basic.stack import Stack

    	# print('请输入汉诺塔的层数')
     	# N = int(input())
    N = 3
    global A, B, C, step
    A = Stack()
    B = Stack()
    C = Stack()
    x = []
    step = 0
    lst = list(range(1, N + 1))
    lst.reverse()
    for i in lst:
        A.push(i)
    print(A.size())

    def tower(s1, s2, s3, N=-1):  # 汉诺塔算法，借助s2，将s1的N层移动到s3
        global step
        if(N == -1):
            N = s1.size()
        if(N == 0):
            return
        elif(N == 1):  # 判断栈的深度，如果栈深为1，则一次简单移动即可；若大于1，则需要进行递归操作
            moveDisk(s1,s3)
            s3.push(s1.pop())
            print('%-20s %-20s %-20s' % (A.size(), B.size(), C.size()))  # 为了方便展示结果，输出语句做了调整
            step += 1
        else:
            tower(s1, s3, s2, N-1)  # 从s1移到s2
            moveDisk(s1,s3)
            s3.push(s1.pop())
            print('%-20s %-20s %-20s' % (A.size(), B.size(), C.size()))
            step += 1
            tower(s2, s1, s3, N-1) # 从s2移到s3
        return

    def moveDisk(fromPole,toPole):
        print('moving disk from',fromPole.size(),'to',toPole.size())

    print(tower(A, B, C))
    print('所需步数为%d' % step)