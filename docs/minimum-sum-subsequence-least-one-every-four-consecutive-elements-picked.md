# 最小和子序列，使得每四个连续元素中至少有一个被选取

> 原文:[https://www . geeksforgeeks . org/minimum-sum-subsequence-最少每四个连续元素选一个/](https://www.geeksforgeeks.org/minimum-sum-subsequence-least-one-every-four-consecutive-elements-picked/)

给定正整数数组 arr[]。任务是从数组中找到最小和[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，以便在所有四个连续元素的组中选择至少一个值。

**示例:**

```
Input: arr[] = {1, 2, 3, 4, 5, 6, 7, 8}
Output: 6
6 is sum of output subsequence {1, 5}
Note that we have following subarrays of four
consecutive elements
{(1, 2, 3, 4), 
 (2, 3, 4, 5),
 (3, 4, 5, 6)
 (4, 5, 6, 7)
 (5, 6, 7, 8)}
Our subsequence {1, 5} has an element from
all above groups of four consecutive elements.
And this subsequence is minimum sum such
subsequence.

Input : arr[] = {1, 2, 3, 3, 4, 5, 6, 1}
Output : 4
The subsequence is {3, 1}. Here we consider
second three.

Input: arr[] = {1, 2, 3, 2, 1}
Output: 2
The subsequence can be {1, 1} or {2}

Input: arr[] = {6, 7, 8}
Output: 6

Input: arr[] = {6, 7}
Output: 6
```

思路类似 [LIS 问题](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)。我们存储以 arr[]的每个元素结束的最小和子序列。我们最终返回最后四个值中的最小值。

```
dp[i] stores minimum sum subsequence (with at least
one of every four consecutive elements) of arr[0..i] 
such that arr[i] is part of the solution. Note that 
this may not be the best solution for subarray
arr[0..i].

We can recursively compute dp[i] using below formula
dp[i] = arr[i] + min(dp[i-1], dp[i-2], dp[i-3], dp[i-4])

Finally we return minimum of dp[n-1], dp[n-2], 
dp[n-4] and dp[n-3]
```

以下是上述想法的实现。

## C++

```
// C++ program to find minimum sum subsequence
// of an array such that one of every four
// consecutive elements is picked.
#include <iostream>
using namespace std;

// Returns sum of minimum sum subsequence
// such that one of every four consecutive
// elements is picked from arr[].
int minSum(int arr[], int n)
{
    // dp[i] is going to store minimum sum
    // subsequence of arr[0..i] such that arr[i]
    // is part of the solution. Note that this
    // may not be the best solution for subarray
    // arr[0..i]
    int dp[n];

    // If there is single value, we get the
    // minimum sum equal to arr[0]
    if (n == 1)
        return arr[0];

    // If there are two values, we get the
    // minimum sum equal to the minimum of
    // two values
    if (n == 2)
        return min(arr[0], arr[1]);

    // If there are three values, return
    // minimum of the three elements of
    // array
    if (n == 3)
        return min(arr[0], min(arr[1], arr[2]));

    // If there are four values, return minimum
    // of the four elements of array
    if (n == 4)
        return min(min(arr[0], arr[1]),
                   min(arr[2], arr[3]));

    dp[0] = arr[0];
    dp[1] = arr[1];
    dp[2] = arr[2];
    dp[3] = arr[3];

    for (int i = 4; i < n; i++)
        dp[i] = arr[i] + min(min(dp[i - 1], dp[i - 2]),
                             min(dp[i - 3], dp[i - 4]));

    // Return the minimum of last 4 index
    return min(min(dp[n - 1], dp[n - 2]),
               min(dp[n - 4], dp[n - 3]));
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 3, 4, 5, 6, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum sum subsequence
// of an array such that one of every four
// consecutive elements is picked.
import java.io.*;

class GFG {

    // Returns sum of minimum sum subsequence
    // such that one of every four consecutive
    // elements is picked from arr[].
    static int minSum(int[] arr, int n)
    {
        // dp[i] is going to store minimum sum
        // subsequence of arr[0..i] such that arr[i]
        // is part of the solution. Note that this
        // may not be the best solution for subarray
        // arr[0..i]
        int[] dp = new int[n];

        // If there is single value, we get the
        // minimum sum equal to arr[0]
        if (n == 1)
            return arr[0];

        // If there are two values, we get the
        // minimum sum equal to the minimum of
        // two values
        if (n == 2)
            return Math.min(arr[0], arr[1]);

        // If there are three values, return
        // minimum of the three elements of
        // array
        if (n == 3)
        return Math.min(arr[0], Math.min(arr[1], arr[2]));

        // If there are four values, return minimum
        // of the four elements of array
        if (n == 4)
            return Math.min(Math.min(arr[0], arr[1]),
                            Math.min(arr[2], arr[3]));

        dp[0] = arr[0];
        dp[1] = arr[1];
        dp[2] = arr[2];
        dp[3] = arr[3];

        for (int i = 4; i < n; i++)
        dp[i] = arr[i] + Math.min(Math.min(dp[i - 1], dp[i - 2]),
                         Math.min(dp[i - 3], dp[i - 4]));

        // Return the minimum of last 4 index
        return Math.min(Math.min(dp[n - 1], dp[n - 2]),
                        Math.min(dp[n - 4], dp[n - 3]));
    }

    // Driver code
    static public void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 3, 4, 5, 6, 1 };
        int n = arr.length;
        System.out.println(minSum(arr, n));
    }
}

// This Code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find minimum sum
# subsequence of an array such that one
# of every four consecutive elements is picked.

# Returns sum of minimum sum subsequence
# such that one of every four consecutive
# elements is picked from arr[].
def minSum(arr, n):

    # dp[i] is going to store minimum sum
    # subsequence of arr[0..i] such that
    # arr[i] is part of the solution. Note
    # that this may not be the best solution
    # for subarray arr[0..i]
    dp = [0] * n

    # If there is single value, we get
    # the minimum sum equal to arr[0]
    if (n == 1):
        return arr[0]

    # If there are two values, we get the
    # minimum sum equal to the minimum of
    # two values
    if (n == 2):
        return min(arr[0], arr[1])

    # If there are three values, return
    # minimum of the three elements of
    # array
    if (n == 3):
        return min(arr[0],
               min(arr[1], arr[2]))

    # If there are four values,
    # return minimum of the four
    # elements of array
    if (n == 4):
        return min(min(arr[0], arr[1]),
                   min(arr[2], arr[3]))

    dp[0] = arr[0]
    dp[1] = arr[1]
    dp[2] = arr[2]
    dp[3] = arr[3]

    for i in range( 4, n):
        dp[i] = arr[i] + min(min(dp[i - 1], dp[i - 2]),
                             min(dp[i - 3], dp[i - 4]))

    # Return the minimum of last 4 index
    return min(min(dp[n - 1], dp[n - 2]),
                min(dp[n - 4], dp[n - 3]))

# Driver code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 3, 4, 5, 6, 1 ]
    n = len(arr)
    print(minSum(arr, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find minimum sum subsequence
// of an array such that one of every four
// consecutive elements is picked.
using System;

class GFG {

    // Returns sum of minimum sum subsequence
    // such that one of every four consecutive
    // elements is picked from arr[].
    static int minSum(int[] arr, int n)
    {
        // dp[i] is going to store minimum sum
        // subsequence of arr[0..i] such that arr[i]
        // is part of the solution. Note that this
        // may not be the best solution for subarray
        // arr[0..i]
        int[] dp = new int[n];

        // If there is single value, we get the
        // minimum sum equal to arr[0]
        if (n == 1)
            return arr[0];

        // If there are two values, we get the
        // minimum sum equal to the minimum of
        // two values
        if (n == 2)
            return Math.Min(arr[0], arr[1]);

        // If there are three values, return
        // minimum of the three elements of
        // array
        if (n == 3)
            return Math.Min(arr[0], Math.Min(arr[1], arr[2]));

        // If there are four values, return minimum
        // of the four elements of array
        if (n == 4)
            return Math.Min(Math.Min(arr[0], arr[1]),
                            Math.Min(arr[2], arr[3]));

        dp[0] = arr[0];
        dp[1] = arr[1];
        dp[2] = arr[2];
        dp[3] = arr[3];

        for (int i = 4; i < n; i++)
            dp[i] = arr[i] + Math.Min(Math.Min(dp[i - 1], dp[i - 2]),
                             Math.Min(dp[i - 3], dp[i - 4]));

        // Return the minimum of last 4 index
        return Math.Min(Math.Min(dp[n - 1], dp[n - 2]),
                        Math.Min(dp[n - 4], dp[n - 3]));
    }

    // Driver code
    static public void Main()
    {
        int[] arr = { 1, 2, 3, 3, 4, 5, 6, 1 };
        int n = arr.Length;
        Console.WriteLine(minSum(arr, n));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to find minimum sum subsequence
// of an array such that one of every four
// consecutive elements is picked.

// Returns sum of minimum sum subsequence
// such that one of every four consecutive
// elements is picked from arr[].
function minSum(arr, n)
{

    // dp[i] is going to store minimum sum
    // subsequence of arr[0..i] such that arr[i]
    // is part of the solution. Note that this
    // may not be the best solution for subarray
    // arr[0..i]
    let dp = [];

    // If there is single value, we get the
    // minimum sum equal to arr[0]
    if (n == 1)
        return arr[0];

    // If there are two values, we get the
    // minimum sum equal to the minimum of
    // two values
    if (n == 2)
        return Math.min(arr[0], arr[1]);

    // If there are three values, return
    // minimum of the three elements of
    // array
    if (n == 3)
    return Math.min(arr[0],
           Math.min(arr[1], arr[2]));

    // If there are four values, return minimum
    // of the four elements of array
    if (n == 4)
        return Math.min(Math.min(arr[0], arr[1]),
                        Math.min(arr[2], arr[3]));

    dp[0] = arr[0];
    dp[1] = arr[1];
    dp[2] = arr[2];
    dp[3] = arr[3];

    for(let i = 4; i < n; i++)
        dp[i] = arr[i] +
        Math.min(Math.min(dp[i - 1], dp[i - 2]),
                 Math.min(dp[i - 3], dp[i - 4]));

    // Return the minimum of last 4 index
    return Math.min(Math.min(dp[n - 1], dp[n - 2]),
                    Math.min(dp[n - 4], dp[n - 3]));
}

// Driver Code
let arr = [ 1, 2, 3, 3, 4, 5, 6, 1 ];
let n = arr.length;

document.write(minSum(arr, n));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
4
```

**交替解:**
首先，假设我们只有四个元素，那么我们的结果至少是四个给定的元素。现在，在这种情况下，如果我们有四个以上的元素，那么我们必须保持一个数组 sum[]，其中 sum[i]包括第 I 个元素的可能最小和，并且第 I 个元素必须是解的一部分。
在计算和[i]时，我们的基本条件是 arr[i]必须是和[i]的一部分，然后我们必须有最后四个元素中的一个元素。因此，我们可以递归地将和[i]计算为 arr[i]和最小值之和(和[i-1]，和[i-2]，和[i-3]，和[i-4])。由于我们的问题的递归结构中有重叠的子问题，我们可以使用动态规划来解决这个问题。对于最终结果，我们必须计算 sum[]数组最后四个值的最小值，因为结果必须包含最后四个元素中的一个元素。

## C++

```
// CPP program to calculate
// minimum possible sum  for given constraint
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;

// function to calculate min sum using dp
int minSum(int ar[], int n)
{
    // if elements are less than or equal to 4
    if (n <= 4)
        return *min_element(ar, ar + n);

    // save start four element as it is
    int sum[n];
    sum[0] = ar[0];
    sum[1] = ar[1];
    sum[2] = ar[2];
    sum[3] = ar[3];

    // compute sum[] for all rest elements
    for (int i = 4; i < n; i++)
        sum[i] = ar[i] + (*min_element(sum + i - 4, sum + i));

    // Since one of the last 4 elements must be
    // present
    return *min_element(sum + n - 4, sum + n);
}

// driver program
int main()
{
    int ar[] = { 2, 4, 1, 5, 2, 3, 6, 1, 2, 4 };
    int n = sizeof(ar) / sizeof(ar[0]);
    cout << "Minimum sum = " << minSum(ar, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// minimum possible sum for given constraint
import java.util.Arrays;

class GFG
{

// function to calculate min sum using dp
static int minSum(int ar[], int n)
{
    // if elements are less than or equal to 4
    if (n <= 4)
        return Arrays.stream(ar).min().getAsInt();

    // save start four element as it is
    int []sum = new int[n];
    sum[0] = ar[0];
    sum[1] = ar[1];
    sum[2] = ar[2];
    sum[3] = ar[3];

    // compute sum[] for all rest elements
    for (int i = 4; i < n; i++)
        //sum[i] = ar[i] + (*min_element(sum + i - 4, sum + i));
        sum[i] = ar[i] + Arrays.stream(Arrays.copyOfRange(
                           sum, i - 4, i)).min().getAsInt();

    // Since one of the last 4 elements must be
    // present
    return Arrays.stream(Arrays.copyOfRange(
            sum, n - 4, n)).min().getAsInt();
}

// Driver Code
public static void main(String[] args)
{
    int ar[] = { 2, 4, 1, 5, 2, 3, 6, 1, 2, 4 };
    int n = ar.length;
    System.out.println("Minimum sum = " + minSum(ar, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to calculate
# minimum possible sum for given constraint

# function to calculate min sum using dp
def minSum(ar, n):

    # if elements are less than or equal to 4
    if (n <= 4):
        return min(ar)

    # save start four element as it is
    sum = [0 for i in range(n)]
    sum[0] = ar[0]
    sum[1] = ar[1]
    sum[2] = ar[2]
    sum[3] = ar[3]

    # compute sum[] for all rest elements
    for i in range(4, n):
        sum[i] = ar[i] + min(sum[i - 4:i])

    # Since one of the last 4 elements must be
    # present
    return min(sum[n - 4:n])

# Driver Code
ar = [2, 4, 1, 5, 2, 3, 6, 1, 2, 4]
n = len(ar)
print("Minimum sum = ", minSum(ar, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to calculate
// minimum possible sum for given constraint
using System;
using System.Linq;

class GFG
{

// function to calculate min sum using dp
static int minSum(int []ar, int n)
{
    // if elements are less than or equal to 4
    if (n <= 4)
        return ar.Min();

    // save start four element as it is
    int []sum = new int[n];
    sum[0] = ar[0];
    sum[1] = ar[1];
    sum[2] = ar[2];
    sum[3] = ar[3];
    int []tempArr;

    // compute sum[] for all rest elements
    for (int i = 4; i < n; i++)
    {
        //sum[i] = ar[i] + (*min_element(sum + i - 4, sum + i));
        tempArr = new int[4];
        Array.Copy(sum, i - 4, tempArr, 0, 4);
        sum[i] = ar[i] + tempArr.Min();
    }

    // Since one of the last 4 elements must be
    // present
    tempArr = new int[4];
    Array.Copy(sum,n-4,tempArr,0,4);
    return tempArr.Min();
}

// Driver Code
public static void Main(String[] args)
{
    int []ar = { 2, 4, 1, 5, 2, 3, 6, 1, 2, 4 };
    int n = ar.Length;
    Console.WriteLine("Minimum sum = " +
                         minSum(ar, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to calculate
// minimum possible sum  for given constraint

// function to calculate min sum using dp
function minSum(ar, n)
{
    // if elements are less than or equal to 4
    if (n <= 4)
        return Math.min.apply(Math,ar);
    var i;
    // save start four element as it is
    var sum = Array(n).fill(n);
    sum[0] = ar[0];
    sum[1] = ar[1];
    sum[2] = ar[2];
    sum[3] = ar[3];

    // compute sum[] for all rest elements
    for (i = 4; i < n; i++){
        var temp = [];
        var it;
        for(it= i-4;it<i;it++)
          temp.push(sum[it]);
      //(*min_element(sum + i - 4, sum + i));
        sum[i] = ar[i] + Math.min.apply(Math,temp);
    }

    // Since one of the last 4 elements must be
    // present
    var temp1 = [];
    for(i=n-4;i<n;i++)
        temp1.push(sum[i]);

    return Math.min.apply(Math,temp1);
}

// driver program

    var ar = [2, 4, 1, 5, 2, 3, 6, 1, 2, 4];
    var n = ar.length;
    document.write("Minimum sum = "+minSum(ar, n));

</script>
```

**输出:**

```
Minimum sum = 4
```

**时间复杂度:** O(n)。

感谢[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)提供了这个备选方案。
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。