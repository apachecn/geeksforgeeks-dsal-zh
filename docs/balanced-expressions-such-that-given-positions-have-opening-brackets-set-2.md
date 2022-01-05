# 平衡表达式，给定位置有左括号|设置 2

> 原文:[https://www . geesforgeks . org/balanced-expressions-so-给定位置-有-开-括号-set-2/](https://www.geeksforgeeks.org/balanced-expressions-such-that-given-positions-have-opening-brackets-set-2/)

给定一个整数 n 和一个位置数组“position[]”(1 < = length(position[])< = 2n)，找出长度为 2n 的适当括号表达式的数量，以便给定的位置有左括号。

**注意:**位置[]数组是以(基于 1 的索引)[0，1，1，0]的形式给出的。这里 1 表示开放式支架应该放置的位置。在值为 0 的位置，可以放置左括号或右括号。

**示例**:

> **输入** : n = 3，位置[] = [0，1，0，0，0]
> **输出** : 3
> 长度 6 和位置 2 的
> 开括号的合适的括号顺序是:
> [[]][][]
> [[]]
> [[][][]]
> 
> **输入** : n = 2，位置[]=【1，0，1，0】
> **输出** : 1
> 唯一的可能是:
> []

这个问题的动态规划方法已经在[这里](https://www.geeksforgeeks.org/balanced-expressions-such-that-given-positions-have-opening-brackets/)讨论过了。在这篇文章中，将讨论使用记忆化方法的递归和递归。

**算法**–

1.  将给定数组中所有带方括号的位置标记为 1。
2.  运行递归循环，例如–
    *   如果括号总数(左括号减去右括号)小于零，则返回 0。
    *   如果索引达到直到 n，并且如果括号总数=0，则得到一个解并返回 1，否则返回 0。
    *   如果索引预先分配了 1，则用 index+1 递归返回该函数，并增加括号总数。
    *   否则，通过在该索引处插入开括号并将总括号增加 1 +在该索引处插入闭括号并将总括号减少 1 来递归返回该函数，并继续下一个索引，直到 n

以下是上述算法的**递归解**:

## C++

```
// C++ implementation of above
// approach using Recursion
#include <bits/stdc++.h>
using namespace std;

// Function to find Number of
// proper bracket expressions
int find(int index, int openbrk, int n, int adj[])
{
    // If open-closed brackets < 0
    if (openbrk < 0)
        return 0;

    // If index reaches the end of expression
    if (index == n) {

        // IF brackets are balanced
        if (openbrk == 0)
            return 1;
        else
            return 0;
    }

    // If the current index has assigned open bracket
    if (adj[index] == 1) {

        // Move forward increasing the
        // length of open brackets
        return find(index + 1, openbrk + 1, n, adj);
    }

    else {

        // Move forward by inserting open as well
        // as closed brackets on that index
        return find(index + 1, openbrk + 1, n, adj)
               + find(index + 1, openbrk - 1, n, adj);
    }
}
// Driver Code
int main()
{

    int n = 2;

    // Open brackets at position 1
    int adj[4] = { 1, 0, 0, 0 };

    // Calling the find function to calculate the answer
    cout << find(0, 0, 2 * n, adj) << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above
// approach using Recursion

class Test {
// Function to find Number of
// proper bracket expressions

    static int find(int index, int openbrk,
            int n, int[] adj) {
        // If open-closed brackets < 0
        if (openbrk < 0) {
            return 0;
        }

        // If index reaches the end of expression
        if (index == n) {

            // IF brackets are balanced
            if (openbrk == 0) {
                return 1;
            } else {
                return 0;
            }
        }

        // If the current index has assigned open bracket
        if (adj[index] == 1) {

            // Move forward increasing the
            // length of open brackets
            return find(index + 1, openbrk + 1, n, adj);
        } else {

            // Move forward by inserting open as well
            // as closed brackets on that index
            return find(index + 1, openbrk + 1, n, adj)
                    + find(index + 1, openbrk - 1, n, adj);
        }
    }

// Driver Code
    public static void main(String[] args) {
        int n = 2;

        // Open brackets at position 1
        int[] adj = {1, 0, 0, 0};

        // Calling the find function to calculate the answer
        System.out.print(find(0, 0, 2 * n, adj));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of above
# approach using memoizaion
N = 1000

# Function to find Number
# of proper bracket expressions
def find(index, openbrk, n, dp, adj):

    # If open-closed brackets<0
    if (openbrk < 0):
        return 0

    # If index reaches the end of expression
    if (index == n):

        # If brackets are balanced
        if (openbrk == 0):
            return 1
        else:
            return 0

    # If already stored in dp
    if (dp[index][openbrk] != -1):
        return dp[index][openbrk]

    # If the current index has assigned
    # open bracket
    if (adj[index] == 1):

        # Move forward increasing the
        # length of open brackets
        dp[index][openbrk] = find(index + 1,
                                  openbrk + 1, n, dp, adj)
    else:

        # Move forward by inserting open as
        # well as closed brackets on that index
        dp[index][openbrk] = (find(index + 1, openbrk + 1,
                                             n, dp, adj) +
                              find(index + 1, openbrk - 1,
                                              n, dp, adj))
    # return the answer
    return dp[index][openbrk]

# Driver Code

# DP array to precompute the answer
dp=[[-1 for i in range(N)]
        for i in range(N)]
n = 2;

# Open brackets at position 1
adj = [ 1, 0, 0, 0 ]

# Calling the find function to
# calculate the answer
print(find(0, 0, 2 * n, dp, adj))

# This code is contributed by sahishelangia
```

## C#

```
// C# implementation of above
// approach using Recursion
using System;

class GFG
{
// Function to find Number of
// proper bracket expressions
static int find(int index, int openbrk,
                int n, int[] adj)
{
    // If open-closed brackets < 0
    if (openbrk < 0)
        return 0;

    // If index reaches the end of expression
    if (index == n)
    {

        // IF brackets are balanced
        if (openbrk == 0)
            return 1;
        else
            return 0;
    }

    // If the current index has assigned open bracket
    if (adj[index] == 1)
    {

        // Move forward increasing the
        // length of open brackets
        return find(index + 1, openbrk + 1, n, adj);
    }

    else
    {

        // Move forward by inserting open as well
        // as closed brackets on that index
        return find(index + 1, openbrk + 1, n, adj)
            + find(index + 1, openbrk - 1, n, adj);
    }
}

// Driver Code
public static void Main()
{

    int n = 2;

    // Open brackets at position 1
    int[] adj = { 1, 0, 0, 0 };

    // Calling the find function to calculate the answer
    Console.WriteLine(find(0, 0, 2 * n, adj));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
// using Recursion

// Function to find Number of proper
// bracket expressions
function find($index, $openbrk, $n, &$adj)
{
    // If open-closed brackets < 0
    if ($openbrk < 0)
        return 0;

    // If index reaches the end
    // of expression
    if ($index == $n)
    {

        // IF brackets are balanced
        if ($openbrk == 0)
            return 1;
        else
            return 0;
    }

    // If the current index has assigned
    // open bracket
    if ($adj[$index] == 1)
    {

        // Move forward increasing the
        // length of open brackets
        return find($index + 1,
                    $openbrk + 1, $n, $adj);
    }

    else
    {

        // Move forward by inserting open as well
        // as closed brackets on that index
        return find($index + 1,
                    $openbrk + 1, $n, $adj) +
               find($index + 1,
                    $openbrk - 1, $n, $adj);
    }
}

// Driver Code
$n = 2;

// Open brackets at position 1
$adj = array(1, 0, 0, 0);

// Calling the find function to
// calculate the answer
echo find(0, 0, 2 * $n, $adj) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above
// approach using Recursion

// Function to find Number of
// proper bracket expressions
function find(index, openbrk, n, adj)
{

    // If open-closed brackets < 0
    if (openbrk < 0)
    {
        return 0;
    }

    // If index reaches the end of expression
    if (index == n)
    {

        // IF brackets are balanced
        if (openbrk == 0)
        {
            return 1;
        }
        else
        {
            return 0;
        }
    }

    // If the current index has
    // assigned open bracket
    if (adj[index] == 1)
    {

        // Move forward increasing the
        // length of open brackets
        return find(index + 1, openbrk + 1, n, adj);
    }
    else
    {

        // Move forward by inserting open as well
        // as closed brackets on that index
        return find(index + 1, openbrk + 1, n, adj) +
               find(index + 1, openbrk - 1, n, adj);
    }
}

// Driver Code
let n = 2;

// Open brackets at position 1
let adj = [ 1, 0, 0, 0 ];

// Calling the find function to
// calculate the answer
document.write(find(0, 0, 2 * n, adj));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```

**记忆方法:**利用**记忆**可以优化上述算法的时间复杂度。唯一要做的是使用一个数组来存储以前迭代的结果，这样如果已经计算了值，就不需要多次递归调用同一个函数。

以下是所需的实现:

## C++

```
// C++ implementation of above
// approach using memoization
#include <bits/stdc++.h>
using namespace std;

#define N 1000

// Function to find Number
// of proper bracket expressions
int find(int index, int openbrk, int n,
         int dp[N][N], int adj[])
{
    // If open-closed brackets<0
    if (openbrk < 0)
        return 0;

    // If index reaches the end of expression
    if (index == n) {

        // If brackets are balanced
        if (openbrk == 0)
            return 1;

        else
            return 0;
    }

    // If already stored in dp
    if (dp[index][openbrk] != -1)
        return dp[index][openbrk];

    // If the current index has assigned open bracket
    if (adj[index] == 1) {

        // Move forward increasing the
        // length of open brackets
        dp[index][openbrk] = find(index + 1,
                                  openbrk + 1, n, dp, adj);
    }
    else {
        // Move forward by inserting open as
        // well as closed brackets on that index
        dp[index][openbrk] = find(index + 1, openbrk + 1, n, dp, adj)
                             + find(index + 1, openbrk - 1, n, dp, adj);
    }
    // return the answer
    return dp[index][openbrk];
}

// Driver Code
int main()
{
    // DP array to precompute the answer
    int dp[N][N];
    int n = 2;

    memset(dp, -1, sizeof(dp));

    // Open brackets at position 1
    int adj[4] = { 1, 0, 0, 0 };

    // Calling the find function to calculate the answer
    cout << find(0, 0, 2 * n, dp, adj) << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above
// approach using memoization

public class GFG {

    static final int N = 1000;

// Function to find Number
// of proper bracket expressions
    static int find(int index, int openbrk, int n,
            int dp[][], int adj[]) {
        // If open-closed brackets<0
        if (openbrk < 0) {
            return 0;
        }

        // If index reaches the end of expression
        if (index == n) {

            // If brackets are balanced
            if (openbrk == 0) {
                return 1;
            } else {
                return 0;
            }
        }

        // If already stored in dp
        if (dp[index][openbrk] != -1) {
            return dp[index][openbrk];
        }

        // If the current index has assigned open bracket
        if (adj[index] == 1) {

            // Move forward increasing the
            // length of open brackets
            dp[index][openbrk] = find(index + 1,
                    openbrk + 1, n, dp, adj);
        } else {
            // Move forward by inserting open as
            // well as closed brackets on that index
            dp[index][openbrk] = find(index + 1, openbrk + 1, n, dp, adj)
                    + find(index + 1, openbrk - 1, n, dp, adj);
        }
        // return the answer
        return dp[index][openbrk];
    }

// Driver code
    public static void main(String[] args) {
        // DP array to precompute the answer
        int dp[][] = new int[N][N];
        int n = 2;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                dp[i][j] = -1;
            }
        }

        // Open brackets at position 1
        int adj[] = {1, 0, 0, 0};

        // Calling the find function to calculate the answer
        System.out.print(find(0, 0, 2 * n, dp, adj));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach
# using memoization
N = 1000;
dp = [[-1 for x in range(N)]
          for y in range(N)];

# Open brackets at position 1
adj = [ 1, 0, 0, 0 ];

# Function to find Number of proper
# bracket expressions
def find(index, openbrk, n):

    # If open-closed brackets<0
    if (openbrk < 0):
        return 0;

    # If index reaches the end of expression
    if (index == n):

        # If brackets are balanced
        if (openbrk == 0):
            return 1;

        else:
            return 0;

    # If already stored in dp
    if (dp[index][openbrk] != -1):
        return dp[index][openbrk];

    # If the current index has assigned
    # open bracket
    if (adj[index] == 1):

        # Move forward increasing the
        # length of open brackets
        dp[index][openbrk] = find(index + 1,
                                  openbrk + 1, n);
    else:

        # Move forward by inserting open as
        # well as closed brackets on that index
        dp[index][openbrk] = (find(index + 1, openbrk + 1, n) +
                              find(index + 1, openbrk - 1, n));
    # return the answer
    return dp[index][openbrk];

# Driver Code

# DP array to precompute the answer
n = 2;

# Calling the find function to
# calculate the answer
print(find(0, 0, 2 * n));

# This code is contributed by mits
```

## C#

```
// C# implementation of above
// approach using memoization
using System;

class GFG
{
    static readonly int N = 1000;

    // Function to find Number
    // of proper bracket expressions
    static int find(int index, int openbrk, int n,
            int [,]dp, int []adj)
    {
        // If open-closed brackets<0
        if (openbrk < 0)
        {
            return 0;
        }

        // If index reaches the end of expression
        if (index == n)
        {

            // If brackets are balanced
            if (openbrk == 0)
            {
                return 1;
            }
            else
            {
                return 0;
            }
        }

        // If already stored in dp
        if (dp[index,openbrk] != -1)
        {
            return dp[index, openbrk];
        }

        // If the current index has assigned open bracket
        if (adj[index] == 1)
        {

            // Move forward increasing the
            // length of open brackets
            dp[index, openbrk] = find(index + 1,
                    openbrk + 1, n, dp, adj);
        }
        else
        {
            // Move forward by inserting open as
            // well as closed brackets on that index
            dp[index, openbrk] = find(index + 1, openbrk + 1, n, dp, adj)
                    + find(index + 1, openbrk - 1, n, dp, adj);
        }

        // return the answer
        return dp[index,openbrk];
    }

    // Driver code
    public static void Main()
    {

        // DP array to precompute the answer
        int [,]dp = new int[N,N];
        int n = 2;

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                dp[i, j] = -1;
            }
        }

        // Open brackets at position 1
        int []adj = {1, 0, 0, 0};

        // Calling the find function to calculate the answer
        Console.WriteLine(find(0, 0, 2 * n, dp, adj));
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
// using memoization

// Function to find Number of proper
// bracket expressions
function find($index, $openbrk, $n,
                       &$dp, &$adj)
{
    // If open-closed brackets<0
    if ($openbrk < 0)
        return 0;

    // If index reaches the end of expression
    if ($index == $n)
    {

        // If brackets are balanced
        if ($openbrk == 0)
            return 1;

        else
            return 0;
    }

    // If already stored in dp
    if ($dp[$index][$openbrk] != -1)
        return $dp[$index][$openbrk];

    // If the current index has assigned
    // open bracket
    if ($adj[$index] == 1)
    {

        // Move forward increasing the
        // length of open brackets
        $dp[$index][$openbrk] = find($index + 1,
                                     $openbrk + 1, $n,
                                     $dp, $adj);
    }
    else
    {
        // Move forward by inserting open as
        // well as closed brackets on that index
        $dp[$index][$openbrk] = find($index + 1, $openbrk + 1,
                                                 $n, $dp, $adj) +
                                find($index + 1, $openbrk - 1,
                                                 $n, $dp, $adj);
    }
    // return the answer
    return $dp[$index][$openbrk];
}

// Driver Code

// DP array to precompute the answer
$N = 1000;
$dp = array(array());
$n = 2;

for ($i = 0; $i < $N; $i++)
{
    for ($j = 0; $j < $N; $j++)
    {
        $dp[$i][$j] = -1;
    }
}

// Open brackets at position 1
$adj = array( 1, 0, 0, 0 );

// Calling the find function to
// calculate the answer
echo find(0, 0, 2 * $n, $dp, $adj) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above
// approach using memoization
let N = 1000;

// Function to find Number
// of proper bracket expressions
function find(index, openbrk, n, dp, adj)
{

    // If open-closed brackets<0
    if (openbrk < 0)
    {
        return 0;
    }

    // If index reaches the end of expression
    if (index == n)
    {

        // If brackets are balanced
        if (openbrk == 0)
        {
            return 1;
        }
        else
        {
            return 0;
        }
    }

    // If already stored in dp
    if (dp[index][openbrk] != -1)
    {
        return dp[index][openbrk];
    }

    // If the current index has
    // assigned open bracket
    if (adj[index] == 1)
    {

        // Move forward increasing the
        // length of open brackets
        dp[index][openbrk] = find(index + 1,
                openbrk + 1, n, dp, adj);
    }
    else
    {

        // Move forward by inserting open as
        // well as closed brackets on that index
        dp[index][openbrk] = find(index + 1, openbrk + 1,
                                  n, dp, adj) +
                             find(index + 1, openbrk - 1,
                                  n, dp, adj);
    }

    // Return the answer
    return dp[index][openbrk];
}

// Driver code

// DP array to precompute the answer
let dp = new Array(N);
for(let i = 0; i < N; i++)
{
    dp[i] = new Array(N);
    for(let j = 0; j < N; j++)
    {
        dp[i][j] = -1;
    }
}

let n = 2;

// Open brackets at position 1
let adj = [ 1, 0, 0, 0 ];

// Calling the find function to
// calculate the answer
document.write(find(0, 0, 2 * n, dp, adj));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(N <sup>2</sup> )