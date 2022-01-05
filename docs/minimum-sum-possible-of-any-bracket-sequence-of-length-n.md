# 长度为 N 的任何括号序列的最小可能和

> 原文:[https://www . geeksforgeeks . org/最小可能任意长度括号序列之和 n/](https://www.geeksforgeeks.org/minimum-sum-possible-of-any-bracket-sequence-of-length-n/)

给定一个数字 N，表示由括号“(”、“)”组成的括号序列的长度。实际的顺序事先并不知道。给定括号“(”和“)”的值，如果放在表达式的索引![i   ](img/c219860f95052b9f6ddef0ea3ab54389.png "Rendered by QuickLaTeX.com")处。
任务是利用上述信息找到长度为 N 的任何括号序列的最小可能和。
此处 adj[i][0]代表分配给索引处“)”括号的值，adj[i][1]代表分配给索引处“(”括号的值。
**约束**:T6

*   应该有 N/2 对支架。即 N/2 对“(”、“)”。
*   求适当括号表达式的最小和。
*   索引从 0 开始。

**示例** :

```
Input : N = 4 
        adj[N][2] ={{5000, 3000},
                    {6000, 2000}, 
                    {8000, 1000}, 
                    {9000, 6000}} 
Output : 19000
Assigning first index as '(' for proper 
bracket expression is (_ _ _  . 
Now all the possible bracket expressions are ()() and (()). 
where '(' denotes as adj[i][1] and ')' denotes as adj[i][0]. 
Hence, for ()() sum is 3000+6000+1000+9000=19000.
and (()), sum is 3000+2000+8000+9000=220000\. 
Thus answer is 19000

Input : N = 4 
        adj[N][2] = {{435, 111},
                     {43, 33}, 
                     {1241, 1111}, 
                     {234, 22}}
Output : 1499
```

**算法** :

1.  括号序列的第一个元素只能是'('，因此 adj[0][1]的值只能在索引 0 处使用。
2.  调用一个函数，使用 dp 找到合适的括号表达式，如本文所述。
3.  将“_”降级为 adj[i][1]并将“)”降级为 adj[i][0]。
4.  找出所有可能的正确括号表达式的最小和。
5.  返回答案+ adj[0][1]。

以下是上述方法的实现:

## C++

```
// C++ program to find the Minimum sum possible
// of any bracket sequence of length N using
// the given values for brackets

#include <bits/stdc++.h>
using namespace std;

#define MAX_VAL 10000000

// DP array
int dp[100][100];

// Recursive function to check for
// correct bracket expression
int find(int index, int openbrk, int n, int adj[][2])
{
    /// Not a proper bracket expression
    if (openbrk < 0)
        return MAX_VAL;

    // If reaches at end
    if (index == n) {

        /// If proper bracket expression
        if (openbrk == 0) {
            return 0;
        }
        else // if not, return max
            return MAX_VAL;
    }

    // If already visited
    if (dp[index][openbrk] != -1)
        return dp[index][openbrk];

    // To find out minimum sum
    dp[index][openbrk] = min(adj[index][1] + find(index + 1,
                                                  openbrk + 1, n, adj),
                             adj[index][0] + find(index + 1,
                                                  openbrk - 1, n, adj));

    return dp[index][openbrk];
}

// Driver Code
int main()
{
    int n = 4;
    int adj[n][2] = { { 5000, 3000 },
                      { 6000, 2000 },
                      { 8000, 1000 },
                      { 9000, 6000 } };

    memset(dp, -1, sizeof(dp));

    cout << find(1, 1, n, adj) + adj[0][1] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Minimum sum possible
// of any bracket sequence of length N using
// the given values for brackets

public class GFG {

    final static int MAX_VAL = 10000000 ;

    // DP array
    static int dp[][] = new int[100][100];

    // Recursive function to check for
    // correct bracket expression
    static int find(int index, int openbrk, int n, int adj[][])
    {
        /// Not a proper bracket expression
        if (openbrk < 0)
            return MAX_VAL;

        // If reaches at end
        if (index == n) {

            /// If proper bracket expression
            if (openbrk == 0) {
                return 0;
            }
            else // if not, return max
                return MAX_VAL;
        }

        // If already visited
        if (dp[index][openbrk] != -1)
            return dp[index][openbrk];

        // To find out minimum sum
        dp[index][openbrk] = Math.min(adj[index][1] + find(index + 1,
                                                      openbrk + 1, n, adj),
                                 adj[index][0] + find(index + 1,
                                                      openbrk - 1, n, adj));

        return dp[index][openbrk];
    }

// Driver code
    public static void main(String args[])
    {
            int n = 4;
            int adj[][] = { { 5000, 3000 },
                              { 6000, 2000 },
                              { 8000, 1000 },
                              { 9000, 6000 } };

            for (int i = 0; i < dp.length; i ++)
                for (int j = 0; j < dp.length; j++)
                    dp[i][j] = -1 ;

            System.out.println(find(1, 1, n, adj) + adj[0][1]);

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 program to find the Minimum sum
# possible of any bracket sequence of length
# N using the given values for brackets

MAX_VAL = 10000000

# DP array
dp = [[-1 for i in range(100)]
          for i in range(100)]

# Recursive function to check for
# correct bracket expression
def find(index, openbrk, n, adj):

    # Not a proper bracket expression
    if (openbrk < 0):
        return MAX_VAL

    # If reaches at end
    if (index == n):

        # If proper bracket expression
        if (openbrk == 0):
            return 0

    # if not, return max
        else:
            return MAX_VAL

    # If already visited
    if (dp[index][openbrk] != -1):
        return dp[index][openbrk]

    # To find out minimum sum
    dp[index][openbrk] = min(adj[index][1] + find(index + 1,
                                             openbrk + 1, n, adj),
                             adj[index][0] + find(index + 1,
                                             openbrk - 1, n, adj))

    return dp[index][openbrk]

# Driver Code
if __name__ == '__main__':
    n = 4;
    adj = [[5000, 3000],[6000, 2000],
           [8000, 1000],[9000, 6000]]

    print(find(1, 1, n, adj) + adj[0][1])

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find the Minimum sum possible
// of any bracket sequence of length N using
// the given values for brackets
using System;

class GFG
{
    public static int MAX_VAL = 10000000;

    // DP array
    public static int[,] dp = new int[100,100];

    // Recursive function to check for
    // correct bracket expression
    public static int find(int index, int openbrk, int n, int[,] adj)
    {
        /// Not a proper bracket expression
        if (openbrk < 0)
            return MAX_VAL;

        // If reaches at end
        if (index == n) {

            /// If proper bracket expression
            if (openbrk == 0) {
                return 0;
            }
            else // if not, return max
                return MAX_VAL;
        }

        // If already visited
        if (dp[index,openbrk] != -1)
            return dp[index,openbrk];

        // To find out minimum sum
        dp[index,openbrk] = Math.Min(adj[index,1] + find(index + 1,
                                                      openbrk + 1, n, adj),
                                 adj[index,0] + find(index + 1,
                                                      openbrk - 1, n, adj));

        return dp[index,openbrk];
    }

    // Driver Code     

    static void Main()
    {
        int n = 4;

        int[,] adj = new int[,]{
                            { 5000, 3000 },
                            { 6000, 2000 },
                            { 8000, 1000 },
                            { 9000, 6000 }
        };

        for(int i = 0; i < 100; i++)
            for(int j = 0; j < 100; j++)
                dp[i,j] = -1;

        Console.Write(find(1, 1, n, adj) + adj[0,1] + "\n");
    }
    //This code is contributed by DrRoot_
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Minimum sum possible
// of any bracket sequence of length N using
// the given values for brackets
$MAX_VAL = 10000000;
$dp = array_fill(0, 100,
      array_fill(0, 100, -1));

// Recursive function to check for
// correct bracket expression
function find($index, $openbrk, $n, $adj)
{
    global $MAX_VAL;
    global $dp;

    /// Not a proper bracket expression
    if ($openbrk < 0)
        return $MAX_VAL;

    // If reaches at end
    if ($index == $n)
    {

        /// If proper bracket expression
        if ($openbrk == 0)
        {
            return 0;
        }
        else // if not, return max
            return $MAX_VAL;
    }

    // If already visited
    if ($dp[$index][$openbrk] != -1)
        return $dp[$index][$openbrk];

    // To find out minimum sum
    $dp[$index][$openbrk] = min($adj[$index][1] +
                           find($index + 1, $openbrk + 1, $n, $adj),
                                $adj[$index][0] +
                           find($index + 1, $openbrk - 1, $n, $adj));

    return $dp[$index][$openbrk];
}

// Driver Code
$n = 4;
$adj = array(array(5000, 3000),
             array(6000, 2000),
             array(8000, 1000),
             array(9000, 6000));

echo find(1, 1, $n, $adj) + $adj[0][1];

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the Minimum sum possible
    // of any bracket sequence of length N using
    // the given values for brackets

    let MAX_VAL = 10000000 ;

    // DP array
    let dp = new Array(100);
    for(let i = 0; i < 100; i++)
    {
        dp[i] = new Array(100);
        for(let j = 0; j < 100; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Recursive function to check for
    // correct bracket expression
    function find(index, openbrk, n, adj)
    {
        /// Not a proper bracket expression
        if (openbrk < 0)
            return MAX_VAL;

        // If reaches at end
        if (index == n) {

            /// If proper bracket expression
            if (openbrk == 0) {
                return 0;
            }
            else // if not, return max
                return MAX_VAL;
        }

        // If already visited
        if (dp[index][openbrk] != -1)
            return dp[index][openbrk];

        // To find out minimum sum
        dp[index][openbrk] = Math.min(adj[index][1] + find(index + 1,
                                                      openbrk + 1, n, adj),
                                 adj[index][0] + find(index + 1,
                                                      openbrk - 1, n, adj));

        return dp[index][openbrk];
    }

    let n = 4;
    let adj = [ [ 5000, 3000 ],
                [ 6000, 2000 ],
                [ 8000, 1000 ],
                [ 9000, 6000 ] ];

    for (let i = 0; i < dp.length; i ++)
      for (let j = 0; j < dp.length; j++)
        dp[i][j] = -1 ;

    document.write(find(1, 1, n, adj) + adj[0][1]);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
19000
```

**时间复杂度** : O(N <sup>2</sup> )