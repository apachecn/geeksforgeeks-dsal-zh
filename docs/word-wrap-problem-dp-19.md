# 自动换行问题| DP-19

> 原文:[https://www.geeksforgeeks.org/word-wrap-problem-dp-19/](https://www.geeksforgeeks.org/word-wrap-problem-dp-19/)

给定一个单词序列，并限制一行中的字符数(行宽)。将换行符按给定的顺序排列，这样行就能整齐地打印出来。假设每个字的长度小于线宽。
像 MS Word 这样的文字处理器做放置换行符的任务。这个想法是要有平衡的线条。换句话说，不要有几行有大量额外空间的行和一些有少量额外空间的行。

```
The extra spaces includes spaces put at the end of every line except the last one.  
The problem is to minimize the following total cost.
 Cost of a line = (Number of extra spaces in the line)^3
 Total Cost = Sum of costs for all lines

For example, consider the following string and line width M = 15
 "Geeks for Geeks presents word wrap problem" 

Following is the optimized arrangement of words in 3 lines
Geeks for Geeks
presents word
wrap problem 

The total extra spaces in line 1, line 2 and line 3 are 0, 2 and 3 respectively. 
So optimal value of total cost is 0 + 2*2 + 3*3 = 13
```

请注意，总成本函数不是额外空间的总和，而是额外空间的立方之和(或也使用平方)。这个成本函数背后的思想是平衡线之间的空间。例如，考虑以下同一组单词的两种排列:
**1)** 有 3 行。一行有 3 个额外的空格，所有其他行有 0 个额外的空格。总额外空间= 3 + 0 + 0 = 3。总成本= 3*3*3 + 0*0*0 + 0*0*0 = 27。
**2)** 有 3 条线。3 行中的每一行都有一个额外的空格。总额外空间= 1 + 1 + 1 = 3。总成本= 1*1*1 + 1*1*1 + 1*1*1 = 3。
在这两种情况下，总的额外空间都是 3，但是第二种排列应该是优选的，因为额外空间在所有三行中都是平衡的。由于第二种情况下的总成本值较小，所以立方和的成本函数可以达到这个目的。

**方法 1(贪婪的解决方案)**
贪婪的解决方案是在第一行放置尽可能多的单词。然后对第二行做同样的事情，以此类推，直到所有单词都被放置。这个解在很多情况下给出最优解，但不是在所有情况下都给出最优解。例如，考虑以下字符串“aaa bb cc ddddd”，线宽为 6。贪婪方法将产生以下输出。

```
aaa bb 
cc 
ddddd
```

以上 3 行的额外空格分别为 0、4、1。所以总成本是 0 + 64 + 1 = 65。
但以上解决方案并不是最佳方案。跟随排列有更平衡的空间。因此总成本函数的价值较小。

```
aaa
bb cc
ddddd
```

以上 3 行的多余空格分别为 3、1、1。所以总成本是 27 + 1 + 1 = 29。
尽管在某些情况下是次优的，但贪婪方法被许多文字处理器使用，如微软 word 和 OpenOffice.org Writer。

**方法 2(带记忆的递归方法)**

这个问题可以用分治法(递归)来解决。其算法如下:

```
1\. We recur for each word starting with first word, and remaining length of the line (initially k).
2\. The last word would be the base case:
    We check if we can put it on same line:
        if yes, then we return cost as 0.
        if no, we return cost of current line based on its remaining length.
3\. For non-last words, we have to check if it can fit in the current line:
    if yes, then we have two choices i.e. whether to put it in same line or next line.
        if we put it on next line: cost1 = square(remLength) + cost of putting word on next line.
        if we put it on same line: cost2 = cost of putting word on same line.
        return min(cost1, cost2)
    if no, then we have to put it on next line:
        return cost of putting word on next line
4\. We use memoization table of size n (number of words) * k (line length), to keep track of already visited positions.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.Arrays;

public class WordWrapDpMemo {

    private int solveWordWrap(int[] nums, int k) {
        int[][] memo = new int[nums.length][k + 1];
        for (int i = 0; i < nums.length; i++) {
            Arrays.fill(memo[i], -1);
        }
        return solveWordWrapUsingMemo(nums, nums.length, k, 0, k, memo);
    }

    private int solveWordWrap(int[] words, int n, int length, int wordIndex, int remLength, int[][] memo) {

        //base case for last word
        if (wordIndex == n - 1) {
            memo[wordIndex][remLength] = words[wordIndex] < remLength ? 0 : square(remLength);
            return memo[wordIndex][remLength];
        }

        int currWord = words[wordIndex];
        //if word can fit in the remaining line
        if (currWord < remLength) {
            return Math.min(
                    //if word is kept on same line
                    solveWordWrapUsingMemo(words, n, length, wordIndex + 1, remLength == length ? remLength - currWord : remLength - currWord - 1, memo),
                    //if word is kept on next line
                    square(remLength) + solveWordWrapUsingMemo(words, n, length, wordIndex + 1, length - currWord, memo)
            );
        } else {
            //if word is kept on next line
            return square(remLength) + solveWordWrapUsingMemo(words, n, length, wordIndex + 1, length - currWord, memo);
        }
    }

    private int solveWordWrapUsingMemo(int[] words, int n, int length, int wordIndex, int remLength, int[][] memo) {
        if (memo[wordIndex][remLength] != -1) {
            return memo[wordIndex][remLength];
        }

        memo[wordIndex][remLength] = solveWordWrap(words, n, length, wordIndex, remLength, memo);
        return memo[wordIndex][remLength];
    }

    private int square(int n) {
        return n * n;
    }

    public static void main(String[] args) {
        System.out.println(new WordWrapDpMemo().solveWordWrap(new int[]{3, 2, 2, 5}, 6));
    }
}
```

## C#

```
/*package whatever //do not write package name here */
using System;
using System.Collections.Generic;

public class WordWrapDpMemo {

    private int solveWordWrap(int[] nums, int k)
    {
        int[,] memo = new int[nums.Length ,k + 1];
        for (int i = 0; i < memo.GetLength(0); i++)
        {
            for(int j = 0; j < memo.GetLength(1); j++)
            memo[i, j] = -1;
        }
        return solveWordWrapUsingMemo(nums, nums.Length,
                                      k, 0, k, memo);
    }

    private int solveWordWrap(int[] words, int n,
                              int length, int wordIndex,
                              int remLength, int[,] memo)
    {

        // base case for last word
        if (wordIndex == n - 1) {
            memo[wordIndex, remLength] = words[wordIndex] <
              remLength ? 0 : square(remLength);
            return memo[wordIndex, remLength];
        }

        int currWord = words[wordIndex];

        // if word can fit in the remaining line
        if (currWord < remLength) {
            return Math.Min(

                    // if word is kept on same line
                    solveWordWrapUsingMemo(words, n, length, wordIndex + 1,
                            remLength == length ? remLength -
                                           currWord : remLength -
                                           currWord - 1, memo),

              // if word is kept on next line
                    square(remLength)
                            + solveWordWrapUsingMemo(words, n,
                                                     length,
                                                     wordIndex + 1,
                                                     length - currWord,
                                                     memo));
        } else {
            // if word is kept on next line
            return square(remLength) +
              solveWordWrapUsingMemo(words, n, length,
                                     wordIndex + 1,
                                     length - currWord, memo);
        }
    }

    private int solveWordWrapUsingMemo(int[] words, int n,
                                       int length, int wordIndex,
                                       int remLength, int[,] memo)
    {
        if (memo[wordIndex,remLength] != -1)
        {
            return memo[wordIndex,remLength];
        }

        memo[wordIndex,remLength] = solveWordWrap(words,
                                                  n, length,
                                                  wordIndex,
                                                  remLength, memo);
        return memo[wordIndex, remLength];
    }

    private int square(int n) {
        return n * n;
    }

    public static void Main(String[] args) {
        Console.WriteLine(new WordWrapDpMemo().
                          solveWordWrap(new int[] { 3, 2, 2, 5 }, 6));
    }
}

// This code is contributed by gauravrajput1
```

**Output**

```
10
```

**方法 3(动态规划)**
下面的动态方法严格遵循科曼书中给出的算法。首先，我们计算 2D 表 lc[][]中所有可能行的成本。值 lc[i][j]表示将 I 到 j 的单词放在一行中的成本，其中 I 和 j 是输入序列中单词的索引。如果从 I 到 j 的单词序列不能放在一行中，则 lc[i][j]被认为是无限的(以避免它成为解决方案的一部分)。一旦我们构建了 lc[][]表，我们就可以使用以下递归公式计算总成本。在下面的公式中，C[j]是从 1 到 j 排列单词的优化总成本

![](img/0ce1b66c8580d81702547eec5bf4b64c.png)

上面的递归有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。比如子问题 c(2)的解被 c(3)、C(4)等使用。因此，动态规划被用来存储子问题的结果。数组 c[]可以从左到右计算，因为每个值只依赖于较早的值。
为了打印输出，我们跟踪什么字在什么行上，我们可以保持一个平行的 p 数组，指向每个 c 值来自哪里。最后一行从字 p[n]开始，经过字 n。前一行从字 p[p[n]]开始，经过字 p[n]–1，等等。函数 printSolution()使用 p[]打印解决方案。
在下面的程序中，输入是一个数组 l[]，表示序列中单词的长度。值 l[i]表示输入序列中第 I 个单词(I 从 1 开始)的长度。

## C++

```
// A Dynamic programming solution for Word Wrap Problem
#include <bits/stdc++.h>
using namespace std;
#define INF INT_MAX

// A utility function to print the solution
int printSolution (int p[], int n);

// l[] represents lengths of different words in input sequence.
// For example, l[] = {3, 2, 2, 5} is for a sentence like
// "aaa bb cc ddddd". n is size of l[] and M is line width
// (maximum no. of characters that can fit in a line)
void solveWordWrap (int l[], int n, int M)
{
    // For simplicity, 1 extra space is used in all below arrays

    // extras[i][j] will have number of extra spaces if words from i
    // to j are put in a single line
    int extras[n+1][n+1];

    // lc[i][j] will have cost of a line which has words from
    // i to j
    int lc[n+1][n+1];

    // c[i] will have total cost of optimal arrangement of words
    // from 1 to i
    int c[n+1];

    // p[] is used to print the solution.
    int p[n+1];

    int i, j;

    // calculate extra spaces in a single line. The value extra[i][j]
    // indicates extra spaces if words from word number i to j are
    // placed in a single line
    for (i = 1; i <= n; i++)
    {
        extras[i][i] = M - l[i-1];
        for (j = i+1; j <= n; j++)
            extras[i][j] = extras[i][j-1] - l[j-1] - 1;
    }

    // Calculate line cost corresponding to the above calculated extra
    // spaces. The value lc[i][j] indicates cost of putting words from
    // word number i to j in a single line
    for (i = 1; i <= n; i++)
    {
        for (j = i; j <= n; j++)
        {
            if (extras[i][j] < 0)
                lc[i][j] = INF;
            else if (j == n && extras[i][j] >= 0)
                lc[i][j] = 0;
            else
                lc[i][j] = extras[i][j]*extras[i][j];
        }
    }

    // Calculate minimum cost and find minimum cost arrangement.
    // The value c[j] indicates optimized cost to arrange words
    // from word number 1 to j.
    c[0] = 0;
    for (j = 1; j <= n; j++)
    {
        c[j] = INF;
        for (i = 1; i <= j; i++)
        {
            if (c[i-1] != INF && lc[i][j] != INF &&
                           (c[i-1] + lc[i][j] < c[j]))
            {
                c[j] = c[i-1] + lc[i][j];
                p[j] = i;
            }
        }
    }

    printSolution(p, n);
}

int printSolution (int p[], int n)
{
    int k;
    if (p[n] == 1)
        k = 1;
    else
        k = printSolution (p, p[n]-1) + 1;
    cout<<"Line number "<<k<<": From word no. "<<p[n]<<" to "<<n<<endl;
    return k;
}

// Driver program to test above functions
int main()
{
    int l[] = {3, 2, 2, 5};
    int n = sizeof(l)/sizeof(l[0]);
    int M = 6;
    solveWordWrap (l, n, M);
    return 0;
}

//This is code is contributed by rathbhupendra
```

## C

```
// A Dynamic programming solution for Word Wrap Problem
#include <limits.h>
#include <stdio.h>
#define INF INT_MAX

// A utility function to print the solution
int printSolution (int p[], int n);

// l[] represents lengths of different words in input sequence.
// For example, l[] = {3, 2, 2, 5} is for a sentence like
// "aaa bb cc ddddd". n is size of l[] and M is line width
// (maximum no. of characters that can fit in a line)
void solveWordWrap (int l[], int n, int M)
{
    // For simplicity, 1 extra space is used in all below arrays

    // extras[i][j] will have number of extra spaces if words from i
    // to j are put in a single line
    int extras[n+1][n+1]; 

    // lc[i][j] will have cost of a line which has words from
    // i to j
    int lc[n+1][n+1];

    // c[i] will have total cost of optimal arrangement of words
    // from 1 to i
    int c[n+1];

    // p[] is used to print the solution. 
    int p[n+1];

    int i, j;

    // calculate extra spaces in a single line.  The value extra[i][j]
    // indicates extra spaces if words from word number i to j are
    // placed in a single line
    for (i = 1; i <= n; i++)
    {
        extras[i][i] = M - l[i-1];
        for (j = i+1; j <= n; j++)
            extras[i][j] = extras[i][j-1] - l[j-1] - 1;
    }

    // Calculate line cost corresponding to the above calculated extra
    // spaces. The value lc[i][j] indicates cost of putting words from
    // word number i to j in a single line
    for (i = 1; i <= n; i++)
    {
        for (j = i; j <= n; j++)
        {
            if (extras[i][j] < 0)
                lc[i][j] = INF;
            else if (j == n && extras[i][j] >= 0)
                lc[i][j] = 0;
            else
                lc[i][j] = extras[i][j]*extras[i][j];
        }
    }

    // Calculate minimum cost and find minimum cost arrangement.
    //  The value c[j] indicates optimized cost to arrange words
    // from word number 1 to j.
    c[0] = 0;
    for (j = 1; j <= n; j++)
    {
        c[j] = INF;
        for (i = 1; i <= j; i++)
        {
            if (c[i-1] != INF && lc[i][j] != INF &&
               (c[i-1] + lc[i][j] < c[j]))
            {
                c[j] = c[i-1] + lc[i][j];
                p[j] = i;
            }
        }
    }

    printSolution(p, n);
}

int printSolution (int p[], int n)
{
    int k;
    if (p[n] == 1)
        k = 1;
    else
        k = printSolution (p, p[n]-1) + 1;
    printf ("Line number %d: From word no. %d to %d \n", k, p[n], n);
    return k;
}

// Driver program to test above functions
int main()
{
    int l[] = {3, 2, 2, 5};
    int n = sizeof(l)/sizeof(l[0]);
    int M = 6;
    solveWordWrap (l, n, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic programming solution for
// Word Wrap Problem in Java
public class WordWrap
{

    final int MAX = Integer.MAX_VALUE;

    // A utility function to print the solution
    int printSolution (int p[], int n)
    {
        int k;
        if (p[n] == 1)
        k = 1;
        else
        k = printSolution (p, p[n]-1) + 1;
        System.out.println("Line number" + " " + k + ": " +
                    "From word no." +" "+ p[n] + " " + "to" + " " + n);
        return k;
    }

// l[] represents lengths of different words in input sequence.
// For example, l[] = {3, 2, 2, 5} is for a sentence like
// "aaa bb cc ddddd". n is size of l[] and M is line width
// (maximum no. of characters that can fit in a line)
    void solveWordWrap (int l[], int n, int M)
    {
        // For simplicity, 1 extra space is used in all below arrays

        // extras[i][j] will have number of extra spaces if words from i
        // to j are put in a single line
        int extras[][] = new int[n+1][n+1];

        // lc[i][j] will have cost of a line which has words from
        // i to j
        int lc[][]= new int[n+1][n+1];

        // c[i] will have total cost of optimal arrangement of words
        // from 1 to i
        int c[] = new int[n+1];

        // p[] is used to print the solution.
        int p[] =new int[n+1];

        // calculate extra spaces in a single line. The value extra[i][j]
        // indicates extra spaces if words from word number i to j are
        // placed in a single line
        for (int i = 1; i <= n; i++)
        {
            extras[i][i] = M - l[i-1];
            for (int j = i+1; j <= n; j++)
            extras[i][j] = extras[i][j-1] - l[j-1] - 1;
        }

        // Calculate line cost corresponding to the above calculated extra
        // spaces. The value lc[i][j] indicates cost of putting words from
        // word number i to j in a single line
        for (int i = 1; i <= n; i++)
        {
            for (int j = i; j <= n; j++)
            {
                if (extras[i][j] < 0)
                    lc[i][j] = MAX;
                else if (j == n && extras[i][j] >= 0)
                    lc[i][j] = 0;
                else
                    lc[i][j] = extras[i][j]*extras[i][j];
            }
        }

        // Calculate minimum cost and find minimum cost arrangement.
        // The value c[j] indicates optimized cost to arrange words
        // from word number 1 to j.
        c[0] = 0;
        for (int j = 1; j <= n; j++)
        {
            c[j] = MAX;
            for (int i = 1; i <= j; i++)
            {
                if (c[i-1] != MAX && lc[i][j] != MAX &&
                   (c[i-1] + lc[i][j] < c[j]))
                {
                    c[j] = c[i-1] + lc[i][j];
                    p[j] = i;
                }
            }
        }

        printSolution(p, n);
    }

    public static void main(String args[])
    {
        WordWrap w = new WordWrap();
        int l[] = {3, 2, 2, 5};
        int n = l.length;
        int M = 6;
        w.solveWordWrap (l, n, M);
    }
}

// This code is contributed by Saket Kumar
```

## 蟒蛇 3

```
# A Dynamic programming solution
# for Word Wrap Problem

# A utility function to print
# the solution
# l[] represents lengths of different
# words in input sequence. For example,
# l[] = {3, 2, 2, 5} is for a sentence
# like "aaa bb cc ddddd". n is size of
# l[] and M is line width (maximum no.
# of characters that can fit in a line)
INF = 2147483647
def printSolution(p, n):
    k = 0
    if p[n] == 1:
        k = 1
    else:
        k = printSolution(p, p[n] - 1) + 1
    print('Line number ', k, ': From word no. ',
                                 p[n], 'to ', n)
    return k

def solveWordWrap (l, n, M):

    # For simplicity, 1 extra space is
    # used in all below arrays

    # extras[i][j] will have number
    # of extra spaces if words from i
    # to j are put in a single line
    extras = [[0 for i in range(n + 1)]
                 for i in range(n + 1)]

    # lc[i][j] will have cost of a line
    # which has words from i to j
    lc = [[0 for i in range(n + 1)]
             for i in range(n + 1)]

    # c[i] will have total cost of
    # optimal arrangement of words
    # from 1 to i
    c = [0 for i in range(n + 1)]

    # p[] is used to print the solution.
    p = [0 for i in range(n + 1)]

    # calculate extra spaces in a single
    # line. The value extra[i][j] indicates
    # extra spaces if words from word number
    # i to j are placed in a single line
    for i in range(n + 1):
        extras[i][i] = M - l[i - 1]
        for j in range(i + 1, n + 1):
            extras[i][j] = (extras[i][j - 1] -
                                    l[j - 1] - 1)

    # Calculate line cost corresponding
    # to the above calculated extra
    # spaces. The value lc[i][j] indicates
    # cost of putting words from word number
    # i to j in a single line
    for i in range(n + 1):
        for j in range(i, n + 1):
            if extras[i][j] < 0:
                lc[i][j] = INF;
            elif j == n and extras[i][j] >= 0:
                lc[i][j] = 0
            else:
                lc[i][j] = (extras[i][j] *
                            extras[i][j])

    # Calculate minimum cost and find
    # minimum cost arrangement. The value
    # c[j] indicates optimized cost to
    # arrange words from word number 1 to j.
    c[0] = 0
    for j in range(1, n + 1):
        c[j] = INF
        for i in range(1, j + 1):
            if (c[i - 1] != INF and
                lc[i][j] != INF and
                ((c[i - 1] + lc[i][j]) < c[j])):
                c[j] = c[i-1] + lc[i][j]
                p[j] = i
    printSolution(p, n)

# Driver Code
l = [3, 2, 2, 5]
n = len(l)
M = 6
solveWordWrap(l, n, M)

# This code is contributed by sahil shelangia
```

## C#

```
// A Dynamic programming solution for Word Wrap
// Problem in Java
using System;

public class GFG {

    static int MAX = int.MaxValue;

    // A utility function to print the solution
    static int printSolution (int []p, int n)
    {
        int k;

        if (p[n] == 1)
            k = 1;
        else
            k = printSolution (p, p[n]-1) + 1;

        Console.WriteLine("Line number" + " "
                + k + ": From word no." + " "
                + p[n] + " " + "to" + " " + n);
        return k;
    }

    // l[] represents lengths of different
    // words in input sequence. For example,
    // l[] = {3, 2, 2, 5} is for a sentence
    // like "aaa bb cc ddddd". n is size of
    // l[] and M is line width (maximum no.
    // of characters that can fit in a line)
    static void solveWordWrap (int []l, int n,
                                        int M)
    {

        // For simplicity, 1 extra space
        // is used in all below arrays

        // extras[i][j] will have number of
        // extra spaces if words from i
        // to j are put in a single line
        int [,]extras = new int[n+1,n+1];

        // lc[i][j] will have cost of a line
        // which has words from i to j
        int [,]lc = new int[n+1,n+1];

        // c[i] will have total cost of
        // optimal arrangement of words
        // from 1 to i
        int []c = new int[n+1];

        // p[] is used to print the solution.
        int []p = new int[n+1];

        // calculate extra spaces in a single
        // line. The value extra[i][j] indicates
        // extra spaces if words from word number
        // i to j are placed in a single line
        for (int i = 1; i <= n; i++)
        {
            extras[i,i] = M - l[i-1];

            for (int j = i+1; j <= n; j++)
                extras[i,j] = extras[i,j-1]
                                 - l[j-1] - 1;
        }

        // Calculate line cost corresponding to
        // the above calculated extra spaces. The
        // value lc[i][j] indicates cost of
        // putting words from word number i to
        // j in a single line
        for (int i = 1; i <= n; i++)
        {
            for (int j = i; j <= n; j++)
            {
                if (extras[i,j] < 0)
                    lc[i,j] = MAX;
                else if (j == n &&
                              extras[i,j] >= 0)
                    lc[i,j] = 0;
                else
                    lc[i,j] = extras[i,j]
                                 * extras[i,j];
            }
        }

        // Calculate minimum cost and find
        // minimum cost arrangement. The value
        // c[j] indicates optimized cost to
        // arrange words from word number
        // 1 to j.
        c[0] = 0;
        for (int j = 1; j <= n; j++)
        {
            c[j] = MAX;
            for (int i = 1; i <= j; i++)
            {
                if (c[i-1] != MAX && lc[i,j]
                    != MAX && (c[i-1] + lc[i,j]
                                       < c[j]))
                {
                    c[j] = c[i-1] + lc[i,j];
                    p[j] = i;
                }
            }
        }

        printSolution(p, n);
    }

    // Driver code
    public static void Main()
    {
        int []l = {3, 2, 2, 5};
        int n = l.Length;
        int M = 6;
        solveWordWrap (l, n, M);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>
    // A Dynamic programming solution for
    // Word Wrap Problem in Javascript

    let MAX = Number.MAX_VALUE;

    // A utility function to print the solution
    function printSolution (p, n)
    {
        let k;
        if (p[n] == 1)
            k = 1;
        else
            k = printSolution (p, p[n]-1) + 1;
        document.write("Line number" + " " + k + ": " +
                    "From word no." +" "+ p[n] + " " + "to" + " " + n + "</br>");
        return k;
    }

    // l[] represents lengths of different words in input sequence.
    // For example, l[] = {3, 2, 2, 5} is for a sentence like
    // "aaa bb cc ddddd". n is size of l[] and M is line width
    // (maximum no. of characters that can fit in a line)
    function solveWordWrap (l, n, M)
    {
        // For simplicity, 1 extra space is used in all below arrays

        // extras[i][j] will have number of extra spaces if words from i
        // to j are put in a single line
        let extras = new Array(n+1);

        // lc[i][j] will have cost of a line which has words from
        // i to j
        let lc = new Array(n+1);

        for(let i = 0; i < n + 1; i++)
        {
            extras[i] = new Array(n + 1);
            lc[i] = new Array(n + 1);
            for(let j = 0; j < n + 1; j++)
            {
                extras[i][j] = 0;
                lc[i][j] = 0;
            }
        }

        // c[i] will have total cost of optimal arrangement of words
        // from 1 to i
        let c = new Array(n+1);

        // p[] is used to print the solution.
        let p = new Array(n+1);

        // calculate extra spaces in a single line. The value extra[i][j]
        // indicates extra spaces if words from word number i to j are
        // placed in a single line
        for (let i = 1; i <= n; i++)
        {
            extras[i][i] = M - l[i-1];
            for (let j = i+1; j <= n; j++)
                extras[i][j] = extras[i][j-1] - l[j-1] - 1;
        }

        // Calculate line cost corresponding to the above calculated extra
        // spaces. The value lc[i][j] indicates cost of putting words from
        // word number i to j in a single line
        for (let i = 1; i <= n; i++)
        {
            for (let j = i; j <= n; j++)
            {
                if (extras[i][j] < 0)
                    lc[i][j] = MAX;
                else if (j == n && extras[i][j] >= 0)
                    lc[i][j] = 0;
                else
                    lc[i][j] = extras[i][j]*extras[i][j];
            }
        }

        // Calculate minimum cost and find minimum cost arrangement.
        // The value c[j] indicates optimized cost to arrange words
        // from word number 1 to j.
        c[0] = 0;
        for (let j = 1; j <= n; j++)
        {
            c[j] = MAX;
            for (let i = 1; i <= j; i++)
            {
                if (c[i-1] != MAX && lc[i][j] != MAX &&
                   (c[i-1] + lc[i][j] < c[j]))
                {
                    c[j] = c[i-1] + lc[i][j];
                    p[j] = i;
                }
            }
        }

        printSolution(p, n);
    }

    let l = [3, 2, 2, 5];
    let n = l.length;
    let M = 6;
    solveWordWrap (l, n, M);

    // This code is contributed by mukesh07.
</script>
```

**Output**

```
Line number 1: From word no. 1 to 1
Line number 2: From word no. 2 to 3
Line number 3: From word no. 4 to 4
```

时间复杂度:O(n^2)
辅助空间:O(n^2)上述程序中使用的辅助空间可以优化为 O(n)(详见参考文献 2)
[**绕词问题(空间优化解决方案)**](https://www.geeksforgeeks.org/word-wrap-problem-space-optimized-solution/)
**参考文献:**
[http://en.wikipedia.org/wiki/Word_wrap](http://en.wikipedia.org/wiki/Word_wrap)
如发现任何不正确的地方，或者您想分享更多关于上述讨论主题的信息，请写评论。