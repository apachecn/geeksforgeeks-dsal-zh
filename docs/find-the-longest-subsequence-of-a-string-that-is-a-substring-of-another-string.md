# 找出一个字符串中最长的子序列，它是另一个字符串的子串

> 原文:[https://www . geesforgeks . org/find-一个字符串中最长的子序列，也就是另一个字符串中的子字符串/](https://www.geeksforgeeks.org/find-the-longest-subsequence-of-a-string-that-is-a-substring-of-another-string/)

给定由 **N** 和 **M** 字符组成的两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **X** 和 **Y** ，任务是找到字符串 **X** 的[最长子序列，这是字符串 **Y** 的](https://www.geeksforgeeks.org/find-length-longest-subsequence-one-string-substring-another-string/) [子串](https://www.geeksforgeeks.org/substring-in-cpp/)。

**示例:**

> **输入:**X =“ABCD”，Y =“ACDBDCD”
> T3】输出: ACD
> **说明:**
> “ACD”是 X 的最长子序列，是 Y 的子串
> 
> **输入:** X = A，Y = A
> T3】输出: A

**天真方法:**解决给定问题最简单的方法是[找到给定字符串的所有子序列**X**T5】并在所有生成的子序列中打印该子序列，该子序列长度最大，](https://www.geeksforgeeks.org/print-subsequences-string/)[是 **Y** 的子串。](https://www.geeksforgeeks.org/check-string-substring-another/)

***时间复杂度:**O(N * M * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。其思想是创建维度为 **(N + 1)*(M + 1)** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **dp[][]** ，状态 **dp[i][j]** 是 **X[0，i]** 的子序列的最大长度，该子序列是 **Y[0，j]** 的子串。按照以下步骤解决问题:

*   创建一个大小为 **N+1** 行和 **M+1** 列的 [2D 阵列](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **dp[][]** 。
*   用 **0** 初始化矩阵的第一行和第一列。
*   按如下方式填充所有剩余行:
    *   如果**X【I–1】**的值等于**Y【j–1】**的值，则将**DP【I】【j】**的值更新为**(1+DP【I–1】【j–1】)**。
    *   否则，将 **dp[i][j]** 的值更新为**DP[I–1][j]**。
*   通过迭代矩阵中的最后一行，将所需序列的最大长度存储在变量 **len** 中，并将最大单元格值的行和列索引分别存储在变量 **i** 和 **j** 中。
*   创建一个变量，比如说 **res** 来存储结果字符串并从最大单元格值回溯。
*   [迭代直到**透镜**的值大于 **0** ，执行以下步骤:](https://www.geeksforgeeks.org/c-c-do-while-loop-with-examples/)
    *   如果**X[I–1]**的值等于**Y[j–1]**的值，则将**X[I–1]**追加到 **res** 并将 **len** 、 **i** 和 **j** 的值减 1。
    *   否则，将 **i** 的值减 1。
*   完成上述步骤后，打印字符串 **res** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest
// subsequence that matches with
// the substring of other string
string longestSubsequence(string X, string Y)
{

    // Stores the lengths of strings
    // X and Y
    int n = X.size();
    int m = Y.size();

    // Create a matrix
    vector<vector<int>> mat(n + 1, vector<int>(m + 1));

    // Initialize the matrix
    for(int i = 0; i < n + 1; i++)
    {
        for(int j = 0; j < m + 1; j++)
        {
            if (i == 0 || j == 0)
                mat[i][j] = 0;
        }
    }

    // Fill all the remaining rows
    for(int i = 1; i < n + 1; i++)
    {
        for(int j = 1; j < m + 1; j++)
        {

            // If the characters are equal
            if (X[i - 1] == Y[j - 1])
            {
                mat[i][j] = 1 + mat[i - 1][j - 1];
            }

            // If not equal, then
            // just move to next
            // in subsequence string
            else
            {
                mat[i][j] = mat[i - 1][j];
            }
        }
    }

    // Find maximum length of the
    // longest subsequence matching
    // substring of other string
    int len = 0, col = 0;

    // Iterate through the last
    // row of matrix
    for(int i = 0; i < m + 1; i++)
    {
        if (mat[n][i] > len)
        {
            len = mat[n][i];
            col = i;
        }
    }

    // Store the required string
    string res = "";
    int i = n;
    int j = col;

    // Backtrack from the cell
    while (len > 0)
    {

        // If equal, then add the
        // character to res string
        if (X[i - 1] == Y[j - 1])
        {
            res = X[i - 1] + res;
            i--;
            j--;
            len--;
        }
        else
        {
            i--;
        }
    }

    // Return the required string
    return res;
}

// Driver code
int main()
{
    string X = "ABCD";
    string Y = "ACDBDCD";

    cout << (longestSubsequence(X, Y));

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the longest
    // subsequence that matches with
    // the substring of other string
    public static String longestSubsequence(
        String X, String Y)
    {

        // Stores the lengths of strings
        // X and Y
        int n = X.length();
        int m = Y.length();

        // Create a matrix
        int[][] mat = new int[n + 1][m + 1];

        // Initialize the matrix
        for (int i = 0; i < n + 1; i++) {
            for (int j = 0; j < m + 1; j++) {
                if (i == 0 || j == 0)
                    mat[i][j] = 0;
            }
        }

        // Fill all the remaining rows
        for (int i = 1;
             i < n + 1; i++) {

            for (int j = 1;
                 j < m + 1; j++) {

                // If the characters are equal
                if (X.charAt(i - 1)
                    == Y.charAt(j - 1)) {
                    mat[i][j] = 1
                                + mat[i - 1][j - 1];
                }

                // If not equal, then
                // just move to next
                // in subsequence string
                else {
                    mat[i][j] = mat[i - 1][j];
                }
            }
        }

        // Find maximum length of the
        // longest subsequence matching
        // substring of other string
        int len = 0, col = 0;

        // Iterate through the last
        // row of matrix
        for (int i = 0; i < m + 1; i++) {

            if (mat[n][i] > len) {
                len = mat[n][i];
                col = i;
            }
        }

        // Store the required string
        String res = "";
        int i = n;
        int j = col;

        // Backtrack from the cell
        while (len > 0) {

            // If equal, then add the
            // character to res string
            if (X.charAt(i - 1)
                == Y.charAt(j - 1)) {

                res = X.charAt(i - 1) + res;
                i--;
                j--;
                len--;
            }
            else {
                i--;
            }
        }

        // Return the required string
        return res;
    }

    // Driver Code
    public static void main(String args[])
    {
        String X = "ABCD";
        String Y = "ACDBDCD";
        System.out.println(
            longestSubsequence(X, Y));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest
# subsequence that matches with
# the substring of other string
def longestSubsequence(X, Y):

    # Stores the lengths of strings
    # X and Y
    n = len(X)
    m = len(Y)

    # Create a matrix
    mat = [[0 for i in range(m + 1)]
              for j in range(n + 1)]

    # Initialize the matrix
    for i in range(0, n + 1):
        for j in range(0, m + 1):
            if (i == 0 or j == 0):
                mat[i][j] = 0

    # Fill all the remaining rows
    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # If the characters are equal
            if (X[i - 1] == Y[j - 1]):
                mat[i][j] = 1 + mat[i - 1][j - 1]

            # If not equal, then
            # just move to next
            # in subsequence string
            else:
                mat[i][j] = mat[i - 1][j]

    # Find maximum length of the
    # longest subsequence matching
    # substring of other string
    len1 = 0
    col = 0

    # Iterate through the last
    # row of matrix
    for i in range(0, m + 1):
        if (mat[n][i] > len1):
            len1 = mat[n][i]
            col = i

    # Store the required string
    res = ""
    i = n
    j = col

    # Backtrack from the cell
    while (len1 > 0):

        # If equal, then add the
        # character to res string
        if (X[i - 1] == Y[j - 1]):
            res = X[i - 1] + res
            i -= 1
            j -= 1
            len1 -= 1
        else:
            i -= 1

    # Return the required string
    return res

# Driver code
X = "ABCD"
Y = "ACDBDCD"

print(longestSubsequence(X, Y))

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the longest
// subsequence that matches with
// the substring of other string
static string longestSubsequence(string X, string Y)
{
    int i, j;

    // Stores the lengths of strings
    // X and Y
    int n = X.Length;
    int m = Y.Length;

    // Create a matrix
    int [,]mat = new int[n + 1, m + 1];

    // Initialize the matrix
    for(i = 0; i < n + 1; i++)
    {
        for(j = 0; j < m + 1; j++)
        {
            if (i == 0 || j == 0)
                mat[i,j] = 0;
        }
    }

    // Fill all the remaining rows
    for(i = 1; i < n + 1; i++)
    {
        for(j = 1; j < m + 1; j++)
        {

            // If the characters are equal
            if (X[i - 1] == Y[j - 1])
            {
                mat[i, j] = 1 + mat[i - 1, j - 1];
            }

            // If not equal, then
            // just move to next
            // in subsequence string
            else
            {
                mat[i, j] = mat[i - 1, j];
            }
        }
    }

    // Find maximum length of the
    // longest subsequence matching
    // substring of other string
    int len = 0, col = 0;

    // Iterate through the last
    // row of matrix
    for(i = 0; i < m + 1; i++)
    {
        if (mat[n,i] > len)
        {
            len = mat[n,i];
            col = i;
        }
    }

    // Store the required string
    string res = "";
    i = n;
    j = col;

    // Backtrack from the cell
    while (len > 0)
    {

        // If equal, then add the
        // character to res string
        if (X[i - 1] == Y[j - 1])
        {
            res = X[i - 1] + res;
            i--;
            j--;
            len--;
        }
        else
        {
            i--;
        }
    }

    // Return the required string
    return res;
}

// Driver Code
public static void Main()
{
    string X = "ABCD";
    string Y = "ACDBDCD";

    Console.Write(longestSubsequence(X, Y));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the longest
// subsequence that matches with
// the substring of other string
function longestSubsequence(X,Y)
{
        // Stores the lengths of strings
        // X and Y
        let n = X.length;
        let m = Y.length;

        // Create a matrix
        let mat = new Array(n + 1);

        // Initialize the matrix
        for (let i = 0; i < n + 1; i++) {
            mat[i]=new Array(m+1);
            for (let j = 0; j < m + 1; j++) {
                if (i == 0 || j == 0)
                    mat[i][j] = 0;
            }
        }

        // Fill all the remaining rows
        for (let i = 1;
             i < n + 1; i++) {

            for (let j = 1;
                 j < m + 1; j++) {

                // If the characters are equal
                if (X[i-1]
                    == Y[j-1]) {
                    mat[i][j] = 1
                                + mat[i - 1][j - 1];
                }

                // If not equal, then
                // just move to next
                // in subsequence string
                else {
                    mat[i][j] = mat[i - 1][j];
                }
            }
        }

        // Find maximum length of the
        // longest subsequence matching
        // substring of other string
        let len = 0, col = 0;

        // Iterate through the last
        // row of matrix
        for (let i = 0; i < m + 1; i++) {

            if (mat[n][i] > len) {
                len = mat[n][i];
                col = i;
            }
        }

        // Store the required string
        let res = "";
        let i = n;
        let j = col;

        // Backtrack from the cell
        while (len > 0) {

            // If equal, then add the
            // character to res string
            if (X[i-1]
                == Y[j-1]) {

                res = X[i-1] + res;
                i--;
                j--;
                len--;
            }
            else {
                i--;
            }
        }

        // Return the required string
        return res;
}

// Driver Code
let X = "ABCD";
let Y = "ACDBDCD";
document.write(longestSubsequence(X, Y));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
ACD
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*