# 找到左右素数个数相等的数组元素

> 原文:[https://www . geesforgeks . org/find-the-array-element-with-count-of-the-the-the-array-element-with-count-of-the-of-the-the-the-the-array-element-with-it-the-the-it-the-it-the-it-the-it-it-](https://www.geeksforgeeks.org/find-the-array-element-having-equal-count-of-prime-numbers-on-its-left-and-right/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从数组中找到一个索引，该索引的左右素数[个数相等。](https://www.geeksforgeeks.org/count-primes-ranges/)

**示例:**

> **输入:** arr[] = {2，3，4，7，5，10，1，8}
> **输出:** 2
> **解释:**
> 考虑索引 2，那么它左边的素数是{2，3}，它右边的素数是{7，5}。
> As，左右索引的素数个数为 2，相等。因此，打印 2。
> 
> **输入:** arr[] = {8，10，2，7，3 }
> T3】输出: 3

**天真法:**解决给定问题最简单的方法是通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)来计算每个数组元素左右的[素数](https://www.geeksforgeeks.org/prime-numbers/)，并打印素数计数相等的索引。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用厄拉多塞的[筛和](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来优化，以将左右素数预先存储到数组元素中。按照以下步骤解决问题:

*   首先，[找到数组的最大值](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)**arr【】**并将其存储在一个变量中，比如 **maxValue** 。
*   初始化一个[图< int，int >](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ，说 **St** ，把所有[质数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)都存储在里面。
*   迭代范围**【2，最大值】**，推送 **St** 中的所有值。
*   迭代范围**【2，最大值】**并执行以下操作:
    *   将变量 **j** 初始化为 **1** ，当 **i*j** 小于或等于**最大值**时迭代。
    *   在上述步骤的每次迭代中，从 **St** 中移除 **i*j** ，并将 **j** 增加 **1** 。
*   初始化两个变量，比如**左计数**和**右计数**，分别存储前缀数组和后缀数组中质数的计数。
*   初始化两个数组，比如**前缀[]** 和**后缀[]** ，存储数组 **arr[]** 素数个数的前缀和数组和后缀和数组。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下操作:
    *   将**左计数**分配给**前缀【I】**。
    *   如果 **St** 中存在**arr【I】**的值，则将 **LeftCount** 的值增加 **1** 。
*   反向迭代范围**【0，N-1】**，并执行以下操作:
    *   将**右计数**分配给**后缀【I】**。
    *   如果 **St** 中存在**arr【I】**，则将 **RightCount** 的值增加 **1** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，如果**前缀【I】**的值等于**后缀【I】**的值，则打印索引 **i** 作为答案，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果上述情况都不满足，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the index of the
// array such that the count of prime
// numbers to its either ends are same
int findIndex(int arr[], int N)
{
    // Store the maximum value in
    // the array
    int maxValue = INT_MIN;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        maxValue = max(maxValue, arr[i]);
    }

    // Stores all the numbers
    map<int, int> St;

    // Iterate over the range [1, Max]
    for (int i = 1; i <= maxValue; i++) {

        // Increment the value of st[i]
        St[i]++;
    }

    // Removes 1 from the map St
    if (St.find(1) != St.end()) {
        St.erase(1);
    }

    // Perform Sieve of Prime Numbers
    for (int i = 2;
         i <= sqrt(maxValue); i++) {
        int j = 2;

        // While i*j is less than
        // the maxValue
        while ((i * j) <= maxValue) {

            // If i*j is in map St
            if (St.find(i * j)
                != St.end()) {

                // Erase the value (i * j)
                St.erase(i * j);
            }

            // Increment the value of j
            j++;
        }
    }

    // Stores the count of prime from
    // index 0 to i
    int LeftCount = 0;

    // Stores the count of prime numbers
    int Prefix[N];

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        Prefix[i] = LeftCount;

        // If arr[i] is present in the
        // map st
        if (St.find(arr[i])
            != St.end()) {
            LeftCount++;
        }
    }

    // Stores the count of prime from
    // index i to N-1
    int RightCount = 0;

    // Stores the count of prime numbers
    int Suffix[N];

    // Iterate over the range [0, N-1]
    // in reverse order
    for (int i = N - 1; i >= 0; i--) {

        Suffix[i] = RightCount;

        // If arr[i] is in map st
        if (St.find(arr[i])
            != St.end()) {
            RightCount++;
        }
    }

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {

        // If prefix[i] is equal
        // to the Suffix[i]
        if (Prefix[i] == Suffix[i]) {
            return i;
        }
    }

    // Return -1 if no such index
    // is present
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 7, 5, 10, 1, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findIndex(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;

public class GFG
{

    // Function to find the index of the
    // array such that the count of prime
    // numbers to its either ends are same
    static int findIndex(int arr[], int N)
    {

        // Store the maximum value in
        // the array
        int maxValue = Integer.MIN_VALUE;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++)
        {
            maxValue = Math.max(maxValue, arr[i]);
        }

        // Stores all the numbers
        HashMap<Integer, Integer> St = new HashMap<>();

        // Iterate over the range [1, Max]
        for (int i = 1; i <= maxValue; i++) {

            // Increment the value of st[i]
            St.put(i, St.getOrDefault(i, 0) + 1);
        }

        // Removes 1 from the map St
        if (St.containsKey(1)) {
            St.remove(1);
        }

        // Perform Sieve of Prime Numbers
        for (int i = 2; i <= Math.sqrt(maxValue); i++) {
            int j = 2;

            // While i*j is less than
            // the maxValue
            while ((i * j) <= maxValue) {

                // If i*j is in map St
                if (St.containsKey(i * j)) {

                    // Erase the value (i * j)
                    St.remove(i * j);
                }

                // Increment the value of j
                j++;
            }
        }

        // Stores the count of prime from
        // index 0 to i
        int LeftCount = 0;

        // Stores the count of prime numbers
        int Prefix[] = new int[N];

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            Prefix[i] = LeftCount;

            // If arr[i] is present in the
            // map st
            if (St.containsKey(arr[i])) {
                LeftCount++;
            }
        }

        // Stores the count of prime from
        // index i to N-1
        int RightCount = 0;

        // Stores the count of prime numbers
        int Suffix[] = new int[N];

        // Iterate over the range [0, N-1]
        // in reverse order
        for (int i = N - 1; i >= 0; i--) {

            Suffix[i] = RightCount;

            // If arr[i] is in map st
            if (St.containsKey(arr[i])) {
                RightCount++;
            }
        }

        // Iterate over the range [0, N-1]
        for (int i = 0; i < N; i++) {

            // If prefix[i] is equal
            // to the Suffix[i]
            if (Prefix[i] == Suffix[i]) {
                return i;
            }
        }

        // Return -1 if no such index
        // is present
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 7, 5, 10, 1, 8 };
        int N = arr.length;
        System.out.println(findIndex(arr, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict
import sys
import math

# Function to find the index of the
# array such that the count of prime
# numbers to its either ends are same

def findIndex(arr, N):

    # Store the maximum value in
    # the array
    maxValue = -sys.maxsize - 1

    # Traverse the array arr[]
    for i in range(N):
        maxValue = max(maxValue, arr[i])

    # / Stores all the numbers
    St = defaultdict(int)

    # Iterate over the range [1, Max]
    for i in range(1, maxValue + 1):

        # Increment the value of st[i]
        St[i] += 1

    # Removes 1 from the map St
    if (1 in St):
        St.pop(1)

    # Perform Sieve of Prime Numbers
    for i in range(2, int(math.sqrt(maxValue)) + 1):
        j = 2

        # While i*j is less than
        # the maxValue
        while ((i * j) <= maxValue):

            # If i*j is in map St
            if (i * j) in St:

                # Erase the value (i * j)
                St.pop(i * j)

            # Increment the value of j
            j += 1

    # Stores the count of prime from
    # index 0 to i
    LeftCount = 0

    # Stores the count of prime numbers
    Prefix = [0] * N

    # Traverse the array arr[]
    for i in range(N):

        Prefix[i] = LeftCount

        # If arr[i] is present in the
        # map st
        if (arr[i] in St):
            LeftCount += 1

    # Stores the count of prime from
    # index i to N-1
    RightCount = 0

    # Stores the count of prime numbers
    Suffix = [0] * N

    # Iterate over the range [0, N-1]
    # in reverse order
    for i in range(N - 1, -1, -1):

        Suffix[i] = RightCount

        # If arr[i] is in map st
        if arr[i] in St:
            RightCount += 1

    # Iterate over the range [0, N-1]
    for i in range(N):

        # If prefix[i] is equal
        # to the Suffix[i]
        if (Prefix[i] == Suffix[i]):
            return i

    # Return -1 if no such index
    # is present
    return -1

# Driver Code
if __name__ == "__main__":

    arr = [2, 3, 4, 7, 5, 10, 1, 8]
    N = len(arr)
    print(findIndex(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

      // Function to find the index of the
    // array such that the count of prime
    // numbers to its either ends are same
    static int findIndex(int[] arr, int N)
    {

        // Store the maximum value in
        // the array
        int maxValue = Int32.MinValue;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++)
        {
            maxValue = Math.Max(maxValue, arr[i]);
        }

        // Stores all the numbers
        Dictionary<int,int> St = new Dictionary<int,int>();

        // Iterate over the range [1, Max]
        for (int i = 1; i <= maxValue; i++) {

            // Increment the value of st[i]
            St.Add(i, 1);
        }

        // Removes 1 from the map St
        if (St.ContainsKey(1)) {
            St.Remove(1);
        }

        // Perform Sieve of Prime Numbers
        for (int i = 2; i <= Math.Sqrt(maxValue); i++) {
            int j = 2;

            // While i*j is less than
            // the maxValue
            while ((i * j) <= maxValue) {

                // If i*j is in map St
                if (St.ContainsKey(i * j)) {

                    // Erase the value (i * j)
                    St.Remove(i * j);
                }

                // Increment the value of j
                j++;
            }
        }

        // Stores the count of prime from
        // index 0 to i
        int LeftCount = 0;

        // Stores the count of prime numbers
        int[] Prefix = new int[N];

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            Prefix[i] = LeftCount;

            // If arr[i] is present in the
            // map st
            if (St.ContainsKey(arr[i])) {
                LeftCount++;
            }
        }

        // Stores the count of prime from
        // index i to N-1
        int RightCount = 0;

        // Stores the count of prime numbers
        int[] Suffix = new int[N];

        // Iterate over the range [0, N-1]
        // in reverse order
        for (int i = N - 1; i >= 0; i--) {

            Suffix[i] = RightCount;

            // If arr[i] is in map st
            if (St.ContainsKey(arr[i])) {
                RightCount++;
            }
        }

        // Iterate over the range [0, N-1]
        for (int i = 0; i < N; i++) {

            // If prefix[i] is equal
            // to the Suffix[i]
            if (Prefix[i] == Suffix[i]) {
                return i;
            }
        }

        // Return -1 if no such index
        // is present
        return -1;
    }

    // Driver code
    static public void Main (){

        int[] arr = { 2, 3, 4, 7, 5, 10, 1, 8 };
        int N = arr.Length;
        Console.WriteLine(findIndex(arr, N));
    }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program to count frequencies of array items

// Function to find the index of the
// array such that the count of prime
// numbers to its either ends are same
function findIndex( arr,  N)
    {

        // Store the maximum value in
        // the array
        let maxValue = Number.MIN_VALUE;
;

        // Traverse the array arr[]
        for (let i = 0; i < N; i++)
        {
            maxValue = Math.max(maxValue, arr[i]);
        }

        // Stores all the numbers
        var St = new Map();

        // Iterate over the range [1, Max]
        for (let i = 1; i <= maxValue; i++) {

            // Increment the value of st[i]
            St.set(i, 1);
        }

        // Removes 1 from the map St
        if (St.has(1)) {
            St.delete(1);
        }

        // Perform Sieve of Prime Numbers
        for (let i = 2; i <= Math.sqrt(maxValue); i++) {
            let j = 2;

            // While i*j is less than
            // the maxValue
            while ((i * j) <= maxValue) {

                // If i*j is in map St
                if (St.has(i * j)) {

                    // Erase the value (i * j)
                    St.delete(i * j);
                }

                // Increment the value of j
                j++;
            }
        }

        // Stores the count of prime from
        // index 0 to i
        let LeftCount = 0;

        // Stores the count of prime numbers
        let Prefix = new Array(N);

        // Traverse the array arr[]
        for (let i = 0; i < N; i++) {

            Prefix[i] = LeftCount;

            // If arr[i] is present in the
            // map st
            if (St.has(arr[i])) {
                LeftCount++;
            }
        }

        // Stores the count of prime from
        // index i to N-1
        let RightCount = 0;

        // Stores the count of prime numbers
        let Suffix = new Array(N);

        // Iterate over the range [0, N-1]
        // in reverse order
        for (let i = N - 1; i >= 0; i--) {

            Suffix[i] = RightCount;

            // If arr[i] is in map st
            if (St.has(arr[i])) {
                RightCount++;
            }
        }

        // Iterate over the range [0, N-1]
        for (let i = 0; i < N; i++) {

            // If prefix[i] is equal
            // to the Suffix[i]
            if (Prefix[i] == Suffix[i]) {
                return i;
            }
        }

        // Return -1 if no such index
        // is present
        return -1;
    }

// Driver Code
let arr = [ 2, 3, 4, 7, 5, 10, 1, 8 ];
let N = arr.length;
document.write(findIndex(arr, N));

// This code is contributed by jana_sayantan.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*