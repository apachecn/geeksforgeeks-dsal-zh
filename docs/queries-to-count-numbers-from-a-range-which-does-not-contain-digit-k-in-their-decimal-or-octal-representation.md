# 从十进制或八进制表示中不包含数字 K 的范围中对数字进行计数的查询

> 原文:[https://www . geesforgeks . org/query-to-count-numbers-from-a-range-其中不包含十进制或八进制表示中的数字 k/](https://www.geeksforgeeks.org/queries-to-count-numbers-from-a-range-which-does-not-contain-digit-k-in-their-decimal-or-octal-representation/)

给定一个整数 **K** 和一个由 **N** 类型的 **{L，R}** 查询组成的[数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** ，每个查询的任务是打印范围**【L，R】**中不包含数字 **K** 的数字在其[十进制表示](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)或[八进制表示中的计数。](https://www.geeksforgeeks.org/octal-numbers-c/)

**示例:**

> **输入:** K = 7，Q[][] = {{1，15}}
> **输出:** 13
> **解释:**
> 只有数字 7 和 15 在其八进制或十进制表示中包含数字 K。
> 数字 7 的八进制表示是 7。
> 数字 15 的八进制表示是 17。
> 
> **输入:** K = 8，Q[][] = {{1，10}}
> **输出:** 9
> **说明:**
> 只有数字 8 的十进制表示中包含数字 K。
> 数字 8 的八进制表示是 10。

**天真方法:**想法是遍历每个查询的范围**【L，R】**，找到那些十进制和八进制表示不包含数字 **K** 的数字。打印此类数字的计数。

***时间复杂度:**O(N<sup>2</sup>*(log<sub>10</sub>(N)+log<sub>8</sub>(N)))*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，其思想是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术来预先计算所有此类数字的计数。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如**pref【】**，以存储包含数字 **K** 的**【0，I】**范围内的数字的计数，这些数字以其[八进制](https://www.geeksforgeeks.org/octal-numbers-c/)或十进制表示。
*   现在遍历范围**【0，1e 6】**，并执行以下步骤:
    *   如果数字在八进制表示或十进制表示中包含数字 **K** ，则更新**pref【I】**为**pref【I–1】+1**。
    *   否则，将 **pref[i]** 更新为**pref[I–1]**。
*   [遍历给定的查询](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将每个查询的计数打印为

> q[I][1]–q[I][0]+1-(pref[q[I][1]–pref[q[I][0]–1])

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given digit
// 'K' is present in the decimal and octal
// representations of num or not
bool contains(int num, int K, int base)
{
    // Stores if the digit exists
    // or not
    bool isThere = 0;

    // Iterate till nums is non-zero
    while (num) {

        // Find the remainder
        int remainder = num % base;

        // If the remainder is K
        if (remainder == K) {
            isThere = 1;
        }

        num /= base;
    }

    return isThere;
}

// Function to count the numbers in the
// range [1, N] such that it doesn't
// contain the digit 'K' in its decimal
// and octal representation
void count(int n, int k,
           vector<vector<int> > v)
{

    // Stores count of numbers in the
    // range [0, i] that contains the
    // digit 'K' in its octal or
    // decimal representation
    int pref[1000005] = { 0 };

    // Traverse the range [0, 1e6 + 5]
    for (int i = 1; i < 1e6 + 5; i++) {

        // Check if i contains the digit
        // 'K' in its decimal or
        // octal representation
        bool present
            = contains(i, k, 10)
              || contains(i, k, 8);

        // Update pref[i]
        pref[i] += pref[i - 1] + present;
    }

    // Print the answer of queries
    for (int i = 0; i < n; ++i) {

        cout << v[i][1] - v[i][0] + 1
                    - (pref[v[i][1]]
                       - pref[v[i][0] - 1])
             << ' ';
    }
}

// Driver Code
int main()
{
    int K = 7;
    vector<vector<int> > Q = { { 2, 5 },
                               { 1, 15 } };
    int N = Q.size();

    // Function Call
    count(N, K, Q);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to check if the given digit
  // 'K' is present in the decimal and octal
  // representations of num or not
  static boolean contains(int num, int K, int Base)
  {

    // Stores if the digit exists
    // or not
    boolean isThere = false;

    // Iterate till nums is non-zero
    while (num > 0)
    {

      // Find the remainder
      int remainder = num % Base;

      // If the remainder is K
      if (remainder == K)
      {
        isThere = true;
      }

      num /= Base;
    }

    return isThere;
  }

  // Function to count the numbers in the
  // range [1, N] such that it doesn't
  // contain the digit 'K' in its decimal
  // and octal representation
  static void count(int n, int k,
                    Vector<Vector<Integer> > v)
  {

    // Stores count of numbers in the
    // range [0, i] that contains the
    // digit 'K' in its octal or
    // decimal representation
    int[] pref = new int[1000005];

    // Traverse the range [0, 1e6 + 5]
    for (int i = 1; i < 1e6 + 5; i++) {

      // Check if i contains the digit
      // 'K' in its decimal or
      // octal representation
      boolean present
        = contains(i, k, 10)
        || contains(i, k, 8);

      // Update pref[i]
      if(present)
      {
        pref[i] += pref[i - 1] + 1;
      }
    }

    // Print the answer of queries
    System.out.print((v.get(0).get(1) - v.get(0).get(0) +
                      1 - (pref[v.get(0).get(1)] -
                           pref[v.get(0).get(0) - 1])) + " ");
    System.out.print((v.get(1).get(1) - v.get(1).get(0) -
                      (pref[v.get(1).get(1)] -
                       pref[v.get(1).get(0) - 1])) + " ");
  }

  // Driver code
  public static void main(String[] args)
  {
    int K = 7;
    Vector<Vector<Integer> > Q = new Vector<Vector<Integer> >();
    Q.add(new Vector<Integer>());
    Q.get(0).add(2);
    Q.get(0).add(5);
    Q.add(new Vector<Integer>());
    Q.get(1).add(1);
    Q.get(1).add(15);

    int N = Q.size();

    // Function Call
    count(N, K, Q);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given digit
# 'K' is present in the decimal and octal
# representations of num or not
def contains(num, K, base):

    # Stores if the digit exists
    # or not
    isThere = 0

    # Iterate till nums is non-zero
    while (num):

        # Find the remainder
        remainder = num % base

        # If the remainder is K
        if (remainder == K):
            isThere = 1
        num //= base
    return isThere

# Function to count the numbers in the
# range [1, N] such that it doesn't
# contain the digit 'K' in its decimal
# and octal representation
def count(n, k, v):

    # Stores count of numbers in the
    # range [0, i] that contains the
    # digit 'K' in its octal or
    # decimal representation
    pref = [0]*1000005

    # Traverse the range [0, 1e6 + 5]
    for i in range(1, 10 ** 6 + 5):

        # Check if i contains the digit
        # 'K' in its decimal or
        # octal representation
        present = contains(i, k, 10) or contains(i, k, 8)

        # Update pref[i]
        pref[i] += pref[i - 1] + present

    # Print the answer of queries
    for i in range(n):
        print(v[i][1] - v[i][0] + 1- (pref[v[i][1]]- pref[v[i][0] - 1]),end=" ")

# Driver Code
if __name__ == '__main__':
    K = 7
    Q = [ [ 2, 5 ],
       [ 1, 15 ] ]

    N = len(Q)

    # Function Call
    count(N, K, Q)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to check if the given digit
  // 'K' is present in the decimal and octal
  // representations of num or not
  static bool contains(int num, int K, int Base)
  {

    // Stores if the digit exists
    // or not
    bool isThere = false;

    // Iterate till nums is non-zero
    while (num > 0)
    {

      // Find the remainder
      int remainder = num % Base;

      // If the remainder is K
      if (remainder == K)
      {
        isThere = true;
      }

      num /= Base;
    }

    return isThere;
  }

  // Function to count the numbers in the
  // range [1, N] such that it doesn't
  // contain the digit 'K' in its decimal
  // and octal representation
  static void count(int n, int k,
                    List<List<int> > v)
  {

    // Stores count of numbers in the
    // range [0, i] that contains the
    // digit 'K' in its octal or
    // decimal representation
    int[] pref = new int[1000005];

    // Traverse the range [0, 1e6 + 5]
    for (int i = 1; i < 1e6 + 5; i++) {

      // Check if i contains the digit
      // 'K' in its decimal or
      // octal representation
      bool present
        = contains(i, k, 10)
        || contains(i, k, 8);

      // Update pref[i]
      if(present)
      {
        pref[i] += pref[i - 1] + 1;
      }
    }

    // Print the answer of queries
    Console.Write((v[0][1] - v[0][0] + 1 - (pref[v[0][1]] - pref[v[0][0] - 1])) + " ");
    Console.Write((v[1][1] - v[1][0] - (pref[v[1][1]] - pref[v[1][0] - 1])) + " ");
  }

  // Driver code
  static void Main()
  {
    int K = 7;
    List<List<int> > Q = new List<List<int>>();
    Q.Add(new List<int>());
    Q[0].Add(2);
    Q[0].Add(5);
    Q.Add(new List<int>());
    Q[1].Add(1);
    Q[1].Add(15);

    int N = Q.Count;

    // Function Call
    count(N, K, Q);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the given digit
// 'K' is present in the decimal and octal
// representations of num or not
function contains(num, K, base)
{
    // Stores if the digit exists
    // or not
    var isThere = 0;

    // Iterate till nums is non-zero
    while (num) {

        // Find the remainder
        var remainder = num % base;

        // If the remainder is K
        if (remainder == K) {
            isThere = 1;
        }

        num /= base;
    }

    return isThere;
}

// Function to count the numbers in the
// range [1, N] such that it doesn't
// contain the digit 'K' in its decimal
// and octal representation
function count(n, k, v)
{

    // Stores count of numbers in the
    // range [0, i] that contains the
    // digit 'K' in its octal or
    // decimal representation
    var pref = Array(100005).fill(0);

    // Traverse the range [0, 1e6 + 5]
    for (var i = 1; i < 100005; i++) {

        // Check if i contains the digit
        // 'K' in its decimal or
        // octal representation
        var present
            = contains(i, k, 10)
              || contains(i, k, 8);

        // Update pref[i]
        pref[i] += pref[i - 1] + present;
    }

    // Print the answer of queries
    for (var i = 0; i < n; ++i) {

        document.write( v[i][1] - v[i][0] + 1
                    - (pref[v[i][1]]
                       - pref[v[i][0] - 1])
             + ' ');
    }
}

// Driver Code
var K = 7;
var Q = [ [ 2, 5 ], [1, 15 ]];
var N = Q.length;
// Function Call
count(N, K, Q);

</script>
```

**Output:** 

```
4 13
```

***时间复杂度:**O(N *(log<sub>10</sub>(N)+log<sub>8</sub>(N)))*
***辅助空间:** O(N)*