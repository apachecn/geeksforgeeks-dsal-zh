# 包含数组中的唯一元素的最长子数组，

> 原文：[https://www.geeksforgeeks.org/longest-subarray-consisiting-of-unique-elements-from-an-array/](https://www.geeksforgeeks.org/longest-subarray-consisiting-of-unique-elements-from-an-array/)

给定一个由`N`个整数组成的数组`arr[]`，任务是找到仅包含唯一元素的最大子数组。

**示例**：

> **输入**：`arr[] = {1, 2, 3, 4, 5, 1, 2, 3}`
>
> **输出**：5
>
> **说明**：一种可能的子数组是`{1,2,3,4,5}`。
> 
> **输入**：`arr[] = {1, 2, 4, 4, 5, 6, 7, 8, 3, 4, 5, 3, 3, 4, 5, 6, 7, 8, 1 , 2, 3, 4}`
>
> **输出**：8
>
> **说明**：仅可能的子数组为`{3, 4, 5, 6, 6, 7, 8, 1, 2 }`。

**朴素的方法**：解决问题的最简单方法是[从给定数组生成所有子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并使用[`HashSet`](http://www.geeksforgeeks.org/hashset-in-java/)x检查它是否包含任何重复项。 查找满足条件的最长子数组。

 ***时间复杂度**：`O(N ^ 3 logN)`。

**辅助空间**：`O(n)`。

**有效方法**：可以使用[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)优化上述方法。 请按照以下步骤解决问题：

1.  初始化变量`j`，以存储索引的最大值，以使索引`i`和`j`之间没有重复的元素。

2.  遍历数组，并根据存储在`HashMap`中的`a[i]`的先前出现，继续更新`j`。

3.  在更新`j`之后，相应地更新`ans`以存储所需子数组的最大长度。

4.  遍历完成后，打印`ans`。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find largest 
// subarray with no dublicates 
int largest_subarray(int a[], int n) 
{ 
    // Stores index of array elements 
    unordered_map<int, int> index; 
    int ans = 0; 
    for (int i = 0, j = 0; i < n; i++) { 

        // Update j based on previous 
        // occurrence of a[i] 
        j = max(index[a[i]], j); 

        // Update ans to store maximum 
        // length of subarray 
        ans = max(ans, i - j + 1); 

        // Store the index of current 
        // occurrence of a[i] 
        index[a[i]] = i + 1; 
    } 

    // Return final ans 
    return ans; 
} 

// Driver Code 
int32_t main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 1, 2, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << largest_subarray(arr, n); 
} 

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*; 
class GFG{ 

// Function to find largest 
// subarray with no dublicates 
static int largest_subarray(int a[], int n) 
{ 
    // Stores index of array elements 
    HashMap<Integer, 
            Integer> index = new HashMap<Integer, 
                                         Integer>(); 
    int ans = 0; 
    for(int i = 0, j = 0; i < n; i++) 
    { 

        // Update j based on previous 
        // occurrence of a[i] 
        j = Math.max(index.containsKey(a[i]) ?  
                             index.get(a[i]) : 0, j); 

        // Update ans to store maximum 
        // length of subarray 
        ans = Math.max(ans, i - j + 1); 

        // Store the index of current 
        // occurrence of a[i] 
        index.put(a[i], i + 1); 
    } 

    // Return final ans 
    return ans; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 1, 2, 3 }; 
    int n = arr.length; 
    System.out.print(largest_subarray(arr, n)); 
} 
} 

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program to implement 
# the above approach 
from collections import defaultdict 

# Function to find largest 
# subarray with no dublicates 
def largest_subarray(a, n): 

    # Stores index of array elements 
    index = defaultdict(lambda : 0) 

    ans = 0
    j = 0

    for i in range(n): 

        # Update j based on previous 
        # occurrence of a[i] 
        j = max(index[a[i]], j) 

        # Update ans to store maximum 
        # length of subarray 
        ans = max(ans, i - j + 1) 

        # Store the index of current 
        # occurrence of a[i] 
        index[a[i]] = i + 1

        i += 1

    # Return final ans  
    return ans 

# Driver Code 
arr = [ 1, 2, 3, 4, 5, 1, 2, 3 ] 
n = len(arr) 

# Function call 
print(largest_subarray(arr, n)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find largest 
// subarray with no dublicates 
static int largest_subarray(int []a, int n) 
{ 

    // Stores index of array elements 
    Dictionary<int, 
               int> index = new Dictionary<int, 
                                           int>(); 
    int ans = 0; 
    for(int i = 0, j = 0; i < n; i++) 
    { 

        // Update j based on previous 
        // occurrence of a[i] 
        j = Math.Max(index.ContainsKey(a[i]) ?  
                                 index[a[i]] : 0, j); 

        // Update ans to store maximum 
        // length of subarray 
        ans = Math.Max(ans, i - j + 1); 

        // Store the index of current 
        // occurrence of a[i] 
        if(index.ContainsKey(a[i])) 
            index[a[i]] = i + 1; 
        else
            index.Add(a[i], i + 1); 
    } 

    // Return readonly ans 
    return ans; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 1, 2, 3, 4, 5, 1, 2, 3 }; 
    int n = arr.Length; 

    Console.Write(largest_subarray(arr, n)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

**输出**： 

```
5

```

**时间复杂度**：`O(NlogN)`。

**辅助空间**：`O(n)`。



* * *

* * *



