# 查询查找最大和最小数组元素，不包括给定范围内的元素

> 原文:[https://www . geesforgeks . org/query-to-find-最大和最小数组元素-从给定范围中排除元素/](https://www.geeksforgeeks.org/queries-to-find-the-maximum-and-minimum-array-elements-excluding-elements-from-a-given-range/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个由形式为**【L，R】的查询组成的数组**Q【】【】**。**，每个查询的任务是找出数组中的最大和最小数组元素，不包括给定范围内的元素。

**示例:**

> **输入:** arr[] = {2，3，1，8，3，5，7，4}，Q[][] = {{4，6}，{0，4}，{3，7}，{2，5 } }
> T3】输出:T5】8 1
> 7 4
> 3 1
> 7 2
> T10】解释:
> T13】查询 1: max(arr[0，1，…，3]， 7]) = 4
> **查询 3:** 最大值(arr[0，1，…，2]) =3 和最小值(arr[0，1，…，2]) = 1
> **查询 4:** 最大值(arr[0，1]，arr[6，…，7]) =7 和最小值(arr[0，1]，arr[6，…，7]) = 2
> 
> **输入:** *arr[] = {3，2，1，4，5}，Q[][] = {{1，2}，{2，4}}*
> **输出:**
> *5 3*
> *3 2*

**天真方法:**解决问题最简单的方法是[遍历每个查询的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，找到存在于索引范围之外的最大和最小元素**【L，R】**。
***时间复杂度:*****O(N<sup>2</sup>)
***辅助空间:*** O(1)**

****高效方法:**通过将数组划分为子范围，将问题划分为子任务，找出从 **arr[0]** 到**arr[L–1]**以及从 **arr[r + 1]** 到**arr[N–1]**的最大值和最小值，分别存储在前缀和后缀数组中。现在通过比较前缀和后缀数组找到给定范围的最大值和最小值。
遵循以下步骤:**

*   **通过将当前索引处的值与前一个索引的最大值和最小值进行比较，遍历数组并保持 **2D 前缀数组**中每个索引遇到的**最大值**和**最小值**元素。**
*   **现在，[通过将当前索引处的值与下一个索引的最大值和最小值进行比较，遍历](https://www.geeksforgeeks.org/iterating-arrays-java/)[中的数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)反转并保持**最大值**和**最小值**在 **2D 后缀数组**中的索引值。**
*   **现在，对于每个查询，执行以下步骤:

    *   如果**L = 0****R = N–1**，则排除该范围后无元素残留。
    *   否则，如果 **L = 0** ，最大值和最小值将出现在**arr【R+1】**到**arr【N–1】**之间。
    *   否则，如果**R = N–1**，最大值和最小值将出现在**arr【0】**到**arr【L–1】**之间。
    *   否则，在**arr【0】**至**arr【L–1】**和**arr【R+1】**至**arr【N–1】**的范围内寻找最大值和最小值。
    *   打印此查询的最大值和最小值。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum and
// minimum array elements up to the i-th index
void prefixArr(int arr[], int prefix[][2], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++) {
        if (i == 0) {
            prefix[i][0] = arr[i];
            prefix[i][1] = arr[i];
        }

        else {

            // Compare current value with maximum
            // and minimum values up to previous index
            prefix[i][0] = max(prefix[i - 1][0], arr[i]);
            prefix[i][1] = min(prefix[i - 1][1], arr[i]);
        }
    }
}

// Function to find the maximum and
// minimum array elements from i-th index
void suffixArr(int arr[], int suffix[][2], int N)
{

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--) {

        if (i == N - 1) {
            suffix[i][0] = arr[i];
            suffix[i][1] = arr[i];
        }
        else {

            // Compare current value with maximum
            // and minimum values in the next index
            suffix[i][0] = max(suffix[i + 1][0], arr[i]);
            suffix[i][1] = min(suffix[i + 1][1], arr[i]);
        }
    }
}

// Function to find the maximum and
// minimum array elements for each query
void maxAndmin(int prefix[][2],
               int suffix[][2],
               int N, int L, int R)
{

    int maximum, minimum;

    // If no index remains after
    // excluding the elements
    // in a given range
    if (L == 0 && R == N - 1) {
        cout << "No maximum and minimum value" << endl;
        return;
    }

    // Find maximum and minimum from
    // from the range [R + 1, N - 1]
    else if (L == 0) {
        maximum = suffix[R + 1][0];
        minimum = suffix[R + 1][1];
    }

    // Find maximum and minimum from
    // from the range [0, N - 1]
    else if (R == N - 1) {
        maximum = prefix[L - 1][0];
        minimum = prefix[R - 1][1];
    }

    // Find maximum and minimum values from the
    // ranges [0, L - 1] and [R + 1, N - 1]
    else {
        maximum = max(prefix[L - 1][0],
                      suffix[R + 1][0]);
        minimum = min(prefix[L - 1][1],
                      suffix[R + 1][1]);
    }

    // Print the maximum and minimum value
    cout << maximum << " " << minimum << endl;
}

// Function to perform queries to find the
// minimum and maximum array elements excluding
// elements from a given range
void MinMaxQueries(int a[], int Q[][])
{

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Size of query array
    int q = sizeof(queries) / sizeof(queries[0]);

    // prefix[i][0]: Stores the maximum
    // prefix[i][1]: Stores the minimum value
    int prefix[N][2];

    // suffix[i][0]: Stores the maximum
    // suffix[i][1]: Stores the minimum value
    int suffix[N][2];

    // Function calls to store
    // maximum and minimum values
    // for respective ranges
    prefixArr(arr, prefix, N);
    suffixArr(arr, suffix, N);

    for (int i = 0; i < q; i++) {

        int L = queries[i][0];
        int R = queries[i][1];

        maxAndmin(prefix, suffix, N, L, R);
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 2, 3, 1, 8, 3, 5, 7, 4 };

    int queries[][2]
        = { { 4, 6 }, { 0, 4 }, { 3, 7 }, { 2, 5 } };

    MinMaxQueries(arr, Q);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
public class GFG
{

  // Function to find the maximum and
  // minimum array elements up to the i-th index
  static void prefixArr(int arr[], int prefix[][], int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
      if (i == 0)
      {
        prefix[i][0] = arr[i];
        prefix[i][1] = arr[i];
      }
      else
      {

        // Compare current value with maximum
        // and minimum values up to previous index
        prefix[i][0] = Math.max(prefix[i - 1][0], arr[i]);
        prefix[i][1] = Math.min(prefix[i - 1][1], arr[i]);
      }
    }
  }

  // Function to find the maximum and
  // minimum array elements from i-th index
  static void suffixArr(int arr[], int suffix[][], int N)
  {

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--)
    {
      if (i == N - 1)
      {
        suffix[i][0] = arr[i];
        suffix[i][1] = arr[i];
      }
      else
      {

        // Compare current value with maximum
        // and minimum values in the next index
        suffix[i][0] = Math.max(suffix[i + 1][0], arr[i]);
        suffix[i][1] = Math.min(suffix[i + 1][1], arr[i]);
      }
    }
  }

  // Function to find the maximum and
  // minimum array elements for each query
  static void maxAndmin(int prefix[][],
                        int suffix[][],
                        int N, int L, int R)
  {
    int maximum, minimum;

    // If no index remains after
    // excluding the elements
    // in a given range
    if (L == 0 && R == N - 1)
    {
      System.out.println("No maximum and minimum value");
      return;
    }

    // Find maximum and minimum from
    // from the range [R + 1, N - 1]
    else if (L == 0)
    {
      maximum = suffix[R + 1][0];
      minimum = suffix[R + 1][1];
    }

    // Find maximum and minimum from
    // from the range [0, N - 1]
    else if (R == N - 1)
    {
      maximum = prefix[L - 1][0];
      minimum = prefix[R - 1][1];
    }

    // Find maximum and minimum values from the
    // ranges [0, L - 1] and [R + 1, N - 1]
    else
    {
      maximum = Math.max(prefix[L - 1][0],
                         suffix[R + 1][0]);
      minimum = Math.min(prefix[L - 1][1],
                         suffix[R + 1][1]);
    }

    // Print the maximum and minimum value
    System.out.println(maximum + " " + minimum);
  }

  // Function to perform queries to find the
  // minimum and maximum array elements excluding
  // elements from a given range
  static void MinMaxQueries(int a[], int Q[][])
  {

    // Size of the array
    int N = a.length;

    // Size of query array
    int q = Q.length;

    // prefix[i][0]: Stores the maximum
    // prefix[i][1]: Stores the minimum value
    int prefix[][] = new int[N][2];

    // suffix[i][0]: Stores the maximum
    // suffix[i][1]: Stores the minimum value
    int suffix[][] = new int[N][2];

    // Function calls to store
    // maximum and minimum values
    // for respective ranges
    prefixArr(a, prefix, N);
    suffixArr(a, suffix, N);

    for (int i = 0; i < q; i++)
    {
      int L = Q[i][0];
      int R = Q[i][1];
      maxAndmin(prefix, suffix, N, L, R);
    }
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given array
    int arr[] = { 2, 3, 1, 8, 3, 5, 7, 4 };

    int queries[][]
      = { { 4, 6 }, { 0, 4 }, { 3, 7 }, { 2, 5 } };

    MinMaxQueries(arr, queries);
  }
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the maximum and
# minimum array elements up to the i-th index
def prefixArr(arr, prefix, N):

    # Traverse the array
    for i in range(N):
        if (i == 0):
            prefix[i][0] = arr[i]
            prefix[i][1] = arr[i]

        else:

            # Compare current value with maximum
            # and minimum values up to previous index
            prefix[i][0] = max(prefix[i - 1][0], arr[i])
            prefix[i][1] = min(prefix[i - 1][1], arr[i])
    return prefix

# Function to find the maximum and
# minimum array elements from i-th index
def suffixArr(arr, suffix, N):

    # Traverse the array in reverse
    for i in range(N - 1, -1, -1):

        if (i == N - 1):
            suffix[i][0] = arr[i]
            suffix[i][1] = arr[i]

        else:

            # Compare current value with maximum
            # and minimum values in the next index
            suffix[i][0] = max(suffix[i + 1][0], arr[i])
            suffix[i][1] = min(suffix[i + 1][1], arr[i])
    return suffix

# Function to find the maximum and
# minimum array elements for each query
def maxAndmin(prefix, suffix, N, L, R):
    maximum, minimum = 0, 0

    # If no index remains after
    # excluding the elements
    # in a given range
    if (L == 0 and R == N - 1):
        print("No maximum and minimum value")
        return

    # Find maximum and minimum from
    # from the range [R + 1, N - 1]
    elif (L == 0):
        maximum = suffix[R + 1][0]
        minimum = suffix[R + 1][1]

    # Find maximum and minimum from
    # from the range [0, N - 1]
    elif (R == N - 1):
        maximum = prefix[L - 1][0]
        minimum = prefix[R - 1][1]

    # Find maximum and minimum values from the
    # ranges [0, L - 1] and [R + 1, N - 1]
    else:
        maximum = max(prefix[L - 1][0], suffix[R + 1][0])
        minimum = min(prefix[L - 1][1], suffix[R + 1][1])

    # Print maximum and minimum value
    print(maximum, minimum)

# Function to perform queries to find the
# minimum and maximum array elements excluding
# elements from a given range
def MinMaxQueries(a, queries):

    # Size of the array
    N = len(arr)

    # Size of query array
    q = len(queries)

    # prefix[i][0]: Stores the maximum
    # prefix[i][1]: Stores the minimum value
    prefix = [ [ 0 for i in range(2)] for i in range(N)]

    # suffix[i][0]: Stores the maximum
    # suffix[i][1]: Stores the minimum value
    suffix = [ [ 0 for i in range(2)] for i in range(N)]

    # Function calls to store
    # maximum and minimum values
    # for respective ranges
    prefix = prefixArr(arr, prefix, N)
    suffix = suffixArr(arr, suffix, N)

    for i in range(q):
        L = queries[i][0]
        R = queries[i][1]

        maxAndmin(prefix, suffix, N, L, R)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 3, 1, 8, 3, 5, 7, 4 ]
    queries = [ [ 4, 6 ], [ 0, 4 ], [ 3, 7 ], [ 2, 5 ] ]
    MinMaxQueries(arr, queries)

    # This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the maximum and
  // minimum array elements up to the i-th index
  static void prefixArr(int[] arr, int[,] prefix, int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
      if (i == 0)
      {
        prefix[i, 0] = arr[i];
        prefix[i, 1] = arr[i];
      }
      else
      {

        // Compare current value with maximum
        // and minimum values up to previous index
        prefix[i, 0] = Math.Max(prefix[i - 1, 0], arr[i]);
        prefix[i, 1] = Math.Min(prefix[i - 1, 1], arr[i]);
      }
    }
  }

  // Function to find the maximum and
  // minimum array elements from i-th index
  static void suffixArr(int[] arr, int[,] suffix, int N)
  {

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--)
    {
      if (i == N - 1)
      {
        suffix[i, 0] = arr[i];
        suffix[i, 1] = arr[i];
      }
      else
      {

        // Compare current value with maximum
        // and minimum values in the next index
        suffix[i, 0] = Math.Max(suffix[i + 1, 0], arr[i]);
        suffix[i, 1] = Math.Min(suffix[i + 1, 1], arr[i]);
      }
    }
  }

  // Function to find the maximum and
  // minimum array elements for each query
  static void maxAndmin(int[,] prefix,
                        int[,] suffix,
                        int N, int L, int R)
  {
    int maximum, minimum;

    // If no index remains after
    // excluding the elements
    // in a given range
    if (L == 0 && R == N - 1)
    {
      Console.WriteLine("No maximum and minimum value");
      return;
    }

    // Find maximum and minimum from
    // from the range [R + 1, N - 1]
    else if (L == 0)
    {
      maximum = suffix[R + 1, 0];
      minimum = suffix[R + 1, 1];
    }

    // Find maximum and minimum from
    // from the range [0, N - 1]
    else if (R == N - 1)
    {
      maximum = prefix[L - 1, 0];
      minimum = prefix[R - 1, 1];
    }

    // Find maximum and minimum values from the
    // ranges [0, L - 1] and [R + 1, N - 1]
    else
    {
      maximum = Math.Max(prefix[L - 1, 0],
                         suffix[R + 1, 0]);
      minimum = Math.Min(prefix[L - 1, 1],
                         suffix[R + 1, 1]);
    }

    // Print the maximum and minimum value
    Console.WriteLine(maximum + " " + minimum);
  }

  // Function to perform queries to find the
  // minimum and maximum array elements excluding
  // elements from a given range
  static void MinMaxQueries(int[] a, int[,] Q)
  {

    // Size of the array
    int N = a.GetLength(0);

    // Size of query array
    int q = Q.GetLength(0);

    // prefix[i][0]: Stores the maximum
    // prefix[i][1]: Stores the minimum value
    int[,] prefix = new int[N, 2];

    // suffix[i][0]: Stores the maximum
    // suffix[i][1]: Stores the minimum value
    int[,] suffix = new int[N, 2];

    // Function calls to store
    // maximum and minimum values
    // for respective ranges
    prefixArr(a, prefix, N);
    suffixArr(a, suffix, N);

    for (int i = 0; i < q; i++)
    {
      int L = Q[i, 0];
      int R = Q[i, 1];
      maxAndmin(prefix, suffix, N, L, R);
    }
  }

  // Driver Code
  static public void Main ()
  {

    // Given array
    int[] arr = { 2, 3, 1, 8, 3, 5, 7, 4 };
    int[,] queries = { { 4, 6 }, { 0, 4 },
                      { 3, 7 }, { 2, 5 } };
    MinMaxQueries(arr, queries);
  }
}

// This code is contributed by sanjoy_62.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to find the maximum and
// minimum array elements up to the i-th index
function prefixArr(arr, prefix, N)
{

    // Traverse the array
    for (var i = 0; i < N; i++) {
        if (i == 0) {
            prefix[i][0] = arr[i];
            prefix[i][1] = arr[i];
        }

        else {

            // Compare current value with maximum
            // and minimum values up to previous index
            prefix[i][0] = Math.max(prefix[i - 1][0],
            arr[i]);
            prefix[i][1] = Math.min(prefix[i - 1][1],
            arr[i]);
        }
    }
}

// Function to find the maximum and
// minimum array elements from i-th index
function suffixArr(arr, suffix, N)
{

    // Traverse the array in reverse
    for (var i = N - 1; i >= 0; i--) {

        if (i == N - 1) {
            suffix[i][0] = arr[i];
            suffix[i][1] = arr[i];
        }
        else {

            // Compare current value with maximum
            // and minimum values in the next index
            suffix[i][0] = Math.max(suffix[i + 1][0],
            arr[i]);
            suffix[i][1] = Math.min(suffix[i + 1][1],
            arr[i]);
        }
    }
}

// Function to find the maximum and
// minimum array elements for each query
function maxAndmin(prefix, suffix, N, L, R)
{

    var maximum, minimum;

    // If no index remains after
    // excluding the elements
    // in a given range
    if (L == 0 && R == N - 1) {
        document.write( "No maximum and minimum value" +
        "<br>");
        return;
    }

    // Find maximum and minimum from
    // from the range [R + 1, N - 1]
    else if (L == 0) {
        maximum = suffix[R + 1][0];
        minimum = suffix[R + 1][1];
    }

    // Find maximum and minimum from
    // from the range [0, N - 1]
    else if (R == N - 1) {
        maximum = prefix[L - 1][0];
        minimum = prefix[R - 1][1];
    }

    // Find maximum and minimum values from the
    // ranges [0, L - 1] and [R + 1, N - 1]
    else {
        maximum = Math.max(prefix[L - 1][0],
                      suffix[R + 1][0]);
        minimum = Math.min(prefix[L - 1][1],
                      suffix[R + 1][1]);
    }

    // Print the maximum and minimum value
    document.write( maximum + " " + minimum + "<br>");
}

// Function to perform queries to find the
// minimum and maximum array elements excluding
// elements from a given range
function MinMaxQueries(a, Q)
{

    // Size of the array
    var N = arr.length;

    // Size of query array
    var q = queries.length;

    // prefix[i][0]: Stores the maximum
    // prefix[i][1]: Stores the minimum value
    var prefix = Array.from(Array(N), ()=> Array(2));

    // suffix[i][0]: Stores the maximum
    // suffix[i][1]: Stores the minimum value
    var suffix = Array.from(Array(N), ()=> Array(2));

    // Function calls to store
    // maximum and minimum values
    // for respective ranges
    prefixArr(arr, prefix, N);
    suffixArr(arr, suffix, N);

    for (var i = 0; i < q; i++) {

        var L = queries[i][0];
        var R = queries[i][1];

        maxAndmin(prefix, suffix, N, L, R);
    }
}

// Driver Code
// Given array
var arr = [2, 3, 1, 8, 3, 5, 7, 4 ];
var queries
    = [ [ 4, 6 ], [ 0, 4 ], [ 3, 7 ], [ 2, 5 ] ];
MinMaxQueries(arr, queries);

</script>
```

****Output:** 

```
8 1
7 4
3 1
7 2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**