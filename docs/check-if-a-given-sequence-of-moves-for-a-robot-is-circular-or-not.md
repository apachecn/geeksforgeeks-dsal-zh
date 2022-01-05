# 检查机器人的给定移动顺序是否为圆形

> 原文:[https://www . geesforgeks . org/检查机器人的给定移动顺序是否为圆形/](https://www.geeksforgeeks.org/check-if-a-given-sequence-of-moves-for-a-robot-is-circular-or-not/)

给定一个机器人的移动序列，检查该序列是否是循环的。如果机器人的第一个和最后一个位置相同，则移动序列是循环的。移动可以发生在以下情况之一。

```
  G - Go one unit
  L - Turn left
  R - Turn right 
```

示例:

```
Input: path[] = "GLGLGLG"
Output: Given sequence of moves is circular 

Input: path[] = "GLLG"
Output: Given sequence of moves is circular 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/does-robot-moves-circular0414/1)

想法是考虑起始位置为(0，0)，方向为东(我们可以为这些选择任何值)。如果在给定的移动序列之后，我们回到(0，0)，那么给定的序列是循环的，否则不是。

```
           N
           |
           |
   W -------------- E
           |
           |
           S 
```

移动“G”根据以下规则改变 x 或 y。
a)如果当前方向为北，则‘G’递增 y 且不改变 x.
b)如果当前方向为东，则‘G’递增 x 且不改变 y.
c)如果当前方向为南，则‘G’递减 y 且不改变 x.
d)如果当前方向为西，则‘G’递减 x 且不改变 y.
移动“L”和“R”，不改变 x 和 y 坐标，它们仅根据以下规则改变方向
a)如果当前方向为北，则“L”变为西，“R”变为东
b)如果当前方向为东，则“L”变为北，“R”变为南
c)如果当前方向为南，则“L”变为东，“R”变为西
d)如果当前方向为西，则“L”变为南，“R”变为北。
以下是上述思路的实现:

## C++

```
// A c++ program to check if the given path for a robot is circular or not
#include<iostream>
using namespace std;

// Macros for East, North, South and West
#define N 0
#define E 1
#define S 2
#define W 3

// This function returns true if the given path is circular, else false
bool isCircular(char path[])
{
  // Initialize starting point for robot as (0, 0) and starting
  // direction as N North
  int x = 0, y = 0;
  int dir = N;

  // Traverse the path given for robot
  for (int i=0; path[i]; i++)
  {
      // Find current move
      char move = path[i];

      // If move is left or right, then change direction
      if (move == 'R')
        dir = (dir + 1)%4;
      else if (move == 'L')
        dir = (4 + dir - 1)%4;

      // If move is Go, then change  x or y according to
      // current direction
      else // if (move == 'G')
      {
         if (dir == N)
            y++;
         else if (dir == E)
            x++;
         else if (dir == S)
            y--;
         else // dir == W
            x--;
      }
  }

   // If robot comes back to (0, 0), then path is cyclic
  return (x == 0 && y == 0);
}

// Driver program
int main()
{
    char path[] = "GLGLGLG";
    if (isCircular(path))
      cout << "Given sequence of moves is circular";
    else
      cout << "Given sequence of moves is NOT circular";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Write Java code here
// A Java program to check if
// the given path for a robot
// is circular or not
class GFG {

// Macros for East, North, South and West

// This function returns true if
// the given path is circular,
// else false
static boolean isCircular(char path[])
{
  // Initialize starting
  // point for robot as
  // (0, 0) and starting
  // direction as N North
  int x = 0, y = 0;
  int dir = 0;

  // Traverse the path given for robot
  for (int i=0; i < path.length; i++)
  {
      // Find current move
      char move = path[i];

      // If move is left or
      // right, then change direction
      if (move == 'R')
        dir = (dir + 1)%4;
      else if (move == 'L')
        dir = (4 + dir - 1) % 4;

      // If move is Go, then
      // change  x or y according to
      // current direction
      else // if (move == 'G')
      {
         if (dir == 0)
            y++;
         else if (dir == 1)
            x++;
         else if (dir == 2)
            y--;
         else // dir == 3
            x--;
      }
  }

   // If robot comes back to
   // (0, 0), then path is cyclic
  return (x == 0 && y == 0);
}

// Driver program
public static void main(String[] args)
{
    String path_ = "GLGLGLG";
    char path[] = path_.toCharArray();

    if (isCircular(path))
      System.out.println("Given sequence" +
      " of moves is circular");
    else
      System.out.println("Given sequence" +
      " of moves is NOT circular");
}
}

// This code is contributed by prerna saini.
```

## 计算机编程语言

```
# Python program to check if the given path for a robot is circular
# or not
N = 0
E = 1
S = 2
W = 3

# This function returns true if the given path is circular,
# else false
def isCircular(path):

    # Initialize starting point for robot as (0, 0) and starting
    # direction as N North
    x = 0
    y = 0
    dir = N

    # Traverse the path given for robot
    for i in xrange(len(path)):

        # Find current move
        move = path[i]

        # If move is left or right, then change direction
        if move == 'R':
            dir = (dir + 1)%4
        elif move == 'L':
            dir = (4 + dir - 1)%4

        # If move is Go, then change x or y according to
        # current direction
        else:    # if move == 'G'
            if dir == N:
                y += 1
            elif dir == E:
                x += 1
            elif dir == S:
                y -= 1
            else:
                x -= 1

    return (x == 0 and y == 0)

# Driver program
path = "GLGLGLG"
if isCircular(path):
    print "Given sequence of moves is circular"
else:
    print "Given sequence of moves is NOT circular"

# This code is contributed by BHAVYA JAIN
```

## C#

```
// A C# program to check if
// the given path for a robot
// is circular or not
using System;

class GFG {

// Macros for East, North, South and West

// This function returns true if
// the given path is circular,
// else false
static bool isCircular(string path)
{

// Initialize starting
// point for robot as
// (0, 0) and starting
// direction as N North
int x = 0, y = 0;
int dir = 0;

// Traverse the path
// given for robot
for (int i = 0; i < path.Length; i++)
{

    // Find current move
    char move = path[i];

    // If move is left or
    // right, then change direction
    if (move == 'R')
        dir = (dir + 1) % 4;
    else if (move == 'L')
        dir = (4 + dir - 1) % 4;

    // If move is Go, then
    // change x or y according to
    // current direction
    // if (move == 'G')
    else
    {
        if (dir == 0)
            y++;
        else if (dir == 1)
            x++;
        else if (dir == 2)
            y--;
        else // dir == 3
            x--;
    }
}

// If robot comes back to
// (0, 0), then path is cyclic
return (x == 0 && y == 0);
}

// Driver Code
public static void Main(String[] args)
{
    string path = "GLGLGLG";

     if (isCircular(path))
      Console.WriteLine("Given sequence of moves is circular");
     else
      Console.WriteLine("Given sequence of moves is NOT circular");
}
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>
    // A Javascript program to check if
    // the given path for a robot
    // is circular or not

    // Macros for East, North, South and West

    // This function returns true if
    // the given path is circular,
    // else false
    function isCircular(path)
    {

        // Initialize starting
        // point for robot as
        // (0, 0) and starting
        // direction as N North
        let x = 0, y = 0;
        let dir = 0;

        // Traverse the path
        // given for robot
        for (let i = 0; i < path.length; i++)
        {

            // Find current move
            let move = path[i];

            // If move is left or
            // right, then change direction
            if (move == 'R')
                dir = (dir + 1) % 4;
            else if (move == 'L')
                dir = (4 + dir - 1) % 4;

            // If move is Go, then
            // change x or y according to
            // current direction
            // if (move == 'G')
            else
            {
                if (dir == 0)
                    y++;
                else if (dir == 1)
                    x++;
                else if (dir == 2)
                    y--;
                else // dir == 3
                    x--;
            }
        }

        // If robot comes back to
        // (0, 0), then path is cyclic
        return (x == 0 && y == 0);
    }

    let path = "GLGLGLG";

    if (isCircular(path))
      document.write("Given sequence of moves is circular");
    else
      document.write("Given sequence of moves is NOT circular");

    // This code is contributed by decode2207.
</script>
```

输出:

```
Given sequence of moves is circular
```

时间复杂度:O(n)，其中 n 是给定序列中的移动次数。

本文由 **Kaustubh Deshmukh** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。