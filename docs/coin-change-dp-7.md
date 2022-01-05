# 角变化| DP-7

> 原文:[https://www.geeksforgeeks.org/coin-change-dp-7/](https://www.geeksforgeeks.org/coin-change-dp-7/)

给定一个值 N，如果我们想用 N 美分兑换，我们有无限的 S = { S1，S2，..，Sm}估值硬币，我们可以通过多少种方式进行改变？硬币的顺序不重要。
例如，对于 N = 4 和 S = {1，2，3}，有四个解:{1，1，1，1}、{1，1，2}、{2，2}、{1，3}。所以输出应该是 4。对于 N = 10 和 S = {2，5，3，6}，有五种解决方案:{2，2，2，2，2}，{2，2，3，3}，{2，2，6}，{2，3，5}和{5，5}。所以输出应该是 5。

**1)最优子结构**
为了统计解的总数，我们可以将所有集合的解分成两组。
1)不含 mth 币(或 Sm)的溶液。
2)含有至少一种 Sm 的溶液。
设 count(S[]，m，n)为计数解个数的函数，则可写成 count(S[]，m-1，n)与 count(S[]，m，n-Sm)之和。
因此，该问题具有最优子结构性质，因为该问题可以使用子问题的解来解决。

**2)重叠子问题**
以下是硬币兑换问题的简单递归实现。实现简单地遵循上面提到的递归结构。

**3)进场(算法)**

看，这里给定面额的每枚硬币可以出现无限多次。(允许重复)，这就是我们所说的无界背包。对于特定面额的硬币，我们有两种选择，要么 I)包括，要么 ii)排除。但在这里，包容的过程不是一次就够了；在 N<0 之前，我们可以多次包括任何面额。

基本上，如果我们在 s[m-1]，我们可以取该硬币(无界包含)的尽可能多的实例，即**计数(S，m，n–S[m-1])**；然后我们转到 s[m-2]。移动到 s[m-2]后，我们不能后退，不能为 s[m-1]做选择，即**计数(S，m-1，n )** 。

最后，由于我们要找到路的总数，所以我们将这 2 个可能的选择相加，即**计数(S，m，n–S[m-1])+计数(S，m-1，n)；**这将是我们需要的答案。

## C++

```
// Recursive C++ program for
// coin change problem.
#include <bits/stdc++.h>
using namespace std;

// Returns the count of ways we can
// sum S[0...m-1] coins to get sum n
int count(int S[], int m, int n)
{

    // If n is 0 then there is 1 solution
    // (do not include any coin)
    if (n == 0)
        return 1;

    // If n is less than 0 then no
    // solution exists
    if (n < 0)
        return 0;

    // If there are no coins and n
    // is greater than 0, then no
    // solution exist
    if (m <= 0 && n >= 1)
        return 0;

    // count is sum of solutions (i)
    // including S[m-1] (ii) excluding S[m-1]
    return count(S, m - 1, n) +
           count(S, m, n - S[m - 1]);
}

// Driver code
int main()
{
    int i, j;
    int arr[] = { 1, 2, 3 };
    int m = sizeof(arr) / sizeof(arr[0]);

    cout << " " << count(arr, m, 4);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// Recursive C program for
// coin change problem.
#include<stdio.h>

// Returns the count of ways we can
// sum S[0...m-1] coins to get sum n
int count( int S[], int m, int n )
{
    // If n is 0 then there is 1 solution
    // (do not include any coin)
    if (n == 0)
        return 1;

    // If n is less than 0 then no
    // solution exists
    if (n < 0)
        return 0;

    // If there are no coins and n
    // is greater than 0, then no
    // solution exist
    if (m <=0 && n >= 1)
        return 0;

    // count is sum of solutions (i)
    // including S[m-1] (ii) excluding S[m-1]
    return count( S, m - 1, n ) + count( S, m, n-S[m-1] );
}

// Driver program to test above function
int main()
{
    int i, j;
    int arr[] = {1, 2, 3};
    int m = sizeof(arr)/sizeof(arr[0]);
    printf("%d ", count(arr, m, 4));
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive JAVA program for
// coin change problem.
import java.util.*;
class GFG
{

// Returns the count of ways we can
// sum S[0...m-1] coins to get sum n
static int count(int S[], int m, int n)
{

    // If n is 0 then there is 1 solution
    // (do not include any coin)
    if (n == 0)
        return 1;

    // If n is less than 0 then no
    // solution exists
    if (n < 0)
        return 0;

    // If there are no coins and n
    // is greater than 0, then no
    // solution exist
    if (m <= 0 && n >= 1)
        return 0;

    // count is sum of solutions (i)
    // including S[m-1] (ii) excluding S[m-1]
    return count(S, m - 1, n) +
           count(S, m, n - S[m - 1]);
}

// Driver code
public static void  main(String args[])
{
    int arr[] = { 1, 2, 3 };
    int m = arr.length;

    System.out.println(count(arr, m, 4));
}

}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Recursive Python3 program for
# coin change problem.

# Returns the count of ways we can sum
# S[0...m-1] coins to get sum n
def count(S, m, n ):

    # If n is 0 then there is 1
    # solution (do not include any coin)
    if (n == 0):
        return 1

    # If n is less than 0 then no
    # solution exists
    if (n < 0):
        return 0;

    # If there are no coins and n
    # is greater than 0, then no
    # solution exist
    if (m <=0 and n >= 1):
        return 0

    # count is sum of solutions (i)
    # including S[m-1] (ii) excluding S[m-1]
    return count( S, m - 1, n ) + count( S, m, n-S[m-1] );

# Driver program to test above function
arr = [1, 2, 3]
m = len(arr)
print(count(arr, m, 4))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Recursive C# program for
// coin change problem.
using System;

class GFG
{
    // Returns the count of ways we can
    // sum S[0...m-1] coins to get sum n
    static int count( int []S, int m, int n )
    {
        // If n is 0 then there is 1 solution
        // (do not include any coin)
        if (n == 0)
            return 1;

        // If n is less than 0 then no
        // solution exists
        if (n < 0)
            return 0;

        // If there are no coins and n
        // is greater than 0, then no
        // solution exist
        if (m <=0 && n >= 1)
            return 0;

        // count is sum of solutions (i)
        // including S[m-1] (ii) excluding S[m-1]
        return count( S, m - 1, n ) +
            count( S, m, n - S[m - 1] );
    }

    // Driver program
    public static void Main()
    {

        int []arr = {1, 2, 3};
        int m = arr.Length;
        Console.Write( count(arr, m, 4));

    }
}
// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program for
// coin change problem.

// Returns the count of ways we can
// sum S[0...m-1] coins to get sum n
function coun($S, $m, $n)
{

    // If n is 0 then there is
    // 1 solution (do not include
    // any coin)
    if ($n == 0)
        return 1;

    // If n is less than 0 then no
    // solution exists
    if ($n < 0)
        return 0;

    // If there are no coins and n
    // is greater than 0, then no
    // solution exist
    if ($m <= 0 && $n >= 1)
        return 0;

    // count is sum of solutions (i)
    // including S[m-1] (ii) excluding S[m-1]
    return coun($S, $m - 1,$n ) +
           coun($S, $m, $n - $S[$m - 1] );
}

    // Driver Code
    $arr = array(1, 2, 3);
    $m = count($arr);
    echo coun($arr, $m, 4);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// Recursive javascript program for
// coin change problem.

// Returns the count of ways we can
// sum S[0...m-1] coins to get sum n
function count(S , m , n )
{

    // If n is 0 then there is 1 solution
    // (do not include any coin)
    if (n == 0)
        return 1;

    // If n is less than 0 then no
    // solution exists
    if (n < 0)
        return 0;

    // If there are no coins and n
    // is greater than 0, then no
    // solution exist
    if (m <=0 && n >= 1)
        return 0;

    // count is sum of solutions (i)
    // including S[m-1] (ii) excluding S[m-1]
    return count( S, m - 1, n ) +
           count( S, m, n - S[m - 1] );
}

// Driver program to test above function
var arr = [1, 2, 3];
var m = arr.length;
document.write( count(arr, m, 4));

// This code is contributed by Amit Katiyar
</script>
```

**Output**

```
 4
```

需要注意的是，上面的函数一次又一次地计算相同的子问题。S = {1，2，3}和 n = 5 见下面的递归树。

函数 C({1}，3)被调用两次。如果我们画出完整的树，那么我们可以看到有很多子问题被调用了不止一次。

```
C() --> count()
                             C({1,2,3}, 5)                     
                           /             \    
                         /                 \                  
             C({1,2,3}, 2)                 C({1,2}, 5)
            /       \                      /      \         
           /         \                    /         \   
C({1,2,3}, -1)  C({1,2}, 2)        C({1,2}, 3)    C({1}, 5)
               /    \             /     \           /     \
             /       \           /       \         /        \
    C({1,2},0)  C({1},2)   C({1,2},1) C({1},3)    C({1}, 4)  C({}, 5)
                   / \     / \        /\         /     \         
                  /   \   /   \     /   \       /       \  
                .      .  .     .   .     .   C({1}, 3) C({}, 4)
                                               / \ 
                                              /   \   
                                             .      .
```

由于相同的子问题被再次调用，这个问题具有重叠子问题的性质。所以硬币兑换问题同时具有动态规划问题的两个性质(见[这个](https://www.geeksforgeeks.org/archives/12635)和[这个](https://www.geeksforgeeks.org/archives/12819))。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)一样，相同子问题的重新计算可以通过以自下而上的方式构建临时数组表[][]来避免。

**动态规划解**

## C++

```
// C++ program for coin change problem.
#include<bits/stdc++.h>

using namespace std;

int count( int S[], int m, int n )
{
    int i, j, x, y;

    // We need n+1 rows as the table
    // is constructed in bottom up
    // manner using the base case 0
    // value case (n = 0)
    int table[n + 1][m];

    // Fill the entries for 0
    // value case (n = 0)
    for (i = 0; i < m; i++)
        table[0][i] = 1;

    // Fill rest of the table entries
    // in bottom up manner
    for (i = 1; i < n + 1; i++)
    {
        for (j = 0; j < m; j++)
        {
            // Count of solutions including S[j]
            x = (i-S[j] >= 0) ? table[i - S[j]][j] : 0;

            // Count of solutions excluding S[j]
            y = (j >= 1) ? table[i][j - 1] : 0;

            // total count
            table[i][j] = x + y;
        }
    }
    return table[n][m - 1];
}

// Driver Code
int main()
{
    int arr[] = {1, 2, 3};
    int m = sizeof(arr)/sizeof(arr[0]);
    int n = 4;
    cout << count(arr, m, n);
    return 0;
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## C

```
// C program for coin change problem.
#include<stdio.h>

int count( int S[], int m, int n )
{
    int i, j, x, y;

    // We need n+1 rows as the table is constructed
    // in bottom up manner using the base case 0
    // value case (n = 0)
    int table[n+1][m];

    // Fill the entries for 0 value case (n = 0)
    for (i=0; i<m; i++)
        table[0][i] = 1;

    // Fill rest of the table entries in bottom
    // up manner 
    for (i = 1; i < n+1; i++)
    {
        for (j = 0; j < m; j++)
        {
            // Count of solutions including S[j]
            x = (i-S[j] >= 0)? table[i - S[j]][j]: 0;

            // Count of solutions excluding S[j]
            y = (j >= 1)? table[i][j-1]: 0;

            // total count
            table[i][j] = x + y;
        }
    }
    return table[n][m-1];
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 2, 3};
    int m = sizeof(arr)/sizeof(arr[0]);
    int n = 4;
    printf(" %d ", count(arr, m, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic Programming Java implementation of Coin
   Change problem */
import java.util.Arrays;

class CoinChange
{
    static long countWays(int S[], int m, int n)
    {
        //Time complexity of this function: O(mn)
        //Space Complexity of this function: O(n)

        // table[i] will be storing the number of solutions
        // for value i. We need n+1 rows as the table is
        // constructed in bottom up manner using the base
        // case (n = 0)
        long[] table = new long[n+1];

        // Initialize all table values as 0
        Arrays.fill(table, 0);   //O(n)

        // Base case (If given value is 0)
        table[0] = 1;

        // Pick all coins one by one and update the table[]
        // values after the index greater than or equal to
        // the value of the picked coin
        for (int i=0; i<m; i++)
            for (int j=S[i]; j<=n; j++)
                table[j] += table[j-S[i]];

        return table[n];
    }

    // Driver Function to test above function
    public static void main(String args[])
    {
        int arr[] = {1, 2, 3};
        int m = arr.length;
        int n = 4;
        System.out.println(countWays(arr, m, n));
    }
}
// This code is contributed by Pankaj Kumar
```

## 计算机编程语言

```
# Dynamic Programming Python implementation of Coin
# Change problem
def count(S, m, n):
    # We need n+1 rows as the table is constructed
    # in bottom up manner using the base case 0 value
    # case (n = 0)
    table = [[0 for x in range(m)] for x in range(n+1)]

    # Fill the entries for 0 value case (n = 0)
    for i in range(m):
        table[0][i] = 1

    # Fill rest of the table entries in bottom up manner
    for i in range(1, n+1):
        for j in range(m):

            # Count of solutions including S[j]
            x = table[i - S[j]][j] if i-S[j] >= 0 else 0

            # Count of solutions excluding S[j]
            y = table[i][j-1] if j >= 1 else 0

            # total count
            table[i][j] = x + y

    return table[n][m-1]

# Driver program to test above function
arr = [1, 2, 3]
m = len(arr)
n = 4
print(count(arr, m, n))

# This code is contributed by Bhavya Jain
```

## C#

```
/* Dynamic Programming C# implementation of Coin
Change problem */
using System;

class GFG
{
    static long countWays(int []S, int m, int n)
    {
        //Time complexity of this function: O(mn)
        //Space Complexity of this function: O(n)

        // table[i] will be storing the number of solutions
        // for value i. We need n+1 rows as the table is
        // constructed in bottom up manner using the base
        // case (n = 0)
        int[] table = new int[n+1];

        // Initialize all table values as 0
        for(int i = 0; i < table.Length; i++)
        {
            table[i] = 0;
        }

        // Base case (If given value is 0)
        table[0] = 1;

        // Pick all coins one by one and update the table[]
        // values after the index greater than or equal to
        // the value of the picked coin
        for (int i = 0; i < m; i++)
            for (int j = S[i]; j <= n; j++)
                table[j] += table[j - S[i]];

        return table[n];
    }

    // Driver Function
    public static void Main()
    {
        int []arr = {1, 2, 3};
        int m = arr.Length;
        int n = 4;
        Console.Write(countWays(arr, m, n));
    }
}
// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for
// coin change problem.

function count1($S, $m, $n)
{
    // We need n+1 rows as
    // the table is constructed
    // in bottom up manner
    // using the base case 0
    // value case (n = 0)
    $table;
    for ($i = 0; $i < $n + 1; $i++)
    for ($j = 0; $j < $m; $j++)
        $table[$i][$j] = 0;

    // Fill the entries for
    // 0 value case (n = 0)
    for ($i = 0; $i < $m; $i++)
        $table[0][$i] = 1;

    // Fill rest of the table
    // entries in bottom up manner
    for ($i = 1; $i < $n + 1; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        {
            // Count of solutions
            // including S[j]
            $x = ($i-$S[$j] >= 0) ?
                  $table[$i - $S[$j]][$j] : 0;

            // Count of solutions
            // excluding S[j]
            $y = ($j >= 1) ?
                  $table[$i][$j - 1] : 0;

            // total count
            $table[$i][$j] = $x + $y;
        }
    }
    return $table[$n][$m-1];
}

// Driver Code
$arr = array(1, 2, 3);
$m = count($arr);
$n = 4;
echo count1($arr, $m, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

/* Dynamic Programming javascript implementation of Coin
   Change problem */

function countWays(S , m , n)
{
    //Time complexity of this function: O(mn)
    //Space Complexity of this function: O(n)

    // table[i] will be storing the number of solutions
    // for value i. We need n+1 rows as the table is
    // constructed in bottom up manner using the base
    // case (n = 0)
    // Initialize all table values as 0
    //O(n)
    var table = Array(n+1).fill(0);

    // Base case (If given value is 0)
    table[0] = 1;

    // Pick all coins one by one and update the table
    // values after the index greater than or equal to
    // the value of the picked coin
    for (i=0; i<m; i++)
        for (j=S[i]; j<=n; j++)
            table[j] += table[j-S[i]];

    return table[n];
}

// Driver Function to test above function
var arr = [1, 2, 3];
var m = arr.length;
var n = 4;
document.write(countWays(arr, m, n));

// This code is contributed by 29AjayKumar

</script>
```

**Output**

```
4
```

**时间复杂度:** O(mn)
以下是方法 2 的简化版本。此处需要的辅助空间仅为 O(n)。

## C++

```
int count( int S[], int m, int n )         
{         
 // table[i] will be storing the number of solutions for         
 // value i. We need n+1 rows as the table is constructed         
 // in bottom up manner using the base case (n = 0)         
 int table[n+1];         
 // Initialize all table values as 0         
 memset(table, 0, sizeof(table));         
 // Base case (If given value is 0)         
 table[0] = 1;         
 // Pick all coins one by one and update the table[] values         
 // after the index greater than or equal to the value of the         
 // picked coin         
 for(int i=0; i<m; i++)         
 for(int j=S[i]; j<=n; j++)         
 table[j] += table[j-S[i]];         
 return table[n];         
}         
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public static int count( int S[], int m, int n )
{
    // table[i] will be storing the number of solutions for
    // value i. We need n+1 rows as the table is constructed
    // in bottom up manner using the base case (n = 0)
    int table[]=new int[n+1];

    // Base case (If given value is 0)
    table[0] = 1;

    // Pick all coins one by one and update the table[] values
    // after the index greater than or equal to the value of the
    // picked coin
    for(int i=0; i<m; i++)
        for(int j=S[i]; j<=n; j++)
            table[j] += table[j-S[i]];

    return table[n];
}
```

## 计算机编程语言

```
# Dynamic Programming Python implementation of Coin
# Change problem
def count(S, m, n):

    # table[i] will be storing the number of solutions for
    # value i. We need n+1 rows as the table is constructed
    # in bottom up manner using the base case (n = 0)
    # Initialize all table values as 0
    table = [0 for k in range(n+1)]

    # Base case (If given value is 0)
    table[0] = 1

    # Pick all coins one by one and update the table[] values
    # after the index greater than or equal to the value of the
    # picked coin
    for i in range(0,m):
        for j in range(S[i],n+1):
            table[j] += table[j-S[i]]

    return table[n]

# Driver program to test above function
arr = [1, 2, 3]
m = len(arr)
n = 4
x = count(arr, m, n)
print (x)

# This code is contributed by Afzal Ansari
```

## C#

```
// Dynamic Programming C# implementation
// of Coin Change problem
using System;

class GFG
{
static int count(int []S, int m, int n)
{
    // table[i] will be storing the
    // number of solutions for value i.
    // We need n+1 rows as the table
    // is constructed in bottom up manner
    // using the base case (n = 0)
    int [] table = new int[n + 1];

    // Base case (If given value is 0)
    table[0] = 1;

    // Pick all coins one by one and
    // update the table[] values after
    // the index greater than or equal
    // to the value of the picked coin
    for(int i = 0; i < m; i++)
        for(int j = S[i]; j <= n; j++)
            table[j] += table[j - S[i]];

    return table[n];
}

// Driver Code
public static void Main()
{
    int []arr = {1, 2, 3};
    int m = arr.Length;
    int n = 4;
    Console.Write(count(arr, m, n));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
function count_1( &$S, $m, $n )
{
    // table[i] will be storing the number
    // of solutions for value i. We need n+1
    // rows as the table is constructed in
    // bottom up manner using the base case (n = 0)
    $table = array_fill(0, $n + 1, NULl);

    // Base case (If given value is 0)
    $table[0] = 1;

    // Pick all coins one by one and update
    // the table[] values after the index
    // greater than or equal to the value
    // of the picked coin
    for($i = 0; $i < $m; $i++)
        for($j = $S[$i]; $j <= $n; $j++)
            $table[$j] += $table[$j - $S[$i]];

    return $table[$n];
}

// Driver Code
$arr = array(1, 2, 3);
$m = sizeof($arr);
$n = 4;
$x = count_1($arr, $m, $n);
echo $x;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
    // Dynamic Programming Javascript implementation
    // of Coin Change problem

    function count(S, m, n)
    {
        // table[i] will be storing the
        // number of solutions for value i.
        // We need n+1 rows as the table
        // is constructed in bottom up manner
        // using the base case (n = 0)
        let table = new Array(n + 1);
        table.fill(0);

        // Base case (If given value is 0)
        table[0] = 1;

        // Pick all coins one by one and
        // update the table[] values after
        // the index greater than or equal
        // to the value of the picked coin
        for(let i = 0; i < m; i++)
            for(let j = S[i]; j <= n; j++)
                table[j] += table[j - S[i]];

        return table[n];
    }

    let arr = [1, 2, 3];
    let m = arr.length;
    let n = 4;
    document.write(count(arr, m, n));
</script>
```

**输出:**

```
4
```

感谢 Rohan Laishram 提出这个空间优化版本。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。

参考文献:
[http://www.algorithmist.com/index.php/Coin_Change](http://www.algorithmist.com/index.php/Coin_Change)

下面是另一种使用记忆的自上而下的动态规划方法:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int coinchange(vector<int>& a, int v, int n,
               vector<vector<int> >& dp)
{
    if (v == 0)
        return dp[n][v] = 1;
    if (n == 0)
        return 0;
    if (dp[n][v] != -1)
        return dp[n][v];
    if (a[n - 1] <= v) {
        // Either Pick this coin or not
        return dp[n][v] = coinchange(a, v - a[n - 1], n, dp)
                          + coinchange(a, v, n - 1, dp);
    }
    else // We have no option but to leave this coin
        return dp[n][v] = coinchange(a, v, n - 1, dp);
}
int32_t main()
{
    int tc = 1;
    // cin >> tc;
    while (tc--) {
        int n, v;
        n = 3, v = 4;
        vector<int> a = { 1, 2, 3 };
        vector<vector<int> > dp(n + 1,
                                vector<int>(v + 1, -1));
        int res = coinchange(a, v, n, dp);
        cout << res << endl;
    }
}
// This Code is Contributed by
// Harshit Agrawal NITT
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    static int coinchange(int[] a, int v, int n, int[][] dp)
    {
        if (v == 0)
            return dp[n][v] = 1;
        if (n == 0)
            return 0;
        if (dp[n][v] != -1)
            return dp[n][v];
        if (a[n - 1] <= v)
        {

            // Either Pick this coin or not
            return dp[n][v]
                = coinchange(a, v - a[n - 1], n, dp)
                  + coinchange(a, v, n - 1, dp);
        }
        else // We have no option but to leave this coin
            return dp[n][v] = coinchange(a, v, n - 1, dp);
    }

  // Driver code
    public static void main(String[] args)
    {
        int tc = 1;
        while (tc != 0) {
            int n, v;
            n = 3;
            v = 4;
            int[] a = { 1, 2, 3 };
            int[][] dp = new int[n + 1][v + 1];
            for (int[] row : dp)
                Arrays.fill(row, -1);
            int res = coinchange(a, v, n, dp);
            System.out.println(res);
            tc--;
        }
    }
}

// This code is contributed by rajsanghavi9.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    static int coinchange(int[] a, int v, int n, int[, ] dp)
    {
        if (v == 0)
            return dp[n, v] = 1;
        if (n == 0)
            return 0;
        if (dp[n, v] != -1)
            return dp[n, v];
        if (a[n - 1] <= v) {

            // Either Pick this coin or not
            return dp[n, v]
                = coinchange(a, v - a[n - 1], n, dp)
                  + coinchange(a, v, n - 1, dp);
        }
        else // We have no option but to leave this coin
            return dp[n, v] = coinchange(a, v, n - 1, dp);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int tc = 1;
        while (tc != 0) {
            int n, v;
            n = 3;
            v = 4;
            int[] a = { 1, 2, 3 };
            int[, ] dp = new int[n + 1, v + 1];
            for (int j = 0; j < n + 1; j++) {
                for (int l = 0; l < v + 1; l++)
                    dp[j, l] = -1;
            }
            int res = coinchange(a, v, n, dp);
            Console.WriteLine(res);
            tc--;
        }
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript program for the above approach

    function coinchange(a , v , n,  dp) {
        if (v == 0)
            return dp[n][v] = 1;
        if (n == 0)
            return 0;
        if (dp[n][v] != -1)
            return dp[n][v];
        if (a[n - 1] <= v) {

            // Either Pick this coin or not
            return dp[n][v] = coinchange(a, v - a[n - 1], n, dp) + coinchange(a, v, n - 1, dp);
        } else // We have no option but to leave this coin
            return dp[n][v] = coinchange(a, v, n - 1, dp);
    }

    // Driver code

        var tc = 1;
        while (tc != 0) {
            var n, v;
            n = 3;
            v = 4;
            var a = [ 1, 2, 3 ];
            var dp = Array(n+1).fill().map(() => Array(v+1).fill(-1));

            var res = coinchange(a, v, n, dp);
            document.write(res);
            tc--;
        }

// This code contributed by umadevi9616
</script>
```

**Output**

```
4
```

**时间复杂度:**O(M * N)
T3】辅助空间: O(M*N)

供稿人:Mayukh Sinha