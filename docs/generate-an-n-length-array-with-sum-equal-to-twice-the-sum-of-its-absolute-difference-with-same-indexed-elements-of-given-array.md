# 生成一个 N 长度数组，其和等于给定数组中相同索引元素的绝对差之和的两倍

> 原文:[https://www . geesforgeks . org/generate-n-length-array，其和等于给定数组的相同索引元素的绝对差之和的两倍/](https://www.geeksforgeeks.org/generate-an-n-length-array-with-sum-equal-to-twice-the-sum-of-its-absolute-difference-with-same-indexed-elements-of-given-array/)

给定大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是构建大小为 **N** 的阵列 **brr[]** ，满足以下条件:

*   在数组 **brr[]** 中的每对连续元素中，一个元素必须能被另一个元素整除，即 **brr[i]** 必须能被 **brr[i + 1]** 整除，反之亦然。
*   阵列中的每个**I**元素 **brr[]** 必须满足 **brr[i] > = arr[i] / 2** 。
*   数组 **arr[]** 元素的[和必须大于或等于**2 *σABS(arr[I]–brr[I])**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = { 11，5，7，3，2 }
> T3】输出:8 4 4 2
> T6】解释:T8】ABS(11–8)+ABS(5–4)+ABS(7–4)+ABS(3–2)+ABS(2–2)= 8
> arr[0]+arr[1]+…+arr[4]= 28
> 2 * 8<= 28 和
> 因此，brr[]的可能值之一是 8 4 4 2 2。
> 
> **输入:** arr[] = { 11，7，5 }
> **输出:** { 8，4，4 }

**方法:**这个想法基于以下观察:

> 如果 **brr[i]** 是 2 的[最近次幂，并且小于或等于 **arr[i]** ，那么 **brr[i]** 必须大于或等于 **arr[i] / 2** 以及数组的元素之和](https://www.geeksforgeeks.org/find-the-nearest-power-of-2-for-every-array-element/)， **arr[]** 必须大于或等于**2 *σABS(arr[I]–brr**

按照以下步骤解决问题:

*   初始化一个数组 **brr[]** ，存储满足给定条件的元素。
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。[对于每一个 **i <sup>th</sup>** 元素，找到最近的小于或等于**arr【I】**的 **2**](https://www.geeksforgeeks.org/find-the-nearest-power-of-2-for-every-array-element/) 的幂，存入**brr【I】**。
*   最后，[打印数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/) **brr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct an array
// with given conditions
void constructArray(int arr[], int N)
{
    int brr[N] = { 0 };

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        int K = log(arr[i]) / log(2);

        // Stores closest power of 2
        // less than or equal to arr[i]
        int R = pow(2, K);

        // Stores R into brr[i]
        brr[i] = R;
    }

    // Print array elements
    for (int i = 0; i < N; i++) {
        cout << brr[i] << " ";
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 11, 5, 7, 3, 2 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    constructArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to conan array
// with given conditions
static void constructArray(int arr[], int N)
{
    int brr[] = new int[N];

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        int K = (int)(Math.log(arr[i]) /
                      Math.log(2));

        // Stores closest power of 2
        // less than or equal to arr[i]
        int R = (int)Math.pow(2, K);

        // Stores R into brr[i]
        brr[i] = R;
    }

    // Print array elements
    for(int i = 0; i < N; i++)
    {
        System.out.print(brr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 11, 5, 7, 3, 2 };

    // Size of the array
    int N = arr.length;

    // Function Call
    constructArray(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log

# Function to construct an array
# with given conditions
def constructArray(arr, N):
    brr = [0]*N

    # Traverse the array arr[]
    for i in range(N):
        K = int(log(arr[i])/log(2))

        # Stores closest power of 2
        # less than or equal to arr[i]
        R = pow(2, K)

        # Stores R into brr[i]
        brr[i] = R

    # Prarray elements
    for i in range(N):
        print(brr[i], end = " ")

# Driver Code
if __name__ == '__main__':

  # Given array
    arr = [11, 5, 7, 3, 2]

    # Size of the array
    N = len(arr)

    # Function Call
    constructArray(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach   
using System;   

class GFG{   

// Function to construct an array   
// with given conditions   
static void constructArray(int []arr, int N)   
{   
    int[] brr = new int[N];   
    Array.Clear(brr, 0, brr.Length);   

    // Traverse the array arr[]   
    for(int i = 0; i < N; i++)
    {   
        int K = (int)(Math.Log(arr[i]) /
                      Math.Log(2));   

        // Stores closest power of 2   
        // less than or equal to arr[i]   
        int R = (int)Math.Pow(2, K);   

        // Stores R into brr[i]   
        brr[i] = R;   
    }   

    // Print array elements   
    for(int i = 0; i < N; i++)
    {
        Console.Write(brr[i] + " ");   
    }   
}   

// Driver Code   
public static void Main()   
{   

    // Given array   
    int []arr = { 11, 5, 7, 3, 2 };   

    // Size of the array   
    int N = arr.Length;   

    // Function Call   
    constructArray(arr, N);   
}   
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to conan array
    // with given conditions
    function constructArray(arr , N) {
        var brr = Array(N).fill(0);

        // Traverse the array arr
        for (i = 0; i < N; i++) {
            var K = parseInt( (Math.log(arr[i]) / Math.log(2)));

            // Stores closest power of 2
            // less than or equal to arr[i]
            var R = parseInt( Math.pow(2, K));

            // Stores R into brr[i]
            brr[i] = R;
        }

        // Print array elements
        for (i = 0; i < N; i++) {
            document.write(brr[i] + " ");
        }
    }

    // Driver Code

        // Given array
        var arr = [ 11, 5, 7, 3, 2 ];

        // Size of the array
        var N = arr.length;

        // Function Call
        constructArray(arr, N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
8 4 4 2 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)