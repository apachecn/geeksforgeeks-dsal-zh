# 计数为 1s 的最长子数组比计数为 0s 的子数组多

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)

给定大小为 **n** 的数组，仅包含 0 和 1。 问题是要找到最长的子数组的长度，其计数为 1 的数字要大于 0 的数字。

**示例**：

```
Input : arr = {0, 1, 1, 0, 0, 1}
Output : 5
From index 1 to 5.

Input : arr[] = {1, 0, 0, 1, 0}
Output : 1

```

**方法**：以下是步骤：

1.  将数组中的所有 0 都视为“ -1”。

2.  初始化**总和** = 0 和 **maxLen** = 0。

3.  创建具有**（总和，索引）**元组的哈希表。

4.  对于 i = 0 到 n-1，执行以下步骤：

    1.  如果 arr [i]为'0'，则将'-1'累加至**和**，否则将'1'则累加至**总和**。

    2.  如果 sum == 1，则更新 **maxLen** = i + 1。

    3.  否则检查哈希表中是否存在**和**。 如果不存在，则将其作为**（和，i）**对添加到哈希表中。

    4.  检查哈希表中是否存在**（sum-1）**。 如果存在，则从哈希表中获取**（sum-1）**的索引作为**索引**。 现在检查 maxLen 是否小于（i-index），然后更新 **maxLen** =（i-index）。

5.  返回 maxLen。

## C++

```cpp

// C++ implementation to find the length of 
// longest subarray having count of 1's one 
// more than count of 0's 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the length of longest 
// subarray having count of 1's one more 
// than count of 0's 
int lenOfLongSubarr(int arr[], int n) 
{ 
    // unordered_map 'um' implemented as 
    // hash table 
    unordered_map<int, int> um; 
    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++) { 

        // consider '0' as '-1' 
        sum += arr[i] == 0 ? -1 : 1; 

        // when subarray starts form index '0' 
        if (sum == 1) 
            maxLen = i + 1; 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        else if (um.find(sum) == um.end()) 
            um[sum] = i; 

        // check if 'sum-1' is present in 'um' 
        // or not 
        if (um.find(sum - 1) != um.end()) { 

            // update maxLength 
            if (maxLen < (i - um[sum - 1])) 
                maxLen = i - um[sum - 1]; 
        } 
    } 

    // required maximum length 
    return maxLen; 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = { 0, 1, 1, 0, 0, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Length = "
         << lenOfLongSubarr(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the length of 
// longest subarray having count of 1's one 
// more than count of 0's 
import java.util.*; 

class GFG  
{ 

// function to find the length of longest 
// subarray having count of 1's one more 
// than count of 0's 
static int lenOfLongSubarr(int arr[], int n) 
{ 
    // unordered_map 'um' implemented as 
    // hash table 
    HashMap<Integer,  
            Integer> um = new HashMap<Integer,  
                                      Integer>(); 
    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++)  
    { 

        // consider '0' as '-1' 
        sum += arr[i] == 0 ? -1 : 1; 

        // when subarray starts form index '0' 
        if (sum == 1) 
            maxLen = i + 1; 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        else if (!um.containsKey(sum)) 
            um. put(sum, i); 

        // check if 'sum-1' is present in 'um' 
        // or not 
        if (um.containsKey(sum - 1))  
        { 

            // update maxLength 
            if (maxLen < (i - um.get(sum - 1))) 
                maxLen = i - um.get(sum - 1); 
        } 
    } 

    // required maximum length 
    return maxLen; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int arr[] = { 0, 1, 1, 0, 0, 1 }; 
    int n = arr.length; 
    System.out.println("Length = " +  
               lenOfLongSubarr(arr, n)); 
} 
}  

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python 3 implementation to find the length of 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
# longest subarray having count of 1's one 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
# more than count of 0's 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)

# function to find the length of longest 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
# subarray having count of 1's one more 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
# than count of 0's 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
def lenOfLongSubarr(arr, n): 

    # unordered_map 'um' implemented as 
    # hash table 
    um = {i:0 for i in range(10)} 
    sum = 0
    maxLen = 0

    # traverse the given array 
    for i in range(n): 

        # consider '0' as '-1' 
        if arr[i] == 0: 
            sum += -1
        else: 
            sum += 1

        # when subarray starts form index '0' 
        if (sum == 1): 
            maxLen = i + 1

        # make an entry for 'sum' if it is 
        # not present in 'um' 
        elif (sum not in um): 
            um[sum] = i 

        # check if 'sum-1' is present in 'um' 
        # or not 
        if ((sum - 1) in um): 
            # update maxLength 
            if (maxLen < (i - um[sum - 1])): 
                maxLen = i - um[sum - 1] 

    # required maximum length 
    return maxLen 

# Driver code 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
if __name__ == '__main__': 
    arr = [0, 1, 1, 0, 0, 1] 
    n = len(arr) 
    print("Length =",lenOfLongSubarr(arr, n)) 

# This code is contributed by 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
# Surendra_Gangwar 

> 原文：[https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)

```

## C#

```cs

// C# implementation to find the length of 
// longest subarray having count of 1's one 
// more than count of 0's 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// function to find the length of longest 
// subarray having count of 1's one more 
// than count of 0's 
static int lenOfLongSubarr(int []arr, int n) 
{ 
    // unordered_map 'um' implemented as 
    // hash table 
    Dictionary<int,  
               int> um = new Dictionary<int,  
                                        int>(); 
    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++)  
    { 

        // consider '0' as '-1' 
        sum += arr[i] == 0 ? -1 : 1; 

        // when subarray starts form index '0' 
        if (sum == 1) 
            maxLen = i + 1; 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        else if (!um.ContainsKey(sum)) 
            um.Add(sum, i); 

        // check if 'sum-1' is present in 'um' 
        // or not 
        if (um.ContainsKey(sum - 1))  
        { 

            // update maxLength 
            if (maxLen < (i - um[sum - 1])) 
                maxLen = i - um[sum - 1]; 
        } 
    } 

    // required maximum length 
    return maxLen; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 0, 1, 1, 0, 0, 1 }; 
    int n = arr.Length; 
    Console.WriteLine("Length = " +  
            lenOfLongSubarr(arr, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Length = 5

```

**时间复杂度**：O（n）

**辅助空间**：O（n）

本文由 [**Ayush Jauhari**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

