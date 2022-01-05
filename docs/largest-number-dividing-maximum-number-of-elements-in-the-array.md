# 数组中最大元素数的最大数除以

> 原文:[https://www . geesforgeks . org/最大数除法最大数组元素数/](https://www.geeksforgeeks.org/largest-number-dividing-maximum-number-of-elements-in-the-array/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是从数组中找出最大的数除以最大的元素数。

**示例:**

> **输入:** arr[] = {2，12，6}
> **输出:** 2
> 1 和 2 是从数组
> 中除
> 最大元素数(即所有元素)的唯一整数，2 是其中的最大值
> 。
> **输入:** arr[] = {1，7，9}
> **输出:** 1

**方法:**解决这个问题的一个简单方法是获取所有元素的 GCD。为什么这种方法有效？1 是数组中所有元素的除数。现在，任何其他大于 1 的数字将或者分割数组的所有元素(在这种情况下，数字本身就是答案)，或者它将分割数组的一个子集，即 1 是这里的答案，因为它从数组中分割更多的元素。因此，最直接的方法是获取数组中所有元素的 GCD。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest number
// that divides the maximum elements
// from the given array
int findLargest(int* arr, int n)
{

    // Finding gcd of all the numbers
    // in the array
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(arr[i], gcd);
    return gcd;
}

// Driver code
int main()
{
    int arr[] = { 3, 6, 9 };
    int n = sizeof(arr) / sizeof(int);

    cout << findLargest(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the largest number
    // that divides the maximum elements
    // from the given array
    static int findLargest(int[] arr, int n)
    {

        // Finding gcd of all the numbers
        // in the array
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = __gcd(arr[i], gcd);
        return gcd;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 6, 9 };
        int n = arr.length;

        System.out.print(findLargest(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

# Function to return the largest number
# that divides the maximum elements
# from the given array
def findLargest(arr, n):

    # Finding gcd of all the numbers
    # in the array
    gcd = 0
    for i in range(n):
        gcd = __gcd(arr[i], gcd)
    return gcd

# Driver code
if __name__ == '__main__':
    arr = [3, 6, 9]
    n = len(arr)

    print(findLargest(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the largest number
    // that divides the maximum elements
    // from the given array
    static int findLargest(int[] arr, int n)
    {

        // Finding gcd of all the numbers
        // in the array
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = __gcd(arr[i], gcd);
        return gcd;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 6, 9 };
        int n = arr.Length;

        Console.Write(findLargest(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the largest number
    // that divides the maximum elements
    // from the given array
    function findLargest(arr , n) {

        // Finding gcd of all the numbers
        // in the array
        var gcd = 0;
        for (i = 0; i < n; i++)
            gcd = __gcd(arr[i], gcd);
        return gcd;
    }

    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code

        var arr = [ 3, 6, 9 ];
        var n = arr.length;

        document.write(findLargest(arr, n));

// This code contributed by umadevi9616
</script>
```

**Output**

```
3
```

**时间复杂度:** O(N * log(MAX))，其中 N 是数组的大小，MAX 是数组的最大元素。
**辅助空间:** O(log(MAX))