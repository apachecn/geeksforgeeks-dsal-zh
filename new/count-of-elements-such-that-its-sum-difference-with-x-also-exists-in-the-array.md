# 元素计数，以使其与 X 的和/差也存在于数组

> 原文：[https://www.geeksforgeeks.org/count-of-elements-such-that-its-sum-difference-with-x-also-exists-in-the-array/](https://www.geeksforgeeks.org/count-of-elements-such-that-its-sum-difference-with-x-also-exists-in-the-array/)

中

给定数组 **arr []** 和整数 **X** ，任务是对数组中的元素进行计数，以使它们在数组中存在元素![arr[i] - X](img/6481a6ffc9c0d160f8f6f17e3edfb950.png "Rendered by QuickLaTeX.com")或![arr[i] + X](img/e8db3b0f5854bd8b73da0cf3e3d4ef2a.png "Rendered by QuickLaTeX.com")。

**示例**：

> **输入**：arr [] = {3，4，2，5}，X = 2
> **输出**：4
> **说明**：
> 在上述示例中，有 4 个此类数字–
> 对于元素 3：数组
> 中可能存在 1、5，而在数组
> 中存在 5 对于元素 4：可能的数字为 2、6，而 2 对于元素 2：存在于数组
> 中；可能的数字为 0、4，而在数组
> 中存在于数字 4：对于元素 5：可能的数字为 3、7，而在数组
> 中存在 3。 计数= 4
> 
> **输入**：arr [] = {2，2，4，5，6}，X = 3
> **输出**：3
> **说明**：
> 在上述示例中，有 3 个这样的数字{2，2，5}

**方法**：这个想法是使用[哈希映射](https://www.geeksforgeeks.org/hashing-data-structure/)检查元素是否在`O(1)`时间出现在哈希映射中。 然后，遍历数组的元素，并针对每个元素检查数组中是否存在![arr[i] - X](img/6481a6ffc9c0d160f8f6f17e3edfb950.png "Rendered by QuickLaTeX.com")或![arr[i] + X](img/e8db3b0f5854bd8b73da0cf3e3d4ef2a.png "Rendered by QuickLaTeX.com")。 如果是，则将此类元素的计数加 1。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count of 
// elements such that its sum/difference 
// with X also exists in the Array 

#include <bits/stdc++.h> 

using namespace std; 

// Function to find the count of 
// elements in the array such that 
// element at the difference at X 
// is present in the array 
void findAns(int arr[], int n, int x) 
{ 
    int ans; 
    unordered_set<int> s; 

    // Loop to insert the elements 
    // of the array into the set 
    for (int i = 0; i < n; i++) 
        s.insert(arr[i]); 

    ans = 0; 

    // Loop to iterate over the array 
    for (int i = 0; i < n; i++) { 

        // if any of the elements are there 
        // then increse the count variable 
        if (s.find(arr[i] + x) != s.end() || s.find(arr[i] - x) != s.end()) 
            ans++; 
    } 
    cout << ans; 
    return; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 2, 2, 4, 5, 6 }; 
    int n = sizeof(arr) / sizeof(int); 
    int x = 3; 

    findAns(arr, n, x); 

    return 0; 
} 

```

## Java

```java

// Java implementation to count of 
// elements such that its sum/difference 
// with X also exists in the Array 
import java.util.*; 
class GFG{ 

// Function to find the count of 
// elements in the array such that 
// element at the difference at X 
// is present in the array 
static void findAns(int arr[], 
                    int n, int x) 
{ 
    int ans; 
    HashSet<Integer> s = new HashSet<Integer>(); 

    // Loop to insert the elements 
    // of the array into the set 
    for (int i = 0; i < n; i++) 
        s.add(arr[i]); 

    ans = 0; 

    // Loop to iterate over the array 
    for (int i = 0; i < n; i++)  
    { 

        // if any of the elements are there 
        // then increse the count variable 
        if (s.contains(arr[i] + x) || 
            s.contains(arr[i] - x)) 
            ans++; 
    } 
    System.out.print(ans); 
    return; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int arr[] = { 2, 2, 4, 5, 6 }; 
    int n = arr.length; 
    int x = 3; 

    findAns(arr, n, x); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 implementation to count of  
# elements such that its sum/difference  
# with X also exists in the array  

# Function to find the count of  
# elements in the array such that  
# element at the difference at X  
# is present in the array  
def findAns(arr, n, x): 

    s = set() 

    # Loop to insert the elements  
    # of the array into the set 
    for i in range(n): 
        s.add(arr[i]) 

    ans = 0

    # Loop to iterate over the array  
    for i in range(n): 

        # If any of the elements are there  
        # then increase the count variable 
        if arr[i] + x in s or arr[i] - x in s: 
            ans = ans + 1

    print(ans) 

# Driver Code  
arr = [ 2, 2, 4, 5, 6 ] 
n = len(arr) 
x = 3

# Function call 
findAns(arr, n, x)  

# This code is contributed by ishayadav181 

```

## C#

```cs

// C# implementation to count of 
// elements such that its sum/difference 
// with X also exists in the Array 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the count of 
// elements in the array such that 
// element at the difference at X 
// is present in the array 
static void findAns(int[] arr, 
                    int n, int x) 
{ 
    int ans; 
    HashSet<int> s = new HashSet<int>(); 

    // Loop to insert the elements 
    // of the array into the set 
    for(int i = 0; i < n; i++) 
       s.Add(arr[i]); 

    ans = 0; 

    // Loop to iterate over the array 
    for(int i = 0; i < n; i++)  
    { 

       // if any of the elements are there 
       // then increse the count variable 
       if (s.Contains(arr[i] + x) || 
           s.Contains(arr[i] - x)) 
           ans++; 
    } 
    Console.Write(ans); 
    return; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int[] arr = { 2, 2, 4, 5, 6 }; 
    int n = arr.Length; 
    int x = 3; 

    findAns(arr, n, x); 
} 
} 

// This code is contributed by ShubhamCoder 

```

**Output:**

```
3

```

**效果分析**：

*   **时间复杂度**：`O(n)`

*   **辅助空间复杂度**：`O(n)`



* * *

* * *



