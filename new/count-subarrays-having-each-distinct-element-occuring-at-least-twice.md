# 计数具有每个不同元素至少出现两次的子数组

> 原文：[https://www.geeksforgeeks.org/count-subarrays-having-each-distinct-element-occuring-at-least-twice/](https://www.geeksforgeeks.org/count-subarrays-having-each-distinct-element-occuring-at-least-twice/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)`arr[]`，任务是计算给定数组中[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，从而 这些子数组中的每个不同元素至少出现两次。

**示例**：

> **输入**：`arr[] = {1, 1, 2, 2, 2}`
>
> **输出**：6
>
> **说明**：具有每个元素的子数组 至少发生两次的是：`{{1, 1}, {1, 1, 2, 2}, {1, 1, 2, 2, 2}, {2, 2}, {2, 2, 2}, {2, 2}}`。
>
> 因此，所需的输出为 6。
> 
> **输入**：`arr[] = {1, 2, 1, 2, 3}`
>
> **输出**：1

**朴素的方法**：解决此问题的最简单方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组的所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子数组，检查是否全部 子数组中的元素至少发生两次或没有。 如果发现为真，则增加计数。 最后，打印获得的**计数**。

**时间复杂度**：`O(N ^ 3)`

**辅助空间**：`O(n)`

**高效方法**：为了优化上述方法，我们的想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。 请按照以下步骤解决问题：

*   初始化一个变量，例如说 **cntSub** ，以存储子数组的数量，以使子数组中的每个元素至少出现两次。

*   创建一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，例如 **cntFreq** ，以存储每个子数组元素的频率。

*   初始化一个变量，例如 **cntUnique** ，以将元素计数存储在频率为 **1** 的子数组中。

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。 对于每个可能的子数组，存储数组每个元素的频率，并检查 **cntUnique** 的值是否为 **0** 。 如果发现为真，则增加 **cntSub** 的值。

*   最后，打印 **cntSub** 的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to get the count 
// of subarrays having each 
// element occuring at least twice 
int cntSubarrays(int arr[], int N) 
{ 
    // Stores count of subarrays 
    // having each distinct element 
    // occuring at least twice 
    int cntSub = 0; 

    // Stores count of unique 
    // elements in a subarray 
    int cntUnique = 0; 

    // Store frequency of 
    // each element of a subarray 
    unordered_map<int, int> cntFreq; 

    // Traverse the given 
    // array 
    for (int i = 0; i < N; 
         i++) { 

        // Count frequency and 
        // check conditions for 
        // each subarray 
        for (int j = i; j < N; 
             j++) { 

            // Update frequency 
            cntFreq[arr[j]]++; 

            // Check if frequency of 
            // arr[j] equal to 1 
            if (cntFreq[arr[j]] 
                == 1) { 

                // Update Count of 
                // unique elements 
                cntUnique++; 
            } 
            else if (cntFreq[arr[j]] 
                     == 2) { 

                // Update count of 
                // unique elements 
                cntUnique--; 
            } 

            // If each element of subarray 
            // occurs at least twice 
            if (cntUnique == 0) { 

                // Update cntSub 
                cntSub++; 
            } 
        } 

        // Remove all elements 
        // from the subarray 
        cntFreq.clear(); 

        // Update cntUnique 
        cntUnique = 0; 
    } 
    return cntSub; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 1, 1, 2, 2, 2 }; 
    int N = sizeof(arr) / sizeof(arr[0]); 
    cout << cntSubarrays(arr, N); 
}

```

## Python3

```py

# Python3 program to implement 
# the above appraoch 
from collections import defaultdict 

# Function to get the count 
# of subarrays having each 
# element occuring at least twice  
def cntSubarrays(arr, N): 

    # Stores count of subarrays 
    # having each distinct element 
    # occuring at least twice 
    cntSub = 0

    # Stores count of unique 
    # elements in a subarray 
    cntUnique = 0

    # Store frequency of 
    # each element of a subarray 
    cntFreq = defaultdict(lambda : 0) 

    # Traverse the given 
    # array 
    for i in range(N): 

        # Count frequency and 
        # check conditions for 
        # each subarray 
        for j in range(i, N): 

            # Update frequency 
            cntFreq[arr[j]] += 1

            # Check if frequency of 
            # arr[j] equal to 1 
            if (cntFreq[arr[j]] == 1): 

                # Update Count of 
                # unique elements 
                cntUnique += 1

            elif (cntFreq[arr[j]] == 2): 

                # Update count of 
                # unique elements 
                cntUnique -= 1

            # If each element of subarray 
            # occurs at least twice 
            if (cntUnique == 0): 

                # Update cntSub 
                cntSub += 1

        # Remove all elements 
        # from the subarray 
        cntFreq.clear() 

        # Update cntUnique 
        cntUnique = 0

    return cntSub 

# Driver code 
if __name__ == '__main__': 

    arr = [ 1, 1, 2, 2, 2 ] 
    N = len(arr) 

    print(cntSubarrays(arr, N)) 

# This code is contributed by Shivam Singh

```

**输出**： 

```
6

```

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`



* * *

* * *



