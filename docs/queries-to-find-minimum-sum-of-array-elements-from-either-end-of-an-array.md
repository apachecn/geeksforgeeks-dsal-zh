# 查询从数组的任一端找到数组元素的最小和

> 原文:[https://www . geeksforgeeks . org/query-to-find-最小数组元素和-从任意一个数组末尾/](https://www.geeksforgeeks.org/queries-to-find-minimum-sum-of-array-elements-from-either-end-of-an-array/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由 **Q** 个查询组成的数组**查询【】**，每个查询的任务是在数组中找到**个查询【I】**，并计算从数组开始和结束到**个查询【I】**的数组元素之和的最小值。

**示例:**

> **输入:** arr[] = {2，3，6，7，4，5，30}，Q = 2，查询[] = {6，5}
> **输出:** 11 27
> **解释:**
> 查询 1:从开始的总和= 2 + 3 + 6 = 11。结束时的总和= 30 + 5 + 4 + 7 + 6 = 52。因此，11 是必需的答案。
> 查询 2:从开始的总和= 27。结束时的总和= 35。因此，27 是必需的答案。
> 
> **输入:** arr[] = {1，2，-3，4}，Q = 2，查询[] = {4，2}
> **输出:** 4 2

**简单方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)直到每个查询的**查询【I】**，并从数组的末尾和开始计算总和。最后，打印所得总和的最小值。

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// sum from either end of the arrays
// for the given queries
void calculateQuery(int arr[], int N,
                    int query[], int M)
{
    // Traverse the query[] array
    for (int i = 0; i < M; i++) {
        int X = query[i];

        // Stores sum from start
        // and end of the array
        int sum_start = 0, sum_end = 0;

        // Calculate distance from start
        for (int j = 0; j < N; j++) {

            sum_start += arr[j];
            if (arr[j] == X)
                break;
        }

        // Calculate distance from end
        for (int j = N - 1; j >= 0; j--) {

            sum_end += arr[j];
            if (arr[j] == X)
                break;
        }

        cout << min(sum_end, sum_start) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 6, 7, 4, 5, 30 };
    int queries[] = { 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(queries)
            / sizeof(queries[0]);

    calculateQuery(arr, N, queries, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
import java.lang.*;

public class GFG
{

  // Function to calculate the minimum
  // sum from either end of the arrays
  // for the given queries
  static void calculateQuery(int arr[], int N,
                             int query[], int M)
  {

    // Traverse the query[] array
    for (int i = 0; i < M; i++)
    {
      int X = query[i];

      // Stores sum from start
      // and end of the array
      int sum_start = 0, sum_end = 0;

      // Calculate distance from start
      for (int j = 0; j < N; j++)
      {
        sum_start += arr[j];
        if (arr[j] == X)
          break;
      }

      // Calculate distance from end
      for (int j = N - 1; j >= 0; j--)
      {
        sum_end += arr[j];
        if (arr[j] == X)
          break;
      }
      System.out.print(Math.min(sum_end, sum_start) + " ");
    }
  }

  // Driver Code
  public static void main (String[] args)
  {
    int arr[] = { 2, 3, 6, 7, 4, 5, 30 };
    int queries[] = { 6, 5 };
    int N = arr.length;
    int M = queries.length;
    calculateQuery(arr, N, queries, M);
  }
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python 3 implementation
# of the above approach

# Function to calculate the minimum
# sum from either end of the arrays
# for the given queries

def calculateQuery(arr, N, query, M):

    # Traverse the query[] array
    for i in range(M):
        X = query[i]

        # Stores sum from start
        # and end of the array
        sum_start = 0
        sum_end = 0

        # Calculate distance from start
        for j in range(N):

            sum_start += arr[j]
            if (arr[j] == X):
                break

        # Calculate distance from end
        for j in range(N - 1, -1, -1):

            sum_end += arr[j]
            if (arr[j] == X):
                break
        print(min(sum_end, sum_start), end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [2, 3, 6, 7, 4, 5, 30]
    queries = [6, 5]
    N = len(arr)
    M = len(queries)

    calculateQuery(arr, N, queries, M)

    # This code is contributed by chitranayal.
```

## C#

```
// C# implementation
// of the above approach
using System;
class GFG {

  // Function to calculate the minimum
  // sum from either end of the arrays
  // for the given queries
  static void calculateQuery(int[] arr, int N,
                             int[] query, int M)
  {

    // Traverse the query[] array
    for (int i = 0; i < M; i++) {
      int X = query[i];

      // Stores sum from start
      // and end of the array
      int sum_start = 0, sum_end = 0;

      // Calculate distance from start
      for (int j = 0; j < N; j++) {

        sum_start += arr[j];
        if (arr[j] == X)
          break;
      }

      // Calculate distance from end
      for (int j = N - 1; j >= 0; j--) {

        sum_end += arr[j];
        if (arr[j] == X)
          break;
      }

      Console.Write(Math.Min(sum_end, sum_start) + " ");
    }
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 2, 3, 6, 7, 4, 5, 30 };
    int[] queries = { 6, 5 };
    int N = arr.Length;
    int M = queries.Length;

    calculateQuery(arr, N, queries, M);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to calculate the minimum
// sum from either end of the arrays
// for the given queries
function calculateQuery(arr, N, query, M)
{

    // Traverse the query[] array
    for(let i = 0; i < M; i++)
    {
        let X = query[i];

        // Stores sum from start
        // and end of the array
        let sum_start = 0, sum_end = 0;

        // Calculate distance from start
        for(let j = 0; j < N; j++)
        {
            sum_start += arr[j];

            if (arr[j] == X)
                break;
        }

        // Calculate distance from end
        for(let j = N - 1; j >= 0; j--)
        {
            sum_end += arr[j];

            if (arr[j] == X)
                break;
        }
        document.write(Math.min(
            sum_end, sum_start) + " ");
    }
}

// Driver code
let arr = [ 2, 3, 6, 7, 4, 5, 30 ];
let queries = [ 6, 5 ];
let N = arr.length;
let M = queries.length;

calculateQuery(arr, N, queries, M);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
11 27
```

***时间复杂度:** O(Q * N)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用额外空间和[前缀和与后缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念进行优化，并以恒定的计算复杂度回答每个查询。其思想是对每个索引的前缀和后缀总和进行预处理。按照以下步骤解决问题:

*   初始化两个变量，说**前缀**和**后缀**。
*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)，比如说 **mp，**将数组元素作为**键**映射成对，其中第一个值给出前缀和，第二个值给出后缀和。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并继续添加**arr【I】**为前缀，[以**arr【I】**为键，**前缀**为值存储在地图](https://www.geeksforgeeks.org/inserting-elements-in-stdmap-insert-emplace-and-operator/)中。
*   [反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并不断添加**arr【I】**为后缀，以**arr【I】**为键，以**后缀**为值存储在地图中。
*   现在[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **查询[]** ，对于每个查询**查询【I】**，打印 **mp【查询[i]】的最小值。首先**和**MP[查询[i]]。第二**作为结果。

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum
// for the given queries
void calculateQuery(int arr[], int N,
                    int query[], int M)
{

    // Stores prefix and suffix sums
    int prefix = 0, suffix = 0;

    // Stores pairs of prefix and suffix sums
    unordered_map<int, pair<int, int> > mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Add element to prefix
        prefix += arr[i];

        // Store prefix for each element
        mp[arr[i]].first = prefix;
    }

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--) {

        // Add element to suffix
        suffix += arr[i];

        // Storing suffix for each element
        mp[arr[i]].second = suffix;
    }

    // Traverse the array queries[]
    for (int i = 0; i < M; i++) {

        int X = query[i];

        // Minimum of suffix
        // and prefix sums
        cout << min(mp[X].first,
                    mp[X].second)
             << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 6, 7, 4, 5, 30 };
    int queries[] = { 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(queries) / sizeof(queries[0]);

    calculateQuery(arr, N, queries, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of the above approach
import java.util.*;

class GFG
{
  static class pair<E,P>
  {
    E first;
    P second;
    public pair(E first, P second) 
    {
      this.first = first;
      this.second = second;
    }   
  }

  // Function to find the minimum sum
  // for the given queries
  @SuppressWarnings({ "unchecked", "rawtypes" })
  static void calculateQuery(int arr[], int N,
                             int query[], int M)
  {

    // Stores prefix and suffix sums
    int prefix = 0, suffix = 0;

    // Stores pairs of prefix and suffix sums
    HashMap<Integer, pair > mp = new HashMap<>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Add element to prefix
      prefix += arr[i];

      // Store prefix for each element
      mp.put(arr[i], new pair(prefix,0));
    }

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--) {

      // Add element to suffix
      suffix += arr[i];

      // Storing suffix for each element
      mp.put(arr[i], new pair(mp.get(arr[i]).first,suffix));
    }

    // Traverse the array queries[]
    for (int i = 0; i < M; i++) {

      int X = query[i];

      // Minimum of suffix
      // and prefix sums
      System.out.print(Math.min((int)mp.get(X).first,
                                (int)mp.get(X).second)
                       + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 2, 3, 6, 7, 4, 5, 30 };
    int queries[] = { 6, 5 };
    int N = arr.length;
    int M = queries.length;

    calculateQuery(arr, N, queries, M);

  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation
# of the above approach

# Function to find the minimum sum
# for the given queries
def calculateQuery(arr, N, query, M):

    # Stores prefix and suffix sums
    prefix = 0
    suffix = 0

    # Stores pairs of prefix and suffix sums
    mp = {}

    # Traverse the array
    for i in range(N):

        # Add element to prefix
        prefix += arr[i]

        # Store prefix for each element
        mp[arr[i]] = [prefix, 0]

    # Traverse the array in reverse
    for i in range(N - 1, -1, -1):

        # Add element to suffix
        suffix += arr[i]

        # Storing suffix for each element
        mp[arr[i]] = [mp[arr[i]][0], suffix]

    # Traverse the array queries[]
    for i in range(M):
        X = query[i]

        # Minimum of suffix
        # and prefix sums
        print(min(mp[X][0], mp[X][1]), end = " ")

# Driver Code
arr = [ 2, 3, 6, 7, 4, 5, 30 ]
queries = [ 6, 5 ]
N = len(arr)
M = len(queries)

calculateQuery(arr, N, queries, M)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation
// of the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find the minimum sum
  // for the given queries
  static void calculateQuery(int[] arr, int N,
                             int[] query, int M)
  {

    // Stores prefix and suffix sums
    int prefix = 0, suffix = 0;

    // Stores pairs of prefix and suffix sums
    Dictionary<int, Tuple<int,int>> mp =
      new Dictionary<int, Tuple<int,int>>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Add element to prefix
      prefix += arr[i];

      // Store prefix for each element
      mp[arr[i]] = new Tuple<int,int>(prefix, 0);
    }

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--)
    {

      // Add element to suffix
      suffix += arr[i];

      // Storing suffix for each element
      mp[arr[i]] = new Tuple<int,int>(mp[arr[i]].Item1, suffix);
    }

    // Traverse the array queries[]
    for (int i = 0; i < M; i++)
    {
      int X = query[i];

      // Minimum of suffix
      // and prefix sums
      Console.Write(Math.Min(mp[X].Item1, mp[X].Item2) + " ");
    }
  }

  // Driver code
  static void Main() {
    int[] arr = { 2, 3, 6, 7, 4, 5, 30 };
    int[] queries = { 6, 5 };
    int N = arr.Length;
    int M = queries.Length;

    calculateQuery(arr, N, queries, M);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript implementation
// of the above approach

// Function to find the minimum sum
// for the given queries
function calculateQuery(arr, N, query, M)
{

    // Stores prefix and suffix sums
    var prefix = 0, suffix = 0;

    // Stores pairs of prefix and suffix sums
    var mp = new Map();

    // Traverse the array
    for(var i = 0; i < N; i++)
    {

        // Add element to prefix
        prefix += arr[i];

        // Store prefix for each element
        if (!mp.has(arr[i]))
        {
            mp.set(arr[i], [0, 0]);
        }
        var tmp = mp.get(arr[i]);
        tmp[0] = prefix;
        mp.set(arr[i], tmp);
    }

    // Traverse the array in reverse
    for(var i = N - 1; i >= 0; i--)
    {

        // Add element to suffix
        suffix += arr[i];

        // Storing suffix for each element
        if (!mp.has(arr[i]))
        {
            mp.set(arr[i], [0, 0]);
        }
        var tmp = mp.get(arr[i]);
        tmp[1] = suffix;
        mp.set(arr[i], tmp);
    }

    // Traverse the array queries[]
    for(var i = 0; i < M; i++)
    {
        var X = query[i];

        var tmp = mp.get(X);

        // Minimum of suffix
        // and prefix sums
        document.write(Math.min(tmp[0], tmp[1]) + " ");
    }
}

// Driver Code
var arr = [ 2, 3, 6, 7, 4, 5, 30 ];
var queries = [ 6, 5 ];
var N = arr.length;
var M = queries.length;

calculateQuery(arr, N, queries, M);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
11 27
```

***时间复杂度:** O(M + N)*
***辅助空间:** O(N)*