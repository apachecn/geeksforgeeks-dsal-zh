# 最长为`k`的子数组

> 原文：[https://www.geeksforgeeks.org/longest-sub-array-sum-k/](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)

给定大小为 **n** 的包含整数的数组`arr[]`。 问题在于找到总和等于给定值 **k** 的最长子数组的长度。

**示例**：

```
Input : arr[] = { 10, 5, 2, 7, 1, 9 }, 
            k = 15
Output : 4
The sub-array is {5, 2, 7, 1}.

Input : arr[] = {-5, 8, -14, 2, 4, 12},
            k = -5
Output : 5

```

**朴素的方法**：考虑所有子数组的总和，并返回总和为`k`的最长子数组的长度。 时间复杂度为`O(N ^ 2)`。

**有效方法**：以下是步骤：

1.  初始化`sum = 0`和`maxLen = 0`。

2.  创建具有`(sum, index)`元组的哈希表。

3.  对于`i = 0`到`n - 1`，执行以下步骤：

    1.  将`arr[i]`累积到`sum`。

    2.  如果`sum == k`，则更新`maxLen = i + 1`。

    3.  检查哈希表中是否存在`sum`。 如果不存在，则将其作为`sum, i`对添加到哈希表中。

    4.  检查哈希表中是否存在`sum - k`。 如果存在，则从哈希表中获取`sum - k`的索引作为`index`。 现在检查`maxLen < (i - index)`，然后更新`maxLen = (i - index)`。

4.  返回`maxLen`。

## C++

```cpp

// C++ implementation to find the length 
// of longest subarray having sum k 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the length of longest 
// subarray having sum k 
int lenOfLongSubarr(int arr[],  
                    int n, 
                    int k) 
{ 

    // unordered_map 'um' implemented  
    // as hash table 
    unordered_map<int, int> um; 
    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++) { 

        // accumulate sum 
        sum += arr[i]; 

        // when subarray starts from index '0' 
        if (sum == k) 
            maxLen = i + 1; 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        if (um.find(sum) == um.end()) 
            um[sum] = i; 

        // check if 'sum-k' is present in 'um' 
        // or not 
        if (um.find(sum - k) != um.end()) { 

            // update maxLength 
            if (maxLen < (i - um[sum - k])) 
                maxLen = i - um[sum - k]; 
        } 
    } 

    // required maximum length 
    return maxLen; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {10, 5, 2, 7, 1, 9}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 15; 
    cout << "Length = "
         << lenOfLongSubarr(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the length 
// of longest subarray having sum k 
import java.io.*; 
import java.util.*; 

class GFG { 

      // function to find the length of longest 
      // subarray having sum k 
      static int lenOfLongSubarr(int[] arr, int n, int k) 
      { 
             // HashMap to store (sum, index) tuples 
             HashMap<Integer, Integer> map = new HashMap<>(); 
             int sum = 0, maxLen = 0; 

             // traverse the given array 
             for (int i = 0; i < n; i++) { 

                  // accumulate sum 
                  sum += arr[i]; 

                  // when subarray starts from index '0' 
                  if (sum == k) 
                      maxLen = i + 1; 

                  // make an entry for 'sum' if it is 
                  // not present in 'map' 
                  if (!map.containsKey(sum)) { 
                      map.put(sum, i); 
                  } 

                  // check if 'sum-k' is present in 'map' 
                  // or not 
                  if (map.containsKey(sum - k)) { 

                      // update maxLength 
                      if (maxLen < (i - map.get(sum - k))) 
                          maxLen = i - map.get(sum - k); 
                  } 
             } 

             return maxLen;              
      } 

      // Driver code 
      public static void main(String args[]) 
      { 
             int[] arr = {10, 5, 2, 7, 1, 9}; 
             int n = arr.length; 
             int k = 15; 
             System.out.println("Length = " +  
                                lenOfLongSubarr(arr, n, k)); 
      } 
} 

// This code is contibuted by rachana soma 

```

## Python3

```py

# Python3 implementation to find the length 
# of longest subArray having sum k 

# function to find the longest 
# subarray having sum k 
def lenOfLongSubarr(arr, n, k): 

    # dictionary mydict implemented 
    # as hash map 
    mydict = dict() 

    # Initialize sum and maxLen with 0 
    sum = 0
    maxLen = 0

    # traverse the given array 
    for i in range(n): 

        # accumulate the sum 
        sum += arr[i] 

        # when subArray starts from index '0' 
        if (sum == k): 
            maxLen = i + 1

        # check if 'sum-k' is present in 
        # mydict or not 
        elif (sum - k) in mydict: 
            maxLen = max(maxLen, i - mydict[sum - k]) 

        # if sum is not present in dictionary 
        # push it in the dictionary with its index 
        if sum not in mydict: 
            mydict[sum] = i 

    return maxLen 

# Driver Code 
if __name__ == '__main__': 
    arr = [10, 5, 2, 7, 1, 9] 
    n = len(arr) 
    k = 15
    print("Length =", lenOfLongSubarr(arr, n, k)) 

# This code is contributed by  
# chaudhary_19 (Mayank Chaudhary) 

```

## C#

```cs

// C# implementation to find the length  
// of longest subarray having sum k  
using System; 
using System.Collections.Generic; 

class GFG  
{  

// function to find the length of longest  
// subarray having sum k  
static int lenOfLongSubarr(int[] arr,  
                           int n, int k)  
{  
    // HashMap to store (sum, index) tuples  
    Dictionary<int, 
               int> map = new Dictionary<int, 
                                         int>();  
    int sum = 0, maxLen = 0;  

    // traverse the given array  
    for (int i = 0; i < n; i++) 
    {  

        // accumulate sum  
        sum += arr[i];  

        // when subarray starts from index '0'  
        if (sum == k)  
            maxLen = i + 1;  

        // make an entry for 'sum' if it is  
        // not present in 'map'  
        if (!map.ContainsKey(sum)) 
        {  
            map.Add(sum, i);  
        }  

        // check if 'sum-k' is present in 'map'  
        // or not  
        if (map.ContainsKey(sum - k))  
        {  

            // update maxLength  
            if (maxLen < (i - map[sum - k]))  
                maxLen = i - map[sum - k];  
        }  
    }  

    return maxLen;          
}  

// Driver code  
public static void Main()  
{  
    int[] arr = {10, 5, 2, 7, 1, 9};  
    int n = arr.Length;  
    int k = 15;  
    Console.WriteLine("Length = " +  
                       lenOfLongSubarr(arr, n, k));  
}  
}  

// This code is contibuted by PrinciRaj1992 

```

**输出**：

```
Length = 4

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



