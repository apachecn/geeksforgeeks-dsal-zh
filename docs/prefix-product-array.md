# 前缀积数组

> 原文:[https://www.geeksforgeeks.org/prefix-product-array/](https://www.geeksforgeeks.org/prefix-product-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是根据给定的数组生成一个前缀乘积数组。

> 在前缀乘积数组中，i <sup>第</sup>项**优先于[I]**= arr[I]* arr[I–1]*……* arr[0]

**例:**

> **输入:** {1，2，3，4，5}
> **输出:** {1，2，6，24，120}
> **解释:**
> 前缀积数组将为{1，2*1，3*2*1，4*3*2*1，5*4*3*2*1} = {1，2，6，24，120}
> **输入:** {2，4

**进场:**
按照以下步骤解决问题:

*   迭代给定数组，从索引 **1** 到**N–1**。

*   计算每个 **i <sup>第</sup>T3】指数的 arr[i] = arr[i] * arr[i-1]。** 
*   最后，打印前缀产品数组。

下面是上述方法的实现。

## C++

```
// C++ Program to generate
// Prefix Product Array
#include <bits/stdc++.h>
using namespace std;

// Function to generate
// prefix product array
int prefixProduct(int a[],
                  int n)
{
    // Update the array
    // with the product of
    // prefixes
    for (int i = 1; i < n; i++) {
        a[i] = a[i] * a[i - 1];
    }

    // Print the array
    for (int j = 0; j < n; j++) {
        cout << a[j] << ", ";
    }

    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 6, 5, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    prefixProduct(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate
// Prefix Product Array
class GFG{

// Function to generate
// prefix product array
static int prefixProduct(int []a, int n)
{

    // Update the array
    // with the product of
    // prefixes
    for(int i = 1; i < n; i++)
    {
       a[i] = a[i] * a[i - 1];
    }

    // Print the array
    for(int j = 0; j < n; j++)
    {
       System.out.print(a[j] + ", ");
    }

    return 0;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = new int[]{ 2, 4, 6, 5, 10 };
    int N = 5;

    prefixProduct(arr, N);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 Program to generate
# Prefix Product Array

# Function to generate
# prefix product array
def prefixProduct(a, n):

    # Update the array
    # with the product of
    # prefixes
    for i in range(1, n):
        a[i] = a[i] * a[i - 1];

    # Print the array
    for j in range(0, n):
        print(a[j], end = ", ");

    return 0;

# Driver Code
arr = [ 2, 4, 6, 5, 10 ];
N = len(arr);
prefixProduct(arr, N);

# This code is contributed by Code_Mech
```

## C#

```
// C# program to generate
// Prefix Product Array
using System;
class GFG{

// Function to generate
// prefix product array
static int prefixProduct(int []a, int n)
{

    // Update the array
    // with the product of
    // prefixes
    for(int i = 1; i < n; i++)
    {
        a[i] = a[i] * a[i - 1];
    }

    // Print the array
    for(int j = 0; j < n; j++)
    {
        Console.Write(a[j] + ", ");
    }
    return 0;
}

// Driver Code
public static void Main (string[] args)
{
    int []arr = new int[]{ 2, 4, 6, 5, 10 };
    int N = 5;

    prefixProduct(arr, N);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

    // Javascript Program to generate
    // Prefix Product Array

    // Function to generate
    // prefix product array
    function prefixProduct(a, n)
    {
        // Update the array
        // with the product of
        // prefixes
        for (let i = 1; i < n; i++) {
            a[i] = a[i] * a[i - 1];
        }

        // Print the array
        for (let j = 0; j < n; j++) {
            document.write(a[j] + ", ");
        }

        return 0;
    }

    let arr = [ 2, 4, 6, 5, 10 ];
    let N = arr.length;
    prefixProduct(arr, N);

</script>
```

**Output:** 

```
2, 8, 48, 240, 2400
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*