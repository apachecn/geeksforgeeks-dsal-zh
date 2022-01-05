# 尼姆的一个修改游戏

> 原文:[https://www.geeksforgeeks.org/a-modified-game-of-nim/](https://www.geeksforgeeks.org/a-modified-game-of-nim/)

给定一个整数数组 **arr[]** ，两个玩家 **A** 和 **B** 正在玩一个游戏，其中 **A** 可以从数组中移除任意数量的非零元素，这些元素是**的 3 的倍数**。同样的， **B** 可以去掉 5 的**倍数**。不能移除任何元素的玩家将输掉游戏。任务是找到游戏的赢家，如果 **A** 先开始，两者都发挥最佳。
**举例:**

> **输入:** arr[] = {1，2，3，5，6}
> **输出:** A
> 3 和 6 是 A 可以移除的元素。
> 5 是 B 唯一可以去除的元素。
> 甲可以在第一次移动中移除 3，然后乙必须移除 5。在下一回合中，A 将移除 6，B 将没有更多的动作可做。
> **输入:** arr[] = {3，5，15，20，6，9}
> **输出:** A

**方法:**在 **movesA** 中存储只能被 3 整除的元素计数，在 **movesB** 中存储只能被 5 整除的元素计数，在 **movesBoth** 中存储能被两者整除的元素计数。现在，

*   如果 **movesBoth = 0** ，那么两个玩家只能移除可被各自数字整除的元素，并且 **A** 只有在 **movesA > movesB** 时才会赢得游戏。
*   如果**移动了第> 0** 个元素，那么为了达到最佳的游戏效果， **A** 将移除所有可以被 **3** 和 **5** 整除的元素，这样 **B** 就没有可以从普通元素中移除的元素了，那么 **A** 只有在**移动了 sA + 1 >移动了 sB** 的情况下才会成为赢家

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the winner of the game
string getWinner(int arr[], int n)
{
    int movesA = 0, movesB = 0, movesBoth = 0;

    for (int i = 0; i < n; i++) {

        // Increment common moves
        if (arr[i] % 3 == 0 && arr[i] % 5 == 0)
            movesBoth++;

        // Increment A's moves
        else if (arr[i] % 3 == 0)
            movesA++;

        // Increment B's moves
        else if (arr[i] % 5 == 0)
            movesB++;
    }

    // If there are no common moves
    if (movesBoth == 0) {
        if (movesA > movesB)
            return "A";
        return "B";
    }

    // 1 is added because A can remove all the elements
    // that are part of the common moves in a single move
    if (movesA + 1 > movesB)
        return "A";
    return "B";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << getWinner(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

    // Function to return the winner of the game
    static String getWinner(int arr[], int n)
    {
        int movesA = 0, movesB = 0, movesBoth = 0;

        for (int i = 0; i < n; i++)
        {

            // Increment common moves
            if (arr[i] % 3 == 0 && arr[i] % 5 == 0)
                movesBoth++;

            // Increment A's moves
            else if (arr[i] % 3 == 0)
                movesA++;

            // Increment B's moves
            else if (arr[i] % 5 == 0)
                movesB++;
        }

        // If there are no common moves
        if (movesBoth == 0)
        {
            if (movesA > movesB)
                return "A";
            return "B";
        }

        // 1 is added because A can remove
        // all the elements that are part
        // of the common moves in a single move
        if (movesA + 1 > movesB)
            return "A";
        return "B";
    }

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 1, 2, 3, 5, 6 };
        int n = arr.length;
        System.out.println(getWinner(arr, n));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the winner of the game
def getWinner(arr, n):

    movesA, movesB, movesBoth = 0, 0, 0
    for i in range(0, n):

        # Increment common moves
        if arr[i] % 3 == 0 and arr[i] % 5 == 0:
            movesBoth += 1

        # Increment A's moves
        elif arr[i] % 3 == 0:
            movesA += 1

        # Increment B's moves
        elif arr[i] % 5 == 0:
            movesB += 1

    # If there are no common moves
    if movesBoth == 0:
        if movesA > movesB:
            return "A"
        return "B"

    # 1 is added because A can
    # remove all the elements
    # that are part of the common
    # moves in a single move
    if movesA + 1 > movesB:
        return "A"
    return "B"

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 3, 5, 6]
    n = len(arr)
    print(getWinner(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the winner of the game
    static String getWinner(int []arr, int n)
    {
        int movesA = 0, movesB = 0, movesBoth = 0;

        for (int i = 0; i < n; i++)
        {

            // Increment common moves
            if (arr[i] % 3 == 0 && arr[i] % 5 == 0)
                movesBoth++;

            // Increment A's moves
            else if (arr[i] % 3 == 0)
                movesA++;

            // Increment B's moves
            else if (arr[i] % 5 == 0)
                movesB++;
        }

        // If there are no common moves
        if (movesBoth == 0)
        {
            if (movesA > movesB)
                return "A";
            return "B";
        }

        // 1 is added because A can remove
        // all the elements that are part
        // of the common moves in a single move
        if (movesA + 1 > movesB)
            return "A";
        return "B";
    }

    // Driver code
    public static void Main(String []args)
    {

        int []arr = { 1, 2, 3, 5, 6 };
        int n = arr.Length;
        Console.WriteLine(getWinner(arr, n));
    }
}

// This code is contributed by
// Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the winner of the game
function getWinner($arr, $n)
{
    $movesA = 0;
    $movesB = 0;
    $movesBoth = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Increment common moves
        if ($arr[$i] % 3 == 0 && $arr[$i] % 5 == 0)
            $movesBoth++;

        // Increment A's moves
        else if ($arr[$i] % 3 == 0)
            $movesA++;

        // Increment B's moves
        else if ($arr[$i] % 5 == 0)
            $movesB++;
    }

    // If there are no common moves
    if ($movesBoth == 0)
    {
        if ($movesA > $movesB)
            return "A";
        return "B";
    }

    // 1 is added because A can remove all the elements
    // that are part of the common moves in a single move
    if ($movesA + 1 > $movesB)
        return "A";
    return "B";
}

    // Driver code
    $arr = array( 1, 2, 3, 5, 6 );
    $n = sizeof($arr) / sizeof($arr[0]);
    echo getWinner($arr, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the winner of the game
function getWinner(arr, n)
{
    let movesA = 0, movesB = 0, movesBoth = 0;

    for (let i = 0; i < n; i++) {

        // Increment common moves
        if (arr[i] % 3 == 0 && arr[i] % 5 == 0)
            movesBoth++;

        // Increment A's moves
        else if (arr[i] % 3 == 0)
            movesA++;

        // Increment B's moves
        else if (arr[i] % 5 == 0)
            movesB++;
    }

    // If there are no common moves
    if (movesBoth == 0) {
        if (movesA > movesB)
            return "A";
        return "B";
    }

    // 1 is added because A can
    // remove all the elements
    // that are part of the common
    // moves in a single move
    if (movesA + 1 > movesB)
        return "A";
    return "B";
}

// Driver code
    let arr = [ 1, 2, 3, 5, 6 ];
    let n = arr.length;
    document.write(getWinner(arr, n));

</script>
```

**Output:** 

```
A
```