# 最长和可被 k 整除的子数组

> 原文：[https://www.geeksforgeeks.org/longest-subarray-sum-divisible-k/](https://www.geeksforgeeks.org/longest-subarray-sum-divisible-k/)

给定 **arr []** ，它包含 **n 个**整数和一个正整数 **k** 。 问题是找到最长子数组的长度，其中元素的总和可被给定值 **k** 整除。

**范例**：

```
Input : arr[] = {2, 7, 6, 1, 4, 5}, k = 3
Output : 4
The subarray is {7, 6, 1, 4} with sum 18,
which is divisible by 3.

Input : arr[] = {-2, 2, -5, 12, -11, -1, 7}
Output : 5

```

**方法 1（朴素方法）**：考虑所有子阵列，并返回总和可被 **k** 整除且长度最长的子阵列的长度。

时间复杂度：`O(N ^ 2)`。

**方法 2（有效方法）**：创建一个数组 **mod_arr []** ，其中 **mod_arr [i]** 存储**（sum（arr [0] + arr [ 1] .. + arr [i]）％k）**。 创建一个具有元组为**（ele，idx）**的哈希表，其中 **ele** 代表 **mod_arr []** 的元素， **idx** 代表 元素在 **mod_arr []** 中首次出现的索引。 现在，从 i = 0 到 n 遍历 **mod_arr []** ，然后执行以下步骤。

1.  如果 mod_arr [i] == 0，则更新 **maxLen** =（i +1）。

2.  否则，如果哈希表中不存在 mod_arr [i]，则在哈希表中创建元组**（mod_arr [i]，i）**。

3.  否则，获取与哈希表中的 **mod_arr [i]** 相关的值。 使其为 **idx** 。

4.  如果 maxLen < (i – idx), then update **maxLen** =（i – idx）。

最后返回 **maxLen** 。

## C++

```cpp

// C++ implementation to find the longest subarray 
// with sum divisible by k 
#include <bits/stdc++.h> 

using namespace std; 

// function to find the longest subarray 
// with sum divisible by k 
int longSubarrWthSumDivByK(int arr[],  
                          int n, int k) 
{ 
    // unodered map 'um' implemented as 
    // hash table 
    unordered_map<int, int> um; 

    // 'mod_arr[i]' stores (sum[0..i] % k) 
    int mod_arr[n], max = 0; 
    int curr_sum = 0; 

    // traverse arr[] and build up the 
    // array 'mod_arr[]' 
    for (int i = 0; i < n; i++) 
    { 
        curr_sum += arr[i]; 

        // as the sum can be negative, taking modulo twice 
        mod_arr[i] = ((curr_sum % k) + k) % k;         
    }     

    for (int i = 0; i < n; i++) 
    { 
        // if true then sum(0..i) is divisible 
        // by k 
        if (mod_arr[i] == 0) 
            // update 'max' 
            max = i + 1; 

        // if value 'mod_arr[i]' not present in 'um' 
        // then store it in 'um' with index of its 
        // first occurrence         
        else if (um.find(mod_arr[i]) == um.end()) 
            um[mod_arr[i]] = i; 

        else
            // if true, then update 'max' 
            if (max < (i - um[mod_arr[i]])) 
                max = i - um[mod_arr[i]];             
    } 

    // required length of longest subarray with 
    // sum divisible by 'k' 
    return max; 
}                           

// Driver program to test above 
int main() 
{ 
    int arr[] = {2, 7, 6, 1, 4, 5}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 

    cout << "Length = "
         << longSubarrWthSumDivByK(arr, n, k); 

    return 0;      
} 

```

## Java

```java

// Java implementation to find the longest  
// subarray with sum divisible by k 
import java.io.*; 
import java.util.*; 

class GfG { 

    // function to find the longest subarray 
    // with sum divisible by k 
    static int longSubarrWthSumDivByK(int arr[],  
                                      int n, int k) 
    { 
        // unodered map 'um' implemented as 
        // hash table 
        HashMap<Integer, Integer> um= new HashMap<Integer, Integer>(); 

        // 'mod_arr[i]' stores (sum[0..i] % k) 
        int mod_arr[]= new int[n]; 
        int max = 0; 
        int curr_sum = 0; 

        // traverse arr[] and build up the 
        // array 'mod_arr[]' 
        for (int i = 0; i < n; i++) 
        { 
            curr_sum += arr[i]; 

            // as the sum can be negative,  
            // taking modulo twice 
            mod_arr[i] = ((curr_sum % k) + k) % k;      
        }  

        for (int i = 0; i < n; i++) 
        { 
            // if true then sum(0..i) is  
            // divisible by k 
            if (mod_arr[i] == 0) 
                // update 'max' 
                max = i + 1; 

            // if value 'mod_arr[i]' not present in 'um' 
            // then store it in 'um' with index of its 
            // first occurrence      
            else if (um.containsKey(mod_arr[i]) == false) 
                um.put(mod_arr[i] , i); 

            else
                // if true, then update 'max' 
                if (max < (i - um.get(mod_arr[i]))) 
                    max = i - um.get(mod_arr[i]);          
        } 

        // required length of longest subarray with 
        // sum divisible by 'k' 
        return max; 
    }     

    public static void main (String[] args)  
    { 
        int arr[] = {2, 7, 6, 1, 4, 5}; 
        int n = arr.length; 
        int k = 3; 

        System.out.println("Length = "+  
                            longSubarrWthSumDivByK(arr, n, k)); 

    } 
} 

// This code is contributed by Gitanjali. 

```

## Python3

```py

# Python3 implementation to find the  
# longest subarray with sum divisible by k 

# Function to find the longest 
# subarray with sum divisible by k 
def longSubarrWthSumDivByK(arr, n, k): 

    # unodered map 'um' implemented  
    # as hash table 
    um = {} 

    # 'mod_arr[i]' stores (sum[0..i] % k) 
    mod_arr = [0 for i in range(n)] 
    max = 0
    curr_sum = 0

    # Traverse arr[] and build up  
    # the array 'mod_arr[]' 
    for i in range(n): 
        curr_sum += arr[i] 

        # As the sum can be negative, 
        # taking modulo twice 
        mod_arr[i] = ((curr_sum % k) + k) % k  

    for i in range(n): 

        # If true then sum(0..i) is  
        # divisible by k 
        if (mod_arr[i] == 0): 

            # Update 'max' 
            max = i + 1

        # If value 'mod_arr[i]' not present in  
        # 'um' then store it in 'um' with index  
        # of its first occurrence  
        elif (mod_arr[i] not in um): 
            um[mod_arr[i]] = i 

        else: 

            # If true, then update 'max' 
            if (max < (i - um[mod_arr[i]])): 
                max = i - um[mod_arr[i]]          

    # Required length of longest subarray  
    # with sum divisible by 'k' 
    return max    

# Driver Code 
if __name__ == '__main__': 

    arr = [ 2, 7, 6, 1, 4, 5 ] 
    n = len(arr) 
    k = 3

    print("Length =",  
           longSubarrWthSumDivByK(arr, n, k)) 

# This code is contributed by 
# Surendra_Gangwar 

```

## C#

```cs

using System; 
using System.Collections.Generic; 

// C# implementation to find the longest   
// subarray with sum divisible by k  

public class GfG 
{ 

    // function to find the longest subarray  
    // with sum divisible by k  
    public static int longSubarrWthSumDivByK(int[] arr, int n, int k) 
    { 
        // unodered map 'um' implemented as  
        // hash table  
        Dictionary<int, int> um = new Dictionary<int, int>(); 

        // 'mod_arr[i]' stores (sum[0..i] % k)  
        int[] mod_arr = new int[n]; 
        int max = 0; 
        int curr_sum = 0; 

        // traverse arr[] and build up the  
        // array 'mod_arr[]'  
        for (int i = 0; i < n; i++) 
        { 
            curr_sum += arr[i]; 

            // as the sum can be negative,   
            // taking modulo twice  
            mod_arr[i] = ((curr_sum % k) + k) % k; 
        } 

        for (int i = 0; i < n; i++) 
        { 
            // if true then sum(0..i) is   
            // divisible by k  
            if (mod_arr[i] == 0) 
            { 
                // update 'max'  
                max = i + 1; 
            } 

            // if value 'mod_arr[i]' not present in 'um'  
            // then store it in 'um' with index of its  
            // first occurrence       
            else if (um.ContainsKey(mod_arr[i]) == false) 
            { 
                um[mod_arr[i]] = i; 
            } 

            else
            { 
                // if true, then update 'max'  
                if (max < (i - um[mod_arr[i]])) 
                { 
                    max = i - um[mod_arr[i]]; 
                } 
            } 
        } 

        // required length of longest subarray with  
        // sum divisible by 'k'  
        return max; 
    } 

    public static void Main(string[] args) 
    { 
        int[] arr = new int[] {2, 7, 6, 1, 4, 5}; 
        int n = arr.Length; 
        int k = 3; 

        Console.WriteLine("Length = " + longSubarrWthSumDivByK(arr, n, k)); 

    } 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```
Length = 4 

```

时间复杂度：`O(n)`。

辅助空间：`O(N ^ 2)`。

对于`O(1)`查找，可以通过使用大小等于 k 的数组来改善此方法的时间复杂度，因为在对输入数组的元素进行模运算之后，所有元素都将小于 k。



* * *

* * *



