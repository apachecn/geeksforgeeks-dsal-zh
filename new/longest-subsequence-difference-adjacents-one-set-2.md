# 最长的子序列，使得相邻元素之间的差为 1 | 设置 2

> 原文：[https://www.geeksforgeeks.org/longest-subsequence-difference-adjacents-one-set-2/](https://www.geeksforgeeks.org/longest-subsequence-difference-adjacents-one-set-2/)

给定大小为 **n** 的数组。 任务是找到最长的子序列，以使相邻序列之间的差异为 1。 需要`O(n)`的时间复杂度。

**示例**：

```
Input :  arr[] = {10, 9, 4, 5, 4, 8, 6}
Output :  3
As longest subsequences with difference 1 are, "10, 9, 8", 
"4, 5, 4" and "4, 5, 6".

Input :  arr[] = {1, 2, 3, 2, 3, 7, 2, 1}
Output :  7
As longest consecutive sequence is "1, 2, 3, 2, 3, 2, 1".

```

**方法 1**：先前在的[中讨论了时间复杂度为`O(N ^ 2)`的方法。](https://www.geeksforgeeks.org/longest-subsequence-such-that-difference-between-adjacents-is-one/)

**方法 2（有效方法）**：的想法是创建一个具有**（ele，len）**形式的元组的哈希映射，其中 **len** 表示长度 以元素 **ele** 结尾的最长子序列。 现在，对于每个元素 arr [i]，我们可以在哈希表中找到值 arr [i] -1 和 arr [i] +1 的长度，并考虑其中的最大值。 将该最大值设为 **max** 。 现在，以 arr [i]结尾的最长子序列的长度为 **max + 1** 。 与哈希表中的元素 arr [i]一起更新此长度。 最后，在哈希表中具有最大长度的元素给出了最长的子序列。

## C++

```cpp

// C++ implementation to find longest subsequence  
// such that difference between adjacents is one 
#include <bits/stdc++.h> 
using namespace std; 

// function to find longest subsequence such 
// that difference between adjacents is one 
int longLenSub(int arr[], int n) 
{ 
    // hash table to map the array element with the 
    // length of the longest subsequence of which 
    // it is a part of and is the last element of 
    // that subsequence 
    unordered_map<int, int> um; 

    // to store the longest length subsequence 
    int longLen = 0; 

    // traverse the array elements 
    for (int i=0; i<n; i++) 
    { 
        // initialize current length  
        // for element arr[i] as 0 
        int len = 0; 

        // if 'arr[i]-1' is in 'um' and its length   
        // of subsequence is greater than 'len' 
        if (um.find(arr[i]-1) != um.end() &&  
            len < um[arr[i]-1]) 
            len = um[arr[i]-1]; 

        // if 'arr[i]+1' is in 'um' and its length   
        // of subsequence is greater than 'len'         
        if (um.find(arr[i]+1) != um.end() &&  
            len < um[arr[i]+1]) 
            len = um[arr[i]+1];     

        // update arr[i] subsequence length in 'um'     
        um[arr[i]] = len + 1; 

        // update longest length 
        if (longLen < um[arr[i]])     
            longLen = um[arr[i]]; 
    } 

    // required longest length subsequence 
    return longLen;         
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = {1, 2, 3, 4, 5, 3, 2}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Longest length subsequence = "
         << longLenSub(arr, n); 
    return 0; 
}    

```

## Java

```java

// Java implementation to find longest subsequence  
// such that difference between adjacents is one 
import java.util.*; 

class GFG  
{ 

// function to find longest subsequence such 
// that difference between adjacents is one 
static int longLenSub(int []arr, int n) 
{ 
    // hash table to map the array element with the 
    // length of the longest subsequence of which 
    // it is a part of and is the last element of 
    // that subsequence 
    HashMap<Integer,  
            Integer> um = new HashMap<Integer,  
                                      Integer>(); 

    // to store the longest length subsequence 
    int longLen = 0; 

    // traverse the array elements 
    for (int i = 0; i < n; i++) 
    { 
        // initialize current length  
        // for element arr[i] as 0 
        int len = 0; 

        // if 'arr[i]-1' is in 'um' and its length  
        // of subsequence is greater than 'len' 
        if (um.containsKey(arr[i] - 1) &&  
              len < um.get(arr[i] - 1)) 
              len = um.get(arr[i] - 1); 

        // if 'arr[i]+1' is in 'um' and its length  
        // of subsequence is greater than 'len'      
        if (um.containsKey(arr[i] + 1) &&  
              len < um.get(arr[i] + 1)) 
              len = um.get(arr[i] + 1);  

        // update arr[i] subsequence length in 'um'  
        um. put(arr[i], len + 1); 

        // update longest length 
        if (longLen < um.get(arr[i]))  
            longLen = um.get(arr[i]); 
    } 

    // required longest length subsequence 
    return longLen;      
} 

// Driver Code 
public static void main(String[] args)  
{ 
    int[] arr = {1, 2, 3, 4, 5, 3, 2}; 
    int n = arr.length; 
    System.out.println("Longest length subsequence = " +  
                                    longLenSub(arr, n)); 
} 
}  

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 implementation to find longest  
# subsequence such that difference between  
# adjacents is one  
from collections import defaultdict 

# function to find longest subsequence such  
# that difference between adjacents is one  
def longLenSub(arr, n): 

    # hash table to map the array element  
    # with the length of the longest  
    # subsequence of which it is a part of  
    # and is the last element of that subsequence  
    um = defaultdict(lambda:0) 
    longLen = 0
    for i in range(n): 

        # / initialize current length  
        # for element arr[i] as 0  
        len1 = 0

        # if 'arr[i]-1' is in 'um' and its length  
        # of subsequence is greater than 'len'  
        if (arr[i - 1] in um and 
            len1 < um[arr[i] - 1]): 
            len1 = um[arr[i] - 1] 

        # f 'arr[i]+1' is in 'um' and its length  
        # of subsequence is greater than 'len'      
        if (arr[i] + 1 in um and 
            len1 < um[arr[i] + 1]): 
            len1 = um[arr[i] + 1] 

        # update arr[i] subsequence  
        # length in 'um'      
        um[arr[i]] = len1 + 1

        # update longest length  
        if longLen < um[arr[i]]: 
            longLen = um[arr[i]] 

    # required longest length 
    # subsequence  
    return longLen 

# Driver code 
arr = [1, 2, 3, 4, 5, 3, 2] 
n = len(arr) 
print("Longest length subsequence =", 
                  longLenSub(arr, n)) 

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# implementation to find longest subsequence  
// such that difference between adjacents is one 
using System; 
using System.Collections.Generic; 

class GFG 
{  

// function to find longest subsequence such 
// that difference between adjacents is one 
static int longLenSub(int []arr, int n) 
{ 
    // hash table to map the array element with the 
    // length of the longest subsequence of which 
    // it is a part of and is the last element of 
    // that subsequence 
    Dictionary<int,  
               int> um = new Dictionary<int, 
                                        int>(); 

    // to store the longest length subsequence 
    int longLen = 0; 

    // traverse the array elements 
    for (int i = 0; i < n; i++) 
    { 
        // initialize current length  
        // for element arr[i] as 0 
        int len = 0; 

        // if 'arr[i]-1' is in 'um' and its length  
        // of subsequence is greater than 'len' 
        if (um.ContainsKey(arr[i] - 1) &&  
            len < um[arr[i] - 1]) 
            len = um[arr[i] - 1]; 

        // if 'arr[i]+1' is in 'um' and its length  
        // of subsequence is greater than 'len'      
        if (um.ContainsKey(arr[i] + 1) &&  
            len < um[arr[i] + 1]) 
            len = um[arr[i] + 1];  

        // update arr[i] subsequence length in 'um'  
        um[arr[i]] = len + 1; 

        // update longest length 
        if (longLen < um[arr[i]])  
            longLen = um[arr[i]]; 
    } 

    // required longest length subsequence 
    return longLen;      
} 

// Driver program to test above 
static void Main() 
{ 
    int[] arr = {1, 2, 3, 4, 5, 3, 2}; 
    int n = arr.Length; 
    Console.Write("Longest length subsequence = " +  
                               longLenSub(arr, n)); 
} 
}  

// This code is contributed by Mohit Kumar 

```

**Output:**

```
Longest length subsequence = 6

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。

本文由 [**Ayush Jauhari**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

