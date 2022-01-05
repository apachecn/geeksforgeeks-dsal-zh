# 和可被 m 整除的子集数

> 原文:[https://www . geesforgeks . org/sum 可被 m 整除的子集数/](https://www.geeksforgeeks.org/number-of-subsets-with-sum-divisible-by-m/)

给定一个整数数组，求多个子序列，使得子序列的和可被 m 整除。给定数组元素的和很小。
**例:**

```
Input : arr[] = {1, 2, 3};
        m = 3;
Output : 3
Subsequence of given set are
{1}, {2}, {3}, {1, 2}, {2, 3}, {1, 3} and {1, 2, 3}. 
And their sums are 1, 2, 3, 3, 5, 4 and 6.

Input : arr[] = {1, 2, 3, 4};
        m = 2;
Output : 7
{2}, {4}, {1, 3}, {2, 4}, {1, 2, 3}, {1, 3, 4} 
and {1, 2, 3, 4}
```

一个**简单的解决方案**就是生成所有可能的子集。对于每个子集，计算其和，如果和是 m 的倍数，则将结果增加 1。这种方法的时间复杂度是 **O(2 <sup>len</sup> )** ，其中 len 是输入阵列的长度。
一个**高效解**(针对小值)是基于子集和问题的[动态规划解。我们制作一个大小为和×n 的 2D 数组](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/) 

## C++

```
// C++ program which returns the Number of sub sequences
// (or subsets) which are divisible by m.
#include <bits/stdc++.h>
using namespace std;

// Use Dynamic Programming to find
// sum of subsequences.
int sumSubSequence(vector<int> arr, int len, int m)
{
    // Find sum pf array elements
    int sum = 0;
    for (auto x : arr)
       sum += x;

    // dp[i][j] would be > 0 if arr[0..i-1] has
    // a subsequence with sum equal to j.
    vector<vector<int> > dp(len + 1, vector<int>(sum + 1, 0));

    // There is always sum equals zero
    for (int i = 0; i <= len; i++)
        dp[i][0]++;

    // Fill up the dp table
    for (int i = 1; i <= len; i++) {

        dp[i][arr[i - 1]]++;
        for (int j = 1; j <= sum; j++) {

            if (dp[i - 1][j] > 0) {
                dp[i][j]++;
                dp[i][j + arr[i - 1]]++;
            }
        }
    }

    // Initialize the counter
    int count = 0;
    for (int j = 1; j <= sum; j++)

        // Check if the sum exists
        if (dp[len][j] > 0)

            // check sum is divisible by m
            if (j % m == 0)
                count += dp[len][j];

    return count;
}

// Driver Code
int main()
{
    vector<int> arr{ 1, 2, 3 };
    int m = 3;
    int len = arr.size();
    cout << sumSubSequence(arr, len, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program which returns the Number of sub sequences
// (or subsets) which are divisible by m.

class GFG
{

// Use Dynamic Programming to find
// sum of subsequences.
static int sumSubSequence(int []arr, int len, int m)
{
    // Find sum pf array elements
    int sum = 0;
    for (int x : arr)
    {
        sum += x;
    }

    // dp[i][j] would be > 0 if arr[0..i-1] has
    // a subsequence with sum equal to j.
    int [][]dp = new int[len + 1][sum + 1];

    // There is always sum equals zero
    for (int i = 0; i <= len; i++)
        dp[i][0]++;

    // Fill up the dp table
    for (int i = 1; i <= len; i++)
    {

        dp[i][arr[i - 1]]++;
        for (int j = 1; j <= sum; j++)
        {

            if (dp[i - 1][j] > 0)
            {
                dp[i][j]++;
                dp[i][j + arr[i - 1]]++;
            }
        }
    }

    // Initialize the counter
    int count = 0;
    for (int j = 1; j <= sum; j++)

        // Check if the sum exists
        if (dp[len][j] > 0)

            // check sum is divisible by m
            if (j % m == 0)
                count += dp[len][j];

    return count;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 1, 2, 3 };
    int m = 3;
    int len = arr.length;
    System.out.print(sumSubSequence(arr, len, m) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program which returns
# the Number of sub sequences
# (or subsets) which are divisible by m.

# Use Dynamic Programming to find
# sum of subsequences.
def sumSubSequence(arr, length, m):

    # Find sum pf array elements
    summ = 0
    for i in arr:
        summ += i

    # dp[i][j] would be > 0 if arr[0..i-1] has
    # a subsequence with sum equal to j.
    dp = [[0 for i in range(summ + 1)]
             for j in range(length + 1)]

    # There is always sum equals zero
    for i in range(length + 1):
        dp[i][0] += 1

    # Fill up the dp table
    for i in range(1, length + 1):
        dp[i][arr[i - 1]] += 1
        for j in range(1, summ + 1):
            if dp[i - 1][j] > 0:
                dp[i][j] += 1
                dp[i][j + arr[i - 1]] += 1

    # Initialize the counter
    count = 0
    for i in range(1, summ + 1):

        # Check if the sum exists
        if dp[length][i] > 0:

            # check sum is divisible by m
            if i % m == 0:
                count += dp[length][i]

    return count

# Driver Code
if __name__ == "__main__":
    arr = [1, 2, 3]
    m = 3
    length = len(arr)
    print(sumSubSequence(arr, length, m))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program which returns
// the Number of sub sequences
// (or subsets) which are
// divisible by m.
using System;
class GFG{

// Use Dynamic Programming
// to find sum of subsequences.
static int sumSubSequence(int []arr,
                          int len,
                          int m)
{
  // Find sum pf array elements
  int sum = 0;
  foreach (int x in arr)
  {
    sum += x;
  }

  // dp[i][j] would be > 0 if
  // arr[0..i-1] has a
  // subsequence with sum equal
  // to j.
  int [,]dp = new int[len + 1,
                      sum + 1];

  // There is always sum equals
  // zero
  for (int i = 0; i <= len; i++)
    dp[i, 0]++;

  // Fill up the dp table
  for (int i = 1; i <= len; i++)
  {
    dp[i, arr[i - 1]]++;
    for (int j = 1; j <= sum; j++)
    {
      if (dp[i - 1, j] > 0)
      {
        dp[i, j]++;
        dp[i, j + arr[i - 1]]++;
      }
    }
  }

  // Initialize the counter
  int count = 0;
  for (int j = 1; j <= sum; j++)

    // Check if the sum exists
    if (dp[len, j] > 0)

      // check sum is divisible
      // by m
      if (j % m == 0)
        count += dp[len, j];

  return count;
}

// Driver Code
public static void Main(string[] args)
{
  int []arr = {1, 2, 3};
  int m = 3;
  int len = arr.Length;
  Console.Write(
  sumSubSequence(arr,
                 len, m) + "\n");
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript program which returns the Number of sub sequences
// (or subsets) which are divisible by m.

// Use Dynamic Programming to find
// sum of subsequences.
function sumSubSequence(arr,len,m)
{
    // Find sum pf array elements
    let sum = 0;
    for (let x=0;x<arr.length;x++)
    {
        sum += arr[x];
    }

    // dp[i][j] would be > 0 if arr[0..i-1] has
    // a subsequence with sum equal to j.
    let dp = new Array(len + 1);
    for(let i=0;i<dp.length;i++)
    {
        dp[i]=new Array(sum+1);
        for(let j=0;j<dp[i].length;j++)
        {
            dp[i][j]=0;
        }
    }

    // There is always sum equals zero
    for (let i = 0; i <= len; i++)
        dp[i][0]++;

    // Fill up the dp table
    for (let i = 1; i <= len; i++)
    {

        dp[i][arr[i - 1]]++;
        for (let j = 1; j <= sum; j++)
        {

            if (dp[i - 1][j] > 0)
            {
                dp[i][j]++;
                dp[i][j + arr[i - 1]]++;
            }
        }
    }

    // Initialize the counter
    let count = 0;
    for (let j = 1; j <= sum; j++)

        // Check if the sum exists
        if (dp[len][j] > 0)

            // check sum is divisible by m
            if (j % m == 0)
                count += dp[len][j];

    return count;
}

// Driver Code
let arr=[ 1, 2, 3];
let m = 3;
let len = arr.length;
document.write(sumSubSequence(arr, len, m) +"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```

上述方法的时间复杂度为 **O(len*sum)** ，其中 len 是数组的大小，sum 是数组中所有整数的和。