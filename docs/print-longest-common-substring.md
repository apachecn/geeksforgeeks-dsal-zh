# 打印最长的常用子串

> 原文:[https://www . geesforgeks . org/print-long-common-substring/](https://www.geeksforgeeks.org/print-longest-common-substring/)

给定两个字符串“X”和“Y”，打印最长的公共子字符串的长度。如果两个或多个子字符串中最长的公共子字符串具有相同的值，则打印其中任何一个。

**示例:**

```
Input :  X = "GeeksforGeeks", 
         Y = "GeeksQuiz"
Output : Geeks

Input : X = "zxabcdezy", 
        Y = "yzabcdezx"
Output : abcdez
```

我们讨论了一种求最长公共字符串长度的方法。在这篇文章中，我们已经讨论了打印常用字符串的讨论。

**天真的做法:**让字符串 **X** 和 **Y** 分别为长度 **m** 和 **n** 。生成所有可能的子串 **X** ，这需要 0(m<sup>2</sup>的时间复杂度，并使用 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)搜索字符串 **Y** 中的每个子串，这可以在 0(n)的时间复杂度中实现。整体时间复杂度为 O(n * m <sup>2</sup> )。

**高效途径:**是基于[这篇](https://www.geeksforgeeks.org/longest-common-substring/)帖子里解释的动态编程实现。建立最长后缀矩阵**lcsuf[][]**，并跟踪具有最大值的单元的索引。让该索引由**(行，列)**对表示。现在，通过对角遍历**lcsuf[][]**矩阵，直到 lcsuf[row][col]为止，最终最长的公共子串在该索引的帮助下被构建！= 0，在迭代过程中，从 **X[row-1]** 或 **Y[col-1]** 中获取字符，并将其从右向左添加到结果公共字符串中。

## C++

```
// C++ implementation to print the longest common substring
#include <iostream>
#include <stdlib.h>
#include <string.h>

using namespace std;

/* function to find and print the longest common
   substring of X[0..m-1] and Y[0..n-1] */
void printLCSubStr(char* X, char* Y, int m, int n)
{
    // Create a table to store lengths of longest common
    // suffixes of substrings.   Note that LCSuff[i][j]
    // contains length of longest common suffix of X[0..i-1]
    // and Y[0..j-1]. The first row and first column entries
    // have no logical meaning, they are used only for
    // simplicity of program
    int LCSuff[m + 1][n + 1];

    // To store length of the longest common substring
    int len = 0;

    // To store the index of the cell which contains the
    // maximum value. This cell's index helps in building
    // up the longest common substring from right to left.
    int row, col;

    /* Following steps build LCSuff[m+1][n+1] in bottom
       up fashion. */
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                LCSuff[i][j] = 0;

            else if (X[i - 1] == Y[j - 1]) {
                LCSuff[i][j] = LCSuff[i - 1][j - 1] + 1;
                if (len < LCSuff[i][j]) {
                    len = LCSuff[i][j];
                    row = i;
                    col = j;
                }
            }
            else
                LCSuff[i][j] = 0;
        }
    }

    // if true, then no common substring exists
    if (len == 0) {
        cout << "No Common Substring";
        return;
    }

    // allocate space for the longest common substring
    char* resultStr = (char*)malloc((len + 1) * sizeof(char));

    // traverse up diagonally form the (row, col) cell
    // until LCSuff[row][col] != 0
    while (LCSuff[row][col] != 0) {
        resultStr[--len] = X[row - 1]; // or Y[col-1]

        // move diagonally up to previous cell
        row--;
        col--;
    }

    // required longest common substring
    cout << resultStr;
}

/* Driver program to test above function */
int main()
{
    char X[] = "OldSite:GeeksforGeeks.org";
    char Y[] = "NewSite:GeeksQuiz.com";

    int m = strlen(X);
    int n = strlen(Y);

    printLCSubStr(X, Y, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the longest common substring
public class Longest_common_substr {

    /* function to find and print the longest common
       substring of X[0..m-1] and Y[0..n-1] */
    static void printLCSubStr(String X, String Y, int m, int n)
    {
        // Create a table to store lengths of longest common
        // suffixes of substrings.   Note that LCSuff[i][j]
        // contains length of longest common suffix of X[0..i-1]
        // and Y[0..j-1]. The first row and first column entries
        // have no logical meaning, they are used only for
        // simplicity of program
        int[][] LCSuff = new int[m + 1][n + 1];

        // To store length of the longest common substring
        int len = 0;

        // To store the index of the cell which contains the
        // maximum value. This cell's index helps in building
        // up the longest common substring from right to left.
        int row = 0, col = 0;

        /* Following steps build LCSuff[m+1][n+1] in bottom
           up fashion. */
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0)
                    LCSuff[i][j] = 0;

                else if (X.charAt(i - 1) == Y.charAt(j - 1)) {
                    LCSuff[i][j] = LCSuff[i - 1][j - 1] + 1;
                    if (len < LCSuff[i][j]) {
                        len = LCSuff[i][j];
                        row = i;
                        col = j;
                    }
                }
                else
                    LCSuff[i][j] = 0;
            }
        }

        // if true, then no common substring exists
        if (len == 0) {
            System.out.println("No Common Substring");
            return;
        }

        // allocate space for the longest common substring
        String resultStr = "";

        // traverse up diagonally form the (row, col) cell
        // until LCSuff[row][col] != 0
        while (LCSuff[row][col] != 0) {
            resultStr = X.charAt(row - 1) + resultStr; // or Y[col-1]
            --len;

            // move diagonally up to previous cell
            row--;
            col--;
        }

        // required longest common substring
        System.out.println(resultStr);
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
        String X = "OldSite:GeeksforGeeks.org";
        String Y = "NewSite:GeeksQuiz.com";

        int m = X.length();
        int n = Y.length();

        printLCSubStr(X, Y, m, n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 implementation to print
# the longest common substring

# function to find and print 
# the longest common substring of
# X[0..m-1] and Y[0..n-1]
def printLCSSubStr(X: str, Y: str,
                   m: int, n: int):

    # Create a table to store lengths of
    # longest common suffixes of substrings.
    # Note that LCSuff[i][j] contains length
    # of longest common suffix of X[0..i-1] and
    # Y[0..j-1]. The first row and first
    # column entries have no logical meaning,
    # they are used only for simplicity of program
    LCSuff = [[0 for i in range(n + 1)]
                 for j in range(m + 1)]

    # To store length of the
    # longest common substring
    length = 0

    # To store the index of the cell
    # which contains the maximum value.
    # This cell's index helps in building
    # up the longest common substring
    # from right to left.
    row, col = 0, 0

    # Following steps build LCSuff[m+1][n+1]
    # in bottom up fashion.
    for i in range(m + 1):
        for j in range(n + 1):
            if i == 0 or j == 0:
                LCSuff[i][j] = 0
            elif X[i - 1] == Y[j - 1]:
                LCSuff[i][j] = LCSuff[i - 1][j - 1] + 1
                if length < LCSuff[i][j]:
                    length = LCSuff[i][j]
                    row = i
                    col = j
            else:
                LCSuff[i][j] = 0

    # if true, then no common substring exists
    if length == 0:
        print("No Common Substring")
        return

    # allocate space for the longest
    # common substring
    resultStr = ['0'] * length

    # traverse up diagonally form the
    # (row, col) cell until LCSuff[row][col] != 0
    while LCSuff[row][col] != 0:
        length -= 1
        resultStr[length] = X[row - 1] # or Y[col-1]

        # move diagonally up to previous cell
        row -= 1
        col -= 1

    # required longest common substring
    print(''.join(resultStr))

# Driver Code
if __name__ == "__main__":
    X = "OldSite:GeeksforGeeks.org"
    Y = "NewSite:GeeksQuiz.com"
    m = len(X)
    n = len(Y)

    printLCSSubStr(X, Y, m, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to print the
// longest common substring
using System;

class GFG {

    /* function to find and print the longest common
    substring of X[0..m-1] and Y[0..n-1] */
    static void printLCSubStr(String X, String Y, int m, int n)
    {
        // Create a table to store lengths of longest common
        // suffixes of substrings. Note that LCSuff[i][j]
        // contains length of longest common suffix of X[0..i-1]
        // and Y[0..j-1]. The first row and first column entries
        // have no logical meaning, they are used only for
        // simplicity of program
        int[, ] LCSuff = new int[m + 1, n + 1];

        // To store length of the longest common substring
        int len = 0;

        // To store the index of the cell which contains the
        // maximum value. This cell's index helps in building
        // up the longest common substring from right to left.
        int row = 0, col = 0;

        /* Following steps build LCSuff[m+1][n+1] in bottom
        up fashion. */
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0)
                    LCSuff[i, j] = 0;

                else if (X[i - 1] == Y[j - 1]) {
                    LCSuff[i, j] = LCSuff[i - 1, j - 1] + 1;
                    if (len < LCSuff[i, j]) {
                        len = LCSuff[i, j];
                        row = i;
                        col = j;
                    }
                }
                else
                    LCSuff[i, j] = 0;
            }
        }

        // if true, then no common substring exists
        if (len == 0) {
            Console.Write("No Common Substring");
            return;
        }

        // allocate space for the longest common substring
        String resultStr = "";

        // traverse up diagonally form the (row, col) cell
        // until LCSuff[row][col] != 0
        while (LCSuff[row, col] != 0) {
            resultStr = X[row - 1] + resultStr; // or Y[col-1]
            --len;

            // move diagonally up to previous cell
            row--;
            col--;
        }

        // required longest common substring
        Console.WriteLine(resultStr);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        String X = "OldSite:GeeksforGeeks.org";
        String Y = "NewSite:GeeksQuiz.com";

        int m = X.Length;
        int n = Y.Length;

        printLCSubStr(X, Y, m, n);
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>
// Javascript implementation to print the longest common substring

    /* function to find and print the longest common
       substring of X[0..m-1] and Y[0..n-1] */
    function printLCSubStr(X,Y,m,n)
    {
        // Create a table to store lengths of longest common
        // suffixes of substrings.   Note that LCSuff[i][j]
        // contains length of longest common suffix of X[0..i-1]
        // and Y[0..j-1]. The first row and first column entries
        // have no logical meaning, they are used only for
        // simplicity of program
        let LCSuff = new Array(m+1);

        // To store length of the longest common substring
        let len = 0;

        // To store the index of the cell which contains the
        // maximum value. This cell's index helps in building
        // up the longest common substring from right to left.
        let row = 0, col = 0;

        /* Following steps build LCSuff[m+1][n+1] in bottom
           up fashion. */
        for (let i = 0; i <= m; i++) {
            LCSuff[i] = Array(n+1);
            for (let j = 0; j <= n; j++) {
                LCSuff[i][j]=0;   
                if (i == 0 || j == 0)
                    LCSuff[i][j] = 0;

                else if (X[i-1] == Y[j-1]) {
                    LCSuff[i][j] = LCSuff[i - 1][j - 1] + 1;
                    if (len < LCSuff[i][j]) {
                        len = LCSuff[i][j];
                        row = i;
                        col = j;
                    }
                }
                else
                    LCSuff[i][j] = 0;
            }
        }

        // if true, then no common substring exists
        if (len == 0) {
            document.write("No Common Substring");
            return;
        }

        // allocate space for the longest common substring
        let resultStr = "";

        // traverse up diagonally form the (row, col) cell
        // until LCSuff[row][col] != 0
        while (LCSuff[row][col] != 0) {
            resultStr = X[row-1] + resultStr; // or Y[col-1]
            --len;

            // move diagonally up to previous cell
            row--;
            col--;
        }

        // required longest common substring
        document.write(resultStr);
    }

    /* Driver program to test above function */
    let X = "OldSite:GeeksforGeeks.org";
    let Y = "NewSite:GeeksQuiz.com";
    let m = X.length;
    let n = Y.length;
    printLCSubStr(X, Y, m, n);

    //This code is contributed by rag2127

</script>
```

**Output:** 

```
Site:Geeks
```

**时间复杂度:** O(m*n)。
**辅助空间:** O(m*n)。

**空间优化途径:**
上解使用的辅助空间为 **O(m*n)** ，其中 m 和 n 为字符串 X 和 y 的长度，上解使用的空间可以缩减为 **O(2*n)** 。变量 end 用于存储字符串 X 中最长公共子串的结束点，变量 maxlen 用于存储最长公共子串的长度。

假设当 X 的长度为 I，Y 的长度为 j 时，我们处于 DP 状态，其结果存储在 len[i][j]中。
现在如果 **X[i-1] == Y[j-1]，那么 len[i][j] = 1 + len[i-1][j-1]** ，即矩阵 len[][]中当前行的结果取决于前一行的值。因此，最长公共子串的所需长度可以通过仅保持两个连续行的值来获得，从而将空间需求减少到 0(2 * n)。

为了打印最长的公共子串，我们使用变量 end。当计算 len[i][j]时，将其与 maxlen 进行比较。如果 maxlen 小于 len[i][j]，则 end 被更新为 i-1，以显示最长公共子串在 X 中的索引 i-1 处结束，maxlen 被更新为 len[i][j]。最长的公共子串是从索引**结束–maxlen+1 到 x 中的索引结束。**
变量 currRow 用于表示 len[2][n]矩阵的行 0 或行 1 当前用于查找长度。最初，当字符串 X 的长度为零时，第 0 行用作当前行。在每次迭代结束时，当前行成为前一行，前一行成为新的当前行。

下面给出了上述方法的实现:

## C++

```
// Space optimized CPP implementation to print
// longest common substring.
#include <bits/stdc++.h>
using namespace std;

// Function to find longest common substring.
string LCSubStr(string X, string Y)
{
    // Find length of both the strings.
    int m = X.length();
    int n = Y.length();

    // Variable to store length of longest
    // common substring.
    int result = 0;

    // Variable to store ending point of
    // longest common substring in X.
    int end;

    // Matrix to store result of two
    // consecutive rows at a time.
    int len[2][n];

    // Variable to represent which row of
    // matrix is current row.
    int currRow = 0;

    // For a particular value of i and j,
    // len[currRow][j] stores length of longest
    // common substring in string X[0..i] and Y[0..j].
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0) {
                len[currRow][j] = 0;
            }
            else if (X[i - 1] == Y[j - 1]) {
                len[currRow][j] = len[1 - currRow][j - 1] + 1;
                if (len[currRow][j] > result) {
                    result = len[currRow][j];
                    end = i - 1;
                }
            }
            else {
                len[currRow][j] = 0;
            }
        }

        // Make current row as previous row and
        // previous row as new current row.
        currRow = 1 - currRow;
    }

    // If there is no common substring, print -1.
    if (result == 0) {
        return "-1";
    }

    // Longest common substring is from index
    // end - result + 1 to index end in X.
    return X.substr(end - result + 1, result);
}
// Driver Code
int main()
{
    string X = "GeeksforGeeks";
    string Y = "GeeksQuiz";
    // function call
    cout << LCSubStr(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Space optimized Java implementation to print
// longest common substring.

public class GFG {

// Function to find longest common substring.
    static String LCSubStr(String X, String Y) {
        // Find length of both the Strings.
        int m = X.length();
        int n = Y.length();

        // Variable to store length of longest
        // common subString.
        int result = 0;

        // Variable to store ending point of
        // longest common subString in X.
        int end = 0;

        // Matrix to store result of two
        // consecutive rows at a time.
        int len[][] = new int[2][m];

        // Variable to represent which row of
        // matrix is current row.
        int currRow = 0;

        // For a particular value of i and j,
        // len[currRow][j] stores length of longest
        // common subString in String X[0..i] and Y[0..j].
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    len[currRow][j] = 0;
                } else if (X.charAt(i - 1) == Y.charAt(j - 1)) {
                    len[currRow][j] = len[1 - currRow][j - 1] + 1;
                    if (len[currRow][j] > result) {
                        result = len[currRow][j];
                        end = i - 1;
                    }
                } else {
                    len[currRow][j] = 0;
                }
            }

            // Make current row as previous row and
            // previous row as new current row.
            currRow = 1 - currRow;
        }

        // If there is no common subString, print -1.
        if (result == 0) {
            return "-1";
        }

        // Longest common subString is from index
        // end - result + 1 to index end in X.
        return X.substring(end - result + 1, result);
    }

    // Driver Code
    public static void main(String[] args) {
        String X = "GeeksforGeeks";
        String Y = "GeeksQuiz";
        // function call
        System.out.println(LCSubStr(X, Y));

    }

}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Space optimized Python3 implementation to
# print longest common substring.

# Function to find longest common substring.
def LCSubStr(X, Y):

    # Find length of both the strings.
    m = len(X)
    n = len(Y)

    # Variable to store length of longest
    # common substring.
    result = 0

    # Variable to store ending point of
    # longest common substring in X.
    end = 0

    # Matrix to store result of two
    # consecutive rows at a time.
    length = [[0 for j in range(m)]
                 for i in range(2)]

    # Variable to represent which row of
    # matrix is current row.
    currRow = 0

    # For a particular value of i and j,
    # length[currRow][j] stores length
    # of longest common substring in
    # string X[0..i] and Y[0..j].
    for i in range(0, m + 1):
        for j in range(0, n + 1):
            if (i == 0 or j == 0):
                length[currRow][j] = 0

            elif (X[i - 1] == Y[j - 1]):
                length[currRow][j] = length[1 - currRow][j - 1] + 1

                if (length[currRow][j] > result):
                    result = length[currRow][j]
                    end = i - 1
            else:
                length[currRow][j] = 0

        # Make current row as previous row and
        # previous row as new current row.
        currRow = 1 - currRow

    # If there is no common substring, print -1.
    if (result == 0):
        return "-1"

    # Longest common substring is from index
    # end - result + 1 to index end in X.
    return X[end - result + 1 : end + 1]

# Driver code
if __name__=="__main__":

    X = "GeeksforGeeks"
    Y = "GeeksQuiz"

    # Function call
    print(LCSubStr(X, Y))

# This code is contributed by rutvik_56
```

## C#

```
using System;
// Space optimized Java implementation to print
// longest common substring.

public class GFG {

// Function to find longest common substring.
    static string LCSubStr(string X, string Y) {
        // Find length of both the Strings.
        int m = X.Length;
        int n = Y.Length;

        // Variable to store length of longest
        // common subString.
        int result = 0;

        // Variable to store ending point of
        // longest common subString in X.
        int end = 0;

        // Matrix to store result of two
        // consecutive rows at a time.
        int[,] len = new int[2,m];

        // Variable to represent which row of
        // matrix is current row.
        int currRow = 0;

        // For a particular value of i and j,
        // len[currRow][j] stores length of longest
        // common subString in String X[0..i] and Y[0..j].
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    len[currRow,j] = 0;
                } else if (X[i - 1] == Y[j - 1]) {
                    len[currRow,j] = len[1 - currRow,j - 1] + 1;
                    if (len[currRow,j] > result) {
                        result = len[currRow,j];
                        end = i - 1;
                    }
                } else {
                    len[currRow,j] = 0;
                }
            }

            // Make current row as previous row and
            // previous row as new current row.
            currRow = 1 - currRow;
        }

        // If there is no common subString, print -1.
        if (result == 0) {
            return "-1";
        }

        // Longest common subString is from index
        // end - result + 1 to index end in X.
        return X.Substring(end - result + 1, result);
    }

    // Driver Code
    public static void Main() {
        string X = "GeeksforGeeks";
        string Y = "GeeksQuiz";
        // function call
        Console.Write(LCSubStr(X, Y));

    }

}
```

## java 描述语言

```
<script>
// Space optimized javascript implementation to print
// longest common substring.   

    // Function to find longest common substring.
    function LCSubStr(X,Y)
    {
        // Find length of both the strings.
    let m = X.length;
    let n = Y.length;

    // Variable to store length of longest
    // common substring.
    let result = 0;

    // Variable to store ending point of
    // longest common substring in X.
    let end;

    // Matrix to store result of two
    // consecutive rows at a time.
    let len= new Array(2);
    for(let i=0;i<len.length;i++)
    {
        len[i]=new Array(n);
        for(let j=0;j<n;j++)
        {
            len[i][j]=0;
        }
    }

    // Variable to represent which row of
    // matrix is current row.
    let currRow = 0;

    // For a particular value of i and j,
    // len[currRow][j] stores length of longest
    // common substring in string X[0..i] and Y[0..j].
    for (let i = 0; i <= m; i++) {
        for (let j = 0; j <= n; j++) {
            if (i == 0 || j == 0) {
                len[currRow][j] = 0;
            }
            else if (X[i - 1] == Y[j - 1]) {
                len[currRow][j] = len[1 - currRow][j - 1] + 1;
                if (len[currRow][j] > result) {
                    result = len[currRow][j];
                    end = i - 1;
                }
            }
            else {
                len[currRow][j] = 0;
            }
        }

        // Make current row as previous row and
        // previous row as new current row.
        currRow = 1 - currRow;
    }

    // If there is no common substring, print -1.
    if (result == 0) {
        return "-1";
    }

    // Longest common substring is from index
    // end - result + 1 to index end in X.
    return X.substr(end - result + 1, result);
    }

    // Driver Code
    let X = "GeeksforGeeks";
    let Y = "GeeksQuiz";
    // function call
    document.write(LCSubStr(X, Y));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Geeks
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(n)

这种方法是由 nik1996 提出的。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。