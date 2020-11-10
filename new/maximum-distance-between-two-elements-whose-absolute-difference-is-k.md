# 绝对差为`K`的两个元素之间的最大距离

> 原文：[https://www.geeksforgeeks.org/maximum-distance-between-two-elements-whose-absolute-difference-is-k/](https://www.geeksforgeeks.org/maximum-distance-between-two-elements-whose-absolute-difference-is-k/)

给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`和数字`K`，任务是找到两个绝对差为`K`的元素之间的最大距离。如果找不到最大距离，则打印 -1。

**示例**：

> **输入**：`arr[] = {3, 5, 1, 4, 2, 2}`
>
> **输出**：5
>
> **解释**：
>
> 在索引 0 和 5 处的两个元素`(3, 2)`之间的最大距离是 5。
> 
> **输入**：`arr[] = {11, 2, 3, 8, 5, 2}`
>
> **输出**：3
>
> **解释**：
>
> 在索引 2 和 5 处的两个元素`(3, 2)`之间的最大距离是 3。

**朴素的方法**：的想法是一个接一个地选取每个元素（例如`arr[i]`），搜索前一个元素`arr[i] – K`和下一个元素`arr[i] + K`。 如果存在两个元素中的任何一个，则找到当前元素与其下一个或上一个元素之间的最大距离。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(1)`

**高效方法**：为了优化上述方法，其想法是使用[**哈希映射**](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 。 步骤如下：

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将第一次出现的索引存储在`HashMap`中。

2.  现在，对于数组`arr[]`中的每个元素，检查哈希映射中是否存在`arr[i] + K`和`arr[i] – K`。

3.  如果存在，则使用`arr[i]`更新两个元素之间的距离，并检查下一个元素。

4.  打印完成上述步骤后获得的最大距离。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function that find maximum distance 
// between two elements whose absolute 
// difference is K 
int maxDistance(int arr[], int K, int N) 
{ 

    // To store the first index 
    map<int, int> Map; 

    // Traverse elements and find 
    // maximum distance between 2 
    // elements whose absolute 
    // difference is K 
    int maxDist = 0; 

    for(int i = 0; i < N; i++)  
    { 

        // If this is first occurrence 
        // of element then insert 
        // its index in map 
        if (Map.find(arr[i]) == Map.end()) 
            Map[arr[i]] = i; 

        // If next element present in 
        // map then update max distance 
        if (Map.find(arr[i] + K) != Map.end()) 
        { 
            maxDist = max(maxDist, 
                          i - Map[arr[i] + K]); 
        } 

        // If previous element present 
        // in map then update max distance 
        if (Map.find(arr[i] - K) != Map.end()) 
        { 
            maxDist = max(maxDist, 
                          i - Map[arr[i] - K]); 
        } 
    } 

    // Return the answer 
    if (maxDist == 0) 
        return -1; 
    else
        return maxDist; 
} 

// Driver code 
int main() 
{ 

    // Given array arr[] 
    int arr[] = { 11, 2, 3, 8, 5, 2 }; 

    int N = sizeof(arr) / sizeof(arr[0]); 

    // Given difference K 
    int K = 2; 

    // Function call 
    cout << maxDistance(arr, K, N); 

    return 0; 
} 

// This code is contributed by divyeshrabadiya07 

```

## Java

```java

// Java program for the above approach 

import java.io.*; 
import java.util.*; 

class GFG { 

    // Function that find maximum distance 
    // between two elements whose absolute 
    // difference is K 
    static int maxDistance(int[] arr, int K) 
    { 

        // To store the first index 
        Map<Integer, Integer> map 
            = new HashMap<>(); 

        // Traverse elements and find 
        // maximum distance between 2 
        // elements whose absolute 
        // difference is K 
        int maxDist = 0; 

        for (int i = 0; i < arr.length; i++) { 

            // If this is first occurrence 
            // of element then insert 
            // its index in map 
            if (!map.containsKey(arr[i])) 
                map.put(arr[i], i); 

            // If next element present in 
            // map then update max distance 
            if (map.containsKey(arr[i] + K)) { 
                maxDist 
                    = Math.max( 
                        maxDist, 
                        i - map.get(arr[i] + K)); 
            } 

            // If previous element present 
            // in map then update max distance 
            if (map.containsKey(arr[i] - K)) { 
                maxDist 
                    = Math.max(maxDist, 
                            i - map.get(arr[i] - K)); 
            } 
        } 

        // Return the answer 
        if (maxDist == 0) 
            return -1; 
        else
            return maxDist; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        // Given array arr[] 
        int[] arr = { 11, 2, 3, 8, 5, 2 }; 

        // Given difference K 
        int K = 2; 

        // Function call 
        System.out.println( 
            maxDistance(arr, K)); 
    } 
} 

```

## Python3

```py

# Python3 program for the above approach 

# Function that find maximum distance  
# between two elements whose absolute  
# difference is K  
def maxDistance(arr, K): 

    # To store the first index 
    map = {} 

    # Traverse elements and find  
    # maximum distance between 2  
    # elements whose absolute  
    # difference is K  
    maxDist = 0

    for i in range(len(arr)): 

        # If this is first occurrence  
        # of element then insert  
        # its index in map  
        if not arr[i] in map: 
            map[arr[i]] = i 

        # If next element present in  
        # map then update max distance  
        if arr[i] + K in map: 
            maxDist = max(maxDist,  
                        i - map[arr[i] + K]) 

        # If previous element present  
        # in map then update max distance  
        if arr[i] - K in map: 
            maxDist = max(maxDist,  
                        i - map[arr[i] - K]) 

    # Return the answer 
    if maxDist == 0: 
        return -1
    else: 
        return maxDist 

# Driver code 

# Given array arr[]  
arr = [ 11, 2, 3, 8, 5, 2 ] 

# Given difference K  
K = 2

# Function call 
print(maxDistance(arr,K)) 

# This code is contributed by Stuti Pathak 

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 
class GFG{ 

// Function that find maximum distance 
// between two elements whose absolute 
// difference is K 
static int maxDistance(int[] arr, int K) 
{ 

    // To store the first index 
    Dictionary<int,  
            int> map = new Dictionary<int,  
                                        int>(); 

    // Traverse elements and find 
    // maximum distance between 2 
    // elements whose absolute 
    // difference is K 
    int maxDist = 0; 

    for (int i = 0; i < arr.Length; i++)  
    { 

    // If this is first occurrence 
    // of element then insert 
    // its index in map 
    if (!map.ContainsKey(arr[i])) 
        map.Add(arr[i], i); 

    // If next element present in 
    // map then update max distance 
    if (map.ContainsKey(arr[i] + K))  
    { 
        maxDist = Math.Max(maxDist,  
                        i - map[arr[i] + K]); 
    } 

    // If previous element present 
    // in map then update max distance 
    if (map.ContainsKey(arr[i] - K)) 
    { 
        maxDist = Math.Max(maxDist, 
                            i - map[arr[i] - K]); 
    } 
    } 

    // Return the answer 
    if (maxDist == 0) 
    return -1; 
    else
    return maxDist; 
} 

// Driver Code 
public static void Main(String []args) 
{ 
    // Given array []arr 
    int[] arr = { 11, 2, 3, 8, 5, 2 }; 

    // Given difference K 
    int K = 2; 

    // Function call 
    Console.WriteLine( 
    maxDistance(arr, K)); 
} 
} 

// This code is contributed by Princi Singh 

```

**输出**： 

```
2

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



