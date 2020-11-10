# 两组的不重叠总和

> 原文：[https://www.geeksforgeeks.org/overlapping-sum-two-array/](https://www.geeksforgeeks.org/overlapping-sum-two-array/)

给定两个大小为`n`的数组`A[]`和`B[]`。 假定两个数组分别包含不同的元素。 我们需要找到所有不常见元素的总和。

**示例**：

```
Input : A[] = {1, 5, 3, 8}
        B[] = {5, 4, 6, 7}
Output : 29
1 + 3 + 4 + 6 + 7 + 8 = 29

Input : A[] = {1, 5, 3, 8}
        B[] = {5, 1, 8, 3}
Output : 0
All elements are common.

```

**暴力法**：

一种简单的方法是，对`A[]`中的每个元素检查是否在`B[]`中存在，如果存在，则将其添加到结果中。 同样，遍历`B[]`并对于`B`中不存在的每个元素，将其添加到结果中。

时间复杂度：`O(N ^ 2)`。

**哈希概念**：

创建一个空哈希并将两个数组的元素插入到其中。 现在遍历哈希表并添加所有计数为 1 的元素。（根据问题，两个数组分别具有不同的元素）

下面是上述方法的实现：

## C++

```cpp

// CPP program to find Non-overlapping sum 
#include <bits/stdc++.h> 
using namespace std; 

// function for calculating 
// Non-overlapping sum of two array 
int findSum(int A[], int B[], int n) 
{ 
    // Insert elements of both arrays 
    unordered_map<int, int> hash;     
    for (int i = 0; i < n; i++) { 
        hash[A[i]]++; 
        hash[B[i]]++; 
    } 

    // calculate non-overlapped sum 
    int sum = 0; 
    for (auto x: hash)  
        if (x.second == 1) 
            sum += x.first; 

    return sum; 
} 

// driver code 
int main() 
{ 
    int A[] = { 5, 4, 9, 2, 3 }; 
    int B[] = { 2, 8, 7, 6, 3 }; 

    // size of array 
    int n = sizeof(A) / sizeof(A[0]); 

    // function call  
    cout << findSum(A, B, n);  
    return 0; 
} 

```

## Java

```java

// Java program to find Non-overlapping sum  
import java.io.*; 
import java.util.*; 

class GFG  
{ 

    // function for calculating  
    // Non-overlapping sum of two array  
    static int findSum(int[] A, int[] B, int n) 
    { 
        // Insert elements of both arrays 
        HashMap<Integer, Integer> hash = new HashMap<>(); 
        for (int i = 0; i < n; i++) 
        { 
            if (hash.containsKey(A[i])) 
                hash.put(A[i], 1 + hash.get(A[i])); 
            else
                hash.put(A[i], 1); 

            if (hash.containsKey(B[i])) 
                hash.put(B[i], 1 + hash.get(B[i])); 
            else
                hash.put(B[i], 1); 
        } 

        // calculate non-overlapped sum  
        int sum = 0; 
        for (Map.Entry entry : hash.entrySet()) 
        { 
            if (Integer.parseInt((entry.getValue()).toString()) == 1) 
                sum += Integer.parseInt((entry.getKey()).toString()); 
        } 

        return sum; 

    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int[] A = { 5, 4, 9, 2, 3 };  
        int[] B = { 2, 8, 7, 6, 3 };  

        // size of array  
        int n = A.length; 

        // function call  
        System.out.println(findSum(A, B, n)); 
    } 
} 

// This code is contributed by rachana soma 

```

## Python3

```py

# Python3 program to find Non-overlapping sum  
from collections import defaultdict 

# Function for calculating  
# Non-overlapping sum of two array  
def findSum(A, B, n):  

    # Insert elements of both arrays  
    Hash = defaultdict(lambda:0) 
    for i in range(0, n):  
        Hash[A[i]] += 1
        Hash[B[i]] += 1

    # calculate non-overlapped sum  
    Sum = 0
    for x in Hash:  
        if Hash[x] == 1:  
            Sum += x  

    return Sum

# Driver code  
if __name__ == "__main__":  

    A = [5, 4, 9, 2, 3]  
    B = [2, 8, 7, 6, 3]  

    # size of array  
    n = len(A)  

    # Function call  
    print(findSum(A, B, n))  

# This code is contributed  
# by Rituraj Jain 

```

## C#

```cs

// C# program to find Non-overlapping sum 
using System; 
using System.Collections.Generic;  

class GFG  
{ 

    // function for calculating  
    // Non-overlapping sum of two array  
    static int findSum(int[] A, int[] B, int n) 
    { 
        // Insert elements of both arrays 
        Dictionary<int, int> hash = new Dictionary<int, int>(); 
        for (int i = 0; i < n; i++) 
        { 
            if (hash.ContainsKey(A[i])) 
            { 
                var v = hash[A[i]]; 
                hash.Remove(A[i]); 
                hash.Add(A[i], 1 + v); 
            } 
            else
                hash.Add(A[i], 1); 

            if (hash.ContainsKey(B[i])) 
            { 
                var v = hash[B[i]]; 
                hash.Remove(B[i]); 
                hash.Add(B[i], 1 + v); 
            } 
            else
                hash.Add(B[i], 1); 
        } 

        // calculate non-overlapped sum  
        int sum = 0; 
        foreach(KeyValuePair<int, int> entry in hash) 
        { 
            if ((entry.Value) == 1) 
                sum += entry.Key; 
        } 

        return sum; 

    } 

    // Driver code 
    public static void Main(String []args) 
    { 
        int[] A = { 5, 4, 9, 2, 3 };  
        int[] B = { 2, 8, 7, 6, 3 };  

        // size of array  
        int n = A.Length; 

        // function call  
        Console.WriteLine(findSum(A, B, n)); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
39

```



* * *

* * *



