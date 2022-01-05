# 在所有给定的 GCD 超过 K 的整数对中，GCD 最小的整数对

> 原文:[https://www . geeksforgeeks . org/在所有给定的整数对中具有最小 gcd 的整数对具有超过-k 的 gcd/](https://www.geeksforgeeks.org/pair-of-integers-having-least-gcd-among-all-given-pairs-having-gcd-exceeding-k/)

给定一个包含 GCD 递增顺序的整数对的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**和一个整数 **K** ，任务是找到一对其 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 至少为 **K** 并且也是所有可能超过 **K** 的 GCD 中最少的整数。如果没有这样的配对，则打印 **-1** 。
**示例:**

> **输入:** arr[][] = [(3，6)，(15，30)，(25，75)，(30，120)]，K = 16
> **输出:** (25，75)
> **说明:**
> 的 GCD 为 25，大于 16，在所有可能的 GCD 中最小。
> 
> **输入:** arr[] = [(2，5)，(12，36)，(13，26)]，K = 14
> **输出:** -1

**天真方法:**最简单的方法是迭代给定数组的所有对，并检查每个对，如果其 GCD 超过 ***K*** 。从所有这些对中，打印具有最少 **GCD** 的对。

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*

**有效方法:**想法是观察数组元素按其对的 GCD 值的递增顺序排序，因此使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。按照以下步骤解决问题:

*   计算搜索空间的中间值，检查**的 GCD 是否为【中】> K** 。
*   如果超过 **K** ，则更新答案，将搜索空间的上限值降低至**mid–1**。
*   如果**的 GCD arr[mid]≤K**，则将搜索空间的下限值增加到 **mid + 1** 。
*   继续上述过程，直到下限值小于或等于上限值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// the GCD of two numbers
int GCD(int a, int b)
{
    if (b == 0) {
        return a;
    }
    return GCD(b, a % b);
}

// Function to print the pair
// having a gcd value just greater
// than the given integer
void GcdPair(vector<pair<int, int> > arr, int k)
{
    // Initialize variables
    int lo = 0, hi = arr.size() - 1, mid;
    pair<int, int> ans;
    ans = make_pair(-1, 0);

    // Iterate until low less
    // than equal to high
    while (lo <= hi) {

        // Calculate mid
        mid = lo + (hi - lo) / 2;
        if (GCD(arr[mid].first,
                arr[mid].second)
            > k) {
            ans = arr[mid];
            hi = mid - 1;
        }
        // Reducing the search space
        else
            lo = mid + 1;
    }

    // Print the answer
    if (ans.first == -1)
        cout << "-1";
    else
        cout << "( " << ans.first << ", "
             << ans.second << " )";

    return;
}

// Driver Code
int main()
{
    // Given array and K
    vector<pair<int, int> > arr = { { 3, 6 },
                                    { 15, 30 },
                                    { 25, 75 },
                                    { 30, 120 } };
    int K = 16;

    // Function Call
    GcdPair(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to calculate
// the GCD of two numbers
static int GCD(int a, int b)
{
  if (b == 0)
  {
    return a;
  }
  return GCD(b, a % b);
}

// Function to print the pair
// having a gcd value just
// greater than the given integer
static void GcdPair(int [][]arr,
                    int k)
{
  // Initialize variables
  int lo = 0, hi = arr.length - 1, mid;
  int []ans = {-1, 0};

  // Iterate until low less
  // than equal to high
  while (lo <= hi)
  {
    // Calculate mid
    mid = lo + (hi - lo) / 2;
    if (GCD(arr[mid][0],
            arr[mid][1]) > k)
    {
      ans = arr[mid];
      hi = mid - 1;
    }

    // Reducing the search space
    else
      lo = mid + 1;
  }

  // Print the answer
  if (ans[0] == -1)
    System.out.print("-1");
  else
    System.out.print("( " + ans[0] +
                     ", " + ans[1] + " )");
  return;
}

// Driver Code
public static void main(String[] args)
{
  // Given array and K
  int [][]arr = {{3, 6},
                 {15, 30},
                 {25, 75},
                 {30, 120}};
  int K = 16;

  // Function Call
  GcdPair(arr, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# the GCD of two numbers
def GCD(a, b):

    if (b == 0):
        return a

    return GCD(b, a % b)

# Function to print the pair
# having a gcd value just greater
# than the given integer
def GcdPair(arr, k):

    # Initialize variables
    lo = 0
    hi = len(arr) - 1
    ans = [-1, 0]

    # Iterate until low less
    # than equal to high
    while (lo <= hi):

        # Calculate mid
        mid = lo + (hi - lo) // 2
        if (GCD(arr[mid][0], arr[mid][1]) > k):
            ans = arr[mid]
            hi = mid - 1

        # Reducing the search space
        else:
            lo = mid + 1

    # Print the answer
    if (len(ans) == -1):
        print("-1")
    else:
        print("(", ans[0], ",", ans[1], ")")

# Driver Code
if __name__ == '__main__':

    # Given array and K
    arr = [ [ 3, 6 ],
            [ 15, 30 ],
            [ 25, 75 ],
            [ 30, 120 ] ]
    K = 16

    # Function call
    GcdPair(arr, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to calculate
// the GCD of two numbers
static int GCD(int a, int b)
{
  if (b == 0)
  {
    return a;
  }
  return GCD(b, a % b);
}

// Function to print the pair
// having a gcd value just
// greater than the given integer
static void GcdPair(int [,]arr,
                    int k)
{
  // Initialize variables
  int lo = 0, hi = arr.Length - 1, mid;
  int []ans = {-1, 0};

  // Iterate until low less
  // than equal to high
  while (lo <= hi)
  {
    // Calculate mid
    mid = lo + (hi - lo) / 2;
    if (GCD(arr[mid, 0],
            arr[mid, 1]) > k)
    {
      ans = GetRow(arr, mid);
      hi = mid - 1;
    }

    // Reducing the search space
    else
      lo = mid + 1;
  }

  // Print the answer
  if (ans[0] == -1)
    Console.Write("-1");
  else
    Console.Write("( " + ans[0] +
                  ", " + ans[1] + " )");
  return;
}

public static int[] GetRow(int[,] matrix, int row)
{
  var rowLength = matrix.GetLength(1);
  var rowVector = new int[rowLength];

  for (var i = 0; i < rowLength; i++)
    rowVector[i] = matrix[row, i];

  return rowVector;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array and K
  int [,]arr = {{3, 6},
                {15, 30},
                {25, 75},
                {30, 120}};
  int K = 16;

  // Function Call
  GcdPair(arr, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

    // Function to calculate
    // the GCD of two numbers
    function GCD(a , b) {
        if (b == 0) {
            return a;
        }
        return GCD(b, a % b);
    }

    // Function to print the pair
    // having a gcd value just
    // greater than the given integer
    function GcdPair(arr , k) {
        // Initialize variables
        var lo = 0, hi = arr.length - 1, mid;
        var ans = [ -1, 0 ];

        // Iterate until low less
        // than equal to high
        while (lo <= hi) {
            // Calculate mid
            mid = lo + parseInt((hi - lo) / 2);
            if (GCD(arr[mid][0], arr[mid][1]) > k) {
                ans = arr[mid];
                hi = mid - 1;
            }

            // Reducing the search space
            else
                lo = mid + 1;
        }

        // Print the answer
        if (ans[0] == -1)
            document.write("-1");
        else
            document.write("( " + ans[0] + ", " + ans[1] + " )");
        return;
    }

    // Driver Code

        // Given array and K
        var arr = [ [ 3, 6 ], [ 15, 30 ], [ 25, 75 ], [ 30, 120 ] ];
        var K = 16;

        // Function Call
        GcdPair(arr, K);

// This code is contributed by todaysgaurav

</script>
```

**Output**

```
( 25, 75 )
```

***时间复杂度:**O(log(N)<sup>2</sup>)*
***辅助空间:** O(1)*