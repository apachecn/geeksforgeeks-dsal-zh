# 构造位数成本之和为 K 的最大数

> 原文:[https://www . geeksforgeeks . org/construct-最大数字-其数字成本总和为-k/](https://www.geeksforgeeks.org/construct-the-largest-number-whose-sum-of-cost-of-digits-is-k/)

给定一个正整数 **K** ，以及一个由 **N( =9)** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】T5 】,使得 **arr[i]** 代表数字 **(i+1)** 的成本，任务是找到在范围**【1，9】**内使用数字可以形成的最大数字，使得形成的数字的数字成本之和为**K****

**示例:**

> **输入:** K = 14，arr[] = {3，12，9，5，3，4，6，5，10}
> **输出:** 8555
> **解释:**
> 一个可以形成成本 K 的可能数字是，8555。包含数字 8 的成本是 arr[7]( =5)，数字 5 是 arr[2]( =3)。
> 因此，总成本为(5+3*3 = 14)。所以 8555 形成的数字是这个成本下最大可能的数字。
> 
> **输入:** K = 5，arr[] = {3，12，9，5，3，4，6，5，10}
> **输出:** 8
> **解释:**
> 一个可以形成成本 K 的可能数字是，8。包含数字 8 的成本是 arr[7]( =5)。
> 因此，总成本为(5 = 5)。所以用这个代价形成的数字 8 是最大可能的数字。

**方法:**给定的问题可以基于以下观察来解决:

1.  问题是 [0/1 无界背包](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-items-allowed/) 的变化，因为选择形成最大数字的数字也可以重复，它们的成本总和必须是 **K** 。
2.  因此，其思想是重复地包括或排除每个可能的数字，以形成最大的数字，并打印在所有可能的组合之后获得的最大数字。
3.  上述思路可以按照以下[递推关系](https://www.geeksforgeeks.org/algorithms-gq/analysis-of-algorithms-recurrences-gq/)来实现:
    *   记录每一步用来形成数字的**数字**和剩余的和 **K** 。
    *   递归关系的基本条件是:
        1.  如果总和 **K** 变成 **0** ，那么这将产生所形成的数字组合之一。
        2.  如果 **K** 为负或者遍历了所有数组，那么就不可能形成任何成本之和为 **K** 的数。
    *   在每一步，首先包括然后排除任意数字 **D** 和[递归调用](https://www.geeksforgeeks.org/recursion/)[函数](https://www.geeksforgeeks.org/functions-in-c/)的，分别更新剩余成本 **K** 。

按照以下步骤解决给定的问题:

*   初始化大小为 **10*K** 的**2D 数组表示 **dp[][]** ，使得 **dp[i][j]** 存储通过使用具有和 **j** 的第一个 **i** 数字形成的最大数字。**
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，说**递归(I，K)** 其中起始索引，和 **K** ，执行如下步骤:
    1.  将基本情况定义为 **:**
        *   如果总和 **K** 的值变为 **0** ，则从函数中返回一个空字符串作为数字成本总和已经形成的数字。
        *   如果总和 **K** 的值小于 **0** 或 **i** 等于 **N，**则从函数返回**“0”**，因为无法形成数字。
    2.  如果当前状态 **dp[i][N]** 已经计算出来，那么[从功能](https://www.geeksforgeeks.org/c-function-argument-return-values/)返回该值。
    3.  将当前数字 **i+1** 作为 **to_string(i+1) +递归(0，K–arr[D])**的结果存储在变量中，比如说**包含**。
    4.  将排除当前数字 **i+1** 得到的结果作为**递归(i+1，K–arr[D])**存储在变量中，比如说**排除。**
*   将当前 [DP 状态](https://www.geeksforgeeks.org/solve-dynamic-programming-problem/)**DP【I】【K】**更新为 **max(包括，排除)**，并从函数中返回该值。
*   完成上述步骤后，调用递归函数**递归(0，K)** ，检查返回的[字符串](https://www.geeksforgeeks.org/string-data-structure/)是否为空，然后打印**“0”**。否则，将返回的字符串打印为最终形成的最大数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to find the maximum number
// among the two numbers S and T
string getMaximum(string& S, string& T)
{
    // If "0" exists in the string S
    if (S.find("0") != string::npos)
        return T;

    // If "0" exists in the string T
    if (T.find("0") != string::npos)
        return S;

    // Else return the maximum number
    // formed
    return (S.length() > T.length() ? S : T);
}

// Recursive function to find maximum
// number formed such that the sum of
// cost of digits of formed number is K
string recursion(int arr[], int idx,
                 int N, int K,
                 vector<vector<string> >& dp)
{
    // Base Case
    if (K == 0) {
        return "";
    }
    if (K < 0 or idx == N) {
        return "0";
    }

    // Return the stored state
    if (dp[idx][K] != "-1")
        return dp[idx][K];

    // Including the digit (idx + 1)
    string include
        = to_string(idx + 1)
          + recursion(arr, 0, N,
                      K - arr[idx], dp);

    // Excluding the digit (idx + 1)
    string exclude = recursion(
        arr, idx + 1, N, K, dp);

    // Store the result and return
    return dp[idx][K] = getMaximum(
               include, exclude);
}

// Function to find the maximum number
// formed such that the sum of the cost
// digits in the formed number is K
string largestNumber(int arr[], int N, int K)
{
    // Stores all Dp-states
    vector<vector<string> > dp(
        N + 1, vector<string>(K + 1,
                              "-1"));

    // Recursive Call
    string ans = recursion(arr, 0, N,
                           K, dp);

    // Return the result
    return (ans == "" ? "0" : ans);
}

// Driver Code
int main()
{
    int arr[] = { 3, 12, 9, 5, 3, 4, 6, 5, 10 };
    int K = 14;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << largestNumber(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
  // Function to find the maximum number
  // among the two numbers S and T
  static String getMaximum(String S, String T)
  {

    // If "0" exists in the string S
    if (S.indexOf("0") > -1) return T;

    // If "0" exists in the string T
    if (T.indexOf("0") > -1) return S;

    // Else return the maximum number
    // formed
    return S.length() > T.length() ? S : T;
  }

  // Recursive function to find maximum
  // number formed such that the sum of
  // cost of digits of formed number is K
  static String recursion(int[] arr, int idx, int N, int K, Vector<Vector<String>> dp)
  {

    // Base Case
    if (K == 0) {
      return "";
    }
    if (K < 0 || idx == N) {
      return "0";
    }

    // Return the stored state
    if (dp.get(idx).get(K) != "-1") return dp.get(idx).get(K);

    // Including the digit (idx + 1)
    String include = String.valueOf(idx + 1) + recursion(arr, 0, N, K - arr[idx], dp);

    // Excluding the digit (idx + 1)
    String exclude = recursion(arr, idx + 1, N, K, dp);

    // Store the result and return
    dp.get(idx).set(K, getMaximum(include, exclude));
    return dp.get(idx).get(K);
  }

  // Function to find the maximum number
  // formed such that the sum of the cost
  // digits in the formed number is K
  static String largestNumber(int[] arr, int N, int K)
  {

    // Stores all Dp-states
    Vector<Vector<String>> dp = new Vector<Vector<String>>();
    for(int i = 0; i < N + 1; i++)
    {
      dp.add(new Vector<String>());
      for(int j = 0; j < K + 1; j++)
      {
        dp.get(i).add("-1");
      }
    }

    // Recursive Call
    String ans = recursion(arr, 0, N, K, dp);

    // Return the result
    return ans == "" ? "0" : ans;
  }

  public static void main(String[] args) {
    int[] arr = {3, 12, 9, 5, 3, 4, 6, 5, 10};
    int K = 14;
    int N = arr.length;

    System.out.print(largestNumber(arr, N, K));
  }
}

// This code is contributed by decode2207.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum number
# among the two numbers S and T
def getMaximum(S, T):

  # If "0" exists in the string S
  if (S.count("0") > 0):
      return T;

  # If "0" exists in the string T
  if (T.count("0") > 0):
      return S;

  # Else return the maximum number
  # formed
  return S if len(S) > len(T) else T;

# Recursive function to find maximum
# number formed such that the sum of
# cost of digits of formed number is K
def recursion(arr, idx, N, K, dp):

  # Base Case
    if (K == 0):
        return "";

    if (K < 0 or idx == N):
        return "0";

    # Return the stored state
    if (dp[idx][K] != "-1"):
        return dp[idx][K];

    # Including the digit (idx + 1)
    include = str(idx + 1) + recursion(arr, 0, N, K - arr[idx], dp);

    # Excluding the digit (idx + 1)
    exclude = recursion(arr, idx + 1, N, K, dp);

    # Store the result and return
    dp[idx][K] = getMaximum(include, exclude)
    return (dp[idx][K])

# Function to find the maximum number
# formed such that the sum of the cost
# digits in the formed number is K
def largestNumber(arr, N, K):

    # Stores all Dp-states
    dp = [["-1" for i in range(K + 1)] for i in range(N + 1)]

    # Recursive Call
    ans = recursion(arr, 0, N, K, dp);

    # Return the result
    return "0" if ans == "" else ans;

# Driver Code
arr = [3, 12, 9, 5, 3, 4, 6, 5, 10];
K = 14;
N = len(arr);

print(largestNumber(arr, N, K));

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the maximum number
    // among the two numbers S and T
    static string getMaximum(string S, string T)
    {
        // If "0" exists in the string S
        if (S.IndexOf("0") > -1)
            return T;

        // If "0" exists in the string T
        if (T.IndexOf("0") > -1)
            return S;

        // Else return the maximum number
        // formed
        return (S.Length > T.Length ? S : T);
    }

    // Recursive function to find maximum
    // number formed such that the sum of
    // cost of digits of formed number is K
    static string recursion(int[] arr, int idx, int N, int K, List<List<string>> dp)
    {
        // Base Case
        if (K == 0) {
            return "";
        }
        if (K < 0 || idx == N) {
            return "0";
        }

        // Return the stored state
        if (dp[idx][K] != "-1")
            return dp[idx][K];

        // Including the digit (idx + 1)
        string include = (idx + 1).ToString() + recursion(arr, 0, N, K - arr[idx], dp);

        // Excluding the digit (idx + 1)
        string exclude = recursion(arr, idx + 1, N, K, dp);

        // Store the result and return
        return dp[idx][K] = getMaximum(include, exclude);
    }

    // Function to find the maximum number
    // formed such that the sum of the cost
    // digits in the formed number is K
    static string largestNumber(int[] arr, int N, int K)
    {
        // Stores all Dp-states
        List<List<string>> dp = new List<List<string>>();
        for(int i = 0; i < N + 1; i++)
        {
            dp.Add(new List<string>());
            for(int j = 0; j < K + 1; j++)
            {
                dp[i].Add("-1");
            }
        }

        // Recursive Call
        string ans = recursion(arr, 0, N, K, dp);

        // Return the result
        return (ans == "" ? "0" : ans);
    }

  static void Main() {
    int[] arr = {3, 12, 9, 5, 3, 4, 6, 5, 10};
    int K = 14;
    int N = arr.Length;

    Console.Write(largestNumber(arr, N, K));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum number
// among the two numbers S and T
function getMaximum(S, T)
{

  // If "0" exists in the string S
  if (S.indexOf("0") > -1) return T;

  // If "0" exists in the string T
  if (T.indexOf("0") > -1) return S;

  // Else return the maximum number
  // formed
  return S.length > T.length ? S : T;
}

// Recursive function to find maximum
// number formed such that the sum of
// cost of digits of formed number is K
function recursion(arr, idx, N, K, dp)
{

  // Base Case
  if (K == 0) {
    return "";
  }
  if (K < 0 || idx == N) {
    return "0";
  }

  // Return the stored state
  if (dp[idx][K] != "-1") return dp[idx][K];

  // Including the digit (idx + 1)
  let include = String(idx + 1) + recursion(arr, 0, N, K - arr[idx], dp);

  // Excluding the digit (idx + 1)
  let exclude = recursion(arr, idx + 1, N, K, dp);

  // Store the result and return
  return (dp[idx][K] = getMaximum(include, exclude));
}

// Function to find the maximum number
// formed such that the sum of the cost
// digits in the formed number is K
function largestNumber(arr, N, K)
{

  // Stores all Dp-states
  let dp = new Array(N + 1).fill(0).map(() => new Array(K + 1).fill(-1));

  // Recursive Call
  let ans = recursion(arr, 0, N, K, dp);

  // Return the result
  return ans == "" ? "0" : ans;
}

// Driver Code
let arr = [3, 12, 9, 5, 3, 4, 6, 5, 10];
let K = 14;
let N = arr.length;

document.write(largestNumber(arr, N, K));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
8555
```

***时间复杂度:**O(9 * K<sup>2</sup>)*
***辅助空间:** O(9*K)*