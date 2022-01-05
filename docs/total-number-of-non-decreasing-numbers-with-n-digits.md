# n 位数非递减数总数

> 原文:[https://www . geesforgeks . org/n 位数非递减数字总数/](https://www.geeksforgeeks.org/total-number-of-non-decreasing-numbers-with-n-digits/)

如果每个数字(除了第一个)都大于或等于前一个数字，则数字不递减。例如，223、4455567、899 是不递减的数字。
所以，给定位数 n，你需要求 n 位数的非递减总数的计数。
**例:**

```
Input:  n = 1
Output: count  = 10

Input:  n = 2
Output: count  = 55

Input:  n = 3
Output: count  = 220
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
看问题的一个方法是，数数等于数数 n 个以 9 结尾的数字加上以 8 结尾的数字加上以 7 结尾的数字等等。如何获得以特定数字结尾的计数？对于 n-1 长度和小于或等于最后一个数字的数字，我们可以重复出现。下面是递归公式。

```
Count of n digit numbers = (Count of (n-1) digit numbers Ending with digit 9) +
                           (Count of (n-1) digit numbers Ending with digit 8) +
                           .............................................+ 
                           .............................................+
                           (Count of (n-1) digit numbers Ending with digit 0) 
```

让以数字‘d’和长度 n 结束的计数为计数(n，d)

```
count(n, d) = ∑(count(n-1, i)) where i varies from 0 to d

Total count = ∑count(n-1, d) where d varies from 0 to n-1
```

上面的递归解会有很多重叠的子问题。因此，我们可以使用动态编程以自下而上的方式构建一个表。
以下是上述思路的实现:

## C++

```
// C++ program to count non-decreasing number with n digits
#include<bits/stdc++.h>
using namespace std;

long long int countNonDecreasing(int n)
{
    // dp[i][j] contains total count of non decreasing
    // numbers ending with digit i and of length j
    long long int dp[10][n+1];
    memset(dp, 0, sizeof dp);

    // Fill table for non decreasing numbers of length 1
    // Base cases 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
    for (int i = 0; i < 10; i++)
        dp[i][1] = 1;

    // Fill the table in bottom-up manner
    for (int digit = 0; digit <= 9; digit++)
    {
        // Compute total numbers of non decreasing
        // numbers of length 'len'
        for (int len = 2; len <= n; len++)
        {
            // sum of all numbers of length of len-1
            // in which last digit x is <= 'digit'
            for (int x = 0; x <= digit; x++)
                dp[digit][len] += dp[x][len-1];
        }
    }

    long long int count = 0;

    // There total nondecreasing numbers of length n
    // wiint be dp[0][n] +  dp[1][n] ..+ dp[9][n]
    for (int i = 0; i < 10; i++)
        count += dp[i][n];

    return count;
}

// Driver program
int main()
{
    int n = 3;
    cout << countNonDecreasing(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class NDN
{
    static int countNonDecreasing(int n)
    {
        // dp[i][j] contains total count of non decreasing
        // numbers ending with digit i and of length j
        int dp[][] = new int[10][n+1];

        // Fill table for non decreasing numbers of length 1
        // Base cases 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
        for (int i = 0; i < 10; i++)
            dp[i][1] = 1;

        // Fill the table in bottom-up manner
        for (int digit = 0; digit <= 9; digit++)
        {
            // Compute total numbers of non decreasing
            // numbers of length 'len'
            for (int len = 2; len <= n; len++)
            {
                // sum of all numbers of length of len-1
                // in which last digit x is <= 'digit'
                for (int x = 0; x <= digit; x++)
                    dp[digit][len] += dp[x][len-1];
            }
        }

        int count = 0;

        // There total nondecreasing numbers of length n
        // wiint be dp[0][n] +  dp[1][n] ..+ dp[9][n]
        for (int i = 0; i < 10; i++)
            count += dp[i][n];

        return count;
    }
    public static void main(String args[])
    {
       int n = 3;
       System.out.println(countNonDecreasing(n));
    }
}/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# Python3 program to count
# non-decreasing number with n digits
def countNonDecreasing(n):

    # dp[i][j] contains total count
    # of non decreasing numbers ending
    # with digit i and of length j
    dp = [[0 for i in range(n + 1)]
             for i in range(10)]

    # Fill table for non decreasing
    # numbers of length 1.
    # Base cases 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

    for i in range(10):
        dp[i][1] = 1

    # Fill the table in bottom-up manner
    for digit in range(10):

        # Compute total numbers of non
        # decreasing numbers of length 'len'
        for len in range(2, n + 1):

            # sum of all numbers of length
            # of len-1 in which last
            # digit x is <= 'digit'
            for x in range(digit + 1):
                dp[digit][len] += dp[x][len - 1]
    count = 0

    # There total nondecreasing numbers
    # of length n won't be dp[0][n] +
    # dp[1][n] ..+ dp[9][n]
    for i in range(10):
        count += dp[i][n]
    return count

# Driver Code
n = 3
print(countNonDecreasing(n))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to print sum
// triangle for a given array
using System;

class GFG {

    static int countNonDecreasing(int n)
    {
        // dp[i][j] contains total count
        // of non decreasing numbers ending
        // with digit i and of length j
        int [,]dp = new int[10,n + 1];

        // Fill table for non decreasing
        // numbers of length 1 Base cases
        // 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
        for (int i = 0; i < 10; i++)
            dp[i, 1] = 1;

        // Fill the table in bottom-up manner
        for (int digit = 0; digit <= 9; digit++)
        {

            // Compute total numbers of non decreasing
            // numbers of length 'len'
            for (int len = 2; len <= n; len++)
            {

                // sum of all numbers of length of len-1
                // in which last digit x is <= 'digit'
                for (int x = 0; x <= digit; x++)
                    dp[digit, len] += dp[x, len - 1];
            }
        }

        int count = 0;

        // There total nondecreasing numbers
        // of length n wiint be dp[0][n]
        // + dp[1][n] ..+ dp[9][n]
        for (int i = 0; i < 10; i++)
            count += dp[i, n];

        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        Console.WriteLine(countNonDecreasing(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to count non-decreasing number with n digits

function countNonDecreasing($n)
{
    // dp[i][j] contains total count of non decreasing
    // numbers ending with digit i and of length j
    $dp = array_fill(0,10,array_fill(0,$n+1,NULL));

    // Fill table for non decreasing numbers of length 1
    // Base cases 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
    for ($i = 0; $i < 10; $i++)
        $dp[$i][1] = 1;

    // Fill the table in bottom-up manner
    for ($digit = 0; $digit <= 9; $digit++)
    {
        // Compute total numbers of non decreasing
        // numbers of length 'len'
        for ($len = 2; $len <= $n; $len++)
        {
            // sum of all numbers of length of len-1
            // in which last digit x is <= 'digit'
            for ($x = 0; $x <= $digit; $x++)
                $dp[$digit][$len] += $dp[$x][$len-1];
        }
    }

    $count = 0;

    // There total nondecreasing numbers of length n
    // wiint be dp[0][n] +  dp[1][n] ..+ dp[9][n]
    for ($i = 0; $i < 10; $i++)
        $count += $dp[$i][$n];

    return $count;
}

// Driver program

$n = 3;
echo  countNonDecreasing($n);
return 0;
?>
```

## java 描述语言

```
<script>

    function countNonDecreasing(n)
    {
        // dp[i][j] contains total count of non decreasing
        // numbers ending with digit i and of length j
        let dp=new Array(10);
        for(let i=0;i<10;i++)
        {
            dp[i]=new Array(n+1);
        }   

        for(let i=0;i<10;i++)
        {
            for(let j=0;j<n+1;j++)
            {
                dp[i][j]=0;
            }
        }

        // Fill table for non decreasing numbers of length 1
        // Base cases 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
        for (let i = 0; i < 10; i++)
            dp[i][1] = 1;

        // Fill the table in bottom-up manner
        for (let digit = 0; digit <= 9; digit++)
        {
            // Compute total numbers of non decreasing
            // numbers of length 'len'
            for (let len = 2; len <= n; len++)
            {
                // sum of all numbers of length of len-1
                // in which last digit x is <= 'digit'
                for (let x = 0; x <= digit; x++)
                    dp[digit][len] += dp[x][len-1];
            }
        }

        let count = 0;

        // There total nondecreasing numbers of length n
        // wiint be dp[0][n] +  dp[1][n] ..+ dp[9][n]
        for (let i = 0; i < 10; i++)
            count += dp[i][n];

        return count;
    }

    let n = 3;
    document.write(countNonDecreasing(n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
220
```

感谢[高拉夫·阿赫瓦尔](http://qa.geeksforgeeks.org/user/Mr.Lazy)提出上述方法。
**另一种方法是基于下面的直接公式**

```
Count of non-decreasing numbers with n digits = 
                                N*(N+1)/2*(N+2)/3* ....*(N+n-1)/n
Where N = 10
```

下面是使用上述公式计算计数的程序。

## C++

```
// C++ program to count non-decreasing number with n digits
#include<bits/stdc++.h>
using namespace std;

long long int countNonDecreasing(int n)
{
    int N = 10;

    // Compute value of N*(N+1)/2*(N+2)/3* ....*(N+n-1)/n
    long long count = 1;
    for (int i=1; i<=n; i++)
    {
        count *= (N+i-1);
        count /= i;
    }

    return count;
}

// Driver program
int main()
{
    int n = 3;
    cout << countNonDecreasing(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to count non-decreasing
// number with n digits
public class GFG {

    static long countNonDecreasing(int n)
    {
        int N = 10;

        // Compute value of N * (N+1)/2 *
        // (N+2)/3 * ....* (N+n-1)/n
        long count = 1;

        for (int i = 1; i <= n; i++)
        {
            count *= (N + i - 1);
            count /= i;
        }

        return count;
    }

    // Driver code
    public static void main(String args[]) {

        int n = 3;
        System.out.print(countNonDecreasing(n));
    }  
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to count non-decreasing
# number with n digits

def countNonDecreasing(n):
    N = 10

    # Compute value of N*(N+1)/2*(N+2)/3
    # * ....*(N+n-1)/n
    count = 1
    for i in range(1, n+1):
        count = int(count * (N+i-1))
        count = int(count / i )

    return count

# Driver program
n = 3;
print(countNonDecreasing(n))

# This code is contributed by Sam007
```

## C#

```
// C# program to count non-decreasing
// number with n digits
using System;

class GFG {

    static long countNonDecreasing(int n)
    {
        int N = 10;

        // Compute value of N * (N+1)/2 *
        // (N+2)/3 * ....* (N+n-1)/n
        long count = 1;

        for (int i = 1; i <= n; i++)
        {
            count *= (N + i - 1);
            count /= i;
        }

        return count;
    }

    public static void Main()
    {
        int n = 3;

        Console.WriteLine(countNonDecreasing(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count non-decreasing
// number with n digits

function countNonDecreasing($n)
{
    $N = 10;

    // Compute value of N*(N+1)/2*(N+2)/3* ...
    // ....*(N+n-1)/n
    $count = 1;
    for ($i = 1; $i <= $n; $i++)
    {
        $count *= ($N + $i - 1);
        $count /= $i;
    }

    return $count;
}

    // Driver Code
    $n = 3;
    echo countNonDecreasing($n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// javascript program to count non-decreasing
// number with n digits

    function countNonDecreasing(n)
    {
        let N = 10;

        // Compute value of N * (N+1)/2 *
        // (N+2)/3 * ....* (N+n-1)/n
        let count = 1;

        for (let i = 1; i <= n; i++)
        {
            count *= (N + i - 1);
            count = Math.floor(count/ i);
        }

        return count;
    }

    // Driver code
    let n = 3;
    document.write(countNonDecreasing(n));

    //  This code is contributed by rag2127.
</script>
```

**输出:**

```
220
```

感谢 [Abhishek Somani](http://qa.geeksforgeeks.org/user/Abhishek+Somani) 提出这个方法。
**这个公式是如何工作的？**

```
N * (N+1)/2 * (N+2)/3 * .... * (N+n-1)/n
Where N = 10 
```

让我们尝试 n 的不同值

```
For n = 1, the value is N from formula.
Which is true as for n = 1, we have all single digit
numbers, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9.

For n = 2, the value is N(N+1)/2 from formula
We can have N numbers beginning with 0, (N-1) numbers 
beginning with 1, and so on.
So sum is N + (N-1) + .... + 1 = N(N+1)/2

For n = 3, the value is N(N+1)/2(N+2)/3 from formula
We can have N(N+1)/2 numbers beginning with 0, (N-1)N/2 
numbers beginning with 1 (Note that when we begin with 1, 
we have N-1 digits left to consider for remaining places),
(N-2)(N-1)/2 beginning with 2, and so on.
Count = N(N+1)/2 + (N-1)N/2 + (N-2)(N-1)/2 + 
                               (N-3)(N-2)/2 .... 3 + 1 
     [Combining first 2 terms, next 2 terms and so on]
     = 1/2[N2 + (N-2)2 + .... 4]
     = N*(N+1)*(N+2)/6  [Refer this , putting n=N/2 in the 
                         even sum formula]
```

对于一般的 n 位数情况，我们可以应用数学归纳法。计数将等于从 0 开始计数 n-1 个数字，即 N *(N+1)/2 *(N+2)/3 *……。*(N+n-1-1)/(n-1)。加上以 1 开头的 n-1 位数的计数，即(N-1)*(N)/2*(N+1)/3* …。*(N-1+n-1-1)/(n-1)(注意 N 被 N-1 代替)等等。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息