# 排序数组的最小范围增量操作

> 原文:[https://www . geesforgeks . org/最小范围-增量-操作-对数组进行排序/](https://www.geeksforgeeks.org/minimum-range-increment-operations-to-sort-an-array/)

给定一个包含 N 个元素的数组。允许在阵列上执行以下任意次数的移动:

*   选择任意 L 和 R，并将 L 到 R 范围内的所有数字递增 1。

任务是找到按非递减顺序排列数组所需的**最小移动次数**。

**示例:**

```
Input : arr[] = {1, 2, 3, 4}
Output : 0
The array is already sorted

Input : arr[] = {3, 2, 1}
Output : 2
Step 1: L=1 and R=2 (0-based)
Step 2: L=2 and R=2
Resultant array [3, 3, 3]

```

考虑一个排序的数组，递增数组的所有元素仍然会得到一个排序的数组。
所以想法是从最后一个索引开始，从右开始遍历数组的元素，并跟踪最小的元素。如果在任何时候，元素的顺序被发现是增加的，通过从当前元素中减去右边的最小元素来计算移动的次数。

下面是上述方法的实现:

## C++

```
// C++ program to find minimum range
// increments to sort an array

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum range
// increments to sort an array
int minMovesToSort(int arr[], int n)
{
    int moves = 0;

    int i, mn = arr[n - 1];

    for (i = n - 2; i >= 0; i--) {

        // If current element is found greater than
        // last element
        // Increment all terms in
        // range i+1 to n-1
        if (arr[i] > mn)
            moves += arr[i] - mn;

        mn = arr[i]; // Minimum in range i to n-1
    }

    return moves;
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 2, 8, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minMovesToSort(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum range
// increments to sort an array

import java.io.*;

class GFG {

// Function to find minimum range
// increments to sort an array
static int minMovesToSort(int arr[], int n)
{
    int moves = 0;

    int i, mn = arr[n - 1];

    for (i = n - 2; i >= 0; i--) {

        // If current element is found greater than
        // last element
        // Increment all terms in
        // range i+1 to n-1
        if (arr[i] > mn)
            moves += arr[i] - mn;

        mn = arr[i]; // Minimum in range i to n-1
    }

    return moves;
}

// Driver Code

    public static void main (String[] args) {
        int arr[] = { 3, 5, 2, 8, 4 };

    int n = arr.length;

    System.out.println( minMovesToSort(arr, n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find minimum range
# increments to sort an array

# Function to find minimum range
# increments to sort an array
def minMovesToSort(arr, n) :

    moves = 0

    mn = arr[n - 1]

    for i in range(n - 1, -1, -1) :

        # If current element is found
        # greater than last element
        # Increment all terms in
        # range i+1 to n-1
        if (arr[i] > mn) :
            moves += arr[i] - mn

        mn = arr[i] # Minimum in range i to n-1

    return moves

# Driver Code
if __name__ == "__main__" :

    arr = [ 3, 5, 2, 8, 4 ]

    n = len(arr)

    print(minMovesToSort(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find minimum range
// increments to sort an array
using System;

class GFG
{
// Function to find minimum range
// increments to sort an array
static int minMovesToSort(int []arr,
                          int n)
{
    int moves = 0;

    int i, mn = arr[n - 1];

    for (i = n - 2; i >= 0; i--)
    {

        // If current element is found
        // greater than last element
        // Increment all terms in
        // range i+1 to n-1
        if (arr[i] > mn)
            moves += arr[i] - mn;

        mn = arr[i]; // Minimum in range
                     // i to n-1
    }
    return moves;
}

// Driver Code
static public void Main ()
{
    int []arr = { 3, 5, 2, 8, 4 };
    int n = arr.Length;

    Console.WriteLine(minMovesToSort(arr, n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum range
// increments to sort an array

// Function to find minimum range
// increments to sort an array
function minMovesToSort($arr, $n)
{
    $moves = 0;

    $mn = $arr[$n - 1];

    for ($i = $n - 2; $i >= 0; $i--)
    {

        // If current element is found
        // greater than last element
        // Increment all terms in
        // range i+1 to n-1
        if ($arr[$i] > $mn)
            $moves += $arr[$i] - $mn;

        $mn = $arr[$i]; // Minimum in range i to n-1
    }

    return $moves;
}

// Driver Code
$arr = array(3, 5, 2, 8, 4 );

$n = sizeof($arr);

echo minMovesToSort($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum range
// increments to sort an array

// Function to find minimum range
// increments to sort an array
function minMovesToSort(arr, n)
{
    var moves = 0;
    var i, mn = arr[n - 1];

    for(i = n - 2; i >= 0; i--)
    {

        // If current element is found greater
        // than last element
        // Increment all terms in
        // range i+1 to n-1
        if (arr[i] > mn)
            moves += arr[i] - mn;

        // Minimum in range i to n-1
        mn = arr[i];
    }
    return moves;
}

// Driver Code
var arr = [ 3, 5, 2, 8, 4 ];
var n = arr.length;

document.write(minMovesToSort(arr, n));

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N)