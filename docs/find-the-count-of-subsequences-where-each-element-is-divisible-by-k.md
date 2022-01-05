# 求每个元素可被 K 整除的子序列个数

> 原文:[https://www . geeksforgeeks . org/find-子序列的计数-其中每个元素可被 k 整除/](https://www.geeksforgeeks.org/find-the-count-of-subsequences-where-each-element-is-divisible-by-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是从数组中找出子序列的总数，其中每个元素都可以被 **K** 整除。
**举例:**

> **输入:** arr[] = {1，2，3，6}，K = 3
> **输出:** 3
> {3}，{6}和{3，6}是唯一有效的子序列。
> **输入:** arr[] = {5，10，15，20，25}，K = 5
> **输出:** 31

**方法:**由于每个元素必须能被 **K** 整除，总的子序列等于 **2 <sup>cnt</sup>** ，其中 **cnt** 是数组中能被 **K** 整除的元素数。**注意**将从结果中减去 **1** ，以排除空的子序列。所以，最终结果将是**2<sup>CNT</sup>–1**。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of all valid subsequences
int countSubSeq(int arr[], int n, int k)
{

    // To store the count of elements
    // which are divisible by k
    int count = 0;

    for (int i = 0; i < n; i++) {

        // If current element is divisible by
        // k then increment the count
        if (arr[i] % k == 0) {
            count++;
        }
    }

    // Total (2^n - 1) non-empty subsequences
    // are possible with n element
    return (pow(2, count) - 1);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << countSubSeq(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to return the count
// of all valid subsequences
static int countSubSeq(int arr[], int n, int k)
{

    // To store the count of elements
    // which are divisible by k
    int count = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is divisible by
        // k then increment the count
        if (arr[i] % k == 0)
        {
            count++;
        }
    }

    // Total (2^n - 1) non-empty subsequences
    // are possible with n element
    return (int) (Math.pow(2, count) - 1);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 6 };
    int n = arr.length;
    int k = 3;

    System.out.println(countSubSeq(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of all valid subsequences
def countSubSeq(arr, n, k) :

    # To store the count of elements
    # which are divisible by k
    count = 0;

    for i in range(n) :

        # If current element is divisible by
        # k then increment the count
        if (arr[i] % k == 0) :
            count += 1;

    # Total (2^n - 1) non-empty subsequences
    # are possible with n element
    return (2 ** count - 1);

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 6 ];
    n = len(arr);
    k = 3;

    print(countSubSeq(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of all valid subsequences
static int countSubSeq(int []arr, int n, int k)
{

    // To store the count of elements
    // which are divisible by k
    int count = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is divisible by
        // k then increment the count
        if (arr[i] % k == 0)
        {
            count++;
        }
    }

    // Total (2^n - 1) non-empty subsequences
    // are possible with n element
    return (int) (Math.Pow(2, count) - 1);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 6 };
    int n = arr.Length;
    int k = 3;

    Console.WriteLine(countSubSeq(arr, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of all valid subsequences
function countSubSeq(arr, n, k)
{

    // To store the count of elements
    // which are divisible by k
    let count = 0;

    for (let i = 0; i < n; i++) {

        // If current element is divisible by
        // k then increment the count
        if (arr[i] % k == 0) {
            count++;
        }
    }

    // Total (2^n - 1) non-empty subsequences
    // are possible with n element
    return (Math.pow(2, count) - 1);
}

// Driver code
    let arr = [ 1, 2, 3, 6 ];
    let n = arr.length;
    let k = 3;

    document.write(countSubSeq(arr, n, k));

</script>
```

**Output:** 

```
3
```