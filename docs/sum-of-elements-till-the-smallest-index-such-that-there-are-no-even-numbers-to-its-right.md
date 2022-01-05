# 元素的总和直到最小的索引，这样它的右边就没有偶数了

> 原文:[https://www . geeksforgeeks . org/元素之和-直到最小索引-它右边没有偶数/](https://www.geeksforgeeks.org/sum-of-elements-till-the-smallest-index-such-that-there-are-no-even-numbers-to-its-right/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是找到最小索引的元素之和，这样索引的右边就没有偶数元素了。**注意**数组至少有一个偶数元素。
**举例:**

> **输入:** arr[] = {2，3，5，6，3，3 }
> T3】输出:16
> 2+3+5+6 = 16
> T7】输入: arr[] = {3，4 }
> T10】输出: 7
> 3 + 4 = 7

**方法:**从数组中找到最右边偶数元素的索引，并返回从索引 0 开始到找到的索引的所有元素的总和。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required sum
int smallestIndexsum(int arr[], int n)
{

    // Starting from the last index
    int i = n - 1;

    // Skip all odd elements and find the
    // index of the rightmost even element
    while (i >= 0 && arr[i] % 2 == 1)
        i--;

    // To store the required sum
    int sum = 0;
    for (int j = 0; j <= i; j++)
        sum += arr[j];

    return sum;
}

// Driver code
int main()
{

    int arr[] = { 2, 3, 5, 6, 3, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << smallestIndexsum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required sum
static int smallestIndexsum(int arr[], int n)
{

    // Starting from the last index
    int i = n - 1;

    // Skip all odd elements and find the
    // index of the rightmost even element
    while (i >= 0 && arr[i] % 2 == 1)
        i--;

    // To store the required sum
    int sum = 0;
    for (int j = 0; j <= i; j++)
        sum += arr[j];

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 5, 6, 3, 3 };
    int n = arr.length;

    System.out.println(smallestIndexsum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required sum
def smallestIndexsum(arr, n):

    # Starting from the last index
    i = n - 1;

    # Skip all odd elements and find the
    # index of the rightmost even element
    while (i >= 0 and arr[i] % 2 == 1):
        i -= 1;

    # To store the required sum
    sum = 0;
    for j in range(0, i + 1):
        sum += arr[j];

    return sum;

# Driver code
if __name__ == '__main__':

    arr = [ 2, 3, 5, 6, 3, 3 ];
    n = len(arr);

    print(smallestIndexsum(arr, n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required sum
static int smallestIndexsum(int []arr, int n)
{

    // Starting from the last index
    int i = n - 1;

    // Skip all odd elements and find the
    // index of the rightmost even element
    while (i >= 0 && arr[i] % 2 == 1)
        i--;

    // To store the required sum
    int sum = 0;
    for (int j = 0; j <= i; j++)
        sum += arr[j];

    return sum;
}

// Driver code
static public void Main ()
{
    int []arr = { 2, 3, 5, 6, 3, 3 };
    int n = arr.Length;

    Console.Write(smallestIndexsum(arr, n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the required sum
    function smallestIndexsum(arr, n)
    {

        // Starting from the last index
        let i = n - 1;

        // Skip all odd elements and find the
        // index of the rightmost even element
        while (i >= 0 && arr[i] % 2 == 1)
            i--;

        // To store the required sum
        let sum = 0;
        for (let j = 0; j <= i; j++)
            sum += arr[j];

        return sum;
    }

    let arr = [ 2, 3, 5, 6, 3, 3 ];
    let n = arr.length;

    document.write(smallestIndexsum(arr, n));

</script>
```

**Output:** 

```
16
```

**时间复杂度:** O(N)

**辅助空间:** O(1)