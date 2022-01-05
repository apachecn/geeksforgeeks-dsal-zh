# 求一个数组中 k 个元素的最大异或

> 原文:[https://www . geeksforgeeks . org/find-max-xor-of-k-elements in-a-array/](https://www.geeksforgeeks.org/find-maximum-xor-of-k-elements-in-an-array/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** 。任务是找到给定数组的大小 **K** 的最大异或子集。
**举例:**

> **输入:** arr[] = {2，5，4，1，3，7，6，8}，K = 3
> **输出:** 15
> 我们通过选择 4，5，6，8
> **输入:** arr[] = {3，4，7，7，9}，K = 3
> **输出:** 14

**天真方法:**迭代数组的所有大小子集 **K** ，并在它们之间找到最大异或。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum xor for a
// subset of size k from the given array
int Max_Xor(int arr[], int n, int k)
{

    // Initialize result
    int maxXor = INT_MIN;

    // Traverse all subsets of the array
    for (int i = 0; i < (1 << n); i++) {

        // __builtin_popcount() returns the number
        // of sets bits in an integer
        if (__builtin_popcount(i) == k) {

            // Initialize current xor as 0
            int cur_xor = 0;
            for (int j = 0; j < n; j++) {

                // If jth bit is set in i then include
                // jth element in the current xor
                if (i & (1 << j))
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update maximum xor so far
            maxXor = max(maxXor, cur_xor);
        }
    }
    return maxXor;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 4, 1, 3, 7, 6, 8 };
    int n = sizeof(arr) / sizeof(int);
    int k = 3;

    cout << Max_Xor(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the maximum xor for a
// subset of size k from the given array
static int Max_Xor(int arr[], int n, int k)
{

    // Initialize result
    int maxXor = Integer.MIN_VALUE;

    // Traverse all subsets of the array
    for (int i = 0; i < (1 << n); i++)
    {

        // __builtin_popcount() returns the number
        // of sets bits in an integer
        if (Integer.bitCount(i) == k)
        {

            // Initialize current xor as 0
            int cur_xor = 0;
            for (int j = 0; j < n; j++)
            {

                // If jth bit is set in i then include
                // jth element in the current xor
                if ((i & (1 << j)) == 0)
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update maximum xor so far
            maxXor = Math.max(maxXor, cur_xor);
        }
    }
    return maxXor;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 5, 4, 1, 3, 7, 6, 8 };
    int n = arr.length;
    int k = 3;

    System.out.println(Max_Xor(arr, n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of the approach

MAX = 10000
MAX_ELEMENT = 50

dp =[[[-1 for i in range(MAX)]
    for j in range(MAX_ELEMENT)]
    for k in range(MAX_ELEMENT)]

# Function to return the maximum xor for a
# subset of size j from the given array
def Max_Xor(arr, i, j, mask, n):
    if (i >= n):

        # If the subset is complete then return
        # the xor value of the selected elements
        if (j == 0):
            return mask
        else:
            return 0

    # Return if already calculated for some
    # mask and j at the i'th index
    if (dp[i][j][mask] != -1):
        return dp[i][j][mask]

    # Initialize answer to 0
    ans = 0

    # If we can still include elements in our subset
    # include the i'th element
    if (j > 0):
        ans = Max_Xor(arr, i + 1, j - 1, mask ^ arr[i], n)

    # Exclude the i'th element
    # ans store the max of both operations
    ans = max(ans, Max_Xor(arr, i + 1, j, mask, n))
    dp[i][j][mask] = ans
    return ans

# Driver code
arr = [2, 5, 4, 1, 3, 7, 6, 8]
n = len(arr)
k = 3

print(Max_Xor(arr, 0, k, 0, n))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum xor for a
// subset of size k from the given array
static int Max_Xor(int []arr, int n, int k)
{

    // Initialize result
    int maxXor = int.MinValue;

    // Traverse all subsets of the array
    for (int i = 0; i < (1 << n); i++)
    {

        // __builtin_popcount() returns the number
        // of sets bits in an integer
        if (bitCount(i) == k)
        {

            // Initialize current xor as 0
            int cur_xor = 0;
            for (int j = 0; j < n; j++)
            {

                // If jth bit is set in i then include
                // jth element in the current xor
                if ((i & (1 << j)) == 0)
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update maximum xor so far
            maxXor = Math.Max(maxXor, cur_xor);
        }
    }
    return maxXor;
}

static int bitCount(long x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 5, 4, 1, 3, 7, 6, 8 };
    int n = arr.Length;
    int k = 3;

    Console.WriteLine(Max_Xor(arr, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum xor for a
// subset of size k from the given array
function Max_Xor(arr, n, k)
{

    // Initialize result
    let maxXor = Number.MIN_VALUE;

    // Traverse all subsets of the array
    for (let i = 0; i < (1 << n); i++) {

        // bitCount() returns the number
        // of sets bits in an integer
        if (bitCount(i) == k) {

            // Initialize current xor as 0
            let cur_xor = 0;
            for (let j = 0; j < n; j++) {

                // If jth bit is set in i then include
                // jth element in the current xor
                if (i & (1 << j))
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update maximum xor so far
            maxXor = Math.max(maxXor, cur_xor);
        }
    }
    return maxXor;
}

function bitCount(x)
{
    let setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
    let arr = [ 2, 5, 4, 1, 3, 7, 6, 8 ];
    let n = arr.length;
    let k = 3;

    document.write(Max_Xor(arr, n, k));

</script>
```

**Output:** 

```
15
```

**高效途径:**问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。创建一个 dp 表 **dp[i][j][mask]** ，该表在第**I**索引处(包括或不包括)存储可能的最大异或，并且 **j** 表示我们可以包含在 **K** 元素的子集中的剩余元素的数量。掩码是直到第 **i <sup>第</sup>T17】个索引为止所选所有元素的异或。
**注意:**由于 dp 阵列的空间要求，这种方法仅适用于较小的阵列。
以下是上述办法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 10000
#define MAX_ELEMENT 50

int dp[MAX_ELEMENT][MAX_ELEMENT][MAX];

// Function to return the maximum xor for a
// subset of size j from the given array
int Max_Xor(int arr[], int i, int j, int mask, int n)
{
    if (i >= n) {

        // If the subset is complete then return
        // the xor value of the selected elements
        if (j == 0)
            return mask;
        else
            return 0;
    }

    // Return if already calculated for some
    // mask and j at the i'th index
    if (dp[i][j][mask] != -1)
        return dp[i][j][mask];

    // Initialize answer to 0
    int ans = 0;

    // If we can still include elements in our subset
    // include the i'th element
    if (j > 0)
        ans = Max_Xor(arr, i + 1, j - 1, mask ^ arr[i], n);

    // Exclude the i'th element
    // ans store the max of both operations
    ans = max(ans, Max_Xor(arr, i + 1, j, mask, n));

    return dp[i][j][mask] = ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 4, 1, 3, 7, 6, 8 };
    int n = sizeof(arr) / sizeof(int);
    int k = 3;

    memset(dp, -1, sizeof(dp));

    cout << Max_Xor(arr, 0, k, 0, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 10000;
static int MAX_ELEMENT = 50;

static int [][][] dp = new int[MAX_ELEMENT][MAX_ELEMENT][MAX];

// Function to return the maximum xor for a
// subset of size j from the given array
static int Max_Xor(int arr[], int i,
                   int j, int mask, int n)
{
    if (i >= n)
    {

        // If the subset is complete then return
        // the xor value of the selected elements
        if (j == 0)
            return mask;
        else
            return 0;
    }

    // Return if already calculated for some
    // mask and j at the i'th index
    if (dp[i][j][mask] != -1)
        return dp[i][j][mask];

    // Initialize answer to 0
    int ans = 0;

    // If we can still include elements in our subset
    // include the i'th element
    if (j > 0)
        ans = Max_Xor(arr, i + 1, j - 1,
                      mask ^ arr[i], n);

    // Exclude the i'th element
    // ans store the max of both operations
    ans = Math.max(ans, Max_Xor(arr, i + 1, j,
                                mask, n));

    return dp[i][j][mask] = ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 5, 4, 1, 3, 7, 6, 8 };
    int n = arr.length;
    int k = 3;

    for(int i = 0; i < MAX_ELEMENT; i++)
    {
        for(int j = 0; j < MAX_ELEMENT; j++)
        {
            for(int l = 0; l < MAX; l++)
            dp[i][j][l] = -1;
        }
    }

    System.out.println(Max_Xor(arr, 0, k, 0, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of the approach

MAX = 10000
MAX_ELEMENT = 50

dp =[[[-1 for i in range(MAX)] for j in range(MAX_ELEMENT)] for k in range(MAX_ELEMENT)]

# Function to return the maximum xor for a
# subset of size j from the given array
def Max_Xor(arr, i, j, mask, n):
    if (i >= n):

        # If the subset is complete then return
        # the xor value of the selected elements
        if (j == 0):
            return mask
        else:
            return 0

    # Return if already calculated for some
    # mask and j at the i'th index
    if (dp[i][j][mask] != -1):
        return dp[i][j][mask]

    # Initialize answer to 0
    ans = 0

    # If we can still include elements in our subset
    # include the i'th element
    if (j > 0):
        ans = Max_Xor(arr, i + 1, j - 1, mask ^ arr[i], n)

    # Exclude the i'th element
    # ans store the max of both operations
    ans = max(ans, Max_Xor(arr, i + 1, j, mask, n))
    dp[i][j][mask] = ans
    return ans

# Driver code

arr = [2, 5, 4, 1, 3, 7, 6, 8]
n = len(arr)
k = 3

print(Max_Xor(arr, 0, k, 0, n))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
  static int MAX = 10000;
  static int MAX_ELEMENT = 50;
  static int [,,] dp = new int[MAX_ELEMENT, MAX_ELEMENT, MAX];

  // Function to return the maximum xor for a
  // subset of size j from the given array
  static int Max_Xor(int[] arr, int i,
                     int j, int mask, int n)
  {
    if (i >= n)
    {

      // If the subset is complete then return
      // the xor value of the selected elements
      if (j == 0)
        return mask;
      else
        return 0;
    }

    // Return if already calculated for some
    // mask and j at the i'th index
    if (dp[i,j,mask] != -1)
      return dp[i,j,mask];

    // Initialize answer to 0
    int ans = 0;

    // If we can still include elements in our subset
    // include the i'th element
    if (j > 0)
      ans = Max_Xor(arr, i + 1, j - 1,
                    mask ^ arr[i], n);

    // Exclude the i'th element
    // ans store the max of both operations
    ans = Math.Max(ans, Max_Xor(arr, i + 1, j,
                                mask, n));

    return dp[i,j,mask] = ans;
  }

  // Driver code
  public static void Main ()
  {
    int[] arr = { 2, 5, 4, 1, 3, 7, 6, 8 };
    int n = arr.Length;
    int k = 3;

    for(int i = 0; i < MAX_ELEMENT; i++)
    {
      for(int j = 0; j < MAX_ELEMENT; j++)
      {
        for(int l = 0; l < MAX; l++)
          dp[i,j,l] = -1;
      }
    }

    Console.WriteLine(Max_Xor(arr, 0, k, 0, n));
  }
}

// This code is contributed by target_2.
```

**Output:** 

```
15
```