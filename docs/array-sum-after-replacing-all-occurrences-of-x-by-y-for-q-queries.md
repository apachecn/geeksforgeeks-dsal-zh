# Q 查询用 Y 替换所有 X 后的数组和

> 原文:[https://www . geesforgeks . org/array-replace-sum-after-all-occurs-x-by-y-for-q-query/](https://www.geeksforgeeks.org/array-sum-after-replacing-all-occurrences-of-x-by-y-for-q-queries/)

给定整数数组 **arr[]** 和 **Q** 查询，任务是为以下类型的每个查询找到数组的[和:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   每个查询包含 2 个整数 **X** 和 **Y** ，其中**arr【】**中 **X** 的所有出现都将被 **Y** 替换。
*   每次查询后，他们打印数组的总和。

**示例:**

> **输入:** arr[] = { 1，2，1，3，2}，X[] = { 2，3，5 }，Y[] = { 3，1，2 }
> **输出:**11 5
> **解释:**
> 第一次查询后，将 2 替换为 3，arr[] = { 1，3，1，3，3 }，Sum = 11。
> 第二次查询后，将 3 替换为 1，arr[] = { 1，1，1，1，1 }，Sum = 5。
> 第三次查询后，将 5 替换为 2，arr[] = { 1，1，1，1 }，Sum = 5。
> 
> **输入:** arr[] = { 12，22，11，11，2}，X[] = {2，11，22}，Y[] = {12，222，2}
> **输出:** 68 490 470

**天真方法:**
解决上述问题最简单的方法是遍历数组，将每个查询的 **X** 的所有实例替换为 **Y** 并计算总和。

***时间复杂度:** O(N * Q)*

**高效方法:**
要优化上述方法，请遵循以下步骤:

*   将数组的和预先计算并存储在变量 **S** 中，将数组元素的频率存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **计数**中。
*   然后，对每个查询执行以下操作:
    *   找出地图上存储的 X 的频率。
    *   从 **S** 中减去 **X *计数【X】**。
    *   设置**计数【Y】=计数【X】**，然后**计数【X】= 0**。
    *   将**Y * count【Y】**加到 **S** 上。
    *   打印 **S** 的更新值。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the sum
// of the array for the given Q queries

#include <bits/stdc++.h>
using namespace std;

// Function that print the sum of
// the array for Q queries
void sumOfTheArrayForQuery(int* A, int N,
                           int* X, int* Y,
                           int Q)
{
    int sum = 0;

    // Stores the frequencies
    // of array elements
    unordered_map<int, int> count;

    // Calculate the sum of
    // the initial array and
    // store the frequency of
    // each element in map

    for (int i = 0; i < N; i++) {
        sum += A[i];
        count[A[i]]++;
    }

    // Iterate for all the queries

    for (int i = 0; i < Q; i++) {
        // Store query values
        int x = X[i], y = Y[i];

        // Decrement the sum accordingly
        sum -= count[X[i]] * X[i];

        // Increment the sum accordingly
        sum += count[X[i]] * Y[i];

        // Set count of Y[i]
        count[Y[i]] += count[X[i]];

        // Reset count of X[i]
        count[X[i]] = 0;

        // Print the sum
        cout << sum << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 3, 2 };
    int X[] = { 2, 3, 5 };
    int Y[] = { 3, 1, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    int Q = sizeof(X) / sizeof(X[0]);

    // Function call
    sumOfTheArrayForQuery(arr, N, X, Y, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find the sum of the array
// for the given Q queries
import java.util.*;
class GFG{

// Function that print the sum of
// the array for Q queries
public static void sumOfTheArrayForQuery(int[] A, int N,
                                         int[] X, int[] Y,
                                         int Q)
{
  int sum = 0;

  // Stores the frequencies
  // of array elements
  // Create an empty hash map
  HashMap<Integer,
          Integer> count = new HashMap<>();

  // Calculate the sum of
  // the initial array and
  // store the frequency of
  // each element in map
  for (int i = 0; i < N; i++)
  {
    sum += A[i];
    if (count.containsKey(A[i]))
    {
      count.replace(A[i],
      count.get(A[i]) + 1);
    }
    else
    {
      count.put(A[i], 1);
    }
  }

  // Iterate for all the queries
  for (int i = 0; i < Q; i++)
  {
    // Store query values
    int x = X[i], y = Y[i];

    if(count.containsKey(X[i]))
    {
      // Decrement the sum accordingly
      sum -= count.get(X[i]) * X[i];
      // Increment the sum accordingly
      sum += count.get(X[i]) * Y[i];
    }

    // Set count of Y[i]
    if(count.containsKey(Y[i]) &&
       count.containsKey(X[i]))
    {
      count.replace(Y[i],
      count.get(Y[i]) +
      count.get(X[i]));
    }

    // Reset count of X[i]
    if(count.containsKey(X[i]))
    {
      count.replace(X[i], 0);
    }

    // Print the sum
    System.out.print(sum + " ");
  }
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {1, 2, 1, 3, 2};
  int X[] = {2, 3, 5};
  int Y[] = {3, 1, 2};

  int N = arr.length;
  int Q = X.length;

  // Function call
  sumOfTheArrayForQuery(arr, N,
                        X, Y, Q);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to find the sum
# of the array for the given Q queries

# Function that print the sum of
# the array for Q queries
def sumOfTheArrayForQuery(A, N, X, Y, Q):

    sum = 0

    # Stores the frequencies
    # of array elements
    count = {}

    # Calculate the sum of
    # the initial array and
    # store the frequency of
    # each element in map
    for i in range(N):
        sum += A[i]

        if A[i] in count:
            count[A[i]] += 1
        else:
            count[A[i]] = 1

    # Iterate for all the queries
    for i in range(Q):

        # Store query values
        x = X[i]
        y = Y[i]

        if X[i] not in count:
            count[X[i]] = 0
        if Y[i] not in count:
            count[Y[i]] = 0

        # Decrement the sum accordingly
        sum -= (count[X[i]] * X[i])

        # Increment the sum accordingly
        sum += count[X[i]] * Y[i]

        # Set count of Y[i]
        count[Y[i]] += count[X[i]]

        # Reset count of X[i]
        count[X[i]] = 0

        # Print the sum
        print(sum, end = " ")

# Driver Code
arr = [ 1, 2, 1, 3, 2, ]
X = [ 2, 3, 5 ]
Y = [ 3, 1, 2 ]
N = len(arr)
Q = len(X)

# Function call
sumOfTheArrayForQuery(arr, N, X, Y, Q)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to
// find the sum of the array
// for the given Q queries
using System;
using System.Collections.Generic;
class GFG{

// Function that print the sum of
// the array for Q queries
public static void sumOfTheArrayForQuery(int[] A, int N,
                                         int[] X, int[] Y,
                                         int Q)
{
  int sum = 0;

  // Stores the frequencies
  // of array elements
  // Create an empty hash map
  Dictionary<int,
             int> count = new Dictionary<int,
                                         int>();

  // Calculate the sum of
  // the initial array and
  // store the frequency of
  // each element in map
  for (int i = 0; i < N; i++)
  {
    sum += A[i];
    if (count.ContainsKey(A[i]))
    {
      count[A[i]]= count[A[i]] + 1;
    }
    else
    {
      count.Add(A[i], 1);
    }
  }

  // Iterate for all the queries
  for (int i = 0; i < Q; i++)
  {
    // Store query values
    int x = X[i], y = Y[i];

    if(count.ContainsKey(X[i]))
    {
      // Decrement the sum accordingly
      sum -= count[X[i]] * X[i];
      // Increment the sum accordingly
      sum += count[X[i]] * Y[i];
    }

    // Set count of Y[i]
    if(count.ContainsKey(Y[i]) &&
       count.ContainsKey(X[i]))
    {
      count[Y[i]] = count[Y[i]] +
                    count[X[i]];
    }

    // Reset count of X[i]
    if(count.ContainsKey(X[i]))
    {
      count[X[i]] = 0;
    }

    // Print the sum
    Console.Write(sum + " ");
  }
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {1, 2, 1, 3, 2};
  int []X = {2, 3, 5};
  int []Y = {3, 1, 2};

  int N = arr.Length;
  int Q = X.Length;

  // Function call
  sumOfTheArrayForQuery(arr, N,
                        X, Y, Q);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the sum
// of the array for the given Q queries

// Function that print the sum of
// the array for Q queries
function sumOfTheArrayForQuery(A, N, X, Y, Q)
{
    var sum = 0;

    // Stores the frequencies
    // of array elements
    var count = new Map();

    // Calculate the sum of
    // the initial array and
    // store the frequency of
    // each element in map

    for (var i = 0; i < N; i++) {
        sum += A[i];
        if(count.has(A[i]))
            count.set(A[i], count.get(A[i])+1)
        else
            count.set(A[i], 1)
    }

    // Iterate for all the queries

    for (var i = 0; i < Q; i++) {
        // Store query values
        var x = X[i], y = Y[i];

        if(count.has(X[i]))
        {
            // Decrement the sum accordingly
            sum -= count.get(X[i]) * X[i];

                // Increment the sum accordingly
            sum += count.get(X[i]) * Y[i];
        }

        if(count.has(Y[i]))
        {
            // Set count of Y[i]
            count.set(Y[i], count.get(Y[i]) + count.get(X[i]));
        }

        // Reset count of X[i]
        count.set(X[i] , 0);

        // Print the sum
        document.write( sum + " ");
    }
}

// Driver Code
var arr = [1, 2, 1, 3, 2];
var X = [2, 3, 5 ];
var Y = [3, 1, 2 ];
var N = arr.length;
var Q = X.length;
// Function call
sumOfTheArrayForQuery(arr, N, X, Y, Q);

</script>
```

**Output:** 

```
11 5 5
```

***时间复杂度:** O(N)，因为每个查询都有一个* *计算复杂度为 O(1)。*
***辅助空间:** O(N)*