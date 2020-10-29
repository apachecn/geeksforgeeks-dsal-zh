# 数组中可能的最大子集，以使任何元素都不是子集中任何其他元素的 K 倍

> 原文：[https://www.geeksforgeeks.org/largest-possible-subset-from-an-array-such-that-no-element-is-k-times-any-other-element-in-the-subset/](https://www.geeksforgeeks.org/largest-possible-subset-from-an-array-such-that-no-element-is-k-times-any-other-element-in-the-subset/)

给定由 **N** 个不同整数和整数 **K** 组成的数组 **arr []** ，任务是找到可能的最大子集大小，以确保没有元素 子集中的**是 K** 乘以子集的任何其他元素（即，子集中不应存在这样的对 **{n，m}** ，这样 **m = n * K** 或 **n = m * K** ）。

**示例**：

> **输入**：arr [] = {2，8，6，5，3}，K = 2
> **输出**：4
> **说明**：
> 数组中存在一个元素为 K（= 2）乘以另一个元素的唯一可能对为{6，3}。
> 因此，可以考虑不同时包含对{6，3}的两个元素的所有可能的子集。
> 因此，可能的最长子集的长度可以为 4。
> 
> **输入**：arr [] = {1、4、3、2}，K = 3
> **输出**：3

**方法**：[

]请按照以下步骤解决问题：

*   找到可能的对数，以使一个元素是给定数组中另一个元素的 K 倍

*   [按元素的**递增顺序**对](https://www.geeksforgeeks.org/sort-c-stl/)数组进行排序。

*   遍历数组并将数组元素的频率索引存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

*   初始化访问了的数组**，以标记每个索引，无论该元素是否包含在子集中 **0** ）（ **1** ）。**

*   再次遍历数组，对于 **vis [i] = 0** 的每个索引，检查 **Map** 中是否存在 **arr [i] * K** 。 如果找到，则增加对对的**计数，并设置 **vis [mp [arr [i] * K]] = 1** 。**

*   最后，打印 **N –对数**作为答案。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of 
// the above aproach 
#include <bits/stdc++.h> 
#define ll long long 
using namespace std; 

// Function to find the maximum 
// size of the required subset 
int findMaxLen(vector<ll>& a, ll k) 
{ 

    // Size of the array 
    int n = a.size(); 

    // Sort the array 
    sort(a.begin(), a.end()); 

    // Stores which index is 
    // included or excluded 
    vector<bool> vis(n, 0); 

    // Stores the indices of 
    // array elements 
    map<int, int> mp; 

    for (int i = 0; i < n; i++) { 
        mp[a[i]] = i; 
    } 

    // Count of pairs 
    int c = 0; 

    // Iterate through all 
    // the element 
    for (int i = 0; i < n; ++i) { 

        // If element is included 
        if (vis[i] == false) { 
            int check = a[i] * k; 

            // Check if a[i] * k is present 
            // in the array or not 
            if (mp.find(check) != mp.end()) { 

                // Increase count of pair 
                c++; 

                // Exclude the pair 
                vis[mp[check]] = true; 
            } 
        } 
    } 

    return n - c; 
} 

// Driver code 
int main() 
{ 

    int K = 3; 
    vector<ll> arr = { 1, 4, 3, 2 }; 

    cout << findMaxLen(arr, K); 
} 

```

## Java

```java

// Java implementation of 
// the above aproach 
import java.util.*; 

class GFG{ 

// Function to find the maximum 
// size of the required subset 
static int findMaxLen(int[] a, int k) 
{ 

    // Size of the array 
    int n = a.length; 

    // Sort the array 
    Arrays.sort(a); 

    // Stores which index is 
    // included or excluded 
    boolean []vis = new boolean[n]; 

    // Stores the indices of 
    // array elements 
    HashMap<Integer, 
            Integer> mp = new HashMap<Integer, 
                                      Integer>(); 

    for(int i = 0; i < n; i++) 
    { 
        mp.put(a[i], i); 
    } 

    // Count of pairs 
    int c = 0; 

    // Iterate through all 
    // the element 
    for(int i = 0; i < n; ++i) 
    { 

        // If element is included 
        if (vis[i] == false)  
        { 
            int check = a[i] * k; 

            // Check if a[i] * k is present 
            // in the array or not 
            if (mp.containsKey(check)) 
            { 

                // Increase count of pair 
                c++; 

                // Exclude the pair 
                vis[mp.get(check)] = true; 
            } 
        } 
    } 
    return n - c; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int K = 3; 
    int []arr = { 1, 4, 3, 2 }; 

    System.out.print(findMaxLen(arr, K)); 
} 
} 

// This code is contributed by amal kumar choubey  

```

## Python3

```py

# Python3 implementation of 
# the above approach 

# Function to find the maximum 
# size of the required subset 
def findMaxLen(a, k): 

    # Size of the array 
    n = len(a) 

    # Sort the array 
    a.sort() 

    # Stores which index is 
    # included or excluded 
    vis = [0] * n 

    # Stores the indices of 
    # array elements 
    mp = {} 

    for i in range(n): 
        mp[a[i]] = i 

    # Count of pairs 
    c = 0

    # Iterate through all 
    # the element 
    for i in range(n): 

        # If element is included 
        if(vis[i] == False): 
            check = a[i] * k 

            # Check if a[i] * k is present 
            # in the array or not 
            if(check in mp.keys()): 

                # Increase count of pair 
                c += 1

                # Exclude the pair  
                vis[mp[check]] = True

    return n - c 

# Driver Code 
if __name__ == '__main__': 

    K = 3
    arr = [ 1, 4, 3, 2 ] 

    print(findMaxLen(arr, K)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# implementation of 
// the above aproach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the maximum 
// size of the required subset 
static int findMaxLen(int[] a, int k) 
{ 

    // Size of the array 
    int n = a.Length; 

    // Sort the array 
    Array.Sort(a); 

    // Stores which index is 
    // included or excluded 
    bool []vis = new bool[n]; 

    // Stores the indices of 
    // array elements 
    Dictionary<int, 
               int> mp = new Dictionary<int, 
                                        int>(); 

    for(int i = 0; i < n; i++) 
    { 
        mp.Add(a[i], i); 
    } 

    // Count of pairs 
    int c = 0; 

    // Iterate through all 
    // the element 
    for(int i = 0; i < n; ++i) 
    { 

        // If element is included 
        if (vis[i] == false)  
        { 
            int check = a[i] * k; 

            // Check if a[i] * k is present 
            // in the array or not 
            if (mp.ContainsKey(check)) 
            { 

                // Increase count of pair 
                c++; 

                // Exclude the pair 
                vis[mp[check]] = true; 
            } 
        } 
    } 
    return n - c; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int K = 3; 
    int []arr = { 1, 4, 3, 2 }; 

    Console.Write(findMaxLen(arr, K)); 
} 
} 

// This code is contributed by gauravrajput1 

```

**Output:** 

```
3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



