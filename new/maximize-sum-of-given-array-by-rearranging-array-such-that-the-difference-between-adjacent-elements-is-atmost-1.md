# 通过重新排列数组以使相邻元素之间的差最大为 1，来最大化给定数组的总和。

> 原文：[https://www.geeksforgeeks.org/maximize-sum-of-given-array-by-rearranging-array-such-that-the-difference-between-adjacent-elements-is-atmost-1/](https://www.geeksforgeeks.org/maximize-sum-of-given-array-by-rearranging-array-such-that-the-difference-between-adjacent-elements-is-atmost-1/)

给定由`N`个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，任务是最大化数组元素的总和，以使数组的第一个元素为 **1**，执行以下操作后，数组相邻元素之间的差最大为 **1**：

*   以任何方式重新排列数组元素。

*   将任何元素减少为至少 **1** 的任何数字。

**示例**：

> **输入**：`arr[] = {3, 5, 1}`
>
> **输出**：6
>
> **说明**：
>
> 一种可能的排列`{1, 2, 3}`具有最大可能的和 6。
> 
> **输入**：`arr[] = {1, 2, 2, 2, 3, 4, 5}`
>
> **输出**：19
>
> **说明**：
>
> 一种可能的安排是`{1, 2, 2, 2, 3, 4, 5}`，其最大和为 19。

**朴素的方法**：最简单的方法是[对给定的数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)，然后遍历已排序的数组并减少不满足给定条件的元素。

**时间复杂度**：`O(N * log N)`，其中`N`是给定数组的大小。

**辅助空间**：`O(n)`

**高效方法**：的想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)概念来存储给定数组元素的频率。 请按照以下步骤解决问题：

*   创建大小为`N + 1`的辅助数组`count[]`，以存储`arr[i]`的频率。

*   将频率存储在`count[]`中，并且如果`arr[i]`大于`N`，则增加`count[N]`。

*   将`size`和`sum`初始化为 **0**，它们分别存储先前选择的整数和最大可能和。

*   [使用变量`K`遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)`count[]`数组，然后执行以下操作：

    *   对每个`K`执行循环，直到`count[K] > 0`和`size < K`。

    *   在`while`循环中将`size`增大 **1**，将`sum`增大`size`，将`count[k]`减小 **1**。

    *   在`while`循环结束后，以`K * count[K]`递增`sum`。

*   完成上述步骤后，将`sum`的值打印为最大可能值。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <iostream> 
using namespace std; 

// Function to find maximum possible 
// sum after changing the array elements 
// as per the given constraints 
long maxSum(int a[], int n) 
{ 

    // Stores the frequency of 
    // elements in given array 
    int count[n + 1] = {0}; 

    // Update frequncy 
    for(int i = 0; i < n; i++) 
        count[min(a[i], n)]++; 

    // Stores the previously 
    // selected integer 
    int size = 0; 

    // Stores the maximum possible sum 
    long ans = 0; 

    // Traverse over array count[] 
    for(int k = 1; k <= n; k++)  
    { 

        // Run loop for each k 
        while (count[k] > 0 && size < k) 
        { 
            size++; 
            ans += size; 
            count[k]--; 
        } 

        // Update ans 
        ans += k * count[k]; 
    } 

    // Return maximum possible sum 
    return ans; 
} 

// Driver Code 
int main() 
{ 

    // Given array arr[] 
    int arr[] = { 3, 5, 1 }; 

    // Size of array 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Function Call 
    cout << (maxSum(arr, n)); 
    return 0; 
} 

// This code is contributed by akhilsaini

```

## Java

```java

// Java program for the above approach 

import java.util.*; 

class GFG { 

    // Function to find maximum possible 
    // sum after changing the array elements 
    // as per the given constraints 
    static long maxSum(int[] a) 
    { 
        // Length of given array 
        int n = a.length; 

        // Stores the frequency of 
        // elements in given array 
        int[] count = new int[n + 1]; 

        // Update frequncy 
        for (int x : a) 
            count[Math.min(x, n)]++; 

        // stores the previously 
        // selected integer 
        int size = 0; 

        // Stores the maximum possible sum 
        long ans = 0; 

        // Traverse over array count[] 
        for (int k = 1; k <= n; k++) { 

            // Run loop for each k 
            while (count[k] > 0 && size < k) { 
                size++; 
                ans += size; 
                count[k]--; 
            } 

            // Update ans 
            ans += k * count[k]; 
        } 

        // Return maximum possible sum 
        return ans; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given array arr[] 
        int[] arr = { 3, 5, 1 }; 

        // Function Call 
        System.out.println(maxSum(arr)); 
    } 
} 

```

## Python3

```py

# Python3 program for the above approach 

# Function to find maximum possible 
# sum after changing the array elements 
# as per the given constraints 
def maxSum(a, n): 

    # Stores the frequency of 
    # elements in given array 
    count = [0] * (n + 1) 

    # Update frequncy 
    for i in range(0, n): 
        count[min(a[i], n)] += 1

    # stores the previously 
    # selected integer 
    size = 0

    # Stores the maximum possible sum 
    ans = 0

    # Traverse over array count[] 
    for k in range(1, n + 1): 

        # Run loop for each k 
        while (count[k] > 0 and size < k): 
            size += 1
            ans += size 
            count[k] -= 1

        # Update ans 
        ans += k * count[k] 

    # Return maximum possible sum 
    return ans 

# Driver Code 
if __name__ == '__main__': 

    # Given array arr[] 
    arr = [ 3, 5, 1 ] 

    # Size of array 
    n = len(arr) 

    # Function Call 
    print(maxSum(arr, n)) 

# This code is contributed by akhilsaini

```

## C#

```cs

// C# program for the above approach 
using System; 

class GFG{ 

// Function to find maximum possible 
// sum after changing the array elements 
// as per the given constraints 
static long maxSum(int[] a) 
{ 

    // Length of given array 
    int n = a.Length; 

    // Stores the frequency of 
    // elements in given array 
    int[] count = new int[n + 1]; 

    // Update frequncy 
    for(int i = 0; i < n; i++) 
        count[Math.Min(a[i], n)]++; 

    // stores the previously 
    // selected integer 
    int size = 0; 

    // Stores the maximum possible sum 
    long ans = 0; 

    // Traverse over array count[] 
    for(int k = 1; k <= n; k++) 
    { 

        // Run loop for each k 
        while (count[k] > 0 && size < k) 
        { 
            size++; 
            ans += size; 
            count[k]--; 
        } 

        // Update ans 
        ans += k * count[k]; 
    } 

    // Return maximum possible sum 
    return ans; 
} 

// Driver Code 
public static void Main() 
{ 

    // Given array arr[] 
    int[] arr = { 3, 5, 1 }; 

    // Function call 
    Console.Write(maxSum(arr)); 
} 
} 

// This code is contributed by akhilsaini

```

**输出**： 

```
6

```

**时间复杂度**：`O(n)`，其中`N`是给定数组的大小。

**辅助空间**：`O(n)`



* * *

* * *



