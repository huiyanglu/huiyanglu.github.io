---
layout:     post
title:      Directions Reduction
subtitle:   20181024_Codewars_5kyu_dirReduc
date:       2018-10-24
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Directions Reduction
#### Codewars Kata 41√
##### Description
https://www.codewars.com/kata/550f22f4d758534c1100025a
  
-简述：本题给定一个东南西北的方向路径为一个列表，要求简化该路径，若相邻两个方向为相反，则可以消去，若不相邻，则不可消。  
-思路：两两比较，若不相反，则加入新列表，若相等，则从列表中删除，新列表中最后留下的就是最终路径。  
-难点：1 如何正确运用新列表和旧列表中的项进行比较  
   
Create a function that differentiates a polynomial for a given value of x.
Your function will receive 2 arguments: a polynomial as a string, and a point to evaluate the equation as an integer.Once upon a time, on a way through the old wild west,…
… a man was given directions to go from one point to another. The directions were "NORTH", "SOUTH", "WEST", "EAST". Clearly "NORTH" and "SOUTH" are opposite, "WEST" and "EAST" too. Going to one direction and coming back the opposite direction is a needless effort. Since this is the wild west, with dreadfull weather and not much water, it's important to save yourself some energy, otherwise you might die of thirst!
  
How I crossed the desert the smart way.
The directions given to the man are, for example, the following:
  
["NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST"].
or
  
{ "NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST" };
or (haskell)
  
[North, South, South, East, West, North, West]
You can immediatly see that going "NORTH" and then "SOUTH" is not reasonable, better stay to the same place! So the task is to give to the man a simplified version of the plan. A better plan in this case is simply:
  
["WEST"]
or 
  
{ "WEST" }
or (haskell)
  
[West]
or (rust)
  
[WEST];
Other examples:
In ["NORTH", "SOUTH", "EAST", "WEST"], the direction "NORTH" + "SOUTH" is going north and coming back right away. What a waste of time! Better to do nothing.

The path becomes ["EAST", "WEST"], now "EAST" and "WEST" annihilate each other, therefore, the final result is [] (nil in Clojure).

In ["NORTH", "EAST", "WEST", "SOUTH", "WEST", "WEST"], "NORTH" and "SOUTH" are not directly opposite but they become directly opposite after the reduction of "EAST" and "WEST" so the whole path is reducible to ["WEST", "WEST"].  
  
##### Task
Write a function dirReduc which will take an array of strings and returns an array of strings with the needless directions removed (W<->E or S<->N side by side).  
   
The Haskell version takes a list of directions with data Direction = North | East | West | South. The Clojure version returns nil when the path is reduced to nothing. The Rust version takes a slice of enum Direction {NORTH, SOUTH, EAST, WEST}.  
  
##### Notes
Not all paths can be made simpler. The path ["NORTH", "WEST", "SOUTH", "EAST"] is not reducible. "NORTH" and "WEST", "WEST" and "SOUTH", "SOUTH" and "EAST" are not directly opposite of each other and can't become such. Hence the result path is itself : ["NORTH", "WEST", "SOUTH", "EAST"].

##### Given solution
    def dirReduc(arr):
        dir = " ".join(arr)
        dir2 = dir.replace("NORTH SOUTH",'').replace("SOUTH NORTH",'').replace("EAST WEST",'').replace("WEST EAST",'')
        dir3 = dir2.split()
        return dirReduc(dir3) if len(dir3) < len(arr) else dir3
---
    def dirReduc(arr):
        opposite = {'NORTH': 'SOUTH', 'EAST': 'WEST', 'SOUTH': 'NORTH', 'WEST': 'EAST'}
        rst = []
        for x in arr:
            if rst and (rst[-1] == opposite[x]):
                rst.pop()
            else:
                rst.append(x)
        return rst
  
##### Points:  
1 注意审题 必须是直接相邻的两个方向相对时，才能消去，否则不能消掉。
  
2 python中快速进行多个字符替换的方法  
要替换的字符数量不多时，可以直接链式replace()方法进行替换，效率高；
如果要替换的字符数量较多，则推荐在 for 循环中调用 replace() 进行替换。
  
  