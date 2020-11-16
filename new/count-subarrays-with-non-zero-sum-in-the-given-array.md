# 计算给定数组中总和非零的子数组数量

> 原文：[https://www.geeksforgeeks.org/count-subarrays-with-non-zero-sum-in-the-given-array/](https://www.geeksforgeeks.org/count-subarrays-with-non-zero-sum-in-the-given-array/)



给定大小为`N`的数组`arr[]`，任务是计算给定数组`arr[]`的子数组的总数，该子数组具有非零和。

**示例**：

> **输入**：`arr[] = {-2, 2, -3}`
>
> **输出**：4
>
> **说明**：
>
> 非零和子数组为：`[-2], [2], [2, -3], [-3]`。 给定输入数组的所有可能的子数组为`[-2], [2], [-3], [2, -2], [2, -3], [-2, 2, -3]`。 其中`[2, -2]`不包括在计数中，因为`2 + (-2) = 0`且未选择`[-2, 2, -3]`，因为该数组的子数组`[2, -2]`元素的总和为零。
>
> **输入**：`arr[] = {1, 3, -2, 4, -1}`
>
> **输出**：15
>
> **说明**：
>
> 给定数组`{1, 3, -2, 4, -1}`有 15 个子数组，它们的总和不为零。

**方法**：

解决上述问题的主要思想是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[映射数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。

*   首先，构建给定数组的**前缀和数组**，并使用以下公式检查子数组是否具有 0 个元素和。

> 子数组的总和`[L, R] = prefix[R] – prefix[L – 1]`。 因此，如果子数组`[L, R]`的总和为 0
> ，则`Prefix[R] – Prefix[L – 1] = 0`。因此，`Prefix[R] = Prefix[L – 1]`。

*   现在，从 1 迭代到`N`，并保留一个**哈希表**，用于存储元素的上一次出现的索引和一个变量，假设`last`，并将其初始化为 0。

*   检查`Prefix[i]`是否已存在于哈希中。 如果是，则最后更新为`last = max（last，hash [Prefix [i]] + 1）`。 否则，在答案中添加`i – last`并更新哈希表。

下面是上述方法的实现：

## C++

```cpp

// C++ program to Count the total number of 
// subarrays for a given array such that its 
// subarray should have non zero sum

#include <bits/stdc++.h>
using namespace std;

// Function to build the Prefix sum array
vector<int> PrefixSumArray(int arr[], int n)
{
    vector<int> prefix(n);

    // Store prefix of the first position
    prefix[0] = arr[0];

    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    return prefix;
}

// Function to return the Count of
// the total number of subarrays
int CountSubarray(int arr[], int n)
{
    vector<int> Prefix(n);

    // Calculating the prefix array
    Prefix = PrefixSumArray(arr, n);

    int last = 0, ans = 0;

    map<int, int> Hash;

    Hash[0] = -1;

    for (int i = 0; i <= n; i++) {
        // Check if the element already exists
        if (Hash.count(Prefix[i]))
            last = max(last, Hash[Prefix[i]] + 1);

        ans += max(0, i - last);

        // Mark the element
        Hash[Prefix[i]] = i;
    }

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, -2, 4, -1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << CountSubarray(arr, N);
}

```

## Java

```java

// Java program to count the total number of 
// subarrays for a given array such that its 
// subarray should have non zero sum
import java.util.*;

class GFG{

// Function to build the Prefix sum array
static int[] PrefixSumArray(int arr[], int n)
{
    int []prefix = new int[n];

    // Store prefix of the first position
    prefix[0] = arr[0];

    for(int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];

    return prefix;
}

// Function to return the Count of
// the total number of subarrays
static int CountSubarray(int arr[], int n)
{
    int []Prefix = new int[n];

    // Calculating the prefix array
    Prefix = PrefixSumArray(arr, n);

    int last = 0, ans = 0;

    HashMap<Integer,
            Integer> Hash = new HashMap<Integer,
                                        Integer>();

    Hash.put(0, -1);

    for(int i = 0; i <= n; i++) 
    {

        // Check if the element already exists
        if (i < n && Hash.containsKey(Prefix[i]))
            last = Math.max(last, 
                            Hash.get(Prefix[i]) + 1);

        ans += Math.max(0, i - last);

        // Mark the element
        if (i < n)
        Hash.put(Prefix[i], i);
    }

    // Return the final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, -2, 4, -1 };

    int N = arr.length;

    System.out.print(CountSubarray(arr, N));
}
}

// This code is contributed by amal kumar choubey

```

## Python3

```py

# Python3 program to count the total number  
# of subarrays for a given array such that 
# its subarray should have non zero sum 

# Function to build the prefix sum array 
def PrefixSumArray(arr, n):

    prefix = [0] * (n + 1); 

    # Store prefix of the first position 
    prefix[0] = arr[0]; 

    for i in range(1, n):
        prefix[i] = prefix[i - 1] + arr[i]; 

    return prefix; 

# Function to return the count of 
# the total number of subarrays 
def CountSubarray(arr, n): 

    Prefix = [0] * (n + 1); 

    # Calculating the prefix array 
    Prefix = PrefixSumArray(arr, n); 

    last = 0; ans = 0; 

    Hash = {}; 

    Hash[0] = -1; 

    for i in range(n + 1):

        # Check if the element already exists 
        if (Prefix[i] in Hash):
            last = max(last, Hash[Prefix[i]] + 1); 

        ans += max(0, i - last); 

        # Mark the element 
        Hash[Prefix[i]] = i; 

    # Return the final answer 
    return ans; 

# Driver code 
if __name__ == "__main__" : 

    arr = [ 1, 3, -2, 4, -1 ]; 
    N = len(arr); 

    print(CountSubarray(arr, N)); 

# This code is contributed by AnkitRai01

```

## C#

```cs

// C# program to count the total number of 
// subarrays for a given array such that its 
// subarray should have non zero sum
using System;
using System.Collections.Generic;
class GFG{

// Function to build the Prefix sum array
static int[] PrefixSumArray(int []arr, int n)
{
    int []prefix = new int[n];

    // Store prefix of the first position
    prefix[0] = arr[0];

    for(int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + arr[i];
    return prefix;
}

// Function to return the Count of
// the total number of subarrays
static int CountSubarray(int []arr, int n)
{
    int []Prefix = new int[n];

    // Calculating the prefix array
    Prefix = PrefixSumArray(arr, n);

    int last = 0, ans = 0;
    Dictionary<int,
               int> Hash = new Dictionary<int,
                                          int>();
    Hash.Add(0, -1);
    for(int i = 0; i <= n; i++) 
    {        
        // Check if the element already exists
        if (i < n && Hash.ContainsKey(Prefix[i]))
            last = Math.Max(last, 
                            Hash[Prefix[i]] + 1);

        ans += Math.Max(0, i - last);

        // Mark the element
        if (i < n)
        Hash.Add(Prefix[i], i);
    }

    // Return the readonly answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {1, 3, -2, 4, -1};
    int N = arr.Length;
    Console.Write(CountSubarray(arr, N));
}
}

// This code is contributed by shikhasingrajput

```

**输出**： 

```
15

```

**时间复杂度**：`O(n)`。



* * *

* * *



