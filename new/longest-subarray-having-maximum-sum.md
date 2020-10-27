# 具有最大和的最长子数组

给定包含 **n** 个整数的数组 **arr []** 。 问题是找到具有最大和的子数组的长度。 如果存在两个或更多具有最大和的子数组，则打印最长子数组的长度。

**示例：**

```
Input : arr[] = {5, -2, -1, 3, -4}
Output : 4
There are two subarrays with maximum sum:
First is {5}
Second is {5, -2, -1, 3}
Therefore longest one is of length 4.

Input : arr[] = {-2, -3, 4, -1, -2, 1, 5, -3}
Output : 5
The subarray is {4, -1, -2, 1, 5}

```

**方法：**以下是步骤：

1.  找到[最大和连续子数组](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。 令该和为 **maxSum** 。
2.  找到总和等于 **maxSum** 的最长子数组的长度。 请参阅此帖子的[。](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)

## C ++

```

// C++ implementation to find the length of the longest 
// subarray having maximum sum 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the maximum sum that 
// exists in a subarray 
int maxSubArraySum(int arr[], int size) 
{ 
    int max_so_far = arr[0]; 
    int curr_max = arr[0]; 

    for (int i = 1; i < size; i++) { 
        curr_max = max(arr[i], curr_max + arr[i]); 
        max_so_far = max(max_so_far, curr_max); 
    } 
    return max_so_far; 
} 

// function to find the length of longest 
// subarray having sum k 
int lenOfLongSubarrWithGivenSum(int arr[], int n, int k) 
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

// function to find the length of the longest 
// subarray having maximum sum 
int lenLongSubarrWithMaxSum(int arr[], int n) 
{ 
    int maxSum = maxSubArraySum(arr, n); 
    return lenOfLongSubarrWithGivenSum(arr, n, maxSum); 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = { 5, -2, -1, 3, -4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Length of longest subarray having maximum sum = "
         << lenLongSubarrWithMaxSum(arr, n); 
    return 0; 
} 

```

## 爪哇

```

// Java implementation to find 
// the length of the longest  
// subarray having maximum sum  
import java.util.*; 

class GFG 
{ 
// function to find the 
// maximum sum that  
// exists in a subarray  
static int maxSubArraySum(int arr[],  
                          int size)  
{  
    int max_so_far = arr[0];  
    int curr_max = arr[0];  

    for (int i = 1; i < size; i++) 
    {  
        curr_max = Math.max(arr[i],  
                        curr_max + arr[i]);  
        max_so_far = Math.max(max_so_far,  
                              curr_max);  
    }  
    return max_so_far;  
}  

// function to find the  
// length of longest  
// subarray having sum k  
static int lenOfLongSubarrWithGivenSum(int arr[], 
                                       int n, int k)  
{  
    // unordered_map 'um' implemented  
    // as hash table  
    HashMap<Integer,  
            Integer> um = new HashMap<Integer,  
                                      Integer>();  
    int sum = 0, maxLen = 0;  

    // traverse the given array  
    for (int i = 0; i < n; i++)  
    {  

        // accumulate sum  
        sum += arr[i];  

        // when subarray starts 
        // from index '0'  
        if (sum == k)  
            maxLen = i + 1;  

        // make an entry for 'sum' if  
        // it is not present in 'um'  
        if (um.containsKey(sum))  
            um.put(sum, i);  

        // check if 'sum-k' is present  
        // in 'um' or not  
        if (um.containsKey(sum - k)) 
        {  

            // update maxLength  
            if (maxLen < (i - um.get(sum - k)))  
                maxLen = i - um.get(sum - k);  
        }  
    }  

    // required maximum length  
    return maxLen;  
}  

// function to find the length  
// of the longest subarray 
// having maximum sum  
static int lenLongSubarrWithMaxSum(int arr[], int n)  
{  
    int maxSum = maxSubArraySum(arr, n);  
    return lenOfLongSubarrWithGivenSum(arr, n, maxSum);  
}  

// Driver Code 
public static void main(String args[]) 
{  
    int arr[] = { 5, -2, -1, 3, -4 };  
    int n = arr.length;  
    System.out.println("Length of longest subarray " +  
                             "having maximum sum = " + 
                     lenLongSubarrWithMaxSum(arr, n));  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 implementation to find the length  
# of the longest subarray having maximum sum 

# function to find the maximum sum that 
# exists in a subarray 
def maxSubArraySum(arr, size): 

    max_so_far = arr[0] 
    curr_max = arr[0] 

    for i in range(1,size): 
        curr_max = max(arr[i], curr_max + arr[i]) 
        max_so_far = max(max_so_far, curr_max) 
    return max_so_far 

# function to find the length of longest 
# subarray having sum k 
def lenOfLongSubarrWithGivenSum(arr, n, k): 

    # unordered_map 'um' implemented 
    # as hash table 
    um = dict() 
    Sum, maxLen = 0, 0

    # traverse the given array 
    for i in range(n): 

        # accumulate Sum 
        Sum += arr[i] 

        # when subarray starts from index '0' 
        if (Sum == k): 
            maxLen = i + 1

        # make an entry for 'Sum' if it is 
        # not present in 'um' 
        if (Sum not in um.keys()): 
            um[Sum] = i 

        # check if 'Sum-k' is present in 'um' 
        # or not 
        if (Sum in um.keys()): 

            # update maxLength 
            if ((Sum - k) in um.keys() and 
                 maxLen < (i - um[Sum - k])): 
                maxLen = i - um[Sum - k] 

    # required maximum length 
    return maxLen 

# function to find the length of the longest 
# subarray having maximum Sum 
def lenLongSubarrWithMaxSum(arr, n): 

    maxSum = maxSubArraySum(arr, n) 
    return lenOfLongSubarrWithGivenSum(arr, n, maxSum) 

# Driver Code 
arr = [5, -2, -1, 3, -4] 
n = len(arr) 
print("Length of longest subarray having maximum sum = ",  
                         lenLongSubarrWithMaxSum(arr, n)) 

# This code is contributed by mohit kumar 

```

## C＃

```

// C# implementation to find  
// the length of the longest  
// subarray having maximum sum  
using System; 
using System.Collections.Generic; 
public class GFG{  
    // function to find the  
    // maximum sum that  
    // exists in a subarray  
    static int maxSubArraySum(int []arr,  
                            int size)  
    {  
        int max_so_far = arr[0];  
        int curr_max = arr[0];  

        for (int i = 1; i < size; i++)  
        {  
            curr_max = Math.Max(arr[i],  
                            curr_max + arr[i]);  
            max_so_far = Math.Max(max_so_far,  
                                curr_max);  
        }  
        return max_so_far;  
    }  

    // function to find the  
    // length of longest  
    // subarray having sum k  
    static int lenOfLongSubarrWithGivenSum(int []arr,  
                                        int n, int k)  
    {  
        // unordered_map 'um' implemented  
        // as hash table  
        Dictionary<int,  
                int> um = new Dictionary<int,  
                                        int>();  
        int sum = 0, maxLen = 0;  

        // traverse the given array  
        for (int i = 0; i < n; i++)  
        {  

            // accumulate sum  
            sum += arr[i];  

            // when subarray starts  
            // from index '0'  
            if (sum == k)  
                maxLen = i + 1;  

            // make an entry for 'sum' if  
            // it is not present in 'um'  
            if (um.ContainsKey(sum))  
                um.Add(sum, i);  

            // check if 'sum-k' is present  
            // in 'um' or not  
            if (um.ContainsKey(sum - k))  
            {  

                // update maxLength  
                if (maxLen < (i - um[sum - k]))  
                    maxLen = i - um[sum - k];  
            }  
        }  

        // required maximum length  
        return maxLen;  
    }  

    // function to find the length  
    // of the longest subarray  
    // having maximum sum  
    static int lenLongSubarrWithMaxSum(int []arr, int n)  
    {  
        int maxSum = maxSubArraySum(arr, n);  
        return lenOfLongSubarrWithGivenSum(arr, n, maxSum);  
    }  

    // Driver Code  
    public static void Main()  
    {  
        int []arr = { 5, -2, -1, 3, -4 };  
        int n = arr.Length;  
        Console.WriteLine("Length of longest subarray " +  
                                "having maximum sum = " +  
                        lenLongSubarrWithMaxSum(arr, n));  
    }  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Length of longest subarray having maximum sum = 4

```

**时间复杂度：** O（n）。
**辅助空间：** O（n）。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。