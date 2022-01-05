# 最大和最小元素之差大于或等于其长度的子阵列

> 原文:[https://www . geesforgeks . org/subarray-最大和最小元素之差大于或等于其长度/](https://www.geeksforgeeks.org/subarray-with-difference-between-maximum-and-minimum-element-greater-than-or-equal-to-its-length/)

给定一个数组**arr【】**，任务是找到一个最大和最小元素之差大于或等于子数组长度的子数组。如果不存在这样的子阵列，则打印 **-1** 。
**例:**

> **输入:** arr[] = {3，7，5，1}
> **输出:**3 7
> | 3–7 |>长度({3，7})即 4 ≥ 2
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** -1
> 不存在符合标准的子阵列。

**天真的方法:**找到至少有两个元素的所有可能的子阵列，然后检查满足给定条件的每个子阵列，即 max(子阵列)–min(子阵列)≥ len(子阵列)
**高效的方法:**找到长度为 2 的子阵列，其中仅有的两个元素之间的绝对差大于或等于 2。这将涵盖几乎所有的情况，因为只有三种情况下没有这样的子阵列:

1.  当数组长度为 **0** 时。
2.  当数组中所有元素相等时。
3.  当数组中每两个连续元素的绝对差值为 0 或 1 时。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the required subarray
void findSubArr(int arr[], int n)
{

    // For every two consecutive element subarray
    for (int i = 0; i < n - 1; i++) {

        // If the current pair of consecutive
        // elements satisfies the given condition
        if (abs(arr[i] - arr[i + 1]) >= 2) {
            cout << arr[i] << " " << arr[i + 1];
            return;
        }
    }

    // No such subarray found
    cout << -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 6, 7 };
    int n = sizeof(arr) / sizeof(int);

    findSubArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find the required subarray
    static void findSubArr(int arr[], int n)
    {

        // For every two consecutive element subarray
        for (int i = 0; i < n - 1; i++)
        {

            // If the current pair of consecutive
            // elements satisfies the given condition
            if (Math.abs(arr[i] - arr[i + 1]) >= 2)
            {
                System.out.print(arr[i] + " " + arr[i + 1]);
                return;
            }
        }

        // No such subarray found
        System.out.print(-1);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 4, 6, 7 };
        int n = arr.length;

        findSubArr(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required subarray
def findSubArr(arr, n) :

    # For every two consecutive element subarray
    for i in range(n - 1) :

        # If the current pair of consecutive
        # elements satisfies the given condition
        if (abs(arr[i] - arr[i + 1]) >= 2) :
            print(arr[i] ,arr[i + 1],end="");
            return;

    # No such subarray found
    print(-1);

# Driver code
if __name__ == "__main__" :
    arr = [ 1, 2, 4, 6, 7 ];
    n = len(arr);

    findSubArr(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the required subarray
    static void findSubArr(int []arr, int n)
    {

        // For every two consecutive element subarray
        for (int i = 0; i < n - 1; i++)
        {

            // If the current pair of consecutive
            // elements satisfies the given condition
            if (Math.Abs(arr[i] - arr[i + 1]) >= 2)
            {
                Console.Write(arr[i] + " " + arr[i + 1]);
                return;
            }
        }

        // No such subarray found
        Console.Write(-1);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 4, 6, 7 };
        int n = arr.Length;

        findSubArr(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find the required subarray
function findSubArr(arr, n) {

    // For every two consecutive element subarray
    for (let i = 0; i < n - 1; i++) {

        // If the current pair of consecutive
        // elements satisfies the given condition
        if (Math.abs(arr[i] - arr[i + 1]) >= 2) {
            document.write(arr[i] + " " + arr[i + 1]);
            return;
        }
    }

    // No such subarray found
    document.write(-1);
}

// Driver code

let arr = [1, 2, 4, 6, 7];
let n = arr.length

findSubArr(arr, n);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2 4
```

**时间复杂度:** O(N)