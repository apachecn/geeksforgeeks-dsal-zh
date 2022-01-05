# 检查给定字符串中是否存在给定模式

> 原文:[https://www . geesforgeks . org/check-if-a-给定模式-存在于给定字符串中-or-not/](https://www.geeksforgeeks.org/check-if-a-given-pattern-exists-in-a-given-string-or-not/)

给定两个长度分别为 **M** 和 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **文本**和**模式**，任务是检查**模式**是否与**文本**匹配。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**注:** **图案**可以包含字符**' ***和**'**

*   **' ***匹配当前字符前零次或多次出现的字符
*   **'**匹配任何信号字符。

**示例:**

> **输入:**pattern = " ge * ksforgeks "，text = " geeks forgeks "
> T3】输出: Yes
> **解释:**
> 将*替换为' e '，修改模式等于“geeks forgeks”。
> 因此，要求的输出为是。
> 
> **输入:** pattern = "ab*d "，text = "abcds"
> **输出:**否
> **说明:**给定的模式无法与文本匹配。

**天真方法:**解决这个问题最简单的方法是[使用](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)[递归](https://www.geeksforgeeks.org/recursion/)遍历两个字符串的字符。如果当前字符是**' . '**，将当前字符替换为任意字符，并对剩余的**模式**和**文本**字符串重复出现。否则，如果当前字符是**' ***，则对剩余的文本重复出现，并检查它是否与模式的其余部分匹配。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O((M+N)* 2<sup>(M+N/2)</sup>)*
***辅助空间:**O((M+N)* 2<sup>(M+N/2)</sup>)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。以下是循环关系:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)， **dp[M + 1][N + 1]** ，其中 **dp[i][j]** 检查子串 **{ text[0]，…，text[i] }** 是否与子串 **{ pattern[0]，… pattern[j] }** 匹配。
*   [迭代两个字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并根据以下递归关系填充 **dp[][]** 数组:
    *   如果**文本【I】**和**图案【j】**相同，则填充 **dp[i + 1][j + 1] = dp[i][j]** 。
    *   如果**模式【j】**是**' '**然后填充 **dp[i + 1][j + 1] = dp[i][j]。**
    *   如果**模式【j】**为**' ***，则检查以下条件:
        *   如果**文本【I】**不等于**模式【j–1】**和**模式【j–1】**不等于**'**，然后填充**DP[I+1][j+1]= DP[I+1][j–1]**。
        *   否则，填充**DP[I+1][j+1]=(DP[I+1][j]| | DP[I][j+1]| | DP[I+1][j–1])**。
*   最后，打印 **dp[M][N]** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the pattern
// consisting of '*', '.' and lowercase
// characters matches the text or not
int isMatch(string text, string pattern)
{

  // Base Case
  if (text == "" or pattern == "")
    return false;

  // Stores length of text
  int N = text.size();

  // Stores length of pattern
  int M = pattern.size();

  // dp[i][j]: Check if { text[0], .. text[i] }
  // matches {pattern[0], ... pattern[j]} or not
  vector<vector<bool>> dp(N + 1, vector<bool>(M + 1, false));

  // Base Case
  dp[0][0] = true;

  // Iterate over the characters
  // of the string pattern
  for (int i = 0; i < M; i++)
  {
    if (pattern[i] == '*'
        && dp[0][i - 1]) {

      // Update dp[0][i + 1]
      dp[0][i + 1] = true;
    }
  }

  // Iterate over the characters
  // of both the strings
  for (int i = 0; i < N; i++) {

    for (int j = 0; j < M; j++) {

      // If current character
      // in the pattern is '.'
      if (pattern[j] == '.') {

        // Update dp[i + 1][j + 1]
        dp[i + 1][j + 1] = dp[i][j];
      }

      // If current character in
      // both the strings are equal
      if (pattern[j]
          == text[i]) {

        // Update dp[i + 1][j + 1]
        dp[i + 1][j + 1] = dp[i][j];
      }

      // If current character
      // in the pattern is '*'
      if (pattern[j] == '*') {

        if (pattern[j - 1] != text[i]
            && pattern[j - 1] != '.') {

          // Update dp[i + 1][j + 1]
          dp[i + 1][j + 1] = dp[i + 1][j - 1];
        }

        else {

          // Update dp[i+1][j+1]
          dp[i + 1][j + 1] = (dp[i + 1][j]
                              or dp[i][j + 1]
                              or dp[i + 1][j - 1]);
        }
      }
    }
  }

  // Return dp[M][N]
  return dp[N][M];
}

// Driver Code
int main()
{
  string text = "geeksforgeeks";
  string pattern = "ge*ksforgeeks";

  if (isMatch(text, pattern))
    cout<<"Yes";
  else
    cout<<"No";
}

// This code is contributed by mohiy kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to check if the pattern
    // consisting of '*', '.' and lowercase
    // characters matches the text or not
    static boolean isMatch(String text,
                           String pattern)
    {
        // Base Case
        if (text == null || pattern == null) {
            return false;
        }

        // Stores length of text
        int N = text.length();

        // Stores length of pattern
        int M = pattern.length();

        // dp[i][j]: Check if { text[0], .. text[i] }
        // matches {pattern[0], ... pattern[j]} or not
        boolean[][] dp = new boolean[N + 1][M + 1];

        // Base Case
        dp[0][0] = true;

        // Iterate over the characters
        // of the string pattern
        for (int i = 0; i < M; i++) {
            if (pattern.charAt(i) == '*'
                && dp[0][i - 1]) {

                // Update dp[0][i + 1]
                dp[0][i + 1] = true;
            }
        }

        // Iterate over the characters
        // of both the strings
        for (int i = 0; i < N; i++) {

            for (int j = 0; j < M; j++) {

                // If current character
                // in the pattern is '.'
                if (pattern.charAt(j) == '.') {

                    // Update dp[i + 1][j + 1]
                    dp[i + 1][j + 1] = dp[i][j];
                }

                // If current character in
                // both the strings are equal
                if (pattern.charAt(j)
                    == text.charAt(i)) {

                    // Update dp[i + 1][j + 1]
                    dp[i + 1][j + 1] = dp[i][j];
                }

                // If current character
                // in the pattern is '*'
                if (pattern.charAt(j) == '*') {

                    if (pattern.charAt(j - 1) != text.charAt(i)
                        && pattern.charAt(j - 1) != '.') {

                        // Update dp[i + 1][j + 1]
                        dp[i + 1][j + 1] = dp[i + 1][j - 1];
                    }

                    else {

                        // Update dp[i+1][j+1]
                        dp[i + 1][j + 1] = (dp[i + 1][j]
                                            || dp[i][j + 1]
                                            || dp[i + 1][j - 1]);
                    }
                }
            }
        }

        // Return dp[M][N]
        return dp[N][M];
    }

    // Driver Code
    public static void main(String[] args)
    {
        String text = "geeksforgeeks";
        String pattern = "ge*ksforgeeks";

        if (isMatch(text, pattern)) {

            System.out.println("Yes");
        }
        else {

            System.out.println("No");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import numpy as np

# Function to check if the pattern
# consisting of '*', '.' and lowercase
# characters matches the text or not
def isMatch(text, pattern):

  # Base Case
  if (text == "" or pattern == ""):
    return False

  # Stores length of text
  N = len(text)

  # Stores length of pattern
  M = len(pattern)

  # dp[i][j]: Check if { text[0], .. text[i] }
  # matches {pattern[0], ... pattern[j]} or not
  dp = np.zeros((N + 1, M + 1))

  # Base Case
  dp[0][0] = True

  # Iterate over the characters
  # of the string pattern
  for i in range(M):
    if (pattern[i] == '*' and dp[0][i - 1]):

      # Update dp[0][i + 1]
      dp[0][i + 1] = True

  # Iterate over the characters
  # of both the strings
  for i in range(N):
    for j in range(M):

      # If current character
      # in the pattern is '.'
      if (pattern[j] == '.'):

        # Update dp[i + 1][j + 1]
        dp[i + 1][j + 1] = dp[i][j]

      # If current character in
      # both the strings are equal
      if (pattern[j] == text[i]):

        # Update dp[i + 1][j + 1]
        dp[i + 1][j + 1] = dp[i][j]

      # If current character
      # in the pattern is '*'
      if (pattern[j] == '*'):
        if (pattern[j - 1] != text[i] and
            pattern[j - 1] != '.'):

          # Update dp[i + 1][j + 1]
          dp[i + 1][j + 1] = dp[i + 1][j - 1]

        else:

          # Update dp[i+1][j+1]
          dp[i + 1][j + 1] = (dp[i + 1][j] or
                              dp[i][j + 1] or
                              dp[i + 1][j - 1])

  # Return dp[M][N]
  return dp[N][M]

# Driver Code
if __name__ == "__main__" :

  text = "geeksforgeeks"
  pattern = "ge*ksforgeeks"

  if (isMatch(text, pattern)):
    print("Yes")
  else:
    print("No")

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the pattern
// consisting of '*', '.' and lowercase
// characters matches the text or not
static bool isMatch(string text, string pattern)
{

    // Base Case
    if (text == null || pattern == null)
    {
        return false;
    }

    // Stores length of text
    int N = text.Length;

    // Stores length of pattern
    int M = pattern.Length;

    // dp[i][j]: Check if { text[0], .. text[i] }
    // matches {pattern[0], ... pattern[j]} or not
    bool[,] dp = new bool[N + 1, M + 1];

    // Base Case
    dp[0, 0] = true;

    // Iterate over the characters
    // of the string pattern
    for(int i = 0; i < M; i++)
    {
        if (pattern[i] == '*' && dp[0, i - 1])
        {

            // Update dp[0][i + 1]
            dp[0, i + 1] = true;
        }
    }

    // Iterate over the characters
    // of both the strings
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {

            // If current character
            // in the pattern is '.'
            if (pattern[j] == '.')
            {

                // Update dp[i + 1][j + 1]
                dp[i + 1, j + 1] = dp[i, j];
            }

            // If current character in
            // both the strings are equal
            if (pattern[j] == text[i])
            {

                // Update dp[i + 1][j + 1]
                dp[i + 1, j + 1] = dp[i, j];
            }

            // If current character
            // in the pattern is '*'
            if (pattern[j] == '*')
            {
                if (pattern[j - 1] != text[i] &&
                    pattern[j - 1] != '.')
                {

                    // Update dp[i + 1][j + 1]
                    dp[i + 1, j + 1] = dp[i + 1, j - 1];
                }

                else
                {

                    // Update dp[i+1][j+1]
                    dp[i + 1, j + 1] = (dp[i + 1, j] ||
                                        dp[i, j + 1] ||
                                        dp[i + 1, j - 1]);
                }
            }
        }
    }

    // Return dp[M][N]
    return dp[N, M];
}

// Driver Code
public static void Main()
{
    string text = "geeksforgeeks";
    string pattern = "ge*ksforgeeks";

    if (isMatch(text, pattern))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if the pattern
    // consisting of '*', '.' and lowercase
    // characters matches the text or not
    function isMatch(text, pattern)
    {
        // Base Case
        if (text == null || pattern == null) {
            return false;
        }

        // Stores length of text
        let N = text.length;

        // Stores length of pattern
        let M = pattern.length;

        // dp[i][j]: Check if { text[0], .. text[i] }
        // matches {pattern[0], ... pattern[j]} or not
        let dp = new Array(N + 1);
        for (let i = 0; i <= N; i++)
        {
            dp[i] = new Array(M + 1);
            for (let j = 0; j <= M; j++)
            {
                dp[i][j] = false;
            }
        }

        // Base Case
        dp[0][0] = true;

        // Iterate over the characters
        // of the string pattern
        for (let i = 0; i < M; i++) {
            if (pattern[i] == '*'
                && dp[0][i - 1]) {

                // Update dp[0][i + 1]
                dp[0][i + 1] = true;
            }
        }

        // Iterate over the characters
        // of both the strings
        for (let i = 0; i < N; i++) {

            for (let j = 0; j < M; j++) {

                // If current character
                // in the pattern is '.'
                if (pattern[j] == '.') {

                    // Update dp[i + 1][j + 1]
                    dp[i + 1][j + 1] = dp[i][j];
                }

                // If current character in
                // both the strings are equal
                if (pattern[j] == text[i]) {

                    // Update dp[i + 1][j + 1]
                    dp[i + 1][j + 1] = dp[i][j];
                }

                // If current character
                // in the pattern is '*'
                if (pattern[j] == '*') {

                    if (pattern[j - 1] != text[i]
                        && pattern[j - 1] != '.') {

                        // Update dp[i + 1][j + 1]
                        dp[i + 1][j + 1] = dp[i + 1][j - 1];
                    }

                    else {

                        // Update dp[i+1][j+1]
                        dp[i + 1][j + 1] = (dp[i + 1][j]
                                            || dp[i][j + 1]
                                            || dp[i + 1][j - 1]);
                    }
                }
            }
        }

        // Return dp[M][N]
        return dp[N][M];
    }

    let text = "geeksforgeeks";
    let pattern = "ge*ksforgeeks";

    if (isMatch(text, pattern)) {
      document.write("Yes");
    }
    else {
      document.write("No");
    }

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(M * N)*