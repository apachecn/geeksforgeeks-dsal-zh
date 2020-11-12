# 在第一个数组模`M`中添加的最小数字，以使两个数组的频率相等

> 原文：[https://www.geeksforgeeks.org/smallest-number-to-be-added-in-first-array-modulo-m-to-make-frequencies-of-both-arrays-equal/](https://www.geeksforgeeks.org/smallest-number-to-be-added-in-first-array-modulo-m-to-make-frequencies-of-both-arrays-equal/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`A[]`和`B[]`，它们由`N`个正整数和一个整数`M`组成， 任务是找到`X`的最小值，以便对数组`A[]`的每个元素执行`(A[i] + X) %M`导致形成一个元素频率与另一个给定数组`B[]`相同的数组。

**示例**：

> **输入**：`N = 4, M = 3, A[] = {0, 0, 2, 1}, B[] = {2, 0, 1, 1}`
>
> **输出**：1
>
> **说明**：
>
> 将给定数组`A[]`修改为`{(0 + 1) % 3, (0 + 1) % 3, (2 + 1) % 3, (1 + 1) % 3}`。
>
> `= {1 % 3, 1 % 3, 3 % 3, 2 % 3}`, 
>
> `= {1, 1, 0, 2}`, 相当于`B[]`就不同元素的频率而言。
> 
> **输入**：`N = 5, M = 10, A[] = {0, 0, 0, 1, 2}, B[] = {2, 1, 0, 0, 0}`
>
> **输出**：0
>
> **说明**：
>
> 两个数组中元素的频率已经相等。

**方法**：可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决此问题。 请按照以下步骤操作：

*   至少会有一个`X`的可能值，使得对于每个索引`i`，`(A[i] + X) % M = B[0]`。

*   查找将`A[]`的每个元素转换为`B[]`的第一个元素的`X`的所有可能值。

*   检查这些可能的`X`值是否满足`B[]`的其他剩余值。

*   如果有多个答案，则取`X`的最小值。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to find
// the answer
int moduloEquality(int A[], int B[],
                   int n, int m)
{

    // Stores the frequncies of
    // array elements
    map<int, int> mapA, mapB;

    for (int i = 0; i < n; i++) {
        mapA[A[i]]++;
        mapB[B[i]]++;
    }

    // Stores the possible values
    // of X
    set<int> possibleValues;

    int FirstElement = B[0];
    for (int i = 0; i < n; i++) {
        int cur = A[i];

        // Generate possible positive
        // values of X
        possibleValues
            .insert(
                cur > FirstElement
                    ? m - cur + FirstElement
                    : FirstElement - cur);
    }

    // Initialize answer
    // to MAX value
    int ans = INT_MAX;

    for (auto it :
         possibleValues) {

        // Flag to check if the
        // current element of the
        // set can be considered
        bool posible = true;

        for (auto it2 : mapA) {

            // If the frequency of an element
            // in A[] is not equal to that
            // in B[] after the operation
            if (it2.second
                != mapB[(it2.first + it) % m]) {

                // Current set element
                // cannot be considered
                posible = false;
                break;
            }
        }

        // Update minimum value of X
        if (posible) {
            ans = min(ans, it);
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int n = 4;
    int m = 3;

    int A[] = { 0, 0, 2, 1 };
    int B[] = { 2, 0, 1, 1 };

    cout << moduloEquality(A, B, n, m)
         << endl;

    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;

class GFG{

// Utility function to find
// the answer
static int moduloEquality(int A[], int B[],
                          int n, int m)
{

    // Stores the frequncies of
    // array elements
    HashMap<Integer,
            Integer> mapA = new HashMap<Integer,
                                        Integer>();
    HashMap<Integer,
            Integer> mapB = new HashMap<Integer,
                                        Integer>();

    for(int i = 0; i < n; i++)
    {
        if (mapA.containsKey(A[i]))
        {
            mapA.put(A[i], mapA.get(A[i]) + 1);
        }
        else
        {
            mapA.put(A[i], 1);
        }
        if (mapB.containsKey(B[i]))
        {
            mapB.put(B[i], mapB.get(B[i]) + 1);
        }
        else
        {
            mapB.put(B[i], 1);
        }
    }

    // Stores the possible values
    // of X
    HashSet<Integer> possibleValues = new HashSet<Integer>();

    int FirstElement = B[0];
    for(int i = 0; i < n; i++) 
    {
        int cur = A[i];

        // Generate possible positive
        // values of X
        possibleValues.add(cur > FirstElement ? 
                       m - cur + FirstElement :
                  FirstElement - cur);
    }

    // Initialize answer
    // to MAX value
    int ans = Integer.MAX_VALUE;

    for(int it : possibleValues)
    {

        // Flag to check if the
        // current element of the
        // set can be considered
        boolean posible = true;

        for(Map.Entry<Integer, 
                      Integer> it2 : mapA.entrySet())
        {

            // If the frequency of an element
            // in A[] is not equal to that
            // in B[] after the operation
            if (it2.getValue() != 
                mapB.get((it2.getKey() + it) % m)) 
            {

                // Current set element
                // cannot be considered
                posible = false;
                break;
            }
        }

        // Update minimum value of X
        if (posible)
        {
            ans = Math.min(ans, it);
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    int m = 3;

    int A[] = { 0, 0, 2, 1 };
    int B[] = { 2, 0, 1, 1 };

    System.out.print(moduloEquality(A, B, n, m) + "\n");
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program for the above approach
import sys
from collections import defaultdict

# Utility function to find
# the answer
def moduloEquality(A, B, n, m):

    # Stores the frequncies of
    # array elements
    mapA = defaultdict(int)
    mapB = defaultdict(int)

    for i in range(n):
        mapA[A[i]] += 1
        mapB[B[i]] += 1

    # Stores the possible values
    # of X
    possibleValues = set()

    FirstElement = B[0]
    for i in range(n):
        cur = A[i]

        # Generate possible positive
        # values of X
        if cur > FirstElement:
            possibleValues.add(m - cur + FirstElement)
        else:
            possibleValues.add(FirstElement - cur)

    # Initialize answer
    # to MAX value
    ans = sys.maxsize

    for it in possibleValues:

        # Flag to check if the
        # current element of the
        # set can be considered
        posible = True

        for it2 in mapA:

            # If the frequency of an element
            # in A[] is not equal to that
            # in B[] after the operation
            if (mapA[it2] !=
                mapB[(it2 + it) % m]):

                # Current set element
                # cannot be considered
                posible = False
                break

        # Update minimum value of X
        if (posible):
            ans = min(ans, it)

    return ans

# Driver Code
if __name__ == "__main__":

    n = 4
    m = 3

    A = [ 0, 0, 2, 1 ]
    B = [ 2, 0, 1, 1 ]

    print(moduloEquality(A, B, n, m))

# This code is contributed by chitranayal

```

## C#

```cs

// C# program for the above approach 
using System;
using System.Collections.Generic; 

class GFG{

// Utility function to find
// the answer
static int moduloEquality(int[] A, int[] B, 
                          int n, int m)
{

    // Stores the frequncies of
    // array elements
    Dictionary<int, 
               int> mapA = new Dictionary<int,
                                          int>();

    Dictionary<int, 
               int> mapB = new Dictionary<int,
                                          int>();

    for(int i = 0; i < n; i++)
    {
        if (mapA.ContainsKey(A[i]))
        {
            mapA[A[i]] = mapA[A[i]] + 1;
        }
        else
        {
            mapA.Add(A[i], 1);
        }
        if (mapB.ContainsKey(B[i]))
        {
            mapB[B[i]] = mapB[B[i]] + 1;
        }
        else
        {
            mapB.Add(B[i], 1);
        }
    }

    // Stores the possible values
    // of X
    HashSet<int> possibleValues = new HashSet<int>(); 

    int FirstElement = B[0];
    for(int i = 0; i < n; i++) 
    {
        int cur = A[i];

        // Generate possible positive
        // values of X
        possibleValues.Add(cur > FirstElement ? 
                       m - cur + FirstElement :
                  FirstElement - cur);
    }

    // Initialize answer
    // to MAX value
    int ans = Int32.MaxValue;

    foreach(int it in possibleValues)
    {

        // Flag to check if the
        // current element of the
        // set can be considered
        bool posible = true;

        foreach(KeyValuePair<int, int> it2 in mapA)
        {

            // If the frequency of an element
            // in A[] is not equal to that
            // in B[] after the operation
            if (it2.Value != mapB[(it2.Key + it) % m])
            {

                // Current set element
                // cannot be considered
                posible = false;
                break;
            }
        }

        // Update minimum value of X
        if (posible)
        {
            ans = Math.Min(ans, it);
        }
    }
    return ans;
} 

// Driver code
static void Main()
{
    int n = 4;
    int m = 3;

    int[] A = { 0, 0, 2, 1 };
    int[] B = { 2, 0, 1, 1 };

    Console.WriteLine(moduloEquality(A, B, n, m));
}
}

// This code is contributed by divyeshrabadiya07

```

**输出**： 

```
1

```

**时间复杂度**：`O(N ^ 2)`。

**辅助空间**：`O(n)`。



* * *

* * *



