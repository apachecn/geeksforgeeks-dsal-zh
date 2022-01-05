# 通过添加数组中元素的两两差异找到赢家，直到可能

> 原文:[https://www . geeksforgeeks . org/通过在可能的情况下添加成对的数组元素差来找到赢家/](https://www.geeksforgeeks.org/find-the-winner-by-adding-pairwise-difference-of-elements-in-the-array-until-possible/)

给定一个正整数数组 **arr[]** ，两个玩家 **A** 和 **B** 在玩一个游戏。每次移动时，玩家从数组中选择两个数字 **x** 和 **y** ，如果数组中不存在**| x–y |**，则玩家将该数字添加到数组中(数组的大小增加 1)。不会移动的玩家输掉游戏。任务是如果玩家 **A** 总是开始游戏，找到游戏的赢家。
**举例:**

> **输入:** arr[] = {2，3 }
> T3】输出:A
> A 移动后，阵将为{2，3，1}，B 无法移动。
> **输入:** arr[] = {5，6，7}
> **输出:** B

**进场:**在这里观察到，在游戏结束时(当没有更多的移动可以进行时)，结果数组将包含原始数组 gcd 的所有倍数，直到原始数组的最大元素。

> 例如，arr[] = {8，10}
> 自，gcd(8，10) = 2。所以游戏结束时得到的数组将包含所有 2 ≤ max(arr)的倍数，即 10。
> 因此，arr[] = {2，4，6，8，10}

从上面的观察，可以找到在原阵上可以执行的招式数，这将决定游戏的胜局，如果招式数为偶数那么 **B** 将是游戏的胜局否则 **A** 胜局。
移动次数可以发现为，**(最大(arr)/gcd)–n**其中 **gcd** 是原始数组元素的 gcd，**最大(arr) / gcd** 给出结果数组中元素的总数。从结果数组的元素计数中减去元素的原始计数将得到移动的次数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the winner of the game
char getWinner(int arr[], int n)
{
    // To store the gcd of the original array
    int gcd = arr[0];

    // To store the maximum element
    // from the original array
    int maxEle = arr[0];
    for (int i = 1; i < n; i++) {
        gcd = __gcd(gcd, arr[i]);
        maxEle = max(maxEle, arr[i]);
    }

    int totalMoves = (maxEle / gcd) - n;

    // If number of moves are odd
    if (totalMoves % 2 == 1)
        return 'A';

    return 'B';
}

// Driver Code
int main()
{
    int arr[] = { 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << getWinner(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to calculate gcd
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function to return the winner
// of the game
static char getWinner(int []arr, int n)
{
    // To store the gcd of the
    // original array
    int gcd = arr[0];

    // To store the maximum element
    // from the original array
    int maxEle = arr[0];
    for (int i = 1; i < n; i++)
    {
        gcd = __gcd(gcd, arr[i]);
        maxEle = Math.max(maxEle, arr[i]);
    }

    int totalMoves = (maxEle / gcd) - n;

    // If number of moves are odd
    if (totalMoves % 2 == 1)
        return 'A';

    return 'B';
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 5, 6, 7 };
    int n = arr.length;
    System.out.print(getWinner(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the winner
# of the game
def getWinner(arr, n) :

    # To store the gcd of the
    # original array
    __gcd = arr[0];

    # To store the maximum element
    # from the original array
    maxEle = arr[0];
    for i in range(1, n) :
        __gcd = gcd(__gcd, arr[i]);
        maxEle = max(maxEle, arr[i]);

    totalMoves = (maxEle / __gcd) - n;

    # If number of moves are odd
    if (totalMoves % 2 == 1) :
        return 'A';

    return 'B';

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, 6, 7 ];
    n = len(arr)
    print(getWinner(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to calculate gcd
static int __gcd(int a, int b)
{    
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function to return the winner
// of the game
static char getWinner(int []arr, int n)
{
    // To store the gcd of the
    // original array
    int gcd = arr[0];

    // To store the maximum element
    // from the original array
    int maxEle = arr[0];
    for (int i = 1; i < n; i++)
    {
        gcd = __gcd(gcd, arr[i]);
        maxEle = Math.Max(maxEle, arr[i]);
    }

    int totalMoves = (maxEle / gcd) - n;

    // If number of moves are odd
    if (totalMoves % 2 == 1)
        return 'A';

    return 'B';
}

// Driver Code
public static void Main()
{
    int []arr = { 5, 6, 7 };
    int n = arr.Length;
    Console.Write(getWinner(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to calculate gcd
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);
}

// Function to return the winner
// of the game
function getWinner($arr, $n)
{
    // To store the gcd of the
    // original array
    $gcd = $arr[0];

    // To store the maximum element
    // from the original array
    $maxEle = $arr[0];
    for ($i = 1; $i < $n; $i++)
    {
        $gcd = __gcd($gcd, $arr[$i]);
        $maxEle = max($maxEle, $arr[$i]);
    }

    $totalMoves = ($maxEle / $gcd) - $n;

    // If number of moves are odd
    if ($totalMoves % 2 == 1)
        return 'A';

    return 'B';
}

// Driver Code
$arr = array(5, 6, 7);
$n = sizeof($arr);
echo getWinner($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to calculate gcd
    function __gcd(a, b)
    {    
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function to return the winner
    // of the game
    function getWinner(arr, n)
    {
        // To store the gcd of the
        // original array
        let gcd = arr[0];

        // To store the maximum element
        // from the original array
        let maxEle = arr[0];
        for (let i = 1; i < n; i++)
        {
            gcd = __gcd(gcd, arr[i]);
            maxEle = Math.max(maxEle, arr[i]);
        }

        let totalMoves = parseInt(maxEle / gcd, 10) - n;

        // If number of moves are odd
        if (totalMoves % 2 == 1)
            return 'A';

        return 'B';
    }

    let arr = [ 5, 6, 7 ];
    let n = arr.length;
    document.write(getWinner(arr, n));

</script>
```

**Output:** 

```
B
```