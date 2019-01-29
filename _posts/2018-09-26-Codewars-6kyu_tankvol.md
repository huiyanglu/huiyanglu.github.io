---
layout:     post
title:      Tank Truck
subtitle:   20180926_Codewars_tankvol
date:       2018-09-26
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# Tank Truck
#### Codewars Kata 18√
##### Description
Link: [tankvol](https://www.codewars.com/kata/55f3da49e83ca1ddae0000ad)  

-简述：本题假设有一个油罐车，罐内剩余一些液体，给定液体高度、罐的横截面直径和罐的体积，求剩余液体的体积？  
-思路：数学方法直接求  
-难点：无  
  
To introduce the problem think to my neighbor who drives a tanker truck. The level indicator is down and he is worried because he does not know if he will be able to make deliveries. We put the truck on a horizontal ground and measured the height of the liquid in the tank.

Fortunately the tank is a perfect cylinder and the vertical walls on each end are flat. The height of the remaining liquid is h, the diameter of the cylinder is d, the total volume is vt (h, d, vt are positive or null integers). You can assume that h <= d.

Could you calculate the remaining volume of the liquid? Your function tankvol(h, d, vt) returns an integer which is the truncated result (e.g floor) of your float calculation.

##### Examples

tankvol(40,120,3500) should return 1021 (calculation gives about: 1021.26992027)

tankvol(60,120,3500) should return 1750

tankvol(80,120,3500) should return 2478 (calculation gives about: 2478.73007973)

Tank vertical section:

![avatar](http://i.imgur.com/wmt0U43.png)

##### My solution
    import math

    def tankvol(h, d, vt):
        theta = math.acos((d/2-h)/(d/2))*(180/math.pi)
        rec = math.sqrt((d/2)**2-(d/2-h)**2)*(d/2-h)
        fan = math.pi*((d/2)**2)*2*theta/360
        s = math.pi*((d/2)**2)
        result1 = fan - rec
        result2 = result1/s * vt
        return int(result2)

##### Given solutions:
    import math
    def tankvol(h, d, vt):
        r = d/2.0
        if h == r: return vt/2     # is the tank half full?
        half = h>r                 # is it more than half full
        h = d-h if half else h     # adjust h accordingly
        a = r-h                    # perpendicular intercept of the chord
        b = math.sqrt(r**2-a**2)   # half the chord
        t = 2*math.asin(b/r)       # the angle the chord sweeps out
        A = r**2*t/2 - b*a         # the area of the segment
        v = vt*A/(math.pi*r**2)    # the volume of the segment
        return int(vt-v) if half else int(v)
---
    import math
    def tankvol(h, d, vt):
        r=d/2
        theta=math.acos((r-h)/r)
        return int(vt*(theta-math.sin(theta)*(r-h)/r)/math.pi)

##### Points
1 这题就是纯数学解题，用到了math模块的一些函数包括sqrt asin acos pi等
  