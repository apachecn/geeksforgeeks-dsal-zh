# 将 n 写成两个或多个正整数之和的方法

> 原文:[https://www . geeksforgeeks . org/将 n 写成两个或多个正整数之和的方法/](https://www.geeksforgeeks.org/ways-to-write-n-as-sum-of-two-or-more-positive-integers/)

对于给定的 n > 0 的数，找出 n 可以写成至少两个或更多正整数的和的不同方法的个数。
**例:**

```
Input : n = 5
Output : 6
Explanation : All possible six ways are :
4 + 1
3 + 2
3 + 1 + 1
2 + 2 + 1
2 + 1 + 1 + 1
1 + 1 + 1 + 1 + 1

Input : 4
Output : 4
Explanation : All possible four ways are :
3 + 1
2 + 2
2 + 1 + 1
1 + 1 + 1 + 1
```

这个问题可以用类似于[硬币兑换](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)问题的方式来解决，区别只是在这种情况下，我们应该迭代 1 到 n-1，而不是像硬币兑换问题那样迭代硬币的特定值。

## C++

```
// Program to find the number of ways, n can be
// written as sum of two or more positive integers.
#include <bits/stdc++.h>
using namespace std;

// Returns number of ways to write n as sum of
// two or more positive integers
int countWays(int n)
{
    // table[i] will be storing the number of
    // solutions for value i. We need n+1 rows
    // as the table is constructed in bottom up
    // manner using the base case (n = 0)
    int table[n+1];

    // Initialize all table values as 0
    memset(table, 0, sizeof(table));

    // Base case (If given value is 0)
    table[0] = 1;

    // Pick all integer one by one and update the
    // table[] values after the index greater
    // than or equal to n
    for (int i=1; i<n; i++)
        for (int j=i; j<=n; j++)
            table[j] += table[j-i];

    return table[n];
}

// Driver program
int main()
{
    int n = 7;
    cout << countWays(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find the number of ways,
// n can be written as sum of two or
// more positive integers.
import java.util.Arrays;

class GFG {

    // Returns number of ways to write
    // n as sum of two or more positive
    // integers
    static int countWays(int n)
    {

        // table[i] will be storing the
        // number of solutions for value
        // i. We need n+1 rows as the
        // table is constructed in bottom
        // up manner using the base case
        // (n = 0)
        int table[] = new int[n + 1];

        // Initialize all table values as 0
        Arrays.fill(table, 0);

        // Base case (If given value is 0)
        table[0] = 1;

        // Pick all integer one by one and
        // update the table[] values after
        // the index greater than or equal
        // to n
        for (int i = 1; i < n; i++)
            for (int j = i; j <= n; j++)
                table[j] += table[j - i];

        return table[n];
    }

    //driver code
    public static void main (String[] args)
    {
        int n = 7;

        System.out.print(countWays(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Program to find the number of ways, n can be
# written as sum of two or more positive integers.

# Returns number of ways to write n as sum of
# two or more positive integers
def CountWays(n):

    # table[i] will be storing the number of
    # solutions for value i. We need n+1 rows
    # as the table is constructed in bottom up
    # manner using the base case (n = 0)
    # Initialize all table values as 0
    table =[0] * (n + 1)

    # Base case (If given value is 0)
    # Only 1 way to get 0 (select no integer)
    table[0] = 1

    # Pick all integer one by one and update the
    # table[] values after the index greater
    # than or equal to n
    for i in range(1, n ):

        for j in range(i , n + 1):

            table[j] +=  table[j - i]           

    return table[n]

# driver program
def main():

    n = 7

    print CountWays(n)

if __name__ == '__main__':
    main()

#This code is contributed by Neelam Yadav
```

## C#

```
// Program to find the number of ways, n can be
// written as sum of two or more positive integers.
using System;

class GFG {

    // Returns number of ways to write n as sum of
    // two or more positive integers
    static int countWays(int n)
    {

        // table[i] will be storing the number of
        // solutions for value i. We need n+1 rows
        // as the table is constructed in bottom up
        // manner using the base case (n = 0)
        int []table = new int[n+1];

        // Initialize all table values as 0
        for(int i = 0; i < table.Length; i++)
            table[i] = 0;

        // Base case (If given value is 0)
        table[0] = 1;

        // Pick all integer one by one and update the
        // table[] values after the index greater
        // than or equal to n
        for (int i = 1; i < n; i++)
            for (int j = i; j <= n; j++)
                table[j] += table[j-i];

        return table[n];
    }

    //driver code
    public static void Main()
    {
        int n = 7;

        Console.Write(countWays(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find the number of ways, n can be
// written as sum of two or more positive integers.

// Returns number of ways to write n as sum
// of two or more positive integers
function countWays($n)
{
    // table[i] will be storing the number of
    // solutions for value i. We need n+1 rows
    // as the table is constructed in bottom up
    // manner using the base case (n = 0)
    $table = array_fill(0, $n + 1, NULL);

    // Base case (If given value is 0)
    $table[0] = 1;

    // Pick all integer one by one and update
    // the table[] values after the index
    // greater than or equal to n
    for ($i = 1; $i < $n; $i++)
        for ($j = $i; $j <= $n; $j++)
            $table[$j] += $table[$j - $i];

    return $table[$n];
}

// Driver Code
$n = 7;
echo countWays($n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

    function countWays(n)
    {
        // table[i] will be storing the
        // number of solutions for value
        // i. We need n+1 rows as the
        // table is constructed in bottom
        // up manner using the base case
        // (n = 0)
        let table = new Array(n + 1);

        // Initialize all table values as 0
        for(let i = 0; i < n + 1; i++)
        {
            table[i]=0;
        }

        // Base case (If given value is 0)
        table[0] = 1;

        // Pick all integer one by one and
        // update the table[] values after
        // the index greater than or equal
        // to n
        for (let i = 1; i < n; i++)
            for (let j = i; j <= n; j++)
                table[j] += table[j - i];

        return table[n];
    }

    let n = 7;
    document.write(countWays(n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

输出:

```
14
```

时间复杂度 O(n <sup>2</sup> )
本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。