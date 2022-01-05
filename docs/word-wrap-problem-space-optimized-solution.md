# 自动换行问题(空间优化解决方案)

> 原文:[https://www . geesforgeks . org/word-wrap-problem-space-optimized-solution/](https://www.geeksforgeeks.org/word-wrap-problem-space-optimized-solution/)

给定一个单词序列，并限制一行中的字符数(行宽)。将换行符按给定的顺序排列，这样行就能整齐地打印出来。假设每个字的长度小于线宽。插入换行符时，每一行都有可能出现额外的空格。额外的空格包括除最后一行之外放在每一行末尾的空格。
问题是最小化以下总成本。
总成本=所有线路成本之和，其中线路成本=(line)^2.的额外空间数量
例如，考虑下面的字符串和线宽 M = 15
“极客为极客呈现换行问题”
下面是 3 行中单词的优化排列
极客为极客
呈现单词
换行问题
第 1 行和第 2 行的总额外空格为 0 和 2。不考虑 3 号线的空间，因为它不是上述的额外空间。所以总成本的最优值是 0 + 2*2 = 4。
**举例:**

```
Input format: Input will consists of array of integers where each array element represents length of each word of string. For example, for string S = "Geeks for Geeks", input array will be arr[] = {5, 3, 5}.
Output format: Output consists of a series of integers where two consecutive integers represent 
starting word and ending word of each line.

Input : arr[] = {3, 2, 2, 5}
Output : 1 1 2 3 4 4
Line number 1: From word no. 1 to 1
Line number 2: From word no. 2 to 3
Line number 3: From word no. 4 to 4 

Input : arr[] = {3, 2, 2}
Output : 1 1 2 2 3 3
Line number 1: From word no. 1 to 1
Line number 2: From word no. 2 to 2
Line number 3: From word no. 3 to 3 
```

[Recommended: Please solve it on *“PRACTICE”* first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/word-wrap/0)

**方法:**我们已经讨论了基于[动态规划的解决方案](https://www.geeksforgeeks.org/dynamic-programming-set-18-word-wrap/)的自动换行问题。所讨论的解决方案使用了 O(n^2)辅助空间。使用的辅助空间可以减少到 O(n)。想法是使用两个一维数组 dp[]和 ans[]，其中 dp[i]表示 arr[i]是第一个单词的行的最小开销，ans[i]表示 arr[i]是第一个单词的行中最后一个单词的索引。让 k 代表每行字符数的限制。假设对于任何一行 l，该行中的第一个单词位于 arr[]中的索引 I 处。该线路的最低成本存储在 dp[i]中。这一行的最后一个单词在 arr[]中的索引 j 处，其中 j 可以从 I 变化到 n。迭代 j 的所有值，并跟踪第 l 行中到目前为止添加的字符数。如果字符数小于 k，则使用这些字符数查找当前行的成本。将此成本与 dp[i]中的最低成本进行比较，并相应地更新 dp[i]和 ans[i]。对 I 的每个值重复上述过程，1 < = i < = n。每行的起始和结束单词将在索引 I 和索引 ans[i]处，其中 l+1 行的 I 的下一个值是 ans[i] + 1。
**实施:**

## C++

```
// C++ program for space optimized
// solution of Word Wrap problem.

#include <bits/stdc++.h>
using namespace std;

// Function to find space optimized
// solution of Word Wrap problem.
void solveWordWrap(int arr[], int n, int k)
{
    int i, j;

    // Variable to store number of
    // characters in given line.
    int currlen;

    // Variable to store possible
    // minimum cost of line.
    int cost;

    // DP table in which dp[i] represents
    // cost of line starting with word
    // arr[i].
    int dp[n];

    // Array in which ans[i] store index
    // of last word in line starting with
    // word arr[i].
    int ans[n];

    // If only one word is present then
    // only one line is required. Cost
    // of last line is zero. Hence cost
    // of this line is zero. Ending point
    // is also n-1 as single word is
    // present.
    dp[n - 1] = 0;
    ans[n - 1] = n - 1;

    // Make each word first word of line
    // by iterating over each index in arr.
    for (i = n - 2; i >= 0; i--) {
        currlen = -1;
        dp[i] = INT_MAX;

        // Keep on adding words in current
        // line by iterating from starting
        // word upto last word in arr.
        for (j = i; j < n; j++) {

            // Update number of characters
            // in current line. arr[j] is
            // number of characters in
            // current word and 1
            // represents space character
            // between two words.
            currlen += (arr[j] + 1);

            // If limit of characters
            // is violated then no more
            // words can be added to
            // current line.
            if (currlen > k)
                break;

            // If current word that is
            // added to line is last
            // word of arr then current
            // line is last line. Cost of
            // last line is 0\. Else cost
            // is square of extra spaces
            // plus cost of putting line
            // breaks in rest of words
            // from j+1 to n-1.
            if (j == n - 1)
                cost = 0;
            else
                cost = (k - currlen) * (k - currlen) + dp[j + 1];

            // Check if this arrangement gives
            // minimum cost for line starting
            // with word arr[i].
            if (cost < dp[i]) {
                dp[i] = cost;
                ans[i] = j;
            }
        }
    }

    // Print starting index and ending index
    // of words present in each line.
    i = 0;
    while (i < n) {
        cout << i + 1 << " " << ans[i] + 1 << " ";
        i = ans[i] + 1;
    }
}

// Driver function
int main()
{
    int arr[] = { 3, 2, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int M = 6;
    solveWordWrap(arr, n, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for space
// optimized solution of
// Word Wrap problem.
import java.io.*;

class GFG
{

// Function to find space
// optimized solution of
// Word Wrap problem.
static void solveWordWrap(int arr[],
                          int n, int k)
{
    int i, j;

    // Variable to store
    // number of characters
    // in given line.
    int currlen;

    // Variable to store
    // possible minimum
    // cost of line.
    int cost;

    // DP table in which
    // dp[i] represents
    // cost of line starting
    // with word arr[i].
    int dp[] = new int[n];

    // Array in which ans[i]
    // store index of last
    // word in line starting
    // with word arr[i].
    int ans[] = new int[n];

    // If only one word is present
    // then only one line is required.
    // Cost of last line is zero.
    // Hence cost of this line is zero.
    // Ending point is also n-1 as
    // single word is present.
    dp[n - 1] = 0;
    ans[n - 1] = n - 1;

    // Make each word first
    // word of line by iterating
    // over each index in arr.
    for (i = n - 2; i >= 0; i--)
    {
        currlen = -1;
        dp[i] = Integer.MAX_VALUE;

        // Keep on adding words in
        // current line by iterating
        // from starting word upto
        // last word in arr.
        for (j = i; j < n; j++)
        {

            // Update number of characters
            // in current line. arr[j] is
            // number of characters in
            // current word and 1
            // represents space character
            // between two words.
            currlen += (arr[j] + 1);

            // If limit of characters
            // is violated then no more
            // words can be added to
            // current line.
            if (currlen > k)
                break;

            // If current word that is
            // added to line is last
            // word of arr then current
            // line is last line. Cost of
            // last line is 0\. Else cost
            // is square of extra spaces
            // plus cost of putting line
            // breaks in rest of words
            // from j+1 to n-1.
            if (j == n - 1)
                cost = 0;
            else
                cost = (k - currlen) *
                       (k - currlen) +
                            dp[j + 1];

            // Check if this arrangement
            // gives minimum cost for
            // line starting with word
            // arr[i].
            if (cost < dp[i])
            {
                dp[i] = cost;
                ans[i] = j;
            }
        }
    }

    // Print starting index
    // and ending index of
    // words present in each line.
    i = 0;
    while (i < n)
    {
        System.out.print((i + 1) + " " +
                        (ans[i] + 1) + " ");
        i = ans[i] + 1;
    }
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {3, 2, 2, 5};
    int n = arr.length;
    int M = 6;
    solveWordWrap(arr, n, M);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program for space optimized
# solution of Word Wrap problem.
import sys

# Function to find space optimized
# solution of Word Wrap problem.
def solveWordWrap(arr, n, k):

    dp = [0] * n

    # Array in which ans[i] store index
    # of last word in line starting with
    # word arr[i].
    ans = [0] * n

    # If only one word is present then
    # only one line is required. Cost
    # of last line is zero. Hence cost
    # of this line is zero. Ending point
    # is also n-1 as single word is
    # present.
    dp[n - 1] = 0
    ans[n - 1] = n - 1

    # Make each word first word of line
    # by iterating over each index in arr.
    for i in range(n - 2, -1, -1):
        currlen = -1
        dp[i] = sys.maxsize

        # Keep on adding words in current
        # line by iterating from starting
        # word upto last word in arr.
        for j in range(i, n):

            # Update number of characters
            # in current line. arr[j] is
            # number of characters in
            # current word and 1
            # represents space character
            # between two words.
            currlen += (arr[j] + 1)

            # If limit of characters
            # is violated then no more
            # words can be added to
            # current line.
            if (currlen > k):
                break

            # If current word that is
            # added to line is last
            # word of arr then current
            # line is last line. Cost of
            # last line is 0\. Else cost
            # is square of extra spaces
            # plus cost of putting line
            # breaks in rest of words
            # from j+1 to n-1.
            if (j == n - 1):
                cost = 0
            else:
                cost = ((k - currlen) *
                        (k - currlen) + dp[j + 1])

            # Check if this arrangement gives
            # minimum cost for line starting
            # with word arr[i].
            if (cost < dp[i]):
                dp[i] = cost
                ans[i] = j

    # Print starting index and ending index
    # of words present in each line.
    i = 0
    while (i < n):
        print(i + 1 , ans[i] + 1, end = " ")
        i = ans[i] + 1

# Driver Code
if __name__ == "__main__":

    arr = [3, 2, 2, 5 ]
    n = len(arr)
    M = 6
    solveWordWrap(arr, n, M)

# This code is contributed by ita_c
```

## C#

```
// C# program for space
// optimized solution of
// Word Wrap problem.
using System;

class GFG
{

// Function to find space optimized
// solution of Word Wrap problem.
public static void solveWordWrap(int[] arr,
                                 int n, int k)
{
    int i, j;

    // Variable to store number of
    // characters in given line.
    int currlen;

    // Variable to store possible
    // minimum cost of line.
    int cost;

    // DP table in which dp[i]
    // represents cost of line
    // starting with word arr[i].
    int[] dp = new int[n];

    // Array in which ans[i] store
    // index of last word in line
    // starting with word arr[i].
    int[] ans = new int[n];

    // If only one word is present
    // then only one line is required.
    // Cost of last line is zero.
    // Hence cost of this line is zero.
    // Ending point is also n-1 as
    // single word is present.
    dp[n - 1] = 0;
    ans[n - 1] = n - 1;

    // Make each word first
    // word of line by iterating
    // over each index in arr.
    for (i = n - 2; i >= 0; i--)
    {
        currlen = -1;
        dp[i] = int.MaxValue;

        // Keep on adding words in
        // current line by iterating
        // from starting word upto
        // last word in arr.
        for (j = i; j < n; j++)
        {

            // Update number of characters
            // in current line. arr[j] is
            // number of characters in
            // current word and 1
            // represents space character
            // between two words.
            currlen += (arr[j] + 1);

            // If limit of characters
            // is violated then no more
            // words can be added to
            // current line.
            if (currlen > k)
            {
                break;
            }

            // If current word that is
            // added to line is last
            // word of arr then current
            // line is last line. Cost of
            // last line is 0\. Else cost
            // is square of extra spaces
            // plus cost of putting line
            // breaks in rest of words
            // from j+1 to n-1.
            if (j == n - 1)
            {
                cost = 0;
            }
            else
            {
                cost = (k - currlen) *
                       (k - currlen) + dp[j + 1];
            }

            // Check if this arrangement
            // gives minimum cost for
            // line starting with word
            // arr[i].
            if (cost < dp[i])
            {
                dp[i] = cost;
                ans[i] = j;
            }
        }
    }

    // Print starting index
    // and ending index of
    // words present in each line.
    i = 0;
    while (i < n)
    {
        Console.Write((i + 1) + " " +
                      (ans[i] + 1) + " ");
        i = ans[i] + 1;
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {3, 2, 2, 5};
    int n = arr.Length;
    int M = 6;
    solveWordWrap(arr, n, M);
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for space optimized
// solution of Word Wrap problem.

// Function to find space optimized
// solution of Word Wrap problem.
function solveWordWrap($arr, $n, $k)
{

    // Variable to store number of
    // characters in given line.
    $currlen;

    // Variable to store possible
    // minimum cost of line.
    $cost;

    // DP table in which dp[i] represents
    // cost of line starting with word
    // arr[i].
    $dp = array();

    // Array in which ans[i] store index
    // of last word in line starting with
    // word arr[i].
    $ans = array();

    // If only one word is present then
    // only one line is required. Cost
    // of last line is zero. Hence cost
    // of this line is zero. Ending point
    // is also n-1 as single word is
    // present.
    $dp[$n - 1] = 0;
    $ans[$n - 1] = $n - 1;

    // Make each word first word of line
    // by iterating over each index in arr.
    for ($i = $n - 2; $i >= 0; $i--)
    {
        $currlen = -1;
        $dp[$i] = PHP_INT_MAX;

        // Keep on adding words in current
        // line by iterating from starting
        // word upto last word in arr.
        for ($j = $i; $j < $n; $j++)
        {

            // Update number of characters
            // in current line. arr[j] is
            // number of characters in
            // current word and 1
            // represents space character
            // between two words.
            $currlen += ($arr[$j] + 1);

            // If limit of characters
            // is violated then no more
            // words can be added to
            // current line.
            if ($currlen > $k)
                break;

            // If current word that is
            // added to line is last
            // word of arr then current
            // line is last line. Cost of
            // last line is 0\. Else cost
            // is square of extra spaces
            // plus cost of putting line
            // breaks in rest of words
            // from j+1 to n-1.
            if ($j == $n - 1)
                $cost = 0;
            else
                $cost = ($k - $currlen) *
                        ($k - $currlen) + $dp[$j + 1];

            // Check if this arrangement gives
            // minimum cost for line starting
            // with word arr[i].
            if ($cost < $dp[$i])
            {
                $dp[$i] = $cost;
                $ans[$i] = $j;
            }
        }
    }

    // Print starting index and ending index
    // of words present in each line.
    $i = 0;
    while ($i < $n)
    {
        echo ($i + 1) . " " .
             ($ans[$i] + 1) . " ";
        $i = $ans[$i] + 1;
    }
}

// Driver function
$arr = array(3, 2, 2, 5);
$n = sizeof($arr);
$M = 6;
solveWordWrap($arr, $n, $M);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program for space optimized
// solution of Word Wrap problem.

// Function to find space optimized
// solution of Word Wrap problem.
function solveWordWrap(arr, n, k)
{
    var i, j;

    // Variable to store number of
    // characters in given line.
    var currlen;

    // Variable to store possible
    // minimum cost of line.
    var cost;

    // DP table in which dp[i] represents
    // cost of line starting with word
    // arr[i].
    var dp = Array(n);

    // Array in which ans[i] store index
    // of last word in line starting with
    // word arr[i].
    var ans = Array(n);

    // If only one word is present then
    // only one line is required. Cost
    // of last line is zero. Hence cost
    // of this line is zero. Ending point
    // is also n-1 as single word is
    // present.
    dp[n - 1] = 0;
    ans[n - 1] = n - 1;

    // Make each word first word of line
    // by iterating over each index in arr.
    for (i = n - 2; i >= 0; i--)
    {
        currlen = -1;
        dp[i] = 1000000000;

        // Keep on adding words in current
        // line by iterating from starting
        // word upto last word in arr.
        for (j = i; j < n; j++)
        {

            // Update number of characters
            // in current line. arr[j] is
            // number of characters in
            // current word and 1
            // represents space character
            // between two words.
            currlen += (arr[j] + 1);

            // If limit of characters
            // is violated then no more
            // words can be added to
            // current line.
            if (currlen > k)
                break;

            // If current word that is
            // added to line is last
            // word of arr then current
            // line is last line. Cost of
            // last line is 0\. Else cost
            // is square of extra spaces
            // plus cost of putting line
            // breaks in rest of words
            // from j+1 to n-1.
            if (j == n - 1)
                cost = 0;
            else
                cost = (k - currlen) * (k - currlen) + dp[j + 1];

            // Check if this arrangement gives
            // minimum cost for line starting
            // with word arr[i].
            if (cost < dp[i]) {
                dp[i] = cost;
                ans[i] = j;
            }
        }
    }

    // Print starting index and ending index
    // of words present in each line.
    i = 0;
    while (i < n)
    {
        document.write( i + 1 + " " + (ans[i] + 1) + " ");
        i = ans[i] + 1;
    }
}

// Driver function
var arr = [ 3, 2, 2, 5 ];
var n = arr.length;
var M = 6;
solveWordWrap(arr, n, M);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
1 1 2 3 4 4
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(n)