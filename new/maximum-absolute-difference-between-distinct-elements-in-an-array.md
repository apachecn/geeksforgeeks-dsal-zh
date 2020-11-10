# 数组中不同元素之间的最大绝对差

> 原文：[https://www.geeksforgeeks.org/maximum-absolute-difference-between-distinct-elements-in-an-array/](https://www.geeksforgeeks.org/maximum-absolute-difference-between-distinct-elements-in-an-array/)

给定`N`个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，任务是找到数组不同元素之间的最大绝对差。

**示例**：

> **输入**：`arr[] = {12, 10, 9, 45, 2, 10, 10, 45, 10}`
>
> **输出**：10
>
> **说明**：
>
> 给定数组的不同元素是 12、9、2。
>
> 因此，它们之间的最大绝对差为`12 – 2 = 10`。
> 
> **输入**：`arr[] = {2, -1, 10, 3, -2, -1, 10}`
>
> **输出**：5
>
> **说明**：
>
> 给定数组的不同元素是 2、3，-2。
>
> 因此，它们之间的最大绝对差为`3 – (-2)= 5`。

**朴素的方法**：朴素的方法是将[不同元素存储在给定数组](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)中的数组`temp[]`中，并打印出数组`temp[]`的最大和最小元素差。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`

**有效方法**：可以使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)来优化上述幼稚方法。 步骤如下：

1.  将数组`arr[]`的每个元素的频率存储在[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)中。

2.  现在，使用上面创建的`HashMap`找到频率为`1`的数组的最大值和最小值。

3.  打印上一步中获得的最大值和最小值之间的差。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// absolute difference between
// distinct elements in arr[]
int MaxAbsDiff(int arr[], int n)
{

    // Map to store each element
    // with their occurrence in array
    unordered_map<int, int> map;

    // maxElement and minElement to
    // store maximum and minimum
    // distinct element in arr[]
    int maxElement = INT_MIN;
    int minElement = INT_MAX;

    // Traverse arr[] and update each
    // element frequency in Map
    for(int i = 0; i < n; i++)
    {
        map[arr[i]]++;
    }

    // Traverse Map and check if
    // value of any key appears 1
    // then update maxElement and
    // minElement by that key
    for(auto itr = map.begin(); 
             itr != map.end(); itr++)
    {
        if (itr -> second == 1)
        {
            maxElement = max(maxElement, 
                             itr -> first);
            minElement = min(minElement, 
                             itr -> first);
        }
    }

    // Return absolute difference of
    // maxElement and minElement
    return abs(maxElement - minElement);
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 12, 10, 9, 45, 2,
                  10, 10, 45, 10 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << MaxAbsDiff(arr, n) << "\n";

    return 0;
}

// This code is contributed by akhilsaini

```

## Java

```java

// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum
    // absolute difference between
    // distinct elements in arr[]
    static int MaxAbsDiff(int[] arr, int n)
    {
        // HashMap to store each element
        // with their occurrence in array
        Map<Integer, Integer> map
            = new HashMap<>();

        // maxElement and minElement to
        // store maximum and minimum
        // distinct element in arr[]
        int maxElement = Integer.MIN_VALUE;
        int minElement = Integer.MAX_VALUE;

        // Traverse arr[] and update each
        // element frequency in HashMap
        for (int i = 0; i < n; i++) {
            map.put(arr[i],
                    map.getOrDefault(arr[i], 0)
                        + 1);
        }

        // Traverse HashMap and check if
        // value of any key appears 1
        // then update maxElement and
        // minElement by that key
        for (Map.Entry<Integer, Integer> k :
             map.entrySet()) {

            if (k.getValue() == 1) {
                maxElement
                    = Math.max(maxElement,
                               k.getKey());
                minElement
                    = Math.min(minElement,
                               k.getKey());
            }
        }

        // Return absolute difference of
        // maxElement and minElement
        return Math.abs(maxElement
                        - minElement);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 12, 10, 9, 45, 2,
                      10, 10, 45, 10 };
        int n = arr.length;

        // Function Call
        System.out.println(MaxAbsDiff(arr, n));
    }
}

```

## Python3

```py

# Python3 program for 
# the above approach
import sys
from collections import defaultdict

# Function to find the maximum
# absolute difference between
# distinct elements in arr[]
def MaxAbsDiff(arr, n):

    # HashMap to store each element
    # with their occurrence in array
    map = defaultdict (int)

    # maxElement and minElement to
    # store maximum and minimum
    # distinct element in arr[]
    maxElement = -sys.maxsize - 1
    minElement = sys.maxsize

    # Traverse arr[] and update each
    # element frequency in HashMap
    for i in range (n):
        map[arr[i]] += 1

    # Traverse HashMap and check if
    # value of any key appears 1
    # then update maxElement and
    # minElement by that key
    for k in map:
        if (map[k] == 1):
            maxElement = max(maxElement, k)
            minElement = min(minElement, k)

    # Return absolute difference of
    # maxElement and minElement
    return abs(maxElement - minElement)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [12, 10, 9, 45, 2,
           10, 10, 45, 10]
    n = len( arr)

    # Function Call
    print(MaxAbsDiff(arr, n))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// absolute difference between
// distinct elements in []arr
static int MaxAbsDiff(int[] arr, int n)
{

    // Dictionary to store each element
    // with their occurrence in array
    Dictionary<int,
               int> map = new Dictionary<int,
                                         int>();

    // maxElement and minElement to
    // store maximum and minimum
    // distinct element in []arr
    int maxElement = int.MinValue;
    int minElement = int.MaxValue;

    // Traverse []arr and update each
    // element frequency in Dictionary
    for(int i = 0; i < n; i++)
    {
       if(map.ContainsKey(arr[i]))
          map[arr[i]] = map[arr[i]] + 1; 
       else
          map.Add(arr[i], 1);
    }

    // Traverse Dictionary and check if
    // value of any key appears 1
    // then update maxElement and
    // minElement by that key
    foreach (KeyValuePair<int, int> k in map)
    {
        if (k.Value == 1)
        {
            maxElement = Math.Max(maxElement, 
                                  k.Key);
            minElement = Math.Min(minElement,
                                  k.Key);
        }
    }

    // Return absolute difference of
    // maxElement and minElement
    return Math.Abs(maxElement - minElement);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int[] arr = { 12, 10, 9, 45, 2,
                  10, 10, 45, 10 };
    int n = arr.Length;

    // Function call
    Console.WriteLine(MaxAbsDiff(arr, n));
}
}

// This code is contributed by Princi Singh

```

**输出**： 

```
10

```

**时间复杂度**：`O(n)`；

**辅助空间**：`O(n)`



* * *

* * *



