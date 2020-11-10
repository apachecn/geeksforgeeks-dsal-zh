# 由相同元素组成的子序列数

> 原文：[https://www.geeksforgeeks.org/count-of-subsequences-consisting-of-the-same-element/](https://www.geeksforgeeks.org/count-of-subsequences-consisting-of-the-same-element/)

给定由`N`个整数组成的数组`A[]`，任务是找到子序列的总数，该子序列仅包含在整个子序列中重复的一个不同的数。

**示例**：

> **输入**：`A[] = {1, 2, 1, 5, 2}`
>
> **输出**：7
>
> **解释**：
>
> 子序列`{1}, {2}, {1}, {5}, {2}, {1, 1}`和`{2, 2}`满足所需条件。
> 
> **输入**：`A[] = {5, 4, 4, 5, 10, 4}`
>
> **输出**：11
>
> **说明**：
>
> 子序列`{5}, {4}, {4}, {5}, {10}, {4}, {5, 5}, {4, 4}, {4, 4}, {4, 4}`和`{4, 4, 4}`满足要求的条件。

**方法**：

]请按照以下步骤解决问题：

*   遍历数组并计算[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)中每个元素的频率。

*   遍历`HashMap`。 对于每个元素，可通过以下公式计算所需的子序列数：

> `arr[i] = pow(2, freq[arr[i]]) – 1`可能产生的子序列数

*   从给定数组计算可能的子序列总数。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count subsequences in 
// array containing same element 
void CountSubSequence(int A[], int N) 
{ 
    // Stores the count 
    // of subsequences 
    int result = 0; 

    // Stores the frequency 
    // of array elements 
    map<int, int> mp; 

    for (int i = 0; i < N; i++) { 

        // Update frequency of A[i] 
        mp[A[i]]++; 
    } 

    for (auto it : mp) { 

        // Calculate number of subsequences 
        result 
            = result + pow(2, it.second) - 1; 
    } 

    // Print the result 
    cout << result << endl; 
} 

// Driver code 
int main() 
{ 
    int A[] = { 5, 4, 4, 5, 10, 4 }; 

    int N = sizeof(A) / sizeof(A[0]); 

    CountSubSequence(A, N); 

    return 0; 
} 

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*;

class GFG{

// Function to count subsequences in
// array containing same element
static void CountSubSequence(int A[], int N)
{

    // Stores the count
    // of subsequences
    int result = 0;

    // Stores the frequency
    // of array elements
    Map<Integer, 
        Integer> mp = new HashMap<Integer,
                                  Integer>();

    for(int i = 0; i < N; i++)
    {

        // Update frequency of A[i]
        mp.put(A[i], mp.getOrDefault(A[i], 0) + 1);
    }

    for(Integer it : mp.values())
    {

        // Calculate number of subsequences
        result = result + (int)Math.pow(2, it) - 1;
    }

    // Print the result
    System.out.println(result);
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 5, 4, 4, 5, 10, 4 };
    int N = A.length;

    CountSubSequence(A, N);
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program to implement  
# the above approach  

# Function to count subsequences in  
# array containing same element  
def CountSubSequence(A, N):

    # Stores the frequency  
    # of array elements  
    mp = {}

    for element in A:
        if element in mp:
            mp[element] += 1
        else:
            mp[element] = 1

    result = 0

    for key, value in mp.items():

        # Calculate number of subsequences  
        result += pow(2, value) - 1

    # Print the result      
    print(result)

# Driver code
A = [ 5, 4, 4, 5, 10, 4 ]
N = len(A)

CountSubSequence(A, N)

# This code is contributed by jojo9911

```

## C#

```cs

// C# program to implement 
// the above approach 
using System;
using System.Collections.Generic;

class GFG{ 

// Function to count subsequences in 
// array containing same element 
public static void CountSubSequence(int []A, int N) 
{ 

    // Stores the count 
    // of subsequences 
    int result = 0; 

    // Stores the frequency 
    // of array elements 
    var mp = new Dictionary<int, int>();

    for(int i = 0; i < N; i++) 
    { 

        // Update frequency of A[i] 
        if(mp.ContainsKey(A[i]))
            mp[A[i]] += 1;
        else
            mp.Add(A[i], 1);
    } 

    foreach(var it in mp) 
    { 

        // Calculate number of subsequences 
        result = result + 
                 (int)Math.Pow(2, it.Value) - 1; 
    } 

    // Print the result 
    Console.Write(result); 
} 

// Driver code 
public static void Main() 
{ 
    int []A = { 5, 4, 4, 5, 10, 4 }; 
    int N = A.Length; 

    CountSubSequence(A, N); 
} 
} 

// This code is contributed by grand_master

```

**输出**： 

```
11

```

**时间复杂度**：`O(NlogN)`

**辅助空间**：`O(n)`



* * *

* * *



