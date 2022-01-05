# 一个阵列的所有子阵列的乘积|集合 2

> 原文:[https://www . geeksforgeeks . org/全阵列子阵列产品集-2/](https://www.geeksforgeeks.org/product-of-all-subarrays-of-an-array-set-2/)

给定一个大小为 **N** 的整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到数组的所有[子数组的乘积。
**举例:**](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/) 

> **输入:** arr[] = {2，4}
> **输出:** 64
> **解释:**
> 这里，子阵是{2}、{2，4}和{4}。
> 每个子阵的产品是 2、8、4。
> 所有子阵列的乘积= 64
> **输入:** arr[] = {1，2，3}
> **输出:** 432
> **说明:**
> 这里，子阵列为{1}、{1，2}、{1，2，3}、{2}、{2，3}、{3}。
> 每个子阵的产品是 1、2、6、2、6、3。
> 所有子阵列的乘积= 432

**天真迭代的方法:**这些方法请参考[本帖](https://www.geeksforgeeks.org/product-of-all-subarrays-of-an-array/)。
**方法:**想法是统计所有子阵列中出现的每个元素的数量。为了计数，我们有以下观察:

*   在以 **arr[i]** 开始的每个子阵列中，都有以元素 **arr[i]** 开始的**(N–I)**这样的子集。
    **例如:**

> 对于数组 arr[] = {1，2，3}
> N = 3，对于元素 2，即索引= 1
> 有(N–索引)= 3–1 = 2 的子集
> {2}和{2，3}

*   对于任何元素 **arr[i]** ，都有**(N–I)* I**子阵列，其中 **arr[i]** 不是第一个元素。

> 对于数组 arr[] = {1，2，3}
> N = 3，对于元素 2，即索引= 1
> 有(N–索引)*索引=(3–1)* 1 = 2 个子集，其中 2 不是第一个元素。
> {1，2}和{1，2，3}

因此，根据以上观察，每个元素的总数**arr【I】**出现在所有子阵列中，每个索引 I 由下式给出:

```
total_elements = (N - i) + (N - i)*i
total_elements = (N - i)*(i + 1) 
```

其思想是将每个元素**(N–I)*(I+1)**的次数相乘，得到所有子阵列中元素的乘积。
以下是上述办法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the product of
// elements of all subarray
long int SubArrayProdct(int arr[],
                        int n)
{
    // Initialize the result
    long int result = 1;

    // Computing the product of
    // subarray using formula
    for (int i = 0; i < n; i++)
        result *= pow(arr[i],
                      (i + 1) * (n - i));

    // Return the product of all
    // elements of each subarray
    return result;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << SubArrayProdct(arr, N)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the product of
// elements of all subarray
static int SubArrayProdct(int arr[], int n)
{

    // Initialize the result
    int result = 1;

    // Computing the product of
    // subarray using formula
    for(int i = 0; i < n; i++)
       result *= Math.pow(arr[i], (i + 1) *
                                  (n - i));

    // Return the product of all
    // elements of each subarray
    return result;
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = new int[]{2, 4};

    int N = arr.length;

    // Function Call
    System.out.println(SubArrayProdct(arr, N));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the product of
# elements of all subarray
def SubArrayProdct(arr, n):

    # Initialize the result
    result = 1;

    # Computing the product of
    # subarray using formula
    for i in range(0, n):
        result *= pow(arr[i],
                     (i + 1) * (n - i));

    # Return the product of all
    # elements of each subarray
    return result;

# Driver Code

# Given array arr[]
arr = [ 2, 4 ];
N = len(arr);

# Function Call
print(SubArrayProdct(arr, N))

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the product of
// elements of all subarray
static int SubArrayProdct(int []arr, int n)
{

    // Initialize the result
    int result = 1;

    // Computing the product of
    // subarray using formula
    for(int i = 0; i < n; i++)
       result *= (int)(Math.Pow(arr[i], (i + 1) *
                                        (n - i)));

    // Return the product of all
    // elements of each subarray
    return result;
}

// Driver code
public static void Main()
{

    // Given array arr[]
    int []arr = new int[]{2, 4};

    int N = arr.Length;

    // Function Call
    Console.Write(SubArrayProdct(arr, N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the product of
// elements of all subarray
function SubArrayProdct(arr, n)
{

    // Initialize the result
    let result = 1;

    // Computing the product of
    // subarray using formula
    for(let i = 0; i < n; i++)
       result *= Math.pow(arr[i], (i + 1) *
                                  (n - i));

    // Return the product of all
    // elements of each subarray
    return result;
}

// Driver code

     // Given array arr[]
    let arr = [2, 4];

    let N = arr.length;

    // Function Call
    document.write(SubArrayProdct(arr, N));

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
64
```

**时间复杂度:** *O(N)* ，其中 N 为元素个数。
T5【辅助空间: *O(1)*