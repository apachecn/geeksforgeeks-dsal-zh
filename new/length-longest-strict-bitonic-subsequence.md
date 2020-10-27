# 最长严格双子序列

的长度

给定一个包含 n 个整数的数组 arr []。 问题是找到最长的严格双音子序列的长度。 如果子序列先增大然后减小，且条件是在递增和递减部分中相邻项之间的绝对差仅为 1，则该子序列称为**严格**双音。 按升序排序的序列被视为 Bitonic，而降序部分为空。 类似地，降序序列被视为 Bitonic，而升序部分为空。

**示例：**

```
Input : arr[] = {1, 5, 2, 3, 4, 5, 3, 2}
Output : 6
The Longest Strict Bitonic Subsequence is:
{1, 2, 3, 4, 3, 2}.

Input : arr[] = {1, 2, 5, 3, 6, 7, 4, 6, 5}
Output : 5

```

**方法 1：**可以使用找到[最长双子序列](https://www.geeksforgeeks.org/dynamic-programming-set-15-longest-bitonic-subsequence/)的概念来解决该问题。 唯一需要保持的条件是，相邻项之间的差应仅为 1。 它的时间复杂度为 O（n <sup>2</sup> ）。

**方法 2（有效方法）：**的想法是创建两个哈希图 **inc** 和 **dcr** ，其元组的格式为**（ele，len） HTG7]，其中 **len** 表示映射 **inc** 中以元素 **ele** 结尾的最长递增子序列的长度，以及以元素[]开头的最长递减子序列的长度 地图 **dcr** 中的 **ele** 。 还创建两个数组 **len_inc []** 和 **len_dcr []** ，其中 **len_inc [i]** 代表以元素 **arr [结尾的最大递增子序列的长度 [i]** 和 **len_dcr [i]** 表示从元素 **arr [i]** 开始的最大递减子序列的长度。 现在，对于哈希表 **inc** 中存在的每个元素 **arr [i]** ，我们可以找到值**（arr [i] -1）**的长度 ]。 令该值为 **v（最初 v 将为 0）**。 现在，以 **arr [i]** 结尾的最长递增子序列的长度将为 **v + 1** 。 在哈希表 **inc** 和数组 **len_inc []** 中的元素 arr [i]的相应索引 **i** 处更新此长度。 现在，从右向左遍历数组，我们可以类似地填充哈希表 **dcr** 和数组 **len_dcr []** ，以得到最长的递减子序列。 最后，对于每个元素 arr [i]，我们计算**（len_inc [i] + len_dcr [i] – 1）**并返回最大值。**

**注意：**在这里，增加和减少子序列仅表示相邻元素之间的差仅为 1。

## C++

```cpp

// C++ implementation to find length of longest  
// strict bitonic subsequence  
#include <bits/stdc++.h> 
using namespace std; 

// function to find length of longest  
// strict bitonic subsequence  
int longLenStrictBitonicSub(int arr[], int n) 
{ 
    // hash table to map the array element with the 
    // length of the longest subsequence of which 
    // it is a part of and is the last/first element of 
    // that subsequence 
    unordered_map<int, int> inc, dcr; 

    // arrays to store the length of increasing and 
    // decreasing subsequences which end at them 
    // or start from them   
    int len_inc[n], len_dcr[n]; 

    // to store the length of longest strict  
    // bitonic subsequence 
    int longLen = 0; 

    // traverse the array elements 
    // from left to right 
    for (int i=0; i<n; i++) 
    { 
        // initialize current length  
        // for element arr[i] as 0 
        int len = 0; 

        // if 'arr[i]-1' is in 'inc' 
        if (inc.find(arr[i]-1) != inc.end()) 
            len = inc[arr[i]-1]; 

        // update arr[i] subsequence length in 'inc'     
        // and in len_inc[] 
        inc[arr[i]] = len_inc[i] = len + 1;  
    } 

    // traverse the array elements 
    // from right to left 
    for (int i=n-1; i>=0; i--) 
    { 
        // initialize current length  
        // for element arr[i] as 0 
        int len = 0; 

        // if 'arr[i]-1' is in 'dcr'  
        if (dcr.find(arr[i]-1) != dcr.end()) 
            len = dcr[arr[i]-1]; 

        // update arr[i] subsequence length in 'dcr' 
        // and in len_dcr[]     
        dcr[arr[i]] = len_dcr[i] = len + 1;  
    } 

    // calculating the length of all the strict  
    // bitonic subsequence 
    for (int i=0; i<n; i++) 
        if (longLen < (len_inc[i] + len_dcr[i] - 1)) 
            longLen = len_inc[i] + len_dcr[i] - 1; 

    // required longest length strict  
    // bitonic subsequence 
    return longLen;         
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = {1, 5, 2, 3, 4, 5, 3, 2}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Longest length strict bitonic subsequence = "
         << longLenStrictBitonicSub(arr, n); 
    return 0; 
}   

```

## Java

```java

// Java implementation to find length of longest  
// strict bitonic subsequence  
import java.util.*; 

class GfG  
{ 

// function to find length of longest  
// strict bitonic subsequence  
static int longLenStrictBitonicSub(int arr[], int n)  
{  
    // hash table to map the array element with the  
    // length of the longest subsequence of which  
    // it is a part of and is the last/first element of  
    // that subsequence  
    HashMap<Integer, Integer> inc = new HashMap<Integer, Integer> (); 
    HashMap<Integer, Integer> dcr = new HashMap<Integer, Integer> ();  

    // arrays to store the length of increasing and  
    // decreasing subsequences which end at them  
    // or start from them  
    int len_inc[] = new int[n]; 
    int len_dcr[] = new int[n];  

    // to store the length of longest strict  
    // bitonic subsequence  
    int longLen = 0;  

    // traverse the array elements  
    // from left to right  
    for (int i = 0; i < n; i++)  
    {  
        // initialize current length  
        // for element arr[i] as 0  
        int len = 0;  

        // if 'arr[i]-1' is in 'inc'  
        if (inc.containsKey(arr[i] - 1))  
            len = inc.get(arr[i] - 1);  

        // update arr[i] subsequence length in 'inc'      
        // and in len_inc[]  
        len_inc[i] = len + 1; 
        inc.put(arr[i], len_inc[i]); 
    }  

    // traverse the array elements  
    // from right to left  
    for (int i = n - 1; i >= 0; i--)  
    {  
        // initialize current length  
        // for element arr[i] as 0  
        int len = 0;  

        // if 'arr[i]-1' is in 'dcr'  
        if (dcr.containsKey(arr[i] - 1))  
            len = dcr.get(arr[i] - 1);  

        // update arr[i] subsequence length in 'dcr'  
        // and in len_dcr[]  
        len_dcr[i] = len + 1; 
        dcr.put(arr[i], len_dcr[i]);  
    }  

    // calculating the length of all the strict  
    // bitonic subsequence  
    for (int i = 0; i < n; i++)  
        if (longLen < (len_inc[i] + len_dcr[i] - 1))  
            longLen = len_inc[i] + len_dcr[i] - 1;  

    // required longest length strict  
    // bitonic subsequence  
    return longLen;      
}  

// Driver code  
public static void main(String[] args)  
{  
    int arr[] = {1, 5, 2, 3, 4, 5, 3, 2};  
    int n = arr.length;  
    System.out.println("Longest length strict " +  
                            "bitonic subsequence = " +  
                            longLenStrictBitonicSub(arr, n));  
} 
}  

// This code is contributed by  
// prerna saini 

```

## Python3

```py

# Python3 implementation to find length of  
# longest strict bitonic subsequence 

# function to find length of longest 
# strict bitonic subsequence 
def longLenStrictBitonicSub(arr, n): 

    # hash table to map the array element  
    # with the length of the longest subsequence  
    # of which it is a part of and is the  
    # last/first element of that subsequence 
    inc, dcr = dict(), dict() 

    # arrays to store the length of increasing 
    # and decreasing subsequences which end at  
    # them or start from them 
    len_inc, len_dcr = [0] * n, [0] * n 

    # to store the length of longest strict 
    # bitonic subsequence 
    longLen = 0

    # traverse the array elements 
    # from left to right 
    for i in range(n): 

        # initialize current length 
        # for element arr[i] as 0 
        len = 0

        # if 'arr[i]-1' is in 'inc' 
        if inc.get(arr[i] - 1) in inc.values(): 
            len = inc.get(arr[i] - 1) 

        # update arr[i] subsequence length in 'inc'      
        # and in len_inc[]  
        inc[arr[i]] = len_inc[i] = len + 1

    # traverse the array elements 
    # from right to left 
    for i in range(n - 1, -1, -1): 

        # initialize current length 
        # for element arr[i] as 0 
        len = 0

        # if 'arr[i]-1' is in 'dcr' 
        if dcr.get(arr[i] - 1) in dcr.values(): 
            len = dcr.get(arr[i] - 1) 

        # update arr[i] subsequence length   
        # in 'dcr' and in len_dcr[]  
        dcr[arr[i]] = len_dcr[i] = len + 1

    # calculating the length of  
    # all the strict bitonic subsequence  
    for i in range(n): 
        if longLen < (len_inc[i] + len_dcr[i] - 1): 
            longLen = len_inc[i] + len_dcr[i] - 1

    # required longest length strict  
    # bitonic subsequence  
    return longLen 

# Driver Code 
if __name__ == "__main__": 
    arr = [1, 5, 2, 3, 4, 5, 3, 2] 
    n = len(arr) 
    print("Longest length strict bitonic subsequence =", 
           longLenStrictBitonicSub(arr, n)) 

# This code is contributed by sanjeev2552 

```

## C#

```cs

// C# implementation to find length of longest  
// strict bitonic subsequence  
using System; 
using System.Collections.Generic; 

class GfG  
{  

    // function to find length of longest  
    // strict bitonic subsequence  
    static int longLenStrictBitonicSub(int []arr, int n)  
    {  
        // hash table to map the array  
        // element with the length of  
        // the longest subsequence of  
        // which it is a part of and  
        // is the last/first element of  
        // that subsequence  
        Dictionary<int, int> inc = new Dictionary<int, int> ();  
        Dictionary<int, int> dcr = new Dictionary<int, int> ();  

        // arrays to store the length  
        // of increasing and decreasing  
        // subsequences which end at them  
        // or start from them  
        int []len_inc = new int[n];  
        int []len_dcr = new int[n];  

        // to store the length of longest strict  
        // bitonic subsequence  
        int longLen = 0;  

        // traverse the array elements  
        // from left to right  
        for (int i = 0; i < n; i++)  
        {  
            // initialize current length  
            // for element arr[i] as 0  
            int len = 0;  

            // if 'arr[i]-1' is in 'inc'  
            if (inc.ContainsKey(arr[i] - 1))  
                len = inc[arr[i] - 1];  

            // update arr[i] subsequence length       
            // in 'inc' and in len_inc[]  
            len_inc[i] = len + 1;  
            if (inc.ContainsKey(arr[i])) 
            { 
                inc.Remove(arr[i]); 
                inc.Add(arr[i], len_inc[i]);  
            } 
            else
                inc.Add(arr[i], len_inc[i]); 
        }  

        // traverse the array elements  
        // from right to left  
        for (int i = n - 1; i >= 0; i--)  
        {  
            // initialize current length  
            // for element arr[i] as 0  
            int len = 0;  

            // if 'arr[i]-1' is in 'dcr'  
            if (dcr.ContainsKey(arr[i] - 1))  
                len = dcr[arr[i] - 1];  

            // update arr[i] subsequence length in 'dcr'  
            // and in len_dcr[]  
            len_dcr[i] = len + 1;  
            if (dcr.ContainsKey(arr[i])) 
            { 
                dcr.Remove(arr[i]); 
                dcr.Add(arr[i], len_dcr[i]);  
            } 
            else
                dcr.Add(arr[i], len_dcr[i]);  
        }  

        // calculating the length of all the strict  
        // bitonic subsequence  
        for (int i = 0; i < n; i++)  
            if (longLen < (len_inc[i] + len_dcr[i] - 1))  
                longLen = len_inc[i] + len_dcr[i] - 1;  

        // required longest length strict  
        // bitonic subsequence  
        return longLen;  
    }  

    // Driver code  
    public static void Main(String[] args)  
    {  
        int []arr = {1, 5, 2, 3, 4, 5, 3, 2};  
        int n = arr.Length;  
        Console.WriteLine("Longest length strict " +  
                            "bitonic subsequence = " +  
                            longLenStrictBitonicSub(arr, n));  
    }  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Longest length strict bitonic subsequence = 6

```

**时间复杂度：** O（n）。
**辅助空间：** O（n）。



* * *

* * *



