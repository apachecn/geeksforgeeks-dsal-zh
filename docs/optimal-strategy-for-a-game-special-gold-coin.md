# 游戏的最优策略|特殊金币

> 原文:[https://www . geeksforgeeks . org/最优策略-游戏专用-金币/](https://www.geeksforgeeks.org/optimal-strategy-for-a-game-special-gold-coin/)

给定一排银币，其中有一枚特殊的金币。两个玩家玩游戏，每移动一次，玩家必须从排的左端或右端取出一枚硬币，取出特殊硬币的玩家赢得游戏。任务是找到游戏的赢家。

**示例:**

> **输入:**str = " GSSS "
> T3】输出:第一个
> 第一个玩家直接移除特殊金币。
> 
> **输入:** str = "SGS"
> **输出:**秒
> 无论第一个玩家移除哪枚硬币，特殊的
> 金币都会暴露出来并被第二个玩家移除。

**方法:**举几个例子可以观察到，如果银币的计数是奇数，那么第一个玩家赢得游戏，否则第二个玩家赢得游戏。在特殊情况下，当金币在角落时，无论银币的数量是多少，第一个玩家都将是赢家。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// winner of the game
string getWinner(string str, int len)
{

    // To store the count of silver coins
    int total = 0;

    if(str[0]=='G' ||str[len-1]=='G')
        return "First";
    else{
        for (int i = 0; i < len; i++) {

            // Update the position of
           // the gold coin
            if (str[i] == 'S') {
                total++;
            }
        }

        // First player will win the game
        if ((total % 2) == 1)
            return "First";
        return "Second";
    }
}

// Driver code
int main()
{
    string str = "GSSS";
    int len = str.length();

    cout << getWinner(str, len);

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
static String getWinner(String str, int len)
{

    // To store the count of silver coins
    int total = 0;
    for (int i = 0; i < len; i++)
    {

        // Update the position of
        // the gold coin
        if (str.charAt(i) == 'S')
        {
            total++;
        }
    }

    // First player will win the game
    if ((total % 2) == 1)
        return "First";
    return "Second";
}

// Driver code
public static void main(String []args)
{
    String str = "GSSS";
    int len = str.length();

    System.out.println(getWinner(str, len));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# winner of the game
def getWinner(string, length) :

    # To store the count of silver coins
    total = 0;
    for i in range(length) :

        # Update the position of
        # the gold coin
        if (string[i] == 'S') :
            total += 1;

    # First player will win the game
    if ((total % 2) == 1) :
        return "First";
    return "Second";

# Driver code
if __name__ == "__main__" :

    string = "GSSS";
    length = len(string);

    print(getWinner(string, length));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// winner of the game
static String getWinner(String str, int len)
{

    // To store the count of silver coins
    int total = 0;
    for (int i = 0; i < len; i++)
    {

        // Update the position of
        // the gold coin
        if (str[i] == 'S')
        {
            total++;
        }
    }

    // First player will win the game
    if ((total % 2) == 1)
        return "First";
    return "Second";
}

// Driver code
public static void Main(string []args)
{
    string str = "GSSS";
    int len = str.Length;

    Console.WriteLine(getWinner(str, len));
}
}

// This code is contributed by rrrtnx.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// winner of the game
function getWinner(str, len)
{

    // To store the count of silver coins
    var total = 0;

    if (str[0] == 'G' || str[len - 1] == 'G')
        return "First";
    else
    {
        for(var i = 0; i < len; i++)
        {
            // Update the position of
            // the gold coin
            if (str[i] == 'S')
            {
                total++;
            }
        }

        // First player will win the game
        if ((total % 2) == 1)
            return "First";

        return "Second";
    }
}

// Driver code
var str = "GSSS";
var len = str.length;

document.write(getWinner(str, len));

// This code is contributed by importantly

</script>
```

**Output:** 

```
First
```