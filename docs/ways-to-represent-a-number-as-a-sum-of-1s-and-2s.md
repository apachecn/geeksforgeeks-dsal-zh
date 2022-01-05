# 将数字表示为 1 和 2 之和的方法

> 原文:[https://www . geesforgeks . org/将数字表示为 1 和 2 的和的方法/](https://www.geeksforgeeks.org/ways-to-represent-a-number-as-a-sum-of-1s-and-2s/)

给定正整数 **N** 。任务是找出将 N 表示为 1 和 2 之和的方法的数量。
**例:**

```
Input : N = 3
Output : 3
3 can be represented as (1+1+1), (2+1), (1+2).

Input : N = 5
Output : 8
```

对于 N = 1，答案是 1。
为 N = 2。(1 + 1)、(2)，答案是 2。
为 N = 3。(1 + 1 + 1)、(2 + 1)、(1 + 2)，答案是 3。
为 N = 4。(1 + 1 + 1 + 1)，(2 + 1 + 1)，(1 + 2 + 1)，(1 + 1 + 2)，(2 + 2)答案是 5。
以此类推。
可以观察到它形成[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。所以，N 表示为 1s 和 2s 之和的方式数是(N + 1) <sup>第</sup>个斐波那契数。
*如何？*
我们很容易看出递归函数和斐波那契数完全一样。为了得到 N 的和，我们可以把 1 加到 N–1 上。此外，我们可以将 2 加到 N–2。并且只允许 1 和 2 做和 N，所以，用 1 和 2s 求和 N，总的方式是:求(N–1)的方式数+求(N–2)的方式数。
我们可以在 O(Log n)时间内找到第 N 个斐波那契数。请参考本岗位[方法五。
以下是本办法的实施情况:](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) 

## C++

```
// C++ program to find number of ways to representing
// a number as a sum of 1's and 2's
#include <bits/stdc++.h>
using namespace std;

// Function to multiply matrix.
void multiply(int F[2][2], int M[2][2])
{
    int x =  F[0][0]*M[0][0] + F[0][1]*M[1][0];
    int y =  F[0][0]*M[0][1] + F[0][1]*M[1][1];
    int z =  F[1][0]*M[0][0] + F[1][1]*M[1][0];
    int w =  F[1][0]*M[0][1] + F[1][1]*M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Power function in log n
void power(int F[2][2], int n)
{
    if( n == 0 || n == 1)
        return;
    int M[2][2] = {{1,1},{1,0}};

    power(F, n/2);
    multiply(F, F);

    if (n%2 != 0)
        multiply(F, M);
}

/* function that returns (n+1)th Fibonacci number
   Or number of ways to represent n as sum of 1's
   2's */
int countWays(int n)
{
    int F[2][2] = {{1,1},{1,0}};
    if (n == 0)
        return 0;
    power(F, n);
    return F[0][0];
}

// Driver program
int main()
{
    int n = 5;
    cout << countWays(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// ways to representing a number
// as a sum of 1's and 2's
class GFG
{

// Function to multiply matrix.
    static void multiply(int F[][], int M[][])
    {
        int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
        int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
        int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
        int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

        F[0][0] = x;
        F[0][1] = y;
        F[1][0] = z;
        F[1][1] = w;
    }

    // Power function in log n
    static void power(int F[][], int n)
    {
        if (n == 0 || n == 1)
        {
            return;
        }
        int M[][] = {{1, 1}, {1, 0}};

        power(F, n / 2);
        multiply(F, F);

        if (n % 2 != 0)
        {
            multiply(F, M);
        }
    }

    /* function that returns (n+1)th Fibonacci number
    Or number of ways to represent n as sum of 1's
    2's */
    static int countWays(int n)
    {
        int F[][] = {{1, 1}, {1, 0}};
        if (n == 0)
        {
            return 0;
        }
        power(F, n);
        return F[0][0];
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(countWays(n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find number of ways to
# representing a number as a sum of 1's and 2's

# Function to multiply matrix.
def multiply(F, M):

    x = F[0][0] * M[0][0] + F[0][1] * M[1][0]
    y = F[0][0] * M[0][1] + F[0][1] * M[1][1]
    z = F[1][0] * M[0][0] + F[1][1] * M[1][0]
    w = F[1][0] * M[0][1] + F[1][1] * M[1][1]

    F[0][0] = x
    F[0][1] = y
    F[1][0] = z
    F[1][1] = w

# Power function in log n
def power(F, n):

    if( n == 0 or n == 1):
        return
    M = [[1, 1],[1, 0]]

    power(F, n // 2)
    multiply(F, F)

    if (n % 2 != 0):
        multiply(F, M)

#/* function that returns (n+1)th Fibonacci number
# Or number of ways to represent n as sum of 1's
# 2's */
def countWays(n):
    F = [[1, 1], [1, 0]]
    if (n == 0):
        return 0
    power(F, n)

    return F[0][0]

# Driver Code
n = 5
print(countWays(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find number of
// ways to representing a number
// as a sum of 1's and 2's
class GFG
{

    // Function to multiply matrix.
    static void multiply(int [,]F, int [,]M)
    {
        int x = F[0,0] * M[0,0] + F[0,1] * M[1,0];
        int y = F[0,0] * M[0,1] + F[0,1] * M[1,1];
        int z = F[1,0] * M[0,0] + F[1,1] * M[1,0];
        int w = F[1,0] * M[0,1] + F[1,1] * M[1,1];

        F[0,0] = x;
        F[0,1] = y;
        F[1,0] = z;
        F[1,1] = w;
    }

    // Power function in log n
    static void power(int [,]F, int n)
    {
        if (n == 0 || n == 1)
        {
            return;
        }
        int [,]M = {{1, 1}, {1, 0}};

        power(F, n / 2);
        multiply(F, F);

        if (n % 2 != 0)
        {
            multiply(F, M);
        }
    }

    /* function that returns (n+1)th Fibonacci number
    Or number of ways to represent n as sum of 1's
    2's */
    static int countWays(int n)
    {
        int [,]F = {{1, 1}, {1, 0}};
        if (n == 0)
        {
            return 0;
        }
        power(F, n);
        return F[0,0];
    }

    // Driver program
    public static void Main()
    {
        int n = 5;
        System.Console.WriteLine(countWays(n));
    }
}

// This code contributed by mits
```

## java 描述语言

```
<script>

// Javascript program to find number of
// ways to representing a number
// as a sum of 1's and 2's

// Function to multiply matrix.
function multiply(F , M)
{
    var x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    var y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    var z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    var w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Power function in log n
function power(F , n)
{
    if (n == 0 || n == 1)
    {
        return;
    }
    var M = [[1, 1], [1, 0]];

    power(F, parseInt(n / 2));
    multiply(F, F);

    if (n % 2 != 0)
    {
        multiply(F, M);
    }
}

/* function that returns (n+1)th Fibonacci number
Or number of ways to represent n as sum of 1's
2's */
function countWays(n)
{
    var F = [[1, 1], [1, 0]];
    if (n == 0)
    {
        return 0;
    }
    power(F, n);
    return F[0][0];
}

// Driver program
var n = 5;
document.write(countWays(n));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
8
```

**时间复杂度:** O(logn)。
本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。