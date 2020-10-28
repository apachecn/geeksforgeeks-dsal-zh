# 对数组 arr [] & brr []中的对（i，j）进行计数，使得 arr [i] – brr [j] = arr [j] – brr [i]

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 和 **brr []** 数组，它们由 **N** 个整数组成，其任务是计算对数 **]（i，j）**来自两个数组，使得**（arr [i] – brr [j]）**和**（arr [j] – brr [i]）** 相等。

**示例**：

> **输入**：A [] = {1、2、3、2、1}，B [] = {1、2、3、2、1}
> **输出**：2
> **说明**：满足条件的对是：
> 
> 1.  **（1、5）**：arr [1]-brr [5] = 1-1 = 0，arr [5 [-brr [1]] = 1-1 = 0
> 2.  **（2，4）**：arr [2]-brr [4] = 2-2 = 0，arr [4]-brr [2] = 2-2 = 0
> 
> **输入：A** [] = {1、4、20、3、10、5}，B [] = {9、6、1、7、11、6}
> **输出 **：4

**天真的方法**：解决该问题的最简单方法是从两个给定的数组生成所有对，并检查所需条件。 对于发现条件为真的每对，增加此类对的**计数**。 最后，打印获得的**计数**。

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（1）*

**有效方法**：的想法是将给定的表达式**（a [i] – b [j] = a [j] – b [i]）**转换为**形式 （a [i] + b [i] = a [j] + b [j]）**，然后计算满足条件的对。 步骤如下：

1.  转换表达式， **a [i] – b [j] = a [j] – b [i]** == > **a [i] + b [i] = a [j ] + b [j]** 。 表达式的一般形式是为任何对**（i，j）**计数两个数组每个索引处的值之和。

2.  初始化辅助数组 **c []** ，以在每个索引 **i** 处存储对应的总和 **c [i] = a [i] + b [i]** 。

3.  现在，问题减少了，以找到具有相同 **c [i]** 值的可能对的数量。

4.  [计算数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) **c []** 中每个元素的频率，如果任何 **c [i]** 频率值大于 1，则可以成对。

5.  使用公式计算以上步骤中的有效对数：

> ![\frac{c[i]*(c[i] - 1)}{2}      ](img/78a9caad2e79b3d7507060eab6d0d967.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the pairs such that
// given condition is satisfied
int CountPairs(int* a, int* b, int n)
{
    // Stores the sum of element at
    // each corresponding index
    int C[n];

    // Find the sum of each index
    // of both array
    for (int i = 0; i < n; i++) {
        C[i] = a[i] + b[i];
    }

    // Stores frequency of each element
    // present in sumArr
    map<int, int> freqCount;

    for (int i = 0; i < n; i++) {
        freqCount[C[i]]++;
    }

    // Initialize number of pairs
    int NoOfPairs = 0;

    for (auto x : freqCount) {
        int y = x.second;

        // Add possible vaid pairs
        NoOfPairs = NoOfPairs
                    + y * (y - 1) / 2;
    }

    // Return Number of Pairs
    cout << NoOfPairs;
}

// Driver Code
int main()
{
    // Given array arr[] and brr[]
    int arr[] = { 1, 4, 20, 3, 10, 5 };

    int brr[] = { 9, 6, 1, 7, 11, 6 };

    // Size of given array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    CountPairs(arr, brr, N);

    return 0;
}

```

## Java

```java

// Java program for the above approach 
import java.util.*;
import java.io.*;

class GFG{ 

// Function to find the minimum number 
// needed to be added so that the sum 
// of the digits does not exceed K 
static void CountPairs(int a[], int b[], int n) 
{ 

    // Stores the sum of element at 
    // each corresponding index 
    int C[] = new int[n]; 

    // Find the sum of each index 
    // of both array 
    for(int i = 0; i < n; i++) 
    { 
        C[i] = a[i] + b[i]; 
    } 

    // Stores frequency of each element 
    // present in sumArr 
    // map<int, int> freqCount;
    HashMap<Integer,
            Integer> freqCount = new HashMap<>();

    for(int i = 0; i < n; i++) 
    { 
        if (!freqCount.containsKey(C[i]))
            freqCount.put(C[i], 1);
        else
            freqCount.put(C[i], 
            freqCount.get(C[i]) + 1);
    } 

    // Initialize number of pairs 
    int NoOfPairs = 0; 

    for(Map.Entry<Integer,
                  Integer> x : freqCount.entrySet())
    { 
        int y = x.getValue(); 

        // Add possible vaid pairs 
        NoOfPairs = NoOfPairs + 
                  y * (y - 1) / 2; 
    } 

    // Return Number of Pairs 
   System.out.println(NoOfPairs);
} 

// Driver Code 
public static void main(String args[]) 
{ 

    // Given array arr[] and brr[] 
    int arr[] = { 1, 4, 20, 3, 10, 5 }; 
    int brr[] = { 9, 6, 1, 7, 11, 6 };

    // Size of given array 
    int N = arr.length;

    // Function calling 
    CountPairs(arr, brr, N);
} 
}

// This code is contributed by bikram2001jha

```

## Python3

```py

# Python3 program for the above approach

# Function to count the pairs such that
# given condition is satisfied
def CountPairs(a, b, n):

    # Stores the sum of element at
    # each corresponding index
    C = [0] * n

    # Find the sum of each index
    # of both array
    for i in range(n):
        C[i] = a[i] + b[i]

    # Stores frequency of each element
    # present in sumArr
    freqCount = dict() 

    for i in range(n):
        if C[i] in freqCount.keys(): 
            freqCount[C[i]] += 1
        else:
            freqCount[C[i]] = 1

    # Initialize number of pairs
    NoOfPairs = 0

    for x in freqCount:
        y = freqCount[x]

        # Add possible vaid pairs
        NoOfPairs = (NoOfPairs + y *
                       (y - 1) // 2)

    # Return Number of Pairs
    print(NoOfPairs)

# Driver Code

# Given array arr[] and brr[]
arr = [ 1, 4, 20, 3, 10, 5 ]
brr = [ 9, 6, 1, 7, 11, 6 ]

# Size of given array
N = len(arr)

# Function calling
CountPairs(arr, brr, N)

# This code is contributed by code_hunt

```

## C#

```cs

// C# program for the above approach 
using System;
using System.Collections.Generic;

class GFG{ 

// Function to find the minimum number 
// needed to be added so that the sum 
// of the digits does not exceed K 
static void CountPairs(int []a, int []b,
                       int n) 
{ 

    // Stores the sum of element at 
    // each corresponding index 
    int []C = new int[n]; 

    // Find the sum of each index 
    // of both array 
    for(int i = 0; i < n; i++) 
    { 
        C[i] = a[i] + b[i]; 
    } 

    // Stores frequency of each element 
    // present in sumArr 
    // map<int, int> freqCount;
    Dictionary<int,
               int> freqCount = new Dictionary<int,
                                               int>();

    for(int i = 0; i < n; i++) 
    { 
        if (!freqCount.ContainsKey(C[i]))
            freqCount.Add(C[i], 1);
        else
            freqCount[C[i]] = freqCount[C[i]] + 1;
    } 

    // Initialize number of pairs 
    int NoOfPairs = 0; 

    foreach(KeyValuePair<int,
                         int> x in freqCount)
    { 
        int y = x.Value; 

        // Add possible vaid pairs 
        NoOfPairs = NoOfPairs + 
                  y * (y - 1) / 2; 
    } 

    // Return Number of Pairs 
    Console.WriteLine(NoOfPairs);
} 

// Driver Code 
public static void Main(String []args) 
{ 

    // Given array []arr and brr[] 
    int []arr = { 1, 4, 20, 3, 10, 5 }; 
    int []brr = { 9, 6, 1, 7, 11, 6 };

    // Size of given array 
    int N = arr.Length;

    // Function calling 
    CountPairs(arr, brr, N);
} 
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
4

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*



* * *

* * *



