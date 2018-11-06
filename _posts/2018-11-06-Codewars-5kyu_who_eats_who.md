---
layout:     post
title:      The Hunger Games - Zoo Disaster!
subtitle:   20181106_Codewars_5kyu_who_eats_who
date:       2018-11-06
author:     Huiyang_Lu
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Python
    - Codewars
---
# The Hunger Games - Zoo Disaster!
#### Codewars Kata 46√
##### Description
https://www.codewars.com/kata/5902bc7aba39542b4a00003d/solutions/python
Story
A freak power outage at the zoo has caused all of the electric cage doors to malfunction and swing open...

All the animals are out and some of them are eating each other!

It's a Zoo Disaster!
Here is a list of zoo animals, and what they can eat

antelope eats grass
big-fish eats little-fish
bug eats leaves
bear eats big-fish
bear eats bug
bear eats chicken
bear eats cow
bear eats leaves
bear eats sheep
chicken eats bug
cow eats grass
fox eats chicken
fox eats sheep
giraffe eats leaves
lion eats antelope
lion eats cow
panda eats leaves
sheep eats grass

##### Kata Task
INPUT
A comma-separated string representing all the things at the zoo

TASK
Figure out who eats who until no more eating is possible.

OUTPUT
A list of strings (refer to the example below) where:

The first element is the initial zoo (same as INPUT)
The last element is a comma-separated string of what the zoo looks like when all the eating has finished
All other elements (2nd to last-1) are of the form X eats Y describing what happened
Notes
Animals can only eat things beside them

Animals always eat to their LEFT before eating to their RIGHT

Always the LEFTMOST animal capable of eating will eat before any others

Any other things you may find at the zoo (which are not listed above) do not eat anything and are not edible

##### Example
INPUT	
"fox,bug,chicken,grass,sheep"
1	fox can't eat bug	
"fox,bug,chicken,grass,sheep"
2	bug can't eat anything	
"fox,bug,chicken,grass,sheep"
3	chicken eats bug	
"fox,chicken,grass,sheep"
4	fox eats chicken	
"fox,grass,sheep"
5	fox can't eat grass	
"fox,grass,sheep"
6	grass can't eat anything	
"fox,grass,sheep"
7	sheep eats grass	
"fox,sheep"
8	fox eats sheep	
"fox"
OUTPUT	
["fox,bug,chicken,grass,sheep", "chicken eats bug", "fox eats chicken", "sheep eats grass", "fox eats sheep", "fox"]
  
##### My solution
    def who_eats_who(zoo):
        a = [['grass','antelope'],
        ['little-fish', 'big-fish'],
        ['leaves','bug'],
        ['big-fish', 'bear'],
        ['bug', 'bear'],
        ['chicken','bear'],
        ['cow','bear'],
        ['leaves','bear'],
        ['sheep','bear'],
        ['bug','chicken'],
        ['grass', 'cow'],
        ['chicken', 'fox'],
        ['sheep','fox'],
        ['leaves','giraffe'],
        ['antelope','lion'],
        ['cow', 'lion'],
        ['leaves','panda'],
        ['grass','sheep']]
        init = zoo.split(',')
        rst = []
        j = 0
        while j<len(init):
            if j > 0 and [init[j-1],init[j]] in a:
                rst.append(init[j]+' eats '+init[j-1])
                init.pop(j-1) # 不可以用remove，因为remove删除的是第一个该字符，pop对应索引
                j = 0
            elif j<len(init)-1 and [init[j+1],init[j]] in a:
                rst.append(init[j] + ' eats ' + init[j + 1])
                init.pop(j+1)
                j = 0
            else:
                j+=1
        return [zoo]+rst + [",".join(init)]

    print(who_eats_who('cow,cow,sheep,bug,cow,busker,grass,little-fish,lion,sheep,fox'))

ps: 一开始用了几个for循环，果不其然超时了…有想过用dict，不太会写，直接用while+判断也还可以。pop和remove的区别要注意，一开始用remove一直报错，原来是random test里面字符有重复出现的，所以不能用remove.

##### Given solutions
    EATERS = {"antelope": {"grass"},
              "big-fish": {"little-fish"},
              "bug":      {"leaves"},
              "bear":     {"big-fish", "bug", "chicken", "cow", "leaves", "sheep"},
              "chicken":  {"bug"},
              "cow":      {"grass"},
              "fox":      {"chicken", "sheep"},
              "giraffe":  {"leaves"},
              "lion":     {"antelope", "cow"},
              "panda":    {"leaves"},
              "sheep":    {"grass"}}

    def who_eats_who(zoo):
        
        ansLst, zooLst, n = [zoo], zoo.split(","), 0
        
        while n < len(zooLst):
            while n > 0 and zooLst[n-1] in EATERS.get(zooLst[n], set()):                            # Eats on its left
                ansLst.append("{} eats {}".format(zooLst[n], zooLst.pop(n-1)))
                n -= 2
            
            while n >= 0 and n != len(zooLst)-1 and zooLst[n+1] in EATERS.get(zooLst[n], set()):    # Eats on its right
                ansLst.append("{} eats {}".format(zooLst[n], zooLst.pop(n+1)))
            
            n += 1     # Nothing to eat, step forward
            
        return ansLst + [','.join(zooLst)]

---
    zoo_relations = {
    "antelope": ["grass"],
    "big-fish": ["little-fish"],
    "bug": ["leaves"],
    "bear": ["big-fish", "bug", "chicken", "cow", "leaves", "sheep"],
    "chicken": ["bug"],
    "cow": ["grass"],
    "fox": ["chicken", "sheep"],
    "giraffe": ["leaves"],
    "lion": ["antelope", "cow"],
    "panda": ["leaves"],
    "sheep": ["grass"],
    }
    
    def who_eats_who(zoo):
        animals = zoo.split(",")
        idx = 0
        res = [zoo]
        
        while True:
            if len(animals) == 1 or idx >= len(animals):
                res.append(",".join(animals))
                break

            if idx-1 >= 0 and animals[idx-1] in zoo_relations.get(animals[idx], []):
                res.append("{} eats {}".format(animals[idx], animals[idx-1]))
                del animals[idx-1]
                idx = 0
            elif idx+1 < len(animals) and animals[idx+1] in zoo_relations.get(animals[idx], []):
                res.append("{} eats {}".format(animals[idx], animals[idx+1]))
                del animals[idx+1]
                idx = 0
            else:
                idx += 1

        return res