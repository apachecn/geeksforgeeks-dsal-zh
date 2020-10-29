# 可以删除的最大元素数，以使给定阵列的 MEX 保持不变

> 原文：[https://www.geeksforgeeks.org/maximum-number-of-elements-that-can-be-removed-such-that-mex-of-the-given-array-remains-unchanged/](https://www.geeksforgeeks.org/maximum-number-of-elements-that-can-be-removed-such-that-mex-of-the-given-array-remains-unchanged/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是计算在不更改[[ 原始阵列的 **MEX** 。

> **MEX** 是数组中不存在的[最小正整数。](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)

**示例**：

> **输入**：arr [] = {2，3，5，1，6}。
> **输出**：2
> **说明**：
> 数组中不存在的最小正整数为 4。
> 因此，给定数组的 MEX 为 4。
> 因此，可以删除 5 和 6 而无需更改数组的 MEX。
> 
> **输入**：arr [] = {12，4，6，1，7，2}。
> **输出**：4
> **说明**：
> 数组中不存在的最小正整数是 3。
> 因此，给定数组的 MEX 为 3。
> 因此，可以在不更改数组 MEX 的情况下删除 4、6、7 和 12。 。

**朴素的方法**：最简单的方法是[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)排序，然后[从 **i = 0** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，而 **arr [ i]** 等于 **i +1** 。 之后，将答案打印为**（N – i）**，这是在不更改其 **MEX** 的情况下可以从给定数组中删除的最大元素数。

**时间复杂度**：O（N * log N）

**辅助空间**：`O(n)`

**高效方法**：为了优化上述方法，其思想是使用[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)。 请注意，可以删除的最大元素数是大于 **MEX** 的元素数。 请按照以下步骤解决问题：

1.  初始化长度为 **N + 1** 的数组 **hash []** ，其中，如果元素 **i [ **hash [i]** 为 **1** HTG9]存在于给定的数组中，否则 **hash [i] =0。****

2.  用 **N +1** 初始化变量 **mex** ，以存储给定阵列的 **MEX** 。

3.  在 **[1，N]** 范围内遍历数组 **hash []** ，如果有任何索引**，则 hash [i]** 等于 **0** ，将 **mex** 更新为 **mex = i** ，然后退出循环。

4.  打印 **N –（mex – 1）**作为可以从给定数组中删除的最大元素数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the maximum number 
// of elements that can be removed 
void countRemovableElem( 
    int arr[], int N) 
{ 
    // Initialize hash[] with 0s 
    int hash[N + 1] = { 0 }; 

    // Initialize MEX 
    int mex = N + 1; 

    // Set hash[i] = 1, if i is 
    // present in arr[] 
    for (int i = 0; i < N; i++) { 
        if (arr[i] <= N) 
            hash[arr[i]] = 1; 
    } 

    // Find MEX from the hash 
    for (int i = 1; i <= N; i++) { 
        if (hash[i] == 0) { 
            mex = i; 
            break; 
        } 
    } 

    // Print the maximum numbers 
    // that can be removed 
    cout << N - (mex - 1); 
} 

// Driver Code 
int main() 
{ 
    // Given array 
    int arr[] = { 2, 3, 5, 1, 6 }; 

    // Size of the array 
    int N = sizeof(arr) / sizeof(arr[0]); 

    // Function Call 
    countRemovableElem(arr, N); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.io.*; 
import java.util.*; 

class GFG{ 

// Function to find the maximum number 
// of elements that can be removed 
static void countRemovableElem(int[] arr, int N) 
{ 

    // Initialize hash[] with 0s 
    int[] hash = new int[N + 1]; 
    Arrays.fill(hash, 0); 

    // Initialize MEX 
    int mex = N + 1; 

    // Set hash[i] = 1, if i is 
    // present in arr[] 
    for(int i = 0; i < N; i++)  
    { 
        if (arr[i] <= N) 
            hash[arr[i]] = 1; 
    } 

    // Find MEX from the hash 
    for(int i = 1; i <= N; i++)  
    { 
        if (hash[i] == 0) 
        { 
            mex = i; 
            break; 
        } 
    } 

    // Print the maximum numbers 
    // that can be removed 
    System.out.println(N - (mex - 1)); 
} 

// Driver Code 
public static void main(String[] args) 
{ 

    // Given array 
    int[] arr = { 2, 3, 5, 1, 6 }; 

    // Size of the array 
    int N = arr.length; 

    // Function Call 
    countRemovableElem(arr, N); 
} 
} 

// This code is contributed by akhilsaini

```

## Python3

```py

# Pyhton3 program for the above approach 

# Function to find the maximum number 
# of elements that can be removed 
def countRemovableElem(arr, N): 

    # Initialize hash[] with 0s 
    hash = [0] * (N + 1) 

    # Initialize MEX 
    mex = N + 1

    # Set hash[i] = 1, if i is 
    # present in arr[] 
    for i in range(0, N): 
        if (arr[i] <= N): 
            hash[arr[i]] = 1

    # Find MEX from the hash 
    for i in range(1, N + 1): 
        if (hash[i] == 0): 
            mex = i 
            break

    # Print the maximum numbers 
    # that can be removed 
    print(N - (mex - 1)) 

# Driver Code 
if __name__ == '__main__': 

    # Given array 
    arr = [ 2, 3, 5, 1, 6 ] 

    # Size of the array 
    N = len(arr) 

    # Function Call 
    countRemovableElem(arr, N) 

# This code is contributed by akhilsaini

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the maximum number 
// of elements that can be removed 
static void countRemovableElem(int[] arr, int N) 
{ 

    // Initialize hash[] with 0s 
    int[] hash = new int[N + 1]; 
    Array.Fill(hash, 0); 

    // Initialize MEX 
    int mex = N + 1; 

    // Set hash[i] = 1, if i is 
    // present in arr[] 
    for(int i = 0; i < N; i++) 
    { 
        if (arr[i] <= N) 
            hash[arr[i]] = 1; 
    } 

    // Find MEX from the hash 
    for(int i = 1; i <= N; i++)  
    { 
        if (hash[i] == 0) 
        { 
            mex = i; 
            break; 
        } 
    } 

    // Print the maximum numbers 
    // that can be removed 
    Console.WriteLine(N - (mex - 1)); 
} 

// Driver Code 
public static void Main() 
{ 

    // Given array 
    int[] arr = { 2, 3, 5, 1, 6 }; 

    // Size of the array 
    int N = arr.Length; 

    // Function Call 
    countRemovableElem(arr, N); 
} 
} 

// This code is contributed by akhilsaini

```

**Output:** 

```
2

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



