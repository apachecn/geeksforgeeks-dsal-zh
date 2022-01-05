# 不含重复元素的最大长度为 K 的子序列数

> 原文:[https://www . geeksforgeeks . org/最大长度子序列数-k-包含不重复的元素/](https://www.geeksforgeeks.org/number-of-subsequences-of-maximum-length-k-containing-no-repeated-elements/)

给定一个由 **N** 元素和正整数 **K** 组成的数组 **arr[]** ，使得 **K ≤ N** 。任务是找到最大长度 **K** 的子序列的数量，即长度为 0，1，2，…，K–1，K 的子序列都有不同的元素。

**示例:**

> **输入:** arr[] = {2，2，3，3，5}，K = 2
> **输出:** 14
> 所有有效子序列为{}、{2}、{2}、{3}、{5}、
> {2，3}、{2，3}、{2，3}、{2，3}、{2，5}、{2，5}、{2，5}、{3，5}和{3，5}。
> 
> **输入:** arr[] = {1，2，3，4，4}，K = 4
> T3】输出: 24

**进场:**

*   如果数组 **a[]** 尚未排序，则对其进行排序，并在向量 **arr[]** 中存储原始数组中每个元素的频率。例如，如果 **a[] = {2，2，3，3，5}** 那么 **arr[] = {2，2，1}** 因为 2 出现两次，3 出现两次，5 只出现一次。
*   假设 **m** 是向量**arr【】**的长度。所以 **m** 将是不同元素的数量。可以有不重复的最大长度为 m 的子序列。如果 **m < k** ，则没有长度 **k** 的子序列。所以，声明 **n =最小值(m，k)** 。
*   现在应用动态编程。创建一个二维数组 **dp[n + 1][m + 1]** ，这样 **dp[i][j]** 将存储长度为 **i** 的子序列的数量，其第一个元素从**arr【】**中的第 **j** 个元素之后开始。例如， **dp[1][1] = 3** ，因为它表示长度为 1 的子序列的数量
    ，其第一个元素在 **arr[]** 的第一个元素之后开始，第一个元素为{3}、{3}、{5}。
    *   将第一行 **dp[][]** 初始化为 **1** 。
    *   在前一个循环内部，从上到下和从右到左运行两个循环。
    *   如果**j>m–I**这意味着由于缺少元素，不可能有任何这样的序列。所以 **dp[i][j] = 0** 。
    *   否则，**DP[I][j]= DP[I][j+1]+arr[j]* DP[I–1][j+1]**，因为该数将是长度为 **i** 的已有子序列数加上长度为**I–1**的子序列数乘以 **arr[j]** 的重复数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Returns number of subsequences
// of maximum length k and
// contains no repeated element
int countSubSeq(int a[], int n, int k)
{
    // Sort the array a[]
    sort(a, a + n);
    vector<int> arr;

    // Store the frequencies of all the
    // distinct element in the vector arr
    for (int i = 0; i < n;) {
        int count = 1, x = a[i];
        i++;
        while (i < n && a[i] == x) {
            count++;
            i++;
        }
        arr.push_back(count);
    }

    int m = arr.size();
    n = min(m, k);

    // count is the the number
    // of such subsequences
    int count = 1;

    // Create a 2-d array dp[n+1][m+1] to
    // store the intermediate result
    int dp[n + 1][m + 1];

    // Initialize the first row to 1
    for (int i = 0; i <= m; i++)
        dp[0][i] = 1;

    // Update the dp[][] array based
    // on the recurrence relation
    for (int i = 1; i <= n; i++) {
        for (int j = m; j >= 0; j--) {
            if (j > m - i)
                dp[i][j] = 0;
            else {
                dp[i][j] = dp[i][j + 1]
                           + arr[j] * dp[i - 1][j + 1];
            }
        }
        count = count + dp[i][0];
    }

    // Return the number of subsequences
    return count;
}

// Driver code
int main()
{
    int a[] = { 2, 2, 3, 3, 5 };
    int n = sizeof(a) / sizeof(int);
    int k = 3;

    cout << countSubSeq(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Returns number of subsequences
// of maximum length k and
// contains no repeated element
static int countSubSeq(int a[], int n, int k)
{
    // Sort the array a[]
    Arrays.sort(a);
    List<Integer> arr = new LinkedList<>();

    // Store the frequencies of all the
    // distinct element in the vector arr
    for (int i = 0; i < n;)
    {
        int count = 1, x = a[i];
        i++;
        while (i < n && a[i] == x)
        {
            count++;
            i++;
        }
        arr.add(count);
    }

    int m = arr.size();
    n = Math.min(m, k);

    // count is the the number
    // of such subsequences
    int count = 1;

    // Create a 2-d array dp[n+1][m+1] to
    // store the intermediate result
    int [][]dp = new int[n + 1][m + 1];

    // Initialize the first row to 1
    for (int i = 0; i <= m; i++)
        dp[0][i] = 1;

    // Update the dp[][] array based
    // on the recurrence relation
    for (int i = 1; i <= n; i++)
    {
        for (int j = m; j >= 0; j--)
        {
            if (j > m - i)
                dp[i][j] = 0;
            else
            {
                dp[i][j] = dp[i][j + 1] +
                             arr.get(j) *
                           dp[i - 1][j + 1];
            }
        }
        count = count + dp[i][0];
    }

    // Return the number of subsequences
    return count;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 2, 3, 3, 5 };
    int n = a.length;
    int k = 3;

    System.out.println(countSubSeq(a, n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Returns number of subsequences
# of maximum length k and
# contains no repeated element
def countSubSeq(a, n, k):

    # Sort the array a[]
    a.sort(reverse = False)
    arr = []

    # Store the frequencies of all the
    # distinct element in the vector arr
    i = 0
    while(i < n):
        count = 1
        x = a[i]
        i += 1
        while (i < n and a[i] == x):
            count += 1
            i += 1

        arr.append(count)

    m = len(arr)
    n = min(m, k)

    # count is the the number
    # of such subsequences
    count = 1

    # Create a 2-d array dp[n+1][m+1] to
    # store the intermediate result
    dp = [[0 for i in range(m + 1)]
             for j in range(n + 1)]

    # Initialize the first row to 1
    for i in range(m + 1):
        dp[0][i] = 1

    # Update the dp[][] array based
    # on the recurrence relation
    for i in range(1, n + 1, 1):
        j = m
        while(j >= 0):
            if (j > m - i):
                dp[i][j] = 0
            else:
                dp[i][j] = dp[i][j + 1] + \
                  arr[j] * dp[i - 1][j + 1]

            j -= 1

        count = count + dp[i][0]

    # Return the number of subsequences
    return count

# Driver code
if __name__ == '__main__':
    a = [2, 2, 3, 3, 5]
    n = len(a)
    k = 3

    print(countSubSeq(a, n, k))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Returns number of subsequences
// of maximum length k and
// contains no repeated element
static int countSubSeq(int []a, int n, int k)
{
    // Sort the array a[]
    Array.Sort(a);
    List<int> arr = new List<int>();
    int count, x;

    // Store the frequencies of all the
    // distinct element in the vector arr
    for (int i = 0; i < n;)
    {
        count = 1;
        x = a[i];
        i++;
        while (i < n && a[i] == x)
        {
            count++;
            i++;
        }
        arr.Add(count);
    }

    int m = arr.Count;
    n = Math.Min(m, k);

    // count is the the number
    // of such subsequences
    count = 1;

    // Create a 2-d array dp[n+1][m+1] to
    // store the intermediate result
    int [,]dp = new int[n + 1, m + 1];

    // Initialize the first row to 1
    for (int i = 0; i <= m; i++)
        dp[0, i] = 1;

    // Update the dp[][] array based
    // on the recurrence relation
    for (int i = 1; i <= n; i++)
    {
        for (int j = m; j >= 0; j--)
        {
            if (j > m - i)
                dp[i, j] = 0;
            else
            {
                dp[i, j] = dp[i, j + 1] +
                                 arr[j] *
                           dp[i - 1, j + 1];
            }
        }
        count = count + dp[i, 0];
    }

    // Return the number of subsequences
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 2, 2, 3, 3, 5 };
    int n = a.Length;
    int k = 3;

    Console.WriteLine(countSubSeq(a, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Returns number of subsequences
// of maximum length k and
// contains no repeated element
function countSubSeq(a, n, k)
{
    // Sort the array a[]
    a.sort();
    var arr = [];

    // Store the frequencies of all the
    // distinct element in the vector arr
    for (var i = 0; i < n;) {
        var count = 1, x = a[i];
        i++;
        while (i < n && a[i] == x) {
            count++;
            i++;
        }
        arr.push(count);
    }

    var m = arr.length;
    n = Math.min(m, k);

    // count is the the number
    // of such subsequences
    var count = 1;

    // Create a 2-d array dp[n+1][m+1] to
    // store the intermediate result
    var dp = Array.from(Array(n+1), ()=>Array(m+1));

    // Initialize the first row to 1
    for (var i = 0; i <= m; i++)
        dp[0][i] = 1;

    // Update the dp[][] array based
    // on the recurrence relation
    for (var i = 1; i <= n; i++) {
        for (var j = m; j >= 0; j--) {
            if (j > m - i)
                dp[i][j] = 0;
            else {
                dp[i][j] = dp[i][j + 1]
                           + arr[j] * dp[i - 1][j + 1];
            }
        }
        count = count + dp[i][0];
    }

    // Return the number of subsequences
    return count;
}

// Driver code
var a = [2, 2, 3, 3, 5];
var n = a.length;
var k = 3;
document.write( countSubSeq(a, n, k));

</script>
```

**Output:** 

```
18
```