# 由不同元素组成的最长子序列的长度

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是找到最长的[子序列](https://www.geeksforgeeks.org/tag/subsequence/)的长度，该子序列仅包含不同的元素 。

**示例**：

> **输入**：arr [] = {1、1、2、2、2、3、3}
> **输出**：3
> **说明**：
> 具有不同元素的最长子序列为{1、2、3}。
> **输入**：arr [] = {1，2，3，3，4，5，5，5}
> **输出**：5

**天真的方法**：最简单的方法是[生成数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有子序列，并检查它是否仅由不同的元素组成。 不断更新获得的此类子序列的最大长度。 最后，打印获得的最大长度。

***时间复杂度**：O（2 <sup>N</sup> ）*
***辅助空间**：O（1）*

**高效方法**：仅包含不同元素的最长子序列的长度将等于数组中不同元素的数量。 请按照以下步骤解决问题：

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)继续在[哈希集](http://www.geeksforgeeks.org/hashset-in-java/)中插入遇到的元素。
2.  由于 HashSet 仅包含唯一元素，因此在完成遍历数组后，将 HashSet 的[大小打印为所需答案。](https://www.geeksforgeeks.org/hashset-size-method-in-java/)

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find length of
// the longest subsequence
// consisting of distinct elements
int longestSubseq(int arr[], int n)
{
    // Stores the distinct
    // array elements
    unordered_set<int> s;

    // Traverse the input array
    for (int i = 0; i < n; i++) {

        // If current element has not
        // occurred previously
        if (s.find(arr[i]) == s.end()) {

            // Insert it into set
            s.insert(arr[i]);
        }
    }

    return s.size();
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 3, 4, 5, 5, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << longestSubseq(arr, n);
    return 0;
}

```

## Java

```java

// Java program for the above approach 
import java.util.*;

class GFG{

// Function to find length of 
// the longest subsequence 
// consisting of distinct elements 
static int longestSubseq(int arr[], int n) 
{ 
    // Stores the distinct 
    // array elements 
    Set<Integer> s = new HashSet<>(); 

    // Traverse the input array 
    for(int i = 0; i < n; i++)
    { 

        // If current element has not 
        // occurred previously 
        if (!s.contains(arr[i]))
        { 

            // Insert it into set 
            s.add(arr[i]); 
        } 
    } 
    return s.size(); 
}

// Driver code
public static void main (String[] args)
{

    // Given array 
    int arr[] = { 1, 2, 3, 3, 4, 5, 5, 5 }; 
    int n = arr.length; 

    // Function call 
    System.out.println(longestSubseq(arr, n));     
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program for 
# the above approach

# Function to find length of
# the longest subsequence
# consisting of distinct elements
def longestSubseq(arr, n):

    # Stores the distinct
    # array elements
    s = set()

    # Traverse the input array
    for i in range(n):

        # If current element has not
        # occurred previously
        if (arr[i] not in s):

            # Insert it into set
            s.add(arr[i])

    return len(s)

# Given array
arr = [1, 2, 3, 3, 
       4, 5, 5, 5]
n = len(arr)

# Function Call
print(longestSubseq(arr, n))

# This code is contributed by divyeshrabadiya07

```

## C#

```cs

// C# program for the above approach 
using System;
using System.Collections.Generic; 

class GFG{

// Function to find length of 
// the longest subsequence 
// consisting of distinct elements 
static int longestSubseq(int []arr, int n) 
{ 

    // Stores the distinct 
    // array elements 
    HashSet<int> s = new HashSet<int>();

    // Traverse the input array 
    for(int i = 0; i < n; i++)
    { 

        // If current element has not 
        // occurred previously 
        if (!s.Contains(arr[i]))
        { 

            // Insert it into set 
            s.Add(arr[i]); 
        } 
    } 
    return s.Count; 
}

// Driver code
public static void Main(string[] args)
{

    // Given array 
    int []arr = { 1, 2, 3, 3, 4, 5, 5, 5 }; 
    int n = arr.Length; 

    // Function call 
    Console.Write(longestSubseq(arr, n));     
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
5

```

***时间复杂度**：O（N）*
***辅助空间**：O（N）*



* * *

* * *



