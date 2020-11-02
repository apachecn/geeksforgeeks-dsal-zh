# 对数组中的对进行计数，以使一个频率至少等于另一个

> 原文：[https://www.geeksforgeeks.org/count-pairs-in-an-array-such-that-frequency-of-one-is-at-least-value-of-other/](https://www.geeksforgeeks.org/count-pairs-in-an-array-such-that-frequency-of-one-is-at-least-value-of-other/)

的值

给定整数数组`A[]`。 任务是找到正整数`(X, Y)`的有序对总数，以使`X`在`A[]`中至少发生`Y`次，而`Y`在`A`中至少发生`X`次。

**范例**：

```
Input : A[] = { 1, 1, 2, 2, 3 }
Output : 4
Ordered pairs are -> { [1, 1], [1, 2], [2, 1], [2, 2] }

Input : A = { 3, 3, 2, 2, 2 }
Output : 3
Ordered pairs are -> { [3, 2], [2, 2], [2, 3] }

```

**方法**：

1.  创建一个数组`A[]`的元素数量的哈希表`m[]`。

2.  遍历唯一元素的哈希表。 令`X`为哈希表中的当前键，`Y`为频率。

3.  检查每个元素`j ∈ [1, Y]`，如果`m[j] >= X`将答案递增 1。

4.  返回数组`A`的总有序对`(X, Y)`的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find number 
// of ordered pairs 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find count of Ordered pairs 
int countOrderedPairs(int A[], int n) 
{ 
    // Initialize pairs to 0 
    int orderedPairs = 0; 

    // Store frequencies  
    unordered_map<int, int> m; 
    for (int i = 0; i < n; ++i)  
        m[A[i]]++; 

    // Count total Ordered_pairs 
    for (auto entry : m) { 
        int X = entry.first; 
        int Y = entry.second; 

        for (int j = 1; j <= Y; j++) { 
            if (m[j] >= X) 
                orderedPairs++; 
        } 
    } 

    return orderedPairs; 
} 

// Driver Code 
int main() 
{ 
    int A[] = { 1, 1, 2, 2, 3 }; 
    int n = sizeof(A) / sizeof(A[0]); 
    cout << countOrderedPairs(A, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find number 
// of ordered pairs 
import java.util.HashMap; 
import java.util.Map; 

class GFG 
{ 

    // Function to find count of Ordered pairs 
    public static int countOrderedPairs(int[] A, int n)  
    { 

        // Initialize pairs to 0 
        int orderedPairs = 0; 

        // Store frequencies 
        HashMap<Integer, Integer> m = new HashMap<>(); 
        for (int i = 0; i < n; i++) 
        { 
            if (m.get(A[i]) == null) 
                m.put(A[i], 1); 
            else
            { 
                int a = m.get(A[i]); 
                m.put(A[i], ++a); 
            } 
        } 

        // Count total Ordered_pairs 
        for (int entry : m.keySet()) 
        { 

            int X = entry; 
            int Y = m.get(entry); 

            for (int j = 1; j <= Y; j++) 
            { 
                if (m.get(j) >= X) 
                    orderedPairs++; 
            } 
        } 

        return orderedPairs; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int[] A = {1, 1, 2, 2, 3}; 
        int n = A.length; 
        System.out.print(countOrderedPairs(A, n)); 
    } 
} 

// This code is contibuted by 
// sanjeev2552 

```

## Python3

```py

# Python3 program to find the  
# number of ordered pairs  
from collections import defaultdict 

# Function to find count of Ordered pairs  
def countOrderedPairs(A, n):  

    # Initialize pairs to 0  
    orderedPairs = 0

    # Store frequencies  
    m = defaultdict(lambda:0) 
    for i in range(0, n):  
        m[A[i]] += 1

    # Count total Ordered_pairs  
    for X,Y in m.items():  

        for j in range(1, Y + 1):  
            if m[j] >= X:  
                orderedPairs += 1

    return orderedPairs  

# Driver Code  
if __name__ == "__main__": 

    A = [1, 1, 2, 2, 3]  
    n = len(A)  
    print(countOrderedPairs(A, n))  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to illustrate how  
// to create a dictionary  
using System;  
using System.Collections.Generic;  

class GFG 
{ 

    // Function to find count of Ordered pairs 
    public static int countOrderedPairs(int[] A,             
                                        int n)  
    { 

        // Initialize pairs to 0 
        int orderedPairs = 0; 

        // Store frequencies 
        Dictionary<int,      
                   int> m = new Dictionary<int,  
                                           int>(); 
        for (int i = 0; i < n; i++) 
        { 
            if (!m.ContainsKey(A[i])) 
                m.Add(A[i], 1); 
            else
            { 
                m[A[i]]++; 
            } 
        } 

        // Count total Ordered_pairs 
        foreach(KeyValuePair<int, int> entry in m) 
        { 

            int X = entry.Key; 
            int Y = entry.Value; 

            for (int j = 1; j <= Y; j++) 
            { 
                if (m[j] >= X) 
                    orderedPairs++; 
            } 
        } 
        return orderedPairs; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int[] A = {1, 1, 2, 2, 3}; 
        int n = A.Length; 
        Console.Write(countOrderedPairs(A, n)); 
    } 
} 

// This code is contibuted by 
// mohit kumar 

```

**Output:**

```
4

```



* * *

* * *



