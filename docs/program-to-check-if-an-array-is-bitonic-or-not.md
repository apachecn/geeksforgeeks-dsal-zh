# 检查一个数组是否是二进制的程序

> 原文:[https://www . geesforgeks . org/program-to-check-a-array-if-bitonic-or-not/](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/)

给定一个由 N 个元素组成的数组。任务是检查[数组是否是双音素](https://www.geeksforgeeks.org/find-element-bitonic-array/)。
如果一个数组中的元素先严格递增后严格递减，那么这个数组被称为[双音素](https://www.geeksforgeeks.org/find-element-bitonic-array/)。
**示例** :

```
Input: arr[] = {-3, 9, 11, 20, 17, 5, 1}
Output: YES

Input: arr[] = {5, 6, 7, 8, 9, 10, 1, 2, 11};
Output: NO
```

**接近** :

*   开始遍历数组，并继续检查下一个元素是否大于当前元素。
*   如果在任何时候，下一个元素不大于当前元素，则中断循环。
*   再次从当前元素开始遍历，检查下一个元素是否小于当前元素。
*   如果在到达数组末尾之前的任何时候，如果下一个元素不小于当前元素，则中断循环并打印“否”
*   如果成功到达数组末尾，则打印“是”。

以下是上述方法的实现:

## C++

```
// C++ program to check if an array is bitonic
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given array is bitonic
int checkBitonic(int arr[], int n)
{
    int i, j;

    // Check for increasing sequence
    for (i = 1; i < n; i++) {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] <= arr[i - 1])
            break;
    }

    if (i > n - 1)
        return 1;

    // Check for decreasing sequence
    for (j = i + 1; j < n; j++) {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[j] >= arr[j - 1])
            break;
    }

    i = j;

    if (i != n)
        return 0;

    return 1;
}

// Driver code
int main()
{
    int arr[] = { 1,2,3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    (checkBitonic(arr, n) == 1) ? cout << "YES"
                                : cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if an array is bitonic
class GFG
{
// Function to check if the
// given array is bitonic
static int checkBitonic(int arr[], int n)
{
    int i, j;

    // Check for increasing sequence
    for (i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] <= arr[i - 1])
            break;
    }

    if (i == n - 1)
        return 1;

    // Check for decreasing sequence
    for (j = i + 1; j < n; j++)
    {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[j] >= arr[j - 1])
            break;
    }

    i = j;

    if (i != n)
        return 0;

    return 1;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { -3, 9, 7, 20, 17, 5, 1 };

    int n = arr.length;

    System.out.println((checkBitonic(arr, n) == 1) ?
                                             "YES" : "NO");
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python3 program to check if
# an array is bitonic or not.

# Function to check if the
# given array is bitonic
def checkBitonic(arr, n) :

    # Check for increasing sequence
    for i in range(1, n) :
        if arr[i] > arr[i - 1] :
            continue
        else :
            break

    if i == n-1 :
        return 1

    # Check for decreasing sequence
    for j in range(i + 1, n) :

        if arr[j] < arr[j - 1] :
            continue
        else :
            break

    i = j
    if i != n - 1 :
        return 0

    return 1

# Driver Code
if __name__ == "__main__" :

    arr = [-3, 9, 7, 20, 17, 5, 1]

    n = len(arr)

    if checkBitonic(arr, n) == 1 :
        print("YES")
    else :
        print("NO")

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to check
// if an array is bitonic
using System;

class GFG
{
// Function to check if the
// given array is bitonic
static int checkBitonic(int []arr,
                        int n)
{
    int i, j;

    // Check for increasing sequence
    for (i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] <= arr[i - 1])
            break;
    }

    if (i == n - 1)
        return 1;

    // Check for decreasing sequence
    for (j = i + 1; j < n; j++)
    {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[j] >= arr[j - 1])
            break;
    }

    i = j;

    if (i != n)
        return 0;

    return 1;
}

// Driver Code
public static void Main()
{
    int []arr = { -3, 9, 7, 20, 17, 5, 1 };

    int n = arr.Length;

    Console.WriteLine((
            checkBitonic(arr, n) == 1) ?
                                 "YES" : "NO");
}
}

// This code is contributed by Bilal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// an array is bitonic

// Function to check if the
// given array is bitonic
function checkBitonic(&$arr, $n)
{

    // Check for increasing sequence
    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i] > $arr[$i - 1])
            continue;

        if ($arr[$i] <= $arr[$i - 1])
            break;
    }

    if ($i == $n - 1)
        return 1;

    // Check for decreasing sequence
    for ($j = $i + 1; $j < $n; $j++)
    {
        if ($arr[$j] < $arr[$j - 1])
            continue;

        if ($arr[$j] >= $arr[$j - 1])
            break;
    }

    $i = $j;

    if ($i != $n)
        return 0;

    return 1;
}

// Driver code
$arr = array( -3, 9, 7, 20, 17, 5, 1 );

$n = sizeof($arr);

checkBitonic($arr, $n) == 1 ?
               print("YES") : print("NO");

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Java Script program to check
// if an array is bitonic

// Function to check if the
// given array is bitonic
function checkBitonic(arr,n)
{
    let i, j;

    // Check for increasing sequence
    for (i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] <= arr[i - 1])
            break;
    }

    if (i == n - 1)
        return 1;

    // Check for decreasing sequence
    for (j = i + 1; j < n; j++)
    {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[j] >= arr[j - 1])
            break;
    }

    i = j;

    if (i != n)
        return 0;

    return 1;
}

// Driver Code

    let arr = [ -3, 9, 7, 20, 17, 5, 1 ];

    let n = arr.length;

    document.write((checkBitonic(arr, n) == 1) ?
                                            "YES" : "NO");

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
NO
```