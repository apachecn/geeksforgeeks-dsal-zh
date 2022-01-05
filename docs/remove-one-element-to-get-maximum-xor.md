# 去掉一个元素得到最大异或

> 原文:[https://www . geesforgeks . org/remove-one-element-to-get-maximum-xor/](https://www.geeksforgeeks.org/remove-one-element-to-get-maximum-xor/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是从数组中移除一个元素，以使数组的异或值最大化。打印最大值。
**例:**

> **输入:** arr[] = {1，1，3}
> **输出:** 2
> 删除一个元素及其对应 XOR 值的所有可能方式将为:
> a)删除 1 - > (1 XOR 3) = 2
> b)删除 1 - > (1 XOR 3) = 2
> c)删除 3 - > (1 XOR 1) = 0
> 这样，最终答案为 2。
> **输入:** arr[] = {3，3，3}
> **输出:** 0

**天真的方法:**一种方法是逐个移除每个元素，然后找到剩余元素的异或。这种方法的时间复杂度为 0(N<sup>2</sup>)。
**高效进场:**

*   求数组所有元素的异或。我们把这个值叫做 **X** 。
*   对于每个元素 **arr[i]** ，执行 **Y = (X XOR arr[i])** 并将最终答案更新为 **ans = max(Y，ans)** 。

上述方法之所以有效，是因为如果 **(A XOR B) = C** 那么(C XOR B) = A .要找到**XOR(arr[0…I-1])^ xor(arr[I+1…n-1])**，我们所要做的就是 **XOR(arr) ^ arr[i]** 其中 **XOR(arr)** 是数组所有元素的 xor。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized XOR
// after removing an element from the array
int maxXOR(int* arr, int n)
{
    // Find XOR of the complete array
    int xorArr = 0;
    for (int i = 0; i < n; i++)
        xorArr ^= arr[i];

    // To store the final answer
    int ans = 0;

    // Iterating through the array to find
    // the final answer
    for (int i = 0; i < n; i++)
        ans = max(ans, (xorArr ^ arr[i]));

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 3 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxXOR(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximized XOR
    // after removing an element from the array
    static int maxXOR(int arr[], int n)
    {
        // Find XOR of the complete array
        int xorArr = 0;
        for (int i = 0; i < n; i++)
            xorArr ^= arr[i];

        // To store the final answer
        int ans = 0;

        // Iterating through the array to find
        // the final answer
        for (int i = 0; i < n; i++)
            ans = Math.max(ans, (xorArr ^ arr[i]));

        // Return the final answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 1, 3 };
        int n = arr.length;
        System.out.println(maxXOR(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximized XOR
# after removing an element from the array
def maxXOR(arr, n):

    # Find XOR of the complete array
    xorArr = 0
    for i in range(n):
        xorArr ^= arr[i]

    # To store the final answer
    ans = 0

    # Iterating through the array to find
    # the final answer
    for i in range(n):
        ans = max(ans, (xorArr ^ arr[i]))

    # Return the final answer
    return ans

# Driver code
arr = [1, 1, 3]
n = len(arr)

print(maxXOR(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximized XOR
    // after removing an element from the array
    static int maxXOR(int []arr, int n)
    {
        // Find XOR of the complete array
        int xorArr = 0;
        for (int i = 0; i < n; i++)
            xorArr ^= arr[i];

        // To store the readonly answer
        int ans = 0;

        // Iterating through the array to find
        // the readonly answer
        for (int i = 0; i < n; i++)
            ans = Math.Max(ans, (xorArr ^ arr[i]));

        // Return the readonly answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 1, 3 };
        int n = arr.Length;
        Console.WriteLine(maxXOR(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximized XOR
// after removing an element from the array
function maxXOR(arr, n)
{
    // Find XOR of the complete array
    let xorArr = 0;
    for (let i = 0; i < n; i++)
        xorArr ^= arr[i];

    // To store the final answer
    let ans = 0;

    // Iterating through the array to find
    // the final answer
    for (let i = 0; i < n; i++)
        ans = Math.max(ans, (xorArr ^ arr[i]));

    // Return the final answer
    return ans;
}

// Driver code
    let arr = [ 1, 1, 3 ];
    let n = arr.length;

    document.write(maxXOR(arr, n));

</script>
```

**Output:** 

```
2
```