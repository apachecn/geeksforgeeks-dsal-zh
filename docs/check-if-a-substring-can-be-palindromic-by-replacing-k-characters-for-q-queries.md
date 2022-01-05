# 通过为 Q 查询替换 K 个字符来检查子串是否可以回文

> 原文:[https://www . geeksforgeeks . org/check-if-a-substring-be-回文-通过替换-k-characters-for-q-query/](https://www.geeksforgeeks.org/check-if-a-substring-can-be-palindromic-by-replacing-k-characters-for-q-queries/)

给定一个字符串 **str** 和 **Q** 以**【L，R，K】**的形式查询，任务是从最多允许 **K** 变化的**【L，R】**的字符串中找出字符是否可以重新排列，使字符串回文。对于每个查询，如果可以变成回文串，则打印**“是”**，否则打印**“否”**。
**示例:**

> **输入:** str = "GeeksforGeeks "，Q = { { 1，5，3 }、{ 5，7，0 }、{ 8，11，3 }、{3，10，5 }、{ 0，9，5 } }
> **输出:**
> YES
> NO
> YES
> YES
> YES
> **解释:**
> 查询[0] : substring = "eeksf "，可改为“eeksf”
> 查询[1]:substring =“for”，不是回文，替换 atmost 0 字符后不能回文..
> 查询[2]:substring =“Gee”，可以改为“GeG”，是回文。
> 查询[3]:substring =“ksforge”，可以改为“ksfoofsk”，这是回文。
> 查询[4]:substring =“geesforge”，可以改为“GeeksskeeG”，这是回文。
> **输入:** str = "abczwerte "，Q = { { 3，7，4 }，{ 1，8，10 }，{ 0，3，1 } }
> **输出:**
> 是
> 是
> 否

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

*   创建一个 2D 矩阵(比如说 **dp[i][j]** )，其中 dp[i][j]表示子串 **str[0…j]** 中带有字符的**的计数。**
*   下面是上述方法的递归关系:
    *   如果 str[i]等于 str[j]，则 **dp[i][j] = 1 + dp[i][j-1]** 。
    *   如果 str[i]不等于 str[j]，则 **dp[i][j] = dp[i][j-1]** 。
    *   如果 j 等于 0，那么 dp[i][j]将是第一个等于第一个字符的字符之一。
*   对于每个查询，通过以下简单关系找出子串**串【L…R】**中每个字符的个数:

```
count =  dp[i][right] - dp[i][left] + (str[left] == i + 'a').
```

*   获取不匹配对的计数。
*   现在我们需要将一半不匹配的字符转换为剩余的字符。如果一半不匹配字符的计数小于或等于 **K** ，则**打印“是”，否则打印“否”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find whether string can
// be made palindromic or not for each queries
void canMakePaliQueries(
    string str,
    vector<vector<int> >& Q)
{
    int n = str.length();

    // To store the count of ith character
    // of substring str[0...i]
    vector<vector<int> > dp(
        26,
        vector<int>(n, 0));

    for (int i = 0; i < 26; i++) {

        // Current character
        char currentChar = i + 'a';
        for (int j = 0; j < n; j++) {

            // Update dp[][] on the basis
            // recurrence relation
            if (j == 0) {
                dp[i][j]
                    = (str[j] == currentChar);
            }
            else {
                dp[i][j]
                    = dp[i][j - 1]
                      + (str[j] == currentChar);
            }
        }
    }

    // For each queries
    for (auto query : Q) {
        int left = query[0];
        int right = query[1];
        int k = query[2];

        // To store the count of
        // distinct character
        int unMatchedCount = 0;
        for (int i = 0; i < 26; i++) {

            // Find occurrence of i + 'a'
            int occurrence
                = dp[i][right]
                  - dp[i][left]
                  + (str[left] == (i + 'a'));

            if (occurrence & 1)
                unMatchedCount++;
        }

        // Half the distinct Count
        int ans = unMatchedCount / 2;

        // If half the distinct count is
        // less than equals to K then
        // palindromic string can be made
        if (ans <= k) {
            cout << "YES\n";
        }
        else {
            cout << "NO\n";
        }
    }
}

// Driver Code
int main()
{
    // Given string str
    string str = "GeeksforGeeks";

    // Given Queries
    vector<vector<int> > Q;
    Q = { { 1, 5, 3 }, { 5, 7, 0 },
 { 8, 11, 3 }, { 3, 10, 5 },
{ 0, 9, 5 } };

    // Function call
    canMakePaliQueries(str, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find whether String can be
// made palindromic or not for each queries
static void canMakePaliQueries(String str,
                               int [][]Q)
{
    int n = str.length();

    // To store the count of ith character
    // of subString str[0...i]
    int [][]dp = new int[26][n];

    for(int i = 0; i < 26; i++)
    {

       // Current character
       char currentChar = (char)(i + 'a');
       for(int j = 0; j < n; j++)
       {

          // Update dp[][] on the basis
          // recurrence relation
          if (j == 0)
          {
              dp[i][j] = (str.charAt(j) ==
                          currentChar) ? 1 : 0;
          }
          else
          {
              dp[i][j] = dp[i][j - 1] +
                         ((str.charAt(j) ==
                           currentChar) ? 1 : 0);
          }
       }
    }

    // For each queries
    for(int []query : Q)
    {
       int left = query[0];
       int right = query[1];
       int k = query[2];

       // To store the count of
       // distinct character
       int unMatchedCount = 0;
       for(int i = 0; i < 26; i++)
       {

          // Find occurrence of i + 'a'
          int occurrence = dp[i][right] -
                           dp[i][left] +
                           (str.charAt(left) ==
                           (i + 'a') ? 1 : 0);

          if (occurrence % 2 == 1)
              unMatchedCount++;
       }

       // Half the distinct Count
       int ans = unMatchedCount / 2;

       // If half the distinct count is
       // less than equals to K then
       // palindromic String can be made
       if (ans <= k)
       {
           System.out.print("YES\n");
       }
       else
       {
           System.out.print("NO\n");
       }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given a String str
    String str = "GeeksforGeeks";

    // Given Queries
    int [][]Q = { { 1, 5, 3 },
                  { 5, 7, 0 },
                  { 8, 11, 3 },
                  { 3, 10, 5 },
                  { 0, 9, 5 } };

    // Function call
    canMakePaliQueries(str, Q);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find whether
# string can be made palindromic
# or not for each queries
def canMakePaliQueries(str, Q):
    n = len(str)

    # To store the count of
    # ith character of substring
    # str[0...i]
    dp = [[0 for i in range(n)]
             for j in range(26)]\

    for i in range(26):

        # Current character
        currentChar = chr(i + ord('a'))

        for j in range(n):

            # Update dp[][] on the basis
            # recurrence relation
            if(j == 0):
                dp[i][j] = (str[j] ==
                            currentChar)
            else:
                dp[i][j] = dp[i][j - 1] +
                           (str[j] == currentChar)

    # For each queries
    for query in Q:
        left = query[0]
        right = query[1]
        k = query[2]

        # To store the count of
        # distinct character
        unMatchedCount = 0

        for i in range(26):

            # Find occurrence of
            # i + 'a'
            occurrence = dp[i][right] -
                         dp[i][left] +
                         (str[left] ==
                          chr(i + ord('a')))

            if(occurrence & 1):
                unMatchedCount += 1

         # Half the distinct Count
        ans = int(unMatchedCount / 2)

        # If half the distinct count is
        # less than equals to K then
        # palindromic string can be made
        if(ans <= k):
            print("YES")
        else:
            print("NO")

# Driver Code

# Given string str
str = "GeeksforGeeks"

# Given Queries
Q = [[1, 5, 3],
     [5, 7, 0],
     [8, 11, 3],
     [3, 10, 5],
     [0, 9, 5]]

# Function call
canMakePaliQueries(str, Q)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find whether String can be
// made palindromic or not for each queries
static void canMakePaliQueries(String str,
                               int [,]Q)
{
    int n = str.Length;

    // To store the count of ith character
    // of subString str[0...i]
    int [,]dp = new int[26, n];

    for(int i = 0; i < 26; i++)
    {

       // Current character
       char currentChar = (char)(i + 'a');
       for(int j = 0; j < n; j++)
       {

          // Update [,]dp on the basis
          // recurrence relation
          if (j == 0)
          {
              dp[i,j] = (str[j] ==
                         currentChar) ? 1 : 0;
          }
          else
          {
              dp[i,j] = dp[i, j - 1] +
                         ((str[j] ==
                           currentChar) ? 1 : 0);
          }
       }
    }

    // For each queries
    for(int l = 0; l < Q.GetLength(0);l++)
    {
        int []query = GetRow(Q,l);
       int left = query[0];
       int right = query[1];
       int k = query[2];

       // To store the count of
       // distinct character
       int unMatchedCount = 0;
       for(int i = 0; i < 26; i++)
       {

          // Find occurrence of i + 'a'
          int occurrence = dp[i, right] -
                           dp[i, left] +
                           (str[left] ==
                           (i + 'a') ? 1 : 0);

          if (occurrence % 2 == 1)
              unMatchedCount++;
       }

       // Half the distinct Count
       int ans = unMatchedCount / 2;

       // If half the distinct count is
       // less than equals to K then
       // palindromic String can be made
       if (ans <= k)
       {
           Console.Write("YES\n");
       }
       else
       {
           Console.Write("NO\n");
       }
    }
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

    // Given a String str
    String str = "GeeksforGeeks";

    // Given Queries
    int [,]Q = { { 1, 5, 3 },
                 { 5, 7, 0 },
                 { 8, 11, 3 },
                 { 3, 10, 5 },
                 { 0, 9, 5 } };

    // Function call
    canMakePaliQueries(str, Q);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find whether String can be
// made palindromic or not for each queries
function canMakePaliQueries(str,Q)
{
    let n = str.length;

    // To store the count of ith character
    // of subString str[0...i]
    let dp = new Array(26);
    for(let i=0;i<26;i++)
    {
        dp[i]=new Array(n);
        for(let j=0;j<n;j++)
            dp[i][j]=0;
    }

    for(let i = 0; i < 26; i++)
    {

       // Current character
       let currentChar = String.fromCharCode(i + 'a'.charCodeAt(0));
       for(let j = 0; j < n; j++)
       {

          // Update dp[][] on the basis
          // recurrence relation
          if (j == 0)
          {
              dp[i][j] = (str[j] ==
                          currentChar) ? 1 : 0;
          }
          else
          {
              dp[i][j] = dp[i][j - 1] +
                         ((str[j] ==
                           currentChar) ? 1 : 0);
          }
       }
    }

    // For each queries
    for(let query of Q.values())
    {
       let left = query[0];
       let right = query[1];
       let k = query[2];

       // To store the count of
       // distinct character
       let unMatchedCount = 0;
       for(let i = 0; i < 26; i++)
       {

          // Find occurrence of i + 'a'
          let occurrence = dp[i][right] -
                           dp[i][left] +
                           (str[left] ==
                           (i + 'a'.charCodeAt(0)) ? 1 : 0);

          if (occurrence % 2 == 1)
              unMatchedCount++;
       }

       // Half the distinct Count
       let ans = unMatchedCount / 2;

       // If half the distinct count is
       // less than equals to K then
       // palindromic String can be made
       if (ans <= k)
       {
           document.write("YES<br>");
       }
       else
       {
           document.write("NO<br>");
       }
    }
}

// Driver Code

// Given a String str
let str = "GeeksforGeeks";

// Given Queries
let Q=[[ 1, 5, 3 ],
                  [ 5, 7, 0 ],
                  [ 8, 11, 3 ],
                  [ 3, 10, 5 ],
                  [ 0, 9, 5 ]];
// Function call
canMakePaliQueries(str, Q);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
YES
NO
YES
YES
YES
```

***时间复杂度:** O(26*N)，其中 N 是字符串的长度。*
***辅助空间:** O(26*N)，其中 N 为弦的长度。*