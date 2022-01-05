# 给定数组中每对绝对差的乘积

> 原文:[https://www . geeksforgeeks . org/给定阵列中每对绝对差值的乘积/](https://www.geeksforgeeks.org/product-of-absolute-difference-of-every-pair-in-given-array/)

给定一个由 **N** 个元素组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出给定数组中所有对的绝对差的乘积。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 10
> **解释:**
> 积| 2-1 | * | 3-1 | * | 4-1 | * | 3-2 | * | 4-2 | * | 4-3 | = 12
> **输入:** arr[] = {1，8，9，15，16}
> **输出:**

**方法:**思路是[生成给定数组的每一个可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)**arr【】**求所有对的绝对差的乘积。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the product of
// abs diff of all pairs (x, y)
int getProduct(int a[], int n)
{
    // To store product
    int p = 1;

    // Iterate all possible pairs
    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++) {

            // Find the product
            p *= abs(a[i] - a[j]);
        }
    }

    // Return product
    return p;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << getProduct(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the product of
// abs diff of all pairs (x, y)
static int getProduct(int a[], int n)
{

    // To store product
    int p = 1;

    // Iterate all possible pairs
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Find the product
            p *= Math.abs(a[i] - a[j]);
        }
    }

    // Return product
    return p;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;

    // Function call
    System.out.println(getProduct(arr, N));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to return the product of
# abs diff of all pairs (x, y)
def getProduct(a, n):

    # To store product
    p = 1

    # Iterate all possible pairs
    for i in range (n):
        for j in range (i + 1, n):

            # Find the product
            p *= abs(a[i] - a[j])

    # Return product
    return p

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 2, 3, 4]
    N = len(arr)

    # Function Call
    print (getProduct(arr, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the product of
// abs diff of all pairs (x, y)
static int getProduct(int []a, int n)
{

    // To store product
    int p = 1;

    // Iterate all possible pairs
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Find the product
            p *= Math.Abs(a[i] - a[j]);
        }
    }

    // Return product
    return p;
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    // Function call
    Console.Write(getProduct(arr, N));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the product of
// abs diff of all pairs (x, y)
function getProduct( a, n)
{
    // To store product
    var p = 1;

    // Iterate all possible pairs
    for (var i = 0; i < n; i++) {

        for (var j = i + 1; j < n; j++) {

            // Find the product
            p *= Math.abs(a[i] - a[j]);
        }
    }

    // Return product
    return p;
}

// Driver Code

// Given array arr[]
var arr = [ 1, 2, 3, 4 ];
var N = arr.length;

// Function Call
document.write( getProduct(arr, N));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*