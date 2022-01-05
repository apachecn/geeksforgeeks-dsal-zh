# 在 NIM 游戏中以最佳方式玩第一步的方式数

> 原文:[https://www . geeksforgeeks . org/游戏方式数-第一次移动-最佳尼姆游戏/](https://www.geeksforgeeks.org/number-of-ways-for-playing-first-move-optimally-in-a-nim-game/)

两名玩家 **A** 和 **B** 正在互相玩 [NIM 游戏](https://www.geeksforgeeks.org/combinatorial-game-theory-set-2-game-nim/)。两者都发挥得很好。玩家 **A** 开始游戏。任务是为 **A** 找到 **1 <sup>st</sup>** 招式的玩法数量，确保 **A** 有获胜策略，如果可能的话，打印 **-1** 。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** -1
> 无论 A 的打法有多优化，他都没有获胜策略。
> **输入:** arr[] = {2，4，5}
> **输出:** 1
> 为了打出最优，A 会从第一堆中挑一枚硬币，这是唯一的最优棋。

**进场:**

1.  首先通过对所有数组元素进行异或运算来检查谁将赢得游戏。如果异或为零，那么无论 A 玩得多好，A 总是会输。如果异或为非零，则转到步骤 2。
2.  我们将检查每一堆，如果我们可以从那堆中取出一些硬币，这样在这一步之后，所有数组元素的异或将为零。因此，对于所有的堆，我们将逐一对数组的所有剩余元素进行异或运算，并将检查异或值是否大于堆中的硬币数量。如果是这样的话，就不可能用这堆玩第一招了，因为我们一招只能从堆里取出硬币，不能加硬币。否则，我们将增加方法的数量。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to return the XOR
// of all the array elements
int xorArray(int arr[], int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];

    return res;
}

// Function to return the count of ways
// to play the first move optimally
int getTotalWays(int arr[], int n)
{

    // XOR of all the array elements
    int xorArr = xorArray(arr, n);

    // The player making the first move
    // can't win the game no matter
    // how optimally he plays
    if (xorArr == 0)
        return -1;

    // Initialised with zero
    int numberOfWays = 0;

    for (int i = 0; i < n; i++) {

        // requiredCoins is the number of coins
        // the player making the move must leave
        // in the current pile in order to play optimally
        int requiredCoins = xorArr ^ arr[i];

        // If requiredCoins is less than the current
        // amount of coins in the current pile
        // then only the player can make an optimal move
        if (requiredCoins < arr[i])
            numberOfWays++;
    }

    return numberOfWays;
}

// Driver code
int main()
{

    // Coins in each pile
    int arr[] = { 3, 4, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getTotalWays(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Utility function to return the XOR
// of all the array elements
static int xorArray(int arr[], int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];

    return res;
}

// Function to return the count of ways
// to play the first move optimally
static int getTotalWays(int arr[], int n)
{

    // XOR of all the array elements
    int xorArr = xorArray(arr, n);

    // The player making the first move
    // can't win the game no matter
    // how optimally he plays
    if (xorArr == 0)
        return -1;

    // Initialised with zero
    int numberOfWays = 0;

    for (int i = 0; i < n; i++)
    {

        // requiredCoins is the number of coins
        // the player making the move must leave
        // in the current pile in order to play optimally
        int requiredCoins = xorArr ^ arr[i];

        // If requiredCoins is less than the current
        // amount of coins in the current pile
        // then only the player can make an optimal move
        if (requiredCoins < arr[i])
            numberOfWays++;
    }
    return numberOfWays;
}

// Driver code
public static void main(String[] args)
{

    // Coins in each pile
    int arr[] = { 3, 4, 4, 2 };
    int n =arr.length;

    System.out.println(getTotalWays(arr, n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to return the
# XOR of all the array elements
def xorArray(arr, n):

    res = 0
    for i in range(0, n):
        res = res ^ arr[i]

    return res

# Function to return the count of ways
# to play the first move optimally
def getTotalWays(arr, n):

    # XOR of all the array elements
    xorArr = xorArray(arr, n)

    # The player making the first move
    # can't win the game no matter
    # how optimally he plays
    if xorArr == 0:
        return -1

    # Initialised with zero
    numberOfWays = 0

    for i in range(0, n):

        # requiredCoins is the number of coins the
        # player making the move must leave in the
        # current pile in order to play optimally
        requiredCoins = xorArr ^ arr[i]

        # If requiredCoins is less than the current
        # amount of coins in the current pile
        # then only the player can make an optimal move
        if requiredCoins < arr[i]:
            numberOfWays += 1

    return numberOfWays

# Driver code
if __name__ == "__main__":

    # Coins in each pile
    arr = [3, 4, 4, 2]
    n = len(arr)

    print(getTotalWays(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to return the XOR
// of all the array elements
static int xorArray(int []arr, int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];

    return res;
}

// Function to return the count of ways
// to play the first move optimally
static int getTotalWays(int []arr, int n)
{

    // XOR of all the array elements
    int xorArr = xorArray(arr, n);

    // The player making the first move
    // can't win the game no matter
    // how optimally he plays
    if (xorArr == 0)
        return -1;

    // Initialised with zero
    int numberOfWays = 0;

    for (int i = 0; i < n; i++)
    {

        // requiredCoins is the number of coins
        // the player making the move must leave
        // in the current pile in order to play optimally
        int requiredCoins = xorArr ^ arr[i];

        // If requiredCoins is less than the current
        // amount of coins in the current pile
        // then only the player can make an optimal move
        if (requiredCoins < arr[i])
            numberOfWays++;
    }
    return numberOfWays;
}

// Driver code
static public void Main ()
{

    // Coins in each pile
    int []arr = { 3, 4, 4, 2 };
    int n = arr.Length;

    Console.Write(getTotalWays(arr, n));
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to return the XOR
// of all the array elements
function xorArray($arr, $n)
{
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res = $res ^ $arr[$i];

    return $res;
}

// Function to return the count of ways
// to play the first move optimally
function getTotalWays($arr, $n)
{

    // XOR of all the array elements
    $xorArr = xorArray($arr, $n);

    // The player making the first move
    // can't win the game no matter
    // how optimally he plays
    if ($xorArr == 0)
        return -1;

    // Initialised with zero
    $numberOfWays = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // requiredCoins is the number of coins
        // the player making the move must leave
        // in the current pile in order to play optimally
        $requiredCoins = $xorArr ^ $arr[$i];

        // If requiredCoins is less than the current
        // amount of coins in the current pile
        // then only the player can make an optimal move
        if ($requiredCoins < $arr[$i])
            $numberOfWays++;
    }

    return $numberOfWays;
}

// Driver code

// Coins in each pile
$arr = array(3, 4, 4, 2 );
$n = sizeof($arr);

echo getTotalWays($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to return the XOR
// of all the array elements
function xorArray(arr, n)
{
    let res = 0;
    for (let i = 0; i < n; i++)
        res = res ^ arr[i];

    return res;
}

// Function to return the count of ways
// to play the first move optimally
function getTotalWays(arr, n)
{

    // XOR of all the array elements
    let xorArr = xorArray(arr, n);

    // The player making the first move
    // can't win the game no matter
    // how optimally he plays
    if (xorArr == 0)
        return -1;

    // Initialised with zero
    let numberOfWays = 0;

    for (let i = 0; i < n; i++) {

        // requiredCoins is the number of coins
        // the player making the move must leave
        // in the current pile in order to play optimally
        let requiredCoins = xorArr ^ arr[i];

        // If requiredCoins is less than the current
        // amount of coins in the current pile
        // then only the player can make an optimal move
        if (requiredCoins < arr[i])
            numberOfWays++;
    }

    return numberOfWays;
}

// Driver code

    // Coins in each pile
    let arr = [ 3, 4, 4, 2 ];
    let n = arr.length;

    document.write(getTotalWays(arr, n));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)