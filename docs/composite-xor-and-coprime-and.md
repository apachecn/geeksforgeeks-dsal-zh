# 复合异或和互素和

> 原文:[https://www . geeksforgeeks . org/composite-xor-and-互素-and/](https://www.geeksforgeeks.org/composite-xor-and-coprime-and/)

给定一个数组**arr【】**，任务是计算无序索引对 **(i，j)** 的数量，例如 **gcd(2，a[i]^a[j)>1**和 **gcd(2，a[I]&a[j】)<2**，其中 **^** 和**&t11】是**按位异或**和**按位与
**举例:****** 

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 3
> 所有有效对为(1，3)、(1，5)和(3，5)
> **输入:** arr[] = {21，121，13，44，65}
> **输出:** 6

**进场:**

*   **gcd(2，a[i]^a[j)】>1**只有在**a【I】**和**a【j】**均为**偶数**或**奇数**时才会为真。
*   从上一步开始缩小对，如果 **a** 和 **b** 都是**偶数的话，一对 **(a，b)** 永远不会产生 **gcd(2，a[I]&a【j】)<2**。因此，只有 **a** 和 **b** 都是**奇数**的配对才能同时满足给定的两个条件。**
*   计算给定数组中奇数元素的数量，并将其存储在**奇数**中，结果将是**(奇数*(奇数–1))/2**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// odd numbers in the array
int countOdd(int arr[], int n)
{

    // Variable to count odd numbers
    int odd = 0;

    for (int i = 0; i < n; i++) {

        // Odd number
        if (arr[i] % 2 == 1)
            odd++;
    }

    return odd;
}

// Function to return the count of valid pairs
int countValidPairs(int arr[], int n)
{
    int odd = countOdd(arr, n);

    return (odd * (odd - 1)) / 2;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countValidPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to return the count of
    // odd numbers in the array
    static int countOdd(int [] arr, int n)
    {

        // Variable to count odd numbers
        int odd = 0;

        for (int i = 0; i < n; i++)
        {

            // Odd number
            if (arr[i] % 2 == 1)
                odd++;
        }
        return odd;
    }

    // Function to return the count of valid pairs
    static int countValidPairs(int [] arr, int n)
    {
        int odd = countOdd(arr, n);

        return (odd * (odd - 1)) / 2;
    }

    // Driver Code
    public static void main(String []args)
    {
        int [] arr = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        System.out.println(countValidPairs(arr, n));
    }
}

// This code is contributed by ihritik           
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# odd numbers in the array
def countOdd(arr, n):

    # Variable to count odd numbers
    odd = 0;

    for i in range(0, n):

        # Odd number
        if (arr[i] % 2 == 1):
            odd = odd + 1;

    return odd;

# Function to return the count
# of valid pairs
def countValidPairs(arr, n):

    odd = countOdd(arr, n);

    return (odd * (odd - 1)) / 2;

# Driver Code
arr = [1, 2, 3, 4, 5 ];
n = len(arr);
print(int(countValidPairs(arr, n)));

# This code is contributed by
# Shivi_Aggarwal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the count of
    // odd numbers in the array
    static int countOdd(int [] arr, int n)
    {

        // Variable to count odd numbers
        int odd = 0;

        for (int i = 0; i < n; i++)
        {

            // Odd number
            if (arr[i] % 2 == 1)
                odd++;
        }
        return odd;
    }

    // Function to return the count of valid pairs
    static int countValidPairs(int [] arr, int n)
    {
        int odd = countOdd(arr, n);

        return (odd * (odd - 1)) / 2;
    }

    // Driver Code
    public static void Main()
    {
        int [] arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;
        Console.WriteLine(countValidPairs(arr, n));
    }
}

// This code is contributed by ihritik

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// odd numbers in the array
function countOdd($arr, $n)
{

    // Variable to count odd numbers
    $odd = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Odd number
        if ($arr[$i] % 2 == 1)
            $odd++;
    }

    return $odd;
}

// Function to return the count
// of valid pairs
function countValidPairs($arr, $n)
{
    $odd = countOdd($arr, $n);

    return ($odd * ($odd - 1)) / 2;
}

// Driver Code
$arr = array(1, 2, 3, 4, 5);
$n = sizeof($arr);
echo countValidPairs($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// odd numbers in the array
function countOdd(arr, n)
{

    // Variable to count odd numbers
    var odd = 0;

    for(var i = 0; i < n; i++)
    {

        // Odd number
        if (arr[i] % 2 == 1)
            odd++;
    }
    return odd;
}

// Function to return the count of valid pairs
function countValidPairs(arr, n)
{
    var odd = countOdd(arr, n);

    return (odd * (odd - 1)) / 2;
}

// Driver Code
var arr = [ 1, 2, 3, 4, 5 ];
var n = arr.length;

document.write(countValidPairs(arr, n));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)