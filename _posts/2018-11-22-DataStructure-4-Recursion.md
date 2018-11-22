---
layout:     post
title:      Data Structure - 4.Recursion
subtitle:   20181122_dataStructure_4.6to4.10
date:       2018-11-22
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - DataStructure
---
# Data Structure - 4.Recursion
（初稿 待修改添加

#### 4.6

When a function is called in Python, a stack frame is allocated to handle the local variables of the function. When the function returns, the return value is left on top of the stack for the calling function to access.

In our list summing example, you can think of the return value on the stack taking the place of an accumulator variable.

#### 4.7  Visualizing Recursion
spiral 螺旋
fractal 碎片形 分形
magnification 放大
twig 枝条
symmetrically 对称地

Python’s turtle graphics module called turtle

You can create a turtle and the turtle can move forward, backward, turn left, turn right, etc. The turtle can have its tail up or down. 

myWin.exitonclick(), this is a handy little method of the window that puts the turtle into a wait mode until you click inside the window, after which the program cleans up and exits.
---
The definition of a fractal is that when you look at it the fractal has the same basic shape no matter how much you magnify it. 

Using this idea we could say that a tree is a trunk, with a smaller tree going off to the right and another smaller tree going off to the left. If you think of this definition recursively it means that we will apply the recursive definition of a tree to both of the smaller left and right trees.

#### 4.8 Sierpinski triangle

arbitrarily 任意地

We will see that the base case is set arbitrarily as the number of times we want to divide the triangle into pieces. Sometimes we call this number the “degree” of the fractal. 

getMid takes as arguments two endpoints and returns the point halfway between them.

You can learn all the details of the methods available in the turtle module by using help('turtle') from the Python prompt.

#### 4.10

crumble 瓦解 
vanish 消失
the legend said 传说

#### 4.11 Exploring a Maze

In this algorithm, there are four base cases to consider:
1. The turtle has run into a wall. Since the square is occupied by a wall no further exploration can take place.
2. The turtle has found a square that has already been explored. We do not want to continue exploring from this position or we will get into a loop.
3. We have found an outside edge, not occupied by a wall. In other words we have found an exit from the maze.
4. We have explored a square unsuccessfully in all four directions.
---
* __init__ Reads in a data file representing a maze, initializes the internal representation of the maze, and finds the starting position for the turtle.
* drawMaze Draws the maze in a window on the screen.
* updatePosition Updates the internal representation of the maze and changes the position of the turtle in the window.
* isExit Checks to see if the current position is an exit from the maze.
---
def searchForm()
Notice that this function takes three parameters: a maze object, the starting row, and the starting column. This is important because as a recursive function the search logically starts again with each recursive call.