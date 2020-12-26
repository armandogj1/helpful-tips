---
title: Diagramming
nav_exclude: true
---

# Diagramming

- Though it may be tricky to do so on a zoom setting while screen sharing, diagramming is an important step in the interview process. Having an example up where you can iterate through each step may facilitate finding a solution. And also make possible pitfalls apparent.
- Here are lengthy examples of diagrams using a text editor. Some values could be simply updated as you iterate through the steps instead of repeating the whole:

## Container with the Most water

- Find the area of a container which can hold the most water, where the vertical side are the values in the array and the base is the distance between the sides.

```javascript
----------- [1, 8, 6, 2, 5, 4, 8, 3, 7]
i---------=  0
j---------=  0  1  2  3  4  5  6  7  8
width-----=  0  1  2  3  4  5  6  7  8
minHeight-=  1  1  1  1  1  1  1  1  1
currArea--=  0  1  2  3  4  5  6  7  8
maxArea---=  0  1  2  3  4  5  6  7  8

i---------=     1
j---------=     1  2  3  4  5  6  7  8
width-----=     0  1  2  3  4  5  6  7
minHeight-=     8  6  2  5  4  8  3  7
currArea--=     0  6  4 15 16 40 18 49
maxArea---=  8  8  8  8 15 16 40 40 49

i---------=        2
j---------=        2  3  4  5  6  7  8
width-----=        0  1  2  3  4  5  6
minHeight-=        6  2  5  4  6  3  6
currArea--=        0  2 10 12 24 15 36
maxArea---= 49 49 49 49 49 49 49 49 49

	//...
```

## Best Time To Buy And Sell Stock

- Iterating over an array looking for min value and calculate the max profit.

  ### [7, 1, 5, 3, 6, 4]

  | price[i]  | 7   | 1   | 5   | 3   | 6   | 4   |
  | --------- | --- | --- | --- | --- | --- | --- |
  | i         | 0   | 1   | 2   | 3   | 4   | 5   |
  | minPrice  | 7   | 1   | 1   | 1   | 1   | 1   |
  | maxProfit | 0   | 0   | 4   | 4   | 5   | 5   |

## Longest Substring Without Repeating Characters

- Iterate over the string, track the chars with storing the position of the following char.

```javascript
// step 0
s.      =     "a  b  c  a  b  c  b  b"
i       =      0
start   =      0
charObj =     {a: 1}        // store the index of the next char
maxSub  =      i - start + 1 -> 1

// step 1
s       =    "a  b  c  a  b  c  b  b"
i       =     0  1
start.  =     0  0
charObj =     {a:1, b:2}
maxSub. =     i - start + 1 -> 2

// step 2
s       =   "a  b  c  a  b  c  b  b"
i       =    0  1  2
start.  =    0  0  0
charObj =   {a:1, b:2, c:3}
maxSub. =   i - start + 1 -> 3

// step 3
s.      =   "a  b  c  a  b  c  b  b"
i       =    0  1  2  3
start   =    0  0  0  1      // we get it from charObj[s[i]]
charObj =   {a:4, b:2, c:3}  // change 'a' to point to next char
maxSub  =   i - start + 1 -> 3

// step 4
s      =   "a  b  c  a  b  c  b  b"
i      =    0  1  2  3  4
start  =    0  0  0  1  2
charObj=   {a:4, b:5, c:3}
maxSub =   i - start + 1 -> 3

// step 5
s=         "a  b  c  a  b  c  b  b"
i    =      0  1  2  3  4  5
start=      0  0  0  1  2  3
charObj=  {a:4, b:5, c:6}
maxSub=   i - start + 1 -> 3

// step 6
s=         "a  b  c  a  b  c  b  b"
i    =      0  1  2  3  4  5  6
start=      0  0  0  1  2  3  5
charObj=  {a:4, b:7, c:6}
maxSub=   i - start + 1 -> 2 < maxSub // not update

// step 7
s=         "a  b  c  a  b  c  b  b"
i    =      0  1  2  3  4  5  6  7
start=      0  0  0  1  2  3  5  7
charObj=  {a:4, b:8, c:6}
maxSub=   i - start + 1 -> 1 < maxSub // not update
```
