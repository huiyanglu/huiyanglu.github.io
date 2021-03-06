---
layout:     post
title:      Probabilities for Sums in Rolling Cubic Dice
subtitle:   20181108_Codewars_5kyu_rolldice_sum_prob
date:       2018-11-08
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Probabilities for Sums in Rolling Cubic Dice
#### Codewars Kata 48√
##### Description
https://www.codewars.com/kata/56f78a42f749ba513b00037f

-简述：本题是关于掷骰子的概率问题，给定骰子掷出的数字之和，以及骰子的个数n，求n个骰子掷出该数字的概率。  
-思路：求n个骰子总共能掷出的情况总和，以及符合条件的情况，从而求得概率  
-难点：1 骰子的个数是不确定的，如何确定符合条件的骰子情况.  
  
When we throw 2 classical dice (values on each side from 1 to 6) we have 36 (6 * 6) different results.

We want to know the probability of having the sum of the results equals to 11. For that result we have only the combination of 6 and 5. So we will have two events: {5, 6} and {6, 5}

So the probability for that result will be:

P(11, 2) = 2/(6*6) = 1/18    (The two is because we have 2 dice)
Now, we want to calculate the probability of having the sum equals to 8. The combinations for that result will be the following: {4,4}, {3,5}, {5,3}, {2,6}, {6,2} with a total of five combinations.

P(8, 2) = 5/36
Things may be more complicated if we have more dices and sum values higher.

We want to know the probability of having the sum equals to 8 but having 3 dice.

Now the combinations and corresponding events are:

{2,3,3}, {3,2,3}, {3,3,2}
{2,2,4}, {2,4,2}, {4,2,2}
{1,3,4}, {1,4,3}, {3,1,4}, {4,1,3}, {3,4,1}, {4,3,1}
{1,2,5}, {1,5,2}, {2,1,5}, {5,1,2}, {2,5,1}, {5,2,1}
{1,1,6}, {1,6,1}, {6,1,1}

A total amount of 21 different combinations

So the probability is:
P(8, 3) = 21/(6*6*6) = 0.09722222222222222
Summarizing the cases we have seen with a function that receives the two arguments

rolldice_sum_prob(11, 2) == 0.0555555555 # or 1/18

rolldice_sum_prob(8, 2) ==  0.13888888889# or 5/36

rolldice_sum_prob(8, 3) == 0.0972222222222  # or 7/72
And think why we have this result:

rolldice_sum_prob(22, 3) == 0
Create the function rolldice_sum_prob() for this calculation.

##### My solution
    def ans(sum_all, n):
        if n == 1:
            if 1 <= sum_all <= 6:
                return 1
            else:
                return 0
        else:
            return sum([ans(sum_all - i, n - 1) for i in range(1, 7)])

    def rolldice_sum_prob(x, n):
        return 1.0 * ans(x, n) / (6 ** n)

    print(rolldice_sum_prob(8,2))

##### Given solutions:
    def rolldice_sum_prob(sum_, dice_amount):
    
        import itertools
        import collections   
        
        sums  = [sum(list(i)) for i in itertools.product([1,2,3,4,5,6], repeat=dice_amount)]
        count = collections.Counter(sums)
        prob  = count[sum_]*1.0/(len(sums))
    
        return prob


##### Points  
1 迭代  