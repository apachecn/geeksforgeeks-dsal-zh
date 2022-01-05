# 寻找第 n 个斐波那契数最后一位数字的程序

> 原文:[https://www . geesforgeks . org/program-find-last-digit-n th-fibonnaci-number/](https://www.geeksforgeeks.org/program-find-last-digit-nth-fibonnaci-number/)

给定一个数字“n”，编写一个函数，打印第 n 个(n 也可以是一个大数字)斐波那契数的最后一个数字。
**例:**

```
Input : n = 0
Output : 0

Input: n = 2
Output : 1

Input : n = 7
Output : 3
```

**方法一:(天真法)**
简单的做法是计算第 n 个斐波那契数，打印最后一位数字。

## C++

```
// C++ Program to find last digit
// of nth Fibonacci number
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

void multiply(ll F[2][2], ll M[2][2]);
void power(ll F[2][2], ll n);

// Function that returns
// nth Fibonacci number
ll fib(int n)
{
    ll F[2][2] = {{1, 1}, {1, 0}};
    if (n == 0)
        return 0;
    power(F, n - 1);
    return F[0][0];
}

// Utility method to find
// n'th power of F[][]
void power(ll F[2][2], ll n)
{
    // Base cases
    if (n == 0 || n == 1)
        return;

    ll M[2][2] = {{1, 1}, {1, 0}};

    power(F, n / 2);
    multiply(F, F);

    if (n % 2 != 0)
        multiply(F, M);
}

// Utility function to multiply two
// matrices and store result in first.
void multiply(ll F[2][2], ll M[2][2])
{
    ll x = F[0][0] * M[0][0] +
           F[0][1] * M[1][0];
    ll y = F[0][0] * M[0][1] +
           F[0][1] * M[1][1];
    ll z = F[1][0] * M[0][0] +
           F[1][1] * M[1][0];
    ll w = F[1][0] * M[0][1] +
           F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Returns last digit of
// n'th Fibonacci Number
int findLastDigit(int n)
{
return fib(n) % 10;
}

// Driver code
int main()
{
    ll n = 1;
    cout << findLastDigit(n) << endl;
    n = 61;
    cout << findLastDigit(n) << endl;
    n = 7;
    cout << findLastDigit(n) << endl;
    n = 67;
    cout << findLastDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last digit
// of nth Fibonacci number
class GFG
{
    // Function that returns
    // nth Fibonacci number
    static long fib(long n)
    {
        long F[][] = new long[][] {{1, 1}, {1, 0}};
        if (n == 0)
            return 0;
        power(F, n - 1);

        return F[0][0];
    }

    // Utility function to multiply two
    // matrices and store result in first.
    static void multiply(long F[][], long M[][])
    {
        long x = F[0][0] * M[0][0] +
                 F[0][1] * M[1][0];
        long y = F[0][0] * M[0][1] +
                 F[0][1] * M[1][1];
        long z = F[1][0] * M[0][0] +
                 F[1][1] * M[1][0];
        long w = F[1][0] * M[0][1] +
                 F[1][1] * M[1][1];

        F[0][0] = x;
        F[0][1] = y;
        F[1][0] = z;
        F[1][1] = w;
    }

    // Optimized version of power() in method 4
    static void power(long F[][], long n)
    {
        if( n == 0 || n == 1)
            return;
        long M[][] = new long[][] {{1, 1}, {1, 0}};

        power(F, n / 2);
        multiply(F, F);

        if (n % 2 != 0)
            multiply(F, M);
    }

    // Returns last digit of
    // n'th Fibonacci Number
    long findLastDigit(long n)
    {
        return (fib(n) % 10);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n;
        GFG ob = new GFG();
        n = 1;
        System.out.println(ob.findLastDigit(n));
        n = 61;
        System.out.println(ob.findLastDigit(n));
        n = 7;
        System.out.println(ob.findLastDigit(n));
        n = 67;
        System.out.println(ob.findLastDigit(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find last digit of
# nth Fibonacci number

# Function that returns nth Fibonacci number
def fib(n):

    F = [[1, 1], [1, 0]];
    if (n == 0):
        return 0;
    power(F, n - 1);

    return F[0][0];

# Utility function to multiply two
# matrices and store result in first.
def multiply(F, M):

    x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;

# Optimized version of power() in
# method 4
def power(F, n):

    if( n == 0 or n == 1):
        return;
    M = [[1, 1], [1, 0]];

    power(F, int(n / 2));
    multiply(F, F);

    if (n % 2 != 0):
        multiply(F, M);

# Returns last digit of
# n'th Fibonacci Number
def findLastDigit(n):

    return (fib(n) % 10);

# Driver code
n = 1;
print(findLastDigit(n));
n = 61;
print(findLastDigit(n));
n = 7;
print(findLastDigit(n));
n = 67;
print(findLastDigit(n));

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# program to find last digit
// of nth Fibonacci number
using System;

class GFG
{

    // function that returns
    // nth Fibonacci number
    static long fib(long n)
    {
        long [,]F = new long[,] {{1, 1}, {1, 0}};

        if (n == 0)
            return 0;

        power(F, n - 1);

        return F[0, 0];
    }

    // Utility function to multiply two
    // matrices and store result in first.
    static void multiply(long [,]F, long [,]M)
    {
        long x = F[0, 0] * M[0, 0] +
                 F[0, 1] * M[1, 0];
        long y = F[0, 0] * M[0, 1] +
                 F[0, 1] * M[1, 1];
        long z = F[1, 0] * M[0, 0] +
                 F[1, 1] * M[1, 0];
        long w = F[1, 0] * M[0, 1] +
                 F[1, 1] * M[1, 1];

        F[0, 0] = x;
        F[0, 1] = y;
        F[1, 0] = z;
        F[1, 1] = w;
    }

    // Optimized version of power() in method 4
    static void power(long [,]F, long n)
    {
        if( n == 0 || n == 1)
            return;
        long [,]M = new long[,] {{1, 1}, {1, 0}};

        power(F, n / 2);
        multiply(F, F);

        if (n % 2 != 0)
            multiply(F, M);
    }

    // Returns last digit of
    // n'th Fibonacci Number
    static long findLastDigit(long n)
    {
        return (fib(n) % 10);
    }

    // Driver code
    public static void Main()
    {
        int n;
        n = 1;
        Console.WriteLine(findLastDigit(n));
        n = 61;
        Console.WriteLine(findLastDigit(n));
        n = 7;
        Console.WriteLine(findLastDigit(n));
        n = 67;
        Console.WriteLine(findLastDigit(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find last digit of nth
// Fibonacci number

// Function that returns nth Fibonacci number
function fib($n)
{
    $F = array(array(1, 1),
               array(1, 0));
    if ($n == 0)
        return 0;
    power($F, $n - 1);

    return $F[0][0];
}

// Utility function to multiply two
// matrices and store result in first.
function multiply(&$F, &$M)
{
    $x = $F[0][0] * $M[0][0] +
         $F[0][1] * $M[1][0];
    $y = $F[0][0] * $M[0][1] +
         $F[0][1] * $M[1][1];
    $z = $F[1][0] * $M[0][0] +
         $F[1][1] * $M[1][0];
    $w = $F[1][0] * $M[0][1] +
         $F[1][1] * $M[1][1];

    $F[0][0] = $x;
    $F[0][1] = $y;
    $F[1][0] = $z;
    $F[1][1] = $w;
}

// Optimized version of power() in method 4
function power(&$F, $n)
{
    if( $n == 0 || $n == 1)
        return;
    $M = array(array(1, 1), array(1, 0));

    power($F, (int)($n / 2));
    multiply($F, $F);

    if ($n % 2 != 0)
        multiply($F, $M);
}

// Returns last digit of
// n'th Fibonacci Number
function findLastDigit($n)
{
    return (fib($n) % 10);
}

// Driver code
$n = 1;
echo findLastDigit($n) . "\n";
$n = 61;
echo findLastDigit($n) . "\n";
$n = 7;
echo findLastDigit($n) . "\n";
$n = 67;
echo findLastDigit($n) . "\n";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>   
    // Javascript program to find last digit of nth Fibonacci number

    // Function that returns
    // nth Fibonacci number
    function fib(n)
    {
        let F = [[1, 1], [1, 0]];
        if (n == 0)
            return 0;
        power(F, n - 1);

        return F[0][0];
    }

    // Utility function to multiply two
    // matrices and store result in first.
    function multiply(F, M)
    {
        let x = F[0][0] * M[0][0] +
                 F[0][1] * M[1][0];
        let y = F[0][0] * M[0][1] +
                 F[0][1] * M[1][1];
        let z = F[1][0] * M[0][0] +
                 F[1][1] * M[1][0];
        let w = F[1][0] * M[0][1] +
                 F[1][1] * M[1][1];

        F[0][0] = x;
        F[0][1] = y;
        F[1][0] = z;
        F[1][1] = w;
    }

    // Optimized version of power() in method 4
    function power(F, n)
    {
        if( n == 0 || n == 1)
            return;
        let M = [[1, 1], [1, 0]];

        power(F, parseInt(n / 2, 10));
        multiply(F, F);

        if (n % 2 != 0)
            multiply(F, M);
    }

    // Returns last digit of
    // n'th Fibonacci Number
    function findLastDigit(n)
    {
        return (fib(n) % 10);
    }

    let n;
    n = 1;
    document.write(findLastDigit(n) + "</br>");
    n = 61;
    document.write(findLastDigit(n) + "</br>");
    n = 7;
    document.write(findLastDigit(n) + "</br>");
    n = 67;
    document.write(findLastDigit(n));

</script>
```

**输出:**

```
1
1
3
3
```

**复杂度:** O(Log n)。
**这个实现的限制:**
斐波那契数以指数级快速增长。例如，第 200 个斐波那契数等于 280571172992510140037611932413038677189525。F(1000)不适合标准的 C++ int 类型。
为了克服这个困难，不用计算第 n 个斐波那契数，有一个直接的算法就是只计算它的最后一位数字(即 F(n) mod 10)。
**方法 2:(直接法)**
查看每个斐波那契数的最后一位数字–单位数字:

```
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, ...
```

最后几个数字有图案吗？

```
0, 1, 1, 2, 3, 5, 8, 3, 1, 4, 5, 9, 4, 3, 7, 0, 7, ...
```

没错。
过一会儿才明显。事实上，这个数列只有 60 个数字长，然后它在斐波那契数列中一次又一次地重复同样的序列——永远如此。**最后一位数的序列重复，循环长度为 60** (关于该结果的解释，请参考[本](http://math.stackexchange.com/questions/113536/fibonaccis-final-digits-cycle-every-60-numbers))。
因此，与其一次又一次地计算斐波那契数，不如预先计算前 60 个斐波那契数的单位数字，并将其存储在一个数组中，然后使用该数组值进行进一步的计算。

## C++

```
// Optimized Program to find last
// digit of nth Fibonacci number
#include<bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Finds nth fibonacci number
ll fib(ll f[], ll n)
{
    // 0th and 1st number of
    // the series are 0 and 1
    f[0] = 0;
    f[1] = 1;

    // Add the previous 2 numbers
    // in the series and store
    // last digit of result
    for (ll i = 2; i <= n; i++)
        f[i] = (f[i - 1] + f[i - 2]) % 10;

    return f[n];
}

// Returns last digit of n'th Fibonacci Number
int findLastDigit(int n)
{
    ll f[60] = {0};

    // Precomputing units digit of 
    // first 60 Fibonacci numbers
    fib(f, 60);

    return f[n % 60];
}

// Driver code
int main ()
{
    ll n = 1;
    cout << findLastDigit(n) << endl;
    n = 61;
    cout << findLastDigit(n) << endl;
    n = 7;
    cout << findLastDigit(n) << endl;
    n = 67;
    cout << findLastDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Optimized Java program to find last
// digit of n'th Fibonacci number
class GFG
{
    // Filongs f[] with first
    // 60 Fibonacci numbers
    void fib(int f[])
    {
        // 0th and 1st number of
        // the series are 0 and 1
        f[0] = 0;
        f[1] = 1;

        // Add the previous 2 numbers
        // in the series and store
        // last digit of result
        for (int i = 2; i <= 59; i++)
            f[i] = (f[i - 1] + f[i - 2]) % 10;
    }

    // Returns last digit of n'th Fibonacci Number
    int findLastDigit(long n)
    {
        // In Java, values are 0 by default
        int f[] = new int[60];

        // Precomputing units digit of
        // first 60 Fibonacci numbers
        fib(f);

        int index = (int)(n % 60L);

        return f[index];
    }

    // Driver code
    public static void main(String[] args)
    {
        long n;
        GFG ob = new GFG();
        n = 1;
        System.out.println(ob.findLastDigit(n));
        n = 61;
        System.out.println(ob.findLastDigit(n));
        n = 7;
        System.out.println(ob.findLastDigit(n));
        n = 67;
        System.out.println(ob.findLastDigit(n));
    }
}
```

## 蟒蛇 3

```
# Optimized Python3 Program to find last
# digit of nth Fibonacci number

# Finds nth fibonacci number
def fib(f, n):

    # 0th and 1st number of
    # the series are 0 and 1
    f[0] = 0;
    f[1] = 1;

    # Add the previous 2 numbers
    # in the series and store
    # last digit of result
    for i in range(2, n + 1):
        f[i] = (f[i - 1] + f[i - 2]) % 10;

    return f;

# Returns last digit of n'th
# Fibonacci Number
def findLastDigit(n):
    f = [0] * 61;

    # Precomputing units digit of
    # first 60 Fibonacci numbers
    f = fib(f, 60);

    return f[n % 60];

# Driver code
n = 1;
print(findLastDigit(n));
n = 61;
print(findLastDigit(n));
n = 7;
print(findLastDigit(n));
n = 67;
print(findLastDigit(n));

# This code is contributed
# by chandan_jnu
```

## C#

```
// Optimized C# program to find last
// digit of n'th Fibonacci number
using System;

class GFG {

    // Filongs f[] with first
    // 60 Fibonacci numbers
    static void fib(int []f)
    {

        // 0th and 1st number of
        // the series are 0 and 1
        f[0] = 0;
        f[1] = 1;

        // Add the previous 2 numbers
        // in the series and store
        // last digit of result
        for (int i = 2; i <= 59; i++)
            f[i] = (f[i - 1] + f[i - 2]) % 10;
    }

    // Returns last digit of n'th
    // Fibonacci Number
    static int findLastDigit(long n)
    {
        int []f = new int[60];

        // Precomputing units digit of
        // first 60 Fibonacci numbers
        fib(f);

        int index = (int)(n % 60L);

        return f[index];
    }

    // Driver Code
    public static void Main()
    {
        long n;
        n = 1;
        Console.WriteLine(findLastDigit(n));
        n = 61;
        Console.WriteLine(findLastDigit(n));
        n = 7;
        Console.WriteLine(findLastDigit(n));
        n = 67;
        Console.WriteLine(findLastDigit(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Optimized PHP Program to find last
// digit of nth Fibonacci number

// Finds nth fibonacci number
function fib(&$f, $n)
{
    // 0th and 1st number of
    // the series are 0 and 1
    $f[0] = 0;
    $f[1] = 1;

    // Add the previous 2 numbers
    // in the series and store
    // last digit of result
    for ($i = 2; $i <= $n; $i++)
        $f[$i] = ($f[$i - 1] +
                  $f[$i - 2]) % 10;

    return $f[$n];
}

// Returns last digit of n'th
// Fibonacci Number
function findLastDigit($n)
{
    $f = array_fill(0, 60, 0);

    // Precomputing units digit of
    // first 60 Fibonacci numbers
    fib($f, 60);

    return $f[$n % 60];
}

// Driver code
$n = 1;
print(findLastDigit($n) . "\n");
$n = 61;
print(findLastDigit($n) . "\n");
$n = 7;
print(findLastDigit($n) . "\n");
$n = 67;
print(findLastDigit($n) . "\n");

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Optimized Javascript program to find last
    // digit of n'th Fibonacci number

    // Filongs f[] with first
    // 60 Fibonacci numbers
    function fib(f)
    {

        // 0th and 1st number of
        // the series are 0 and 1
        f[0] = 0;
        f[1] = 1;

        // Add the previous 2 numbers
        // in the series and store
        // last digit of result
        for (let i = 2; i <= 59; i++)
            f[i] = (f[i - 1] + f[i - 2]) % 10;
    }

    // Returns last digit of n'th
    // Fibonacci Number
    function findLastDigit(n)
    {
        let f = new Array(60);
        f.fill(0);

        // Precomputing units digit of
        // first 60 Fibonacci numbers
        fib(f);

        let index = (n % 60);

        return f[index];
    }

    let n;
    n = 1;
    document.write(findLastDigit(n) + "</br>");
    n = 61;
    document.write(findLastDigit(n) + "</br>");
    n = 7;
    document.write(findLastDigit(n) + "</br>");
    n = 67;
    document.write(findLastDigit(n) + "</br>");

    // This code is contributed by divyesh072019
</script>
```

**输出:**

```
1
1
3
3
```

**复杂度:** O(1)。
本文由**拉胡尔·阿格拉瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。