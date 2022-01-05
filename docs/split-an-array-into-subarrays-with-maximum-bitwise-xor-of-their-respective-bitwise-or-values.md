# 将一个阵列分割成子阵列，子阵列各自的“位或”值进行最大“位异或”

> 原文:[https://www . geeksforgeeks . org/将数组拆分为子数组，并对其各自的按位或值进行最大按位异或运算/](https://www.geeksforgeeks.org/split-an-array-into-subarrays-with-maximum-bitwise-xor-of-their-respective-bitwise-or-values/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在将数组拆分为[个子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)(可能为零个子数组)后，求每个子数组的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = {1，5，7}，N = 3
> **输出:** 7
> **解释:**
> 给定的数组可以表示为 1 个子数组，即{1，5，7}。
> 形成的子阵列的按位“或”的按位“异或”是 7，这是最大可能值。
> 
> **输入:** arr[] = {1，2}，N = 2
> T3】输出: 3

**天真法:**解决上述给定问题最简单的方法是[使用](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)[递归](https://www.geeksforgeeks.org/recursion/)生成所有可能的子阵列断开组合，并在每次递归调用时，找到所有可能形成的子阵列的 Bitwise OR 的 Bitwise XOR 的最大值并打印出来。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Recursive function to find all the
// possible breaking of arrays into
// subarrays and find the maximum
// Bitwise XOR
int maxXORUtil(int arr[], int N,
               int xrr, int orr)
{
    // If the value of N is 0
    if (N == 0)
        return xrr ^ orr;

    // Stores the result if the new
    // group is formed with the first
    // element as arr[i]
    int x = maxXORUtil(arr, N - 1,
                       xrr ^ orr,
                       arr[N - 1]);

    // Stores if the result if the
    // arr[i] is included in the
    // last group
    int y = maxXORUtil(arr, N - 1,
                       xrr, orr | arr[N - 1]);

    // Returns the maximum of
    // x and y
    return max(x, y);
}

// Function to find the maximum possible
// Bitwise XOR of all possible values of
// the array after breaking the arrays
// into subarrays
int maximumXOR(int arr[], int N)
{
    // Return the result
    return maxXORUtil(arr, N, 0, 0);
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumXOR(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG{

    // Recursive function to find all the
    // possible breaking of arrays into
    // subarrays and find the maximum
    // Bitwise XOR
    static int maxXORUtil(int arr[], int N, int xrr,
                          int orr)
    {

        // If the value of N is 0
        if (N == 0)
            return xrr ^ orr;

        // Stores the result if the new
        // group is formed with the first
        // element as arr[i]
        int x
            = maxXORUtil(arr, N - 1, xrr ^ orr, arr[N - 1]);

        // Stores if the result if the
        // arr[i] is included in the
        // last group
        int y
            = maxXORUtil(arr, N - 1, xrr, orr | arr[N - 1]);

        // Returns the maximum of
        // x and y
        return Math.max(x, y);
    }

    // Function to find the maximum possible
    // Bitwise XOR of all possible values of
    // the array after breaking the arrays
    // into subarrays
    static int maximumXOR(int arr[], int N)
    {

        // Return the result
        return maxXORUtil(arr, N, 0, 0);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 5, 7 };
        int N = arr.length;
        System.out.println(maximumXOR(arr, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# C++ program for the above approach
# Recursive function to find all the
# possible breaking of arrays o
# subarrays and find the maximum
# Bitwise XOR
def maxXORUtil(arr, N, xrr, orr):

    # If the value of N is 0
    if (N == 0):
        return xrr ^ orr

    # Stores the result if the new
    # group is formed with the first
    # element as arr[i]
    x = maxXORUtil(arr, N - 1, xrr ^ orr, arr[N - 1])

    # Stores if the result if the
    # arr[i] is included in the
    # last group
    y = maxXORUtil(arr, N - 1, xrr, orr | arr[N - 1])

    # Returns the maximum of
    # x and y
    return max(x, y)

# Function to find the maximum possible
# Bitwise XOR of all possible values of
# the array after breaking the arrays
# o subarrays
def maximumXOR(arr,  N):

    # Return the result
    return maxXORUtil(arr, N, 0, 0)

# Driver Code
arr =  1, 5, 7
N = len(arr)
print(maximumXOR(arr, N))

# this code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Recursive function to find all the
    // possible breaking of arrays into
    // subarrays and find the maximum
    // Bitwise XOR
    static int maxXORUtil(int[] arr, int N, int xrr,
                          int orr)
    {

        // If the value of N is 0
        if (N == 0)
            return xrr ^ orr;

        // Stores the result if the new
        // group is formed with the first
        // element as arr[i]
        int x
            = maxXORUtil(arr, N - 1, xrr ^ orr, arr[N - 1]);

        // Stores if the result if the
        // arr[i] is included in the
        // last group
        int y
            = maxXORUtil(arr, N - 1, xrr, orr | arr[N - 1]);

        // Returns the maximum of
        // x and y
        return Math.Max(x, y);
    }

    // Function to find the maximum possible
    // Bitwise XOR of all possible values of
    // the array after breaking the arrays
    // into subarrays
    static int maximumXOR(int[] arr, int N)
    {

        // Return the result
        return maxXORUtil(arr, N, 0, 0);
    }

// Driver code
static void Main()
{
    int[] arr = { 1, 5, 7 };
        int N = arr.Length;
        Console.Write(maximumXOR(arr, N));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Recursive function to find all the
// possible breaking of arrays into
// subarrays and find the maximum
// Bitwise XOR
function maxXORUtil(arr,N,xrr,orr)
{

    // If the value of N is 0
        if (N == 0)
            return xrr ^ orr;

        // Stores the result if the new
        // group is formed with the first
        // element as arr[i]
        let x
            = maxXORUtil(arr, N - 1, xrr ^ orr, arr[N - 1]);

        // Stores if the result if the
        // arr[i] is included in the
        // last group
        let y
            = maxXORUtil(arr, N - 1, xrr, orr | arr[N - 1]);

        // Returns the maximum of
        // x and y
        return Math.max(x, y);
}

// Function to find the maximum possible
// Bitwise XOR of all possible values of
// the array after breaking the arrays
// into subarrays
function maximumXOR(arr,N)
{

    // Return the result
    return maxXORUtil(arr, N, 0, 0);
}

// Driver code
let arr=[1, 5, 7 ];
let N = arr.length;
document.write(maximumXOR(arr, N));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效法:**通过观察[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)与 B [的关系，可以优化上述方法，即 **N** 元素的**逐位异或**的值最多为 **N** 元素的**逐位异或**的值。因此，要找到最大值，想法是将该组拆分为整个数组的仅 1 组。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

因此，打印数组元素 **arr[]** 的 [**位“或”**值作为结果最大值。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the bitwise OR of
// array elements
int MaxXOR(int arr[], int N)
{
    // Stores the resultant maximum
    // value of Bitwise XOR
    int res = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        res |= arr[i];
    }

    // Return the maximum value res
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MaxXOR(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the bitwise OR of
// array elements
static int MaxXOR(int arr[], int N)
{

    // Stores the resultant maximum
    // value of Bitwise XOR
    int res = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        res |= arr[i];
    }

    // Return the maximum value res
    return res;
}

public static void main(String[] args)
{
    int arr[] = { 1, 5, 7 };
    int N = arr.length;

    System.out.println(MaxXOR(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the bitwise OR of
# array elements
def MaxXOR(arr, N):

    # Stores the resultant maximum
    # value of Bitwise XOR
    res = 0

    # Traverse the array arr[]
    for i in range(N):
        res |= arr[i]

    # Return the maximum value res
    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 5, 7 ]
    N = len(arr)

    print (MaxXOR(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find the bitwise OR of
// array elements
static int MaxXOR(int []arr, int N)
{

    // Stores the resultant maximum
    // value of Bitwise XOR
    int res = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        res |= arr[i];
    }

    // Return the maximum value res
    return res;
}

public static void Main(String[] args)
{
    int []arr = { 1, 5, 7 };
    int N = arr.Length;

    Console.Write(MaxXOR(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the bitwise OR of
// array elements
function MaxXOR(arr, N)
{

    // Stores the resultant maximum
    // value of Bitwise XOR
    var res = 0;

    // Traverse the array arr[]
    for(var i = 0; i < N; i++)
    {
        res |= arr[i];
    }

    // Return the maximum value res
    return res;
}

// Driver code
var arr = [ 1, 5, 7 ];
var N = arr.length;

document.write(MaxXOR(arr, N));

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)