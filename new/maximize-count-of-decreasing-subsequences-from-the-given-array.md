# 最大化来自给定数组

> 原文：[https://www.geeksforgeeks.org/maximize-count-of-decreasing-subsequences-from-the-given-array/](https://www.geeksforgeeks.org/maximize-count-of-decreasing-subsequences-from-the-given-array/)

的递减子序列数

给定数组 **arr []** ，任务是重新排列数组以生成**最大递减子序列**，并打印的最大 尽可能多的子序列，以使每个数组元素可以是单个子序列的一部分，并且子序列的长度需要最大化。

**示例**：

> **输入**：arr [] = {5，2，3，4}
> **输出**：1
> **说明**：
> 给定数组 可以重新排列为{5，4，3，2}。
> 由于每个元素仅出现一次，因此重新排列的数组会形成最大可能长度的递减子序列。
> 
> **输入**：arr [] = {5，2，6，5，2，4，5，2}
> **输出**：3
> **说明**：
> 可以将给定的数组重新排列为{5，2，6，5，4，2，5，5，2}。
> 给定数组可能的最大可能长度的 3 个递减子序列分别为{6，5，4，2}，{5，2}和{5，2}

**方法**：

要解决此问题，无需实际重新排列给定的数组。 由于每个元素都可以是单个子序列的一部分，因此子序列的数量将等于**最频繁元素**的频率。

请按照以下步骤解决问题：

*   遍历数组并将每个数组元素的频率存储在[哈希图](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)中

*   现在，遍历 HashMap 以找到数组中元素的最大频率。

*   将最大频率打印为最大可能减少的子序列的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count maximum subsequence 
void Maximum_subsequence(int A[], int N) 
{ 
    // Stores the frequency 
    // of array elements 
    unordered_map<int, int> frequency; 

    // Stores max frequency 
    int max_freq = 0; 

    for (int i = 0; i < N; i++) { 

        // Update frequency of A[i] 
        frequency[A[i]]++; 
    } 

    for (auto it : frequency) { 

        // Update max subsequence 
        if (it.second > max_freq) { 
            max_freq = it.second; 
        } 
    } 

    // Print the count 
    cout << max_freq << endl; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 5, 2, 6, 5, 2, 4, 5, 2 }; 

    int N = sizeof(arr) / sizeof(arr[0]); 

    Maximum_subsequence(arr, N); 

    return 0; 
} 

```

## Java

```java

// Java program for rearrange array 
// to generate maximum decreasing 
// subsequences 
import java.util.HashMap; 
import java.util.Map; 
public class Main { 
    // Function to count maximum subsequence 
    public static void Maximum_subsequence( 
        int[] A, int N) 
    { 
        // Stores the frequency 
        // of array elements 
        HashMap<Integer, Integer> frequency 
            = new HashMap<>(); 

        // Stores maximum frequency 
        int max_freq = 0; 

        for (int i = 0; i < N; i++) { 

            // Update frequency of A[i] 
            if (frequency.containsKey(A[i])) { 
                frequency.replace(A[i], 
                                  frequency.get(A[i]) + 1); 
            } 
            else { 
                frequency.put(A[i], 1); 
            } 
        } 

        for (Map.Entry it : frequency.entrySet()) { 

            // Update maximum subsequences 
            if ((int)it.getValue() > max_freq) { 
                max_freq = (int)it.getValue(); 
            } 
        } 

        // Print the result 
        System.out.println(max_freq); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int arr[] = { 5, 2, 6, 5, 2, 4, 5, 2 }; 

        int N = arr.length; 

        Maximum_subsequence(arr, N); 
    } 
} 

```

## Python3

```py

# Python3 program to implement  
# the above approach  

# Function to count maximum subsequence  
def Maximum_subsequence(A, N): 

    # Stores the frequency  
    # of array elements  
    frequency = dict();  

    # Stores max frequency  
    max_freq = 0;  

    for i in range(N):  
        if (A[i] in frequency): 
            frequency[A[i]] += 1
        else: 
            frequency[A[i]] = 1

    for it in frequency: 

        # Update max subsequence  
        if (frequency[it] > max_freq):  
            max_freq = frequency[it];  

    # Print the count  
    print(max_freq);  

# Driver Code  
arr = [ 5, 2, 6, 5, 2, 4, 5, 2 ];  

Maximum_subsequence(arr, len(arr));  

# This code is contributed by grand_master 

```

## C#

```cs

// C# program for rearrange array 
// to generate maximum decreasing 
// subsequences 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to count maximum subsequence 
public static void Maximum_subsequence(int[] A, 
                                       int N) 
{ 

    // Stores the frequency 
    // of array elements 
    Dictionary<int,  
               int> frequency = new Dictionary<int, 
                                               int>(); 

    // Stores maximum frequency 
    int max_freq = 0; 

    for(int i = 0; i < N; i++) 
    { 

        // Update frequency of A[i] 
        if (frequency.ContainsKey(A[i]))  
        { 
            frequency[A[i]] = frequency[A[i]] + 1; 
        } 
        else 
        { 
            frequency.Add(A[i], 1); 
        } 
    } 

    foreach(KeyValuePair<int,  
                         int> it in frequency)  
    { 

        // Update maximum subsequences 
        if ((int)it.Value > max_freq) 
        { 
            max_freq = (int)it.Value; 
        } 
    } 

    // Print the result 
    Console.WriteLine(max_freq); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 5, 2, 6, 5, 2, 4, 5, 2 }; 

    int N = arr.Length; 

    Maximum_subsequence(arr, N); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:** 

```
3

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*



* * *

* * *



