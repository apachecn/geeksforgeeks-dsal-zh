# 最大长度子序列，相邻元素之间的差为 0 或 1 | 设置 2

> 原文：[https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1-set-2/](https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1-set-2/)

给定 **n** 个整数的数组。 问题在于找到子序列的最大长度，且子序列中相邻元素之间的差为 0 或 1。需要`O(n)`的时间复杂度。

**示例**：

```
Input : arr[] = {2, 5, 6, 3, 7, 6, 5, 8}
Output : 5
The subsequence is {5, 6, 7, 6, 5}.

Input : arr[] = {-2, -1, 5, -1, 4, 0, 3}
Output : 4
The subsequence is {-2, -1, -1, 0}.

```

**方法 1**：先前在的[中讨论了具有 O（n <sup>2</sup> ）时间复杂度的方法。](https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1/)

**方法 2（有效方法）**：的想法是创建一个具有**（ele，len）**形式的元组的哈希图，其中 **len** 表示长度 以元素 **ele** 结尾的最长子序列。 现在，对于每个元素 arr [i]，我们可以找到哈希表中值 arr [i] -1，arr [i]和 arr [i] +1 的长度，并考虑其中的最大值。 将该最大值设为 **max** 。 现在，以 arr [i]结尾的最长子序列的长度为 **max + 1** 。 与哈希表中的元素 arr [i]一起更新此长度。 最后，在哈希表中具有最大长度的元素给出最大长度子序列。

## C++

```cpp

// C++ implementation to find maximum length 
// subsequence with difference between adjacent  
// elements as either 0 or 1 
#include <bits/stdc++.h> 
using namespace std; 

// function to find maximum length subsequence  
// with difference between adjacent elements as 
// either 0 or 1 
int maxLenSub(int arr[], int n) 
{ 
    // hash table to map the array element with the 
    // length of the longest subsequence of which 
    // it is a part of and is the last element of 
    // that subsequence 
    unordered_map<int, int> um; 

    // to store the maximum length subsequence 
    int maxLen = 0; 

    // traverse the array elements 
    for (int i=0; i<n; i++) 
    { 
        // initialize current length  
        // for element arr[i] as 0 
        int len = 0; 

        // if 'arr[i]-1' is in 'um' and its length of  
        // subsequence is greater than 'len' 
        if (um.find(arr[i]-1) != um.end() && len < um[arr[i]-1]) 
            len = um[arr[i]-1]; 

        // if 'arr[i]' is in 'um' and its length of  
        // subsequence is greater than 'len'     
        if (um.find(arr[i]) != um.end() && len < um[arr[i]]) 
            len = um[arr[i]]; 

        // if 'arr[i]+1' is in 'um' and its length of  
        // subsequence is greater than 'len'         
        if (um.find(arr[i]+1) != um.end() && len < um[arr[i]+1]) 
            len = um[arr[i]+1];     

        // update arr[i] subsequence length in 'um'     
        um[arr[i]] = len + 1; 

        // update maximum length 
        if (maxLen < um[arr[i]])     
            maxLen = um[arr[i]]; 
    } 

    // required maximum length subsequence 
    return maxLen;         
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = {2, 5, 6, 3, 7, 6, 5, 8}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Maximum length subsequence = "
         << maxLenSub(arr, n); 
    return 0; 
}  

```

## Java

```java

// Java implementation to find maximum length 
// subsequence with difference between adjacent  
// elements as either 0 or 1 
import java.util.HashMap; 

class GFG 
{ 

    // function to find maximum length subsequence  
    // with difference between adjacent elements as 
    // either 0 or 1 
    public static int maxLengthSub(int[] arr) 
    { 

        // to store the maximum length subsequence 
        int max_val = 0; 
        int start = 0; 

        // hash table to map the array element with the 
        // length of the longest subsequence of which 
        // it is a part of and is the last element of 
        // that subsequence 
        HashMap<Integer, Integer> map = new HashMap<>(); 

        // traverse the array elements 
        for (int i = 0; i < arr.length; i++)  
        { 

            // initialize current length  
            // for element arr[i] as 0 
            int temp = 0; 
            if (map.containsKey(arr[i] - 1)) 
            { 
                temp = map.get(arr[i] - 1); 
            } 

            if (map.containsKey(arr[i])) 
            { 
                temp = Math.max(temp, map.get(arr[i])); 
            } 

            if (map.containsKey(arr[i] + 1)) 
            { 
                temp = Math.max(temp, map.get(arr[i] + 1)); 
            } 
            temp++; 

            // update maximum length 
            if (temp > max_val)  
            { 
                max_val = temp; 
            } 
            map.put(arr[i], temp); 
        } 

        // required maximum length subsequence 
        return max_val; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int arr[] = {2, 5, 6, 3, 7, 6, 5, 8}; 
        System.out.println(maxLengthSub(arr)); 
    } 
} 

// This code is contributed  
// by tushar jajodia 

```

## Python3

```py

# Python3 implementation to find maximum  
# length subsequence with difference between  
# adjacent elements as either 0 or 1  
from collections import defaultdict 

# Function to find maximum length subsequence with  
# difference between adjacent elements as either 0 or 1  
def maxLenSub(arr, n):  

    # hash table to map the array element with the  
    # length of the longest subsequence of which it is a  
    # part of and is the last element of that subsequence  
    um = defaultdict(lambda:0) 

    # to store the maximum length subsequence  
    maxLen = 0

    # traverse the array elements  
    for i in range(0, n):  

        # initialize current length  
        # for element arr[i] as 0  
        length = 0

        # if 'arr[i]-1' is in 'um' and its length of  
        # subsequence is greater than 'len'  
        if (arr[i]-1) in um and length < um[arr[i]-1]: 
            length = um[arr[i]-1]  

        # if 'arr[i]' is in 'um' and its length of  
        # subsequence is greater than 'len'  
        if arr[i] in um and length < um[arr[i]]:  
            length = um[arr[i]]  

        # if 'arr[i]+1' is in 'um' and its length of  
        # subsequence is greater than 'len'      
        if (arr[i]+1) in um and length < um[arr[i]+1]:  
            length = um[arr[i]+1]  

        # update arr[i] subsequence length in 'um'  
        um[arr[i]] = length + 1

        # update maximum length  
        if maxLen < um[arr[i]]:  
            maxLen = um[arr[i]]  

    # required maximum length subsequence  
    return maxLen 

# Driver program to test above  
if __name__ == "__main__":  

    arr = [2, 5, 6, 3, 7, 6, 5, 8]  
    n = len(arr)  
    print("Maximum length subsequence =", maxLenSub(arr, n)) 

# This code is contributed by Rituraj Jain 

```

**输出**：

```
Maximum length subsequence = 5

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`

感谢 **Neeraj** 在此帖子的[评论中提出了上述解决方案。](https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1/)

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

