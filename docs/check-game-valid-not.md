# 检查游戏是否有效

> 原文:[https://www.geeksforgeeks.org/check-game-valid-not/](https://www.geeksforgeeks.org/check-game-valid-not/)

三名球员 P1、P2 和 P3 正在打一场比赛。但是一次只有两个玩家可以玩游戏，所以他们决定，一次两个玩家玩游戏，一个玩家观看。当一场比赛结束时，输掉比赛的一方成为下一场比赛的观众，而观看比赛的一方则与获胜者比赛。任何比赛都不能有平局。球员 P1 和 P2 将打第一场比赛。输入是玩了 n 个游戏的数量，在下一行中是 n 个游戏的赢家。

**示例:**

```
Input : 
No. of Games : 4
Winner of the Game Gi : 1 1 2 3 
Output : YES
Explanation : 
Game1 : P1 vs P2 : P1 wins
Game2 : P1 vs P3 : P1 wins
Game3 : P1 vs P2 : P2 wins
Game4 : P3 vs P2 : P3 wins
None of the winners were invalid

Input : 
No. of Games : 2
Winner of the Game Gi : 2 1 
Output : NO
Explanation : 
Game1 : P1 vs P2 : P2 wins
Game2 : P2 vs P3 : P1 wins (Invalid winner)
In Game2 P1 is spectator 
```

**进场:**
从 P1 和 P2 开始，继续比赛，同时从三名选手的总和即 6 中减去当前观众和获胜者，使输家成为新的观众。无效的条目将暂停该过程。

下面是上述方法的实现:

## C++

```
// C++ program to check if the game
// is valid
#include <bits/stdc++.h>
using namespace std;

string check_valid(int a[], int n)
{
    // starting with player P1 and P2
    // so making P3 spectator
    int spec = 3;
    for (int i = 0; i < n; i++) {

        // If spectator wins a game
        // then its not valid
        if (a[i] == spec) {
            return "Invalid";
        }

        // subtracting the current spectator
        // and winner from total sum 6 which
        // makes losing player spectator
        spec = 6 - a[i] - spec;
    }

    // None of the winner is found spectator.
    return "Valid";
}

// Driver program to test above functions
int main()
{
    int n = 4;
    int a[n] = {1, 1, 2, 3};
    cout << check_valid(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the game
// is valid
import java.io.*;

class GFG {

    static String check_valid(int a[], int n)
    {
        // starting with player P1 and P2
        // so making P3 spectator
        int spec = 3;

        for (int i = 0; i < n; i++) {

            // If spectator wins a game
            // then its not valid
            if (a[i] == spec) {
                return "Invalid";
            }

            // subtracting the current spectator
            // and winner from total sum 6 which
            // makes losing player spectator
            spec = 6 - a[i] - spec;
        }

        // None of the winner is found spectator.
        return "Valid";
    }

    // Driver program to test above functions
    public static void main (String[] args) {

        int a[] = {1, 1, 2, 3};
        int n = a.length;

        System.out.println(check_valid(a, n));

        }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 code to check if the game
# is valid

def check_valid( a , n ):

    # starting with player P1 and P2
    # so making P3 spectator
    spec = 3
    for i in range(n):

        # If spectator wins a game
        # then its not valid
        if a[i] == spec:
            return "Invalid"

        # subtracting the current spectator
        # and winner from total sum 6 which
        # makes losing player spectator
        spec = 6 - a[i] - spec

    # None of the winner is found spectator.
    return "Valid"

# Driver code to test above functions
n = 4
a = [1, 1, 2, 3]
print(check_valid(a, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to check if the game
// is valid
using System;

class GFG {

    static String check_valid(int []a, int n)
    {
        // starting with player P1 and P2
        // so making P3 spectator
        int spec = 3;

        for (int i = 0; i < n; i++) {

            // If spectator wins a game
            // then its not valid
            if (a[i] == spec) {
                return "Invalid";
            }

            // subtracting the current spectator
            // and winner from total sum 6 which
            // makes losing player spectator
            spec = 6 - a[i] - spec;
        }

        // None of the winner is found spectator.
        return "Valid";
    }

    // Driver program
    public static void Main ()
    {
        int []a = {1, 1, 2, 3};
        int n = a.Length;

        Console.WriteLine(check_valid(a, n));

        }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// the game is valid
function check_valid( $a, $n)
{
    // starting with player P1 and P2
    // so making P3 spectator
    $spec = 3;
    for ($i = 0; $i < $n; $i++)
    {

        // If spectator wins a game
        // then its not valid
        if ($a[$i] == $spec)
        {
            return "Invalid";
        }

        // subtracting the current
        // spectator and winner from
        // total sum 6 which makes
        // losing player spectator
        $spec = 6 - $a[$i] - $spec;
    }

    // None of the winner is
    // found spectator.
    return "Valid";
}

// Driver Code
$n = 4;
$a = array(1, 1, 2, 3);
echo check_valid($a, $n);

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>

// Javascript program to check if the game
// is valid
function check_valid(a, n)
{

    // Starting with player P1 and P2
    // so making P3 spectator
    let spec = 3;

    for(let i = 0; i < n; i++)
    {

        // If spectator wins a game
        // then its not valid
        if (a[i] == spec)
        {
            return "Invalid";
        }

        // Subtracting the current spectator
        // and winner from total sum 6 which
        // makes losing player spectator
        spec = 6 - a[i] - spec;
    }

    // None of the winner is found spectator.
    return "Valid";
}

// Driver code
let a = [ 1, 1, 2, 3 ];
let n = a.length;

document.write(check_valid(a, n));

// This code is contributed by sanjoy_62

</script>
```

**输出:**

```
Valid
```