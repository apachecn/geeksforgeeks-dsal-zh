# 使用比特操作的石头-纸-剪刀游戏的赢家

> 原文:[https://www . geeksforgeeks . org/石头中的赢家-纸中的赢家-剪刀-游戏-使用位操纵/](https://www.geeksforgeeks.org/winner-in-the-rock-paper-scissor-game-using-bit-manipulation/)

两名玩家正在玩[石头-纸-剪刀](https://en.wikipedia.org/wiki/Rock%E2%80%93paper%E2%80%93scissors)系列游戏。一个数组**arr【】【】】**所代表的 **N** 游戏一共玩了 10 局，其中**arr【I】【0】**是玩家一的招式，**arr【I】【1】**是玩家二在 **i <sup>th</sup>** 游戏中从设定**{“R”、“P”、“S”}**开始的招式。任务是找到每场比赛的获胜者。**注意**如果两个玩家选择同一个物品，游戏就是平局。
**例:**

> **输入:**arr[]= {“RS”、“SR”、“SP”、“PP”}
> **输出:**
> A
> B
> A
> DRAW
> T10】输入:arr[]= {“SS”、“RP”、“PS”}
> **输出:**
> Draw
> B
> B

**进场:**假设一号选手用比特 **1** 表示，二号选手用 **0** 表示。而且，让 Rock 用 **00** (十进制 0)、Paper 用 **01** (十进制 1)、剪刀用 **10** (十进制 2)来表示。
如果一号玩家选择岩石，则用 **100** 、
表示，同样的， **101** 表示纸是一号玩家选择的。
第一位表示玩家号，后两位供其选择。
**图案:**
100(十进制 4)(玩家 1，石头)，001(十进制 1)(玩家 2，纸)- >玩家 2 赢了(4-1 = 3)
101(十进制 5)(玩家 1，纸)，010(十进制 2)(玩家 2，剪刀)- >玩家 2 赢了(5-2 = 3)
110(十进制 6)(玩家 1，剪刀)，000(十进制 0)(玩家 2 000(十进制 0)(玩家 2，石头)—>玩家 1 赢了(5-0 = 5)
110(十进制 6)(玩家 1，剪刀)，001(十进制 1)(玩家 2，纸)—>玩家 1 赢了(6-1 = 5)
100(十进制 4)(玩家 1，石头)，010(十进制 2)(玩家 2，剪刀)—>玩家 1 赢了(4-2 = 2)
根据格局，如果 在其余的情况下，玩家一赢得游戏。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// winner of the game
string winner(string moves)
{
    map<char, int> data;
    data['R'] = 0;
    data['P'] = 1;
    data['S'] = 2;

    // Both the players chose to
    // play the same move
    if (moves[0] == moves[1]) {
        return "Draw";
    }

    // Player A wins the game
    if (((data[moves[0]] | 1 << (2))
         - (data[moves[1]] | 0 << (2)))
        % 3) {
        return "A";
    }

    return "B";
}

// Function to perform the queries
void performQueries(string arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << winner(arr[i]) << endl;
}

// Driver code
int main()
{
    string arr[] = { "RS", "SR", "SP", "PP" };
    int n = sizeof(arr) / sizeof(string);

    performQueries(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the
// winner of the game
static String winner(String moves)
{
    HashMap<Character,
            Integer> data = new HashMap<Character,
                                        Integer>();
    data.put('R', 0);
    data.put('P', 1);
    data.put('S', 2);

    // Both the players chose to
    // play the same move
    if (moves.charAt(0) == moves.charAt(1))
    {
        return "Draw";
    }

    // Player A wins the game
    if (((data.get(moves.charAt(0)) | 1 << (2)) -
         (data.get(moves.charAt(1)) | 0 << (2))) % 3 != 0)
    {
        return "A";
    }

    return "B";
}

// Function to perform the queries
static void performQueries(String arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(winner(arr[i]) + "\n");
}

// Driver code
public static void main(String[] args)
{
    String arr[] = { "RS", "SR", "SP", "PP" };
    int n = arr.length;

    performQueries(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# winner of the game
def winner(moves):
    data = dict()
    data['R'] = 0
    data['P'] = 1
    data['S'] = 2

    # Both the players chose to
    # play the same move
    if (moves[0] == moves[1]):
        return "Draw"

    # Player A wins the game
    if (((data[moves[0]] | 1 << (2)) -
         (data[moves[1]] | 0 << (2))) % 3):
        return "A"

    return "B"

# Function to perform the queries
def performQueries(arr,n):
    for i in range(n):
        print(winner(arr[i]))

# Driver code
arr = ["RS", "SR", "SP", "PP"]
n = len(arr)

performQueries(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the
// winner of the game
static String winner(String moves)
{
    Dictionary<char,
               int> data = new Dictionary<char,
                                          int>();
    data.Add('R', 0);
    data.Add('P', 1);
    data.Add('S', 2);

    // Both the players chose to
    // play the same move
    if (moves[0] == moves[1])
    {
        return "Draw";
    }

    // Player A wins the game
    if (((data[moves[0]] | 1 << (2)) -
         (data[moves[1]] | 0 << (2))) % 3 != 0)
    {
        return "A";
    }

    return "B";
}

// Function to perform the queries
static void performQueries(String []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(winner(arr[i]) + "\n");
}

// Driver code
public static void Main(String[] args)
{
    String []arr = { "RS", "SR", "SP", "PP" };
    int n = arr.Length;

    performQueries(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the
// winner of the game
function winner(moves)
{
    let data = new Map();
    data.set('R', 0);
    data.set('P', 1);
    data.set('S', 2);

    // Both the players chose to
    // play the same move
    if (moves[0] == moves[1])
    {
        return "Draw";
    }

    // Player A wins the game
    if (((data.get(moves[0]) | 1 << (2)) -
         (data.get(moves[1]) | 0 << (2))) % 3 != 0)
    {
        return "A";
    }

    return "B";
}

// Function to perform the queries   
function performQueries(arr,n)
{
    for (let i = 0; i < n; i++)
        document.write(winner(arr[i]) + "<br>");
}

// Driver code
let arr=["RS", "SR", "SP", "PP" ];
let  n = arr.length;
performQueries(arr, n);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
A
B
A
Draw
```