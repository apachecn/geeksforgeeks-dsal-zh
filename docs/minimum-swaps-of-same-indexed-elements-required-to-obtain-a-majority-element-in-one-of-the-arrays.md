# 在一个数组中获得多数元素所需的相同索引元素的最小交换量

> 原文:[https://www . geeksforgeeks . org/同索引元素的最小互换-需要在一个数组中获得多数元素/](https://www.geeksforgeeks.org/minimum-swaps-of-same-indexed-elements-required-to-obtain-a-majority-element-in-one-of-the-arrays/)

给定两个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和**brr【】**，任务是找到这样一个元素出现在数组**arr【】**中至少一半索引处所需的相同索引元素的最小交换次数，即[多数元素](https://www.geeksforgeeks.org/majority-element/)。如果无法获得这样的排列，则打印**-1”**。

**示例:**

> **输入:** arr[] = {3，2，1，4，9}，brr[] = {5，5，3，5，3}
> **输出:** 2
> **解释:**
> 以下是所需的交换:
> T10】交换 1: 交换 arr[1]和 brr[1]将 arr[]修改为{3，2，3，4，9}，将 brr[]修改为{5，5，1，5，3}。
> **交换 2:** 交换 arr[5]和 brr[5]将 arr[]修改为{3，2，3，4，3}，将 brr[]修改为{5，5，1，5，9}。
> 因此，所需的互换总数为 2。
> 
> **输入:** arr[] = {2，4，2}，brr[] = {1，2，9}
> **输出:** 0

**方法:**按照以下步骤解决上述问题:

*   初始化一个变量 **res** 为 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，存储所需的最小交换。
*   使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)找到数组 a[]和 b[]元素的[频率计数，并分别存储在](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **A** 和 **B** 中。
*   创建一个大小为 **2*N** 的数组 **crr[]** ，以存储数组 **arr[]** 和 **brr[]** 中的所有元素。
*   使用变量 **i** 遍历数组 **crr[]** ，并执行以下操作:
    *   如果地图 **A** 中**crr【I】**的频率至少为 **N/2** ，则所需的最小交换为 **0** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)并打印 **0** 。
    *   如果地图 **A** 和 **B** 中**crr【I】**的频率之和至少为 **N/2** ，则更新 **res** 至 **res** 和**的最小值(N/2–A【crr【I】)**。
*   完成上述步骤后，如果 **res** 的值仍为 **INT_MAX** ，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the minimum
// number of swaps required to make
// half of the element same in a[]
int minMoves(int a[], int b[], int n)
{

    // Stores frequency of elements in a[]
    // Stores frequency of elements in b[]
    unordered_map<int, int> A, B;

    // Stores all elements from both arrays
    vector<int> c;

    // Find the maximum occurrence
    // required
    int maxOccur = ceil(floor(n)
                        / (2 * 1.0));

    for (int i = 0; i < n; ++i) {

        c.push_back(a[i]);
        c.push_back(b[i]);

        A[a[i]]++;

        // If a[i] == b[i], then no need
        // of incrementing in map B
        if (b[i] != a[i]) {
            B[b[i]]++;
        }
    }

    // Store the minimum number of swaps
    int res = INT_MAX;

    for (int i = 0; i < c.size(); ++i) {
        // Frequency of c[i] in array a
        int x = A];

        // Frequency of c[i] in array b
        int y = B];

        // Check the frequency condition
        if ((x + y) >= maxOccur) {

            // if c[i] is present at
            // least half times in array
            // a[], then 0 swaps required
            if (x >= maxOccur) {
                return 0;
            }

            // maxOccur - x is the count
            // of swaps needed to make
            // c[i] the majority element
            else {
                res = min(res, maxOccur - x);
            }
        }
    }

    // If not possible
    if (res == INT_MAX) {
        return -1;
    }

    // Otherwise
    else
        return res;
}

// Driver Code
int main()
{

    // Given arrays a[] and b[]
    int arr[] = { 3, 2, 1, 4, 9 };
    int brr[] = { 5, 5, 3, 5, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minMoves(arr, brr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class Main{

// Function that counts the minimum
// number of swaps required to make
// half of the element same in a[]
public static int minMoves(int a[],
                           int b[],
                           int n)
{
  // Stores frequency of elements
  // in a[]
  // Stores frequency of elements
  // in b[]
  HashMap<Integer,
          Integer> A =
          new HashMap<>();
  HashMap<Integer,
          Integer> B =
          new HashMap<>();

  // Stores all elements from
  // both arrays
  Vector<Integer> c =
         new Vector<Integer>();

  // Find the maximum occurrence
  // required
  int maxOccur = (int)Math.ceil(
                 (int)Math.floor(n) /
                 (2 * 1.0));

  for (int i = 0; i < n; ++i)
  {
    c.add(a[i]);
    c.add(b[i]);

    if(A.containsKey(a[i]))
    {
      A.replace(a[i],
      A.get(a[i]) + 1);
    }
    else
    {
      A.put(a[i], 1);
    }

    // If a[i] == b[i], then no need
    // of incrementing in map B
    if (b[i] != a[i])
    {
      if(B.containsKey(b[i]))
      {
        B.replace(b[i],
        B.get(b[i]) + 1);
      }
      else
      {
        B.put(b[i], 1);
      }
    }
  }

  // Store the minimum number
  // of swaps
  int res = Integer.MAX_VALUE;

  for (int i = 0; i < c.size(); ++i)
  {
    // Frequency of c[i] in array a
    int x = 0;
    if(A.containsKey(c.get(i)))
    {
      x = A.get(c.get(i));  
    }

    // Frequency of c[i] in array b
    int y = 0;
    if(B.containsKey(c.get(i)))
    {
      y = B.get(c.get(i));  
    }

    // Check the frequency
    // condition
    if ((x + y) >= maxOccur)
    {
      // if c[i] is present at
      // least half times in array
      // a[], then 0 swaps required
      if (x >= maxOccur)
      {
        return 0;
      }

      // maxOccur - x is the count
      // of swaps needed to make
      // c[i] the majority element
      else
      {
        res = Math.min(res,
                       maxOccur - x);
      }
    }
  }

  // If not possible
  if (res == Integer.MAX_VALUE)
  {
    return -1;
  }

  // Otherwise
  else
    return res;
}

// Driver code
public static void main(String[] args)
{
  // Given arrays a[] and b[]
  int arr[] = {3, 2, 1, 4, 9};
  int brr[] = {5, 5, 3, 5, 3};

  int N = arr.length;

  // Function Call
  System.out.println(minMoves(arr, brr, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import ceil, floor
import sys

# Function that counts the minimum
# number of swaps required to make
# half of the element same in a[]
def minMoves(a, b, n):

    # Stores frequency of elements in a[]
    # Stores frequency of elements in b[]
    A, B = {}, {}

    # Stores all elements from both arrays
    c = []

    # Find the maximum occurrence
    # required
    maxOccur = ceil(floor(n) / (2 * 1.0))

    for i in range(n):
        c.append(a[i])
        c.append(b[i])

        A[a[i]] = A.get(a[i], 0) + 1

        # If a[i] == b[i], then no need
        # of incrementing in map B
        if (b[i] != a[i]):
            B[b[i]] = B.get(b[i], 0) + 1

    # Store the minimum number of swaps
    res = sys.maxsize

    for i in range(len(c)):

        # Frequency of c[i] in array a
        x, y = 0, 0
        if c[i] in A:
            x = A]

        # Frequency of c[i] in array b
        if c[i] in B:
            y = B]

        # Check the frequency condition
        if ((x + y) >= maxOccur):

            # If c[i] is present at
            # least half times in array
            # a[], then 0 swaps required
            if (x >= maxOccur):
                return 0

            # maxOccur - x is the count
            # of swaps needed to make
            # c[i] the majority element
            else:
                res = min(res, maxOccur - x)

    # If not possible
    if (res == sys.maxsize):
        return -1

    # Otherwise
    else:
        return res

# Driver Code
if __name__ == '__main__':

    # Given arrays a[] and b[]
    arr = [ 3, 2, 1, 4, 9 ]
    brr = [ 5, 5, 3, 5, 3 ]

    N = len(arr)

    # Function Call
    print(minMoves(arr, brr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that counts the minimum
// number of swaps required to make
// half of the element same in []a
public static int minMoves(int []a,
                           int []b,
                           int n)
{

  // Stores frequency of elements
  // in []a
  // Stores frequency of elements
  // in []b
  Dictionary<int,
             int> A = new Dictionary<int,
                                     int>();
  Dictionary<int,
             int> B = new Dictionary<int,
                                     int>();

  // Stores all elements from
  // both arrays
  List<int> c = new List<int>();

  // Find the maximum occurrence
  // required
  int maxOccur = (int)(Math.Ceiling(
                 (int)(Math.Floor(
                 (double)n)) / (2 * 1.0)));

  for(int i = 0; i < n; ++i)
  {
    c.Add(a[i]);
    c.Add(b[i]);

    if (A.ContainsKey(a[i]))
    {
      A[a[i]] = A[a[i]] + 1;
    }
    else
    {
      A.Add(a[i], 1);
    }

    // If a[i] == b[i], then no need
    // of incrementing in map B
    if (b[i] != a[i])
    {
      if (B.ContainsKey(b[i]))
      {
        B[b[i]]++;
      }
      else
      {
        B.Add(b[i], 1);
      }
    }
  }

  // Store the minimum number
  // of swaps
  int res = int.MaxValue;

  for(int i = 0; i < c.Count; ++i)
  {

    // Frequency of c[i] in array a
    int x = 0;
    if (A.ContainsKey(c[i]))
    {
      x = A];  
    }

    // Frequency of c[i] in array b
    int y = 0;
    if (B.ContainsKey(c[i]))
    {
      y = B];  
    }

    // Check the frequency
    // condition
    if ((x + y) >= maxOccur)
    {

      // If c[i] is present at
      // least half times in array
      // []a, then 0 swaps required
      if (x >= maxOccur)
      {
        return 0;
      }

      // maxOccur - x is the count
      // of swaps needed to make
      // c[i] the majority element
      else
      {
        res = Math.Min(res,
                       maxOccur - x);
      }
    }
  }

  // If not possible
  if (res == int.MaxValue)
  {
    return -1;
  }

  // Otherwise
  else
    return res;
}

// Driver code
public static void Main(String[] args)
{

  // Given arrays []a and []b
  int []arr = { 3, 2, 1, 4, 9 };
  int []brr = { 5, 5, 3, 5, 3 };

  int N = arr.Length;

  // Function Call
  Console.WriteLine(minMoves(arr, brr, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that counts the minimum
// number of swaps required to make
// half of the element same in a[]
function minMoves(a, b, n)
{

    // Stores frequency of elements in a[]
    // Stores frequency of elements in b[]
    var A = new Map(), B = new Map();

    // Stores all elements from both arrays
    var c = [];

    // Find the maximum occurrence
    // required
    var maxOccur = Math.ceil(Math.floor(n)
                        / (2 * 1.0));

    for (var i = 0; i < n; ++i) {

        c.push(a[i]);
        c.push(b[i]);

        if(A.has(a[i]))
        {
            A.set(a[i], A.get(a[i])+1);
        }
        else
        {
            A.set(a[i], 1);
        }

        // If a[i] == b[i], then no need
        // of incrementing in map B
        if (b[i] != a[i]) {
            if(B.has(b[i]))
            {
                B.set(b[i], B.get(b[i])+1);
            }
            else
            {
                B.set(b[i], 1);
            }

        }
    }

    // Store the minimum number of swaps
    var res = 1000000000;

    for (var i = 0; i < c.length; ++i) {
        // Frequency of c[i] in array a
        var x = A.get(c[i]);

        // Frequency of c[i] in array b
        var y = B.get(c[i]);

        // Check the frequency condition
        if ((x + y) >= maxOccur) {

            // if c[i] is present at
            // least half times in array
            // a[], then 0 swaps required
            if (x >= maxOccur) {
                return 0;
            }

            // maxOccur - x is the count
            // of swaps needed to make
            // c[i] the majority element
            else {
                res = Math.min(res, maxOccur - x);
            }
        }
    }

    // If not possible
    if (res == 1000000000) {
        return -1;
    }

    // Otherwise
    else
        return res;
}

// Driver Code
// Given arrays a[] and b[]
var arr = [3, 2, 1, 4, 9];
var brr = [5, 5, 3, 5, 3];
var N = arr.length;
// Function Call
document.write( minMoves(arr, brr, N));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)