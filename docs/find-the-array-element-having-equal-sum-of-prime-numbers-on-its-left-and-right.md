# 找出左右素数和相等的数组元素

> 原文:[https://www . geeksforgeeks . org/find-the-array-element-with-equal-sum-of-the-the-array-element-with-the-the-the-the-array-element-the-element-with-the-it-it-it-it-it-it-it-it-it-it-it-](https://www.geeksforgeeks.org/find-the-array-element-having-equal-sum-of-prime-numbers-on-its-left-and-right/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是在给定数组中找到一个索引，其中出现在其左侧的[素数](https://www.geeksforgeeks.org/prime-numbers/)之和等于出现在其右侧的素数之和。

**示例:**

> **输入:** arr[] = {11，4，7，6，13，1，5}
> **输出:** 3
> **解释:**索引 3 左边素数之和= 11 + 7 = 18
> 索引 3 右边素数之和= 13 + 5 = 18
> 
> **输入:** arr[] = {5，2，1，7}
> **输出:** 2
> **解释:**索引 2 左边的素数之和= 5 + 2 = 7
> 索引 2 右边的素数之和= 7

**简单方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查范围**【0，N–1】**中每个索引的给定条件。如果发现任何索引的条件为真，则打印该索引的值。

***时间复杂度:** O(N <sup>2</sup> *√M)，其中 **M** 是数组中最大的* [*元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用厄拉多塞的[筛和](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)进行优化，将左右素数之和预先存储到数组元素中。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到数组中存在的[最大值。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   使用厄拉多塞的[筛找出小于或等于数组中最大值的素数。将这些元素存储在](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   初始化一个数组，比如 **first_array** 。遍历数组，将所有素数之和存储到第 i <sup>个</sup>索引处的 **first_array[i]** 。
*   初始化一个数组，比如**秒 _ 数组**。反向遍历数组，将所有元素的总和存储到第 i <sup>个</sup>索引处的**第二个 _ 数组【I】**。
*   遍历数组**第一个 _ 数组**和**第二个 _ 数组**，检查在任何索引处，它们的值是否相等。如果发现为真，则返回该索引。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find an index in the
// array having sum of prime numbers
// to its left and right equal
int find_index(int arr[], int N)
{
    // Stores the maximum value
    // present in the array
    int max_value = INT_MIN;

    for (int i = 0; i < N; i++) {
        max_value = max(max_value, arr[i]);
    }

    // Stores all positive
    // elements which are <= max_value
    map<int, int> store;

    for (int i = 1; i <= max_value; i++) {
        store[i]++;
    }

    // If 1 is present
    if (store.find(1) != store.end()) {

        // Remove 1
        store.erase(1);
    }

    // Sieve of Eratosthenes to
    // store all prime numbers which
    // are <= max_value in the Map
    for (int i = 2; i <= sqrt(max_value); i++) {

        int multiple = 2;

        // Erase non-prime numbers
        while ((i * multiple) <= max_value) {

            if (store.find(i * multiple) != store.end()) {
                store.erase(i * multiple);
            }

            multiple++;
        }
    }

    // Stores the sum of
    // prime numbers from left
    int prime_sum_from_left = 0;

    // Stores the sum of prime numbers
    // to the left of each index
    int first_array[N];

    for (int i = 0; i < N; i++) {

        // Stores the sum of prime numbers
        // to the left of the current index
        first_array[i] = prime_sum_from_left;

        if (store.find(arr[i]) != store.end()) {

            // Add current value to
            // the prime sum if the
            // current value is prime
            prime_sum_from_left += arr[i];
        }
    }

    // Stores the sum of
    // prime numbers from right
    int prime_sum_from_right = 0;

    // Stores the sum of prime numbers
    // to the right of each index
    int second_array[N];

    for (int i = N - 1; i >= 0; i--) {

        // Stores the sum of prime
        // numbers to the right of
        // the current index
        second_array[i] = prime_sum_from_right;

        if (store.find(arr[i]) != store.end()) {

            // Add current value to the
            // prime sum if the
            // current value is prime
            prime_sum_from_right += arr[i];
        }
    }

    // Traverse through the two
    // arrays to find the index
    for (int i = 0; i < N; i++) {

        // Compare the values present
        // at the current index
        if (first_array[i] == second_array[i]) {

            // Return the index where
            // both the values are same
            return i;
        }
    }

    // No index is found.
    return -1;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 11, 4, 7, 6, 13, 1, 5 };

    // Size of Array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << find_index(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find an index in the
// array having sum of prime numbers
// to its left and right equal
static int find_index(int arr[], int N)
{

    // Stores the maximum value
    // present in the array
    int max_value = Integer.MIN_VALUE;

    for(int i = 0; i < N; i++)
    {
        max_value = Math.max(max_value, arr[i]);
    }

    // Stores all positive
    // elements which are <= max_value
    Map<Integer, Integer> store= new HashMap<>();

    for(int i = 1; i <= max_value; i++)
    {
        store.put(i, store.getOrDefault(i, 0) + 1);
    }

    // If 1 is present
    if (store.containsKey(1))
    {

        // Remove 1
        store.remove(1);
    }

    // Sieve of Eratosthenes to
    // store all prime numbers which
    // are <= max_value in the Map
    for(int i = 2; i <= Math.sqrt(max_value); i++)
    {
        int multiple = 2;

        // Erase non-prime numbers
        while ((i * multiple) <= max_value)
        {
            if (store.containsKey(i * multiple))
            {
                store.remove(i * multiple);
            }
            multiple++;
        }
    }

    // Stores the sum of
    // prime numbers from left
    int prime_sum_from_left = 0;

    // Stores the sum of prime numbers
    // to the left of each index
    int[] first_array = new int[N];

    for(int i = 0; i < N; i++)
    {

        // Stores the sum of prime numbers
        // to the left of the current index
        first_array[i] = prime_sum_from_left;

        if (store.containsKey(arr[i]))
        {

            // Add current value to
            // the prime sum if the
            // current value is prime
            prime_sum_from_left += arr[i];
        }
    }

    // Stores the sum of
    // prime numbers from right
    int prime_sum_from_right = 0;

    // Stores the sum of prime numbers
    // to the right of each index
    int[] second_array= new int[N];

    for(int i = N - 1; i >= 0; i--)
    {

        // Stores the sum of prime
        // numbers to the right of
        // the current index
        second_array[i] = prime_sum_from_right;

        if (store.containsKey(arr[i]))
        {

            // Add current value to the
            // prime sum if the
            // current value is prime
            prime_sum_from_right += arr[i];
        }
    }

    // Traverse through the two
    // arrays to find the index
    for(int i = 0; i < N; i++)
    {

        // Compare the values present
        // at the current index
        if (first_array[i] == second_array[i])
        {

            // Return the index where
            // both the values are same
            return i;
        }
    }

    // No index is found.
    return -1;
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 11, 4, 7, 6, 13, 1, 5 };

    // Size of Array
    int N = arr.length;

    // Function Call
    System.out.println(find_index(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Function to find an index in the
# array having sum of prime numbers
# to its left and right equal
def find_index(arr, N):

    # Stores the maximum value
    # present in the array
    max_value = -10**9

    for i in range(N):
        max_value = max(max_value, arr[i])

    # Stores all positive
    # elements which are <= max_value
    store = {}

    for i in range(1, max_value + 1):
        store[i] = store.get(i, 0) + 1

    # If 1 is present
    if (1 in store):

        # Remove 1
        del store[1]

    # Sieve of Eratosthenes to
    # store all prime numbers which
    # are <= max_value in the Map
    for i in range(2, int(sqrt(max_value)) + 1):
        multiple = 2

        # Erase non-prime numbers
        while ((i * multiple) <= max_value):

            if (i * multiple in store):
                del store[i * multiple]

            multiple += 1

    # Stores the sum of
    # prime numbers from left
    prime_sum_from_left = 0

    # Stores the sum of prime numbers
    # to the left of each index
    first_array = [0]*N

    for i in range(N):

        # Stores the sum of prime numbers
        # to the left of the current index
        first_array[i] = prime_sum_from_left
        if arr[i] in store:

            # Add current value to
            # the prime sum if the
            # current value is prime
            prime_sum_from_left += arr[i]

    # Stores the sum of
    # prime numbers from right
    prime_sum_from_right = 0

    # Stores the sum of prime numbers
    # to the right of each index
    second_array = [0]*N

    for i in range(N - 1, -1, -1):

        # Stores the sum of prime
        # numbers to the right of
        # the current index
        second_array[i] = prime_sum_from_right

        if (arr[i] in store):
            # Add current value to the
            # prime sum if the
            # current value is prime
            prime_sum_from_right += arr[i]

    # Traverse through the two
    # arrays to find the index
    for i in range(N):

        # Compare the values present
        # at the current index
        if (first_array[i] == second_array[i]):

            # Return the index where
            # both the values are same
            return i

    # No index is found.
    return -1

# Driver Code
if __name__ == '__main__':
    # Given array arr[]
    arr= [11, 4, 7, 6, 13, 1, 5]

    # Size of Array
    N = len(arr)

    # Function Call
    print (find_index(arr, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find an index in the
// array having sum of prime numbers
// to its left and right equal
static int find_index(int[] arr, int N)
{

    // Stores the maximum value
    // present in the array
    int max_value = Int32.MinValue;

    for(int i = 0; i < N; i++)
    {
        max_value = Math.Max(max_value, arr[i]);
    }

    // Stores all positive
    // elements which are <= max_value
    Dictionary<int,
               int> store = new Dictionary<int,
                                          int>();

    for(int i = 1; i <= max_value; i++)
    {
        if (!store.ContainsKey(i))
            store[i] = 0;

        store[i]++;
    }

    // If 1 is present
    if (store.ContainsKey(1))
    {

        // Remove 1
        store.Remove(1);
    }

    // Sieve of Eratosthenes to
    // store all prime numbers which
    // are <= max_value in the Map
    for(int i = 2; i <= Math.Sqrt(max_value); i++)
    {
        int multiple = 2;

        // Erase non-prime numbers
        while ((i * multiple) <= max_value)
        {
            if (store.ContainsKey(i * multiple))
            {
                store.Remove(i * multiple);
            }
            multiple++;
        }
    }

    // Stores the sum of
    // prime numbers from left
    int prime_sum_from_left = 0;

    // Stores the sum of prime numbers
    // to the left of each index
    int[] first_array = new int[N];

    for(int i = 0; i < N; i++)
    {

        // Stores the sum of prime numbers
        // to the left of the current index
        first_array[i] = prime_sum_from_left;

        if (store.ContainsKey(arr[i]))
        {

            // Add current value to
            // the prime sum if the
            // current value is prime
            prime_sum_from_left += arr[i];
        }
    }

    // Stores the sum of
    // prime numbers from right
    int prime_sum_from_right = 0;

    // Stores the sum of prime numbers
    // to the right of each index
    int[] second_array = new int[N];

    for(int i = N - 1; i >= 0; i--)
    {

        // Stores the sum of prime
        // numbers to the right of
        // the current index
        second_array[i] = prime_sum_from_right;

        if (store.ContainsKey(arr[i]))
        {

            // Add current value to the
            // prime sum if the
            // current value is prime
            prime_sum_from_right += arr[i];
        }
    }

    // Traverse through the two
    // arrays to find the index
    for(int i = 0; i < N; i++)
    {

        // Compare the values present
        // at the current index
        if (first_array[i] == second_array[i])
        {

            // Return the index where
            // both the values are same
            return i;
        }
    }

    // No index is found.
    return -1;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 11, 4, 7, 6, 13, 1, 5 };

    // Size of Array
    int N = arr.Length;

    // Function Call
    Console.WriteLine(find_index(arr, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Function to find an index in the
// array having sum of prime numbers
// to its left and right equal
    function find_index(arr,N)
    {
        // Stores the maximum value
    // present in the array
    let max_value = Number.MIN_VALUE;

    for (let i = 0; i < N; i++) {
        max_value = Math.max(max_value, arr[i]);
    }

    // Stores all positive
    // elements which are <= max_value
    let store=new Map();

    for (let i = 1; i <= max_value; i++) {
        if(!store.has(i))
            store.set(i,0);
        store.set(i,store.get(i)+1);
    }

    // If 1 is present
    if (store.has(1)) {

        // Remove 1
        store.delete(1);
    }

    // Sieve of Eratosthenes to
    // store all prime numbers which
    // are <= max_value in the Map
    for (let i = 2; i <= Math.sqrt(max_value); i++) {

        let multiple = 2;

        // Erase non-prime numbers
        while ((i * multiple) <= max_value) {

            if (store.has(i * multiple)) {
                store.delete(i * multiple);
            }

            multiple++;
        }
    }

    // Stores the sum of
    // prime numbers from left
    let prime_sum_from_left = 0;

    // Stores the sum of prime numbers
    // to the left of each index
    let first_array=new Array(N);

    for (let i = 0; i < N; i++) {

        // Stores the sum of prime numbers
        // to the left of the current index
        first_array[i] = prime_sum_from_left;

        if (store.has(arr[i])) {

            // Add current value to
            // the prime sum if the
            // current value is prime
            prime_sum_from_left += arr[i];
        }
    }

    // Stores the sum of
    // prime numbers from right
    let prime_sum_from_right = 0;

    // Stores the sum of prime numbers
    // to the right of each index
    let second_array=new Array(N);

    for (let i = N - 1; i >= 0; i--) {

        // Stores the sum of prime
        // numbers to the right of
        // the current index
        second_array[i] = prime_sum_from_right;

        if (store.has(arr[i]) ) {

            // Add current value to the
            // prime sum if the
            // current value is prime
            prime_sum_from_right += arr[i];
        }
    }

    // Traverse through the two
    // arrays to find the index
    for (let i = 0; i < N; i++) {

        // Compare the values present
        // at the current index
        if (first_array[i] == second_array[i]) {

            // Return the index where
            // both the values are same
            return i;
        }
    }

    // No index is found.
    return -1;
    }

    // Driver Code

    // Given array arr[]
    let arr=[11, 4, 7, 6, 13, 1, 5];

    // Size of Array
    let N=arr.length;

    // Function Call
    document.write(find_index(arr, N));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N+max(arr[])log log log log(max(arr[])*
***辅助空间:** O(max(arr[]) + N)*