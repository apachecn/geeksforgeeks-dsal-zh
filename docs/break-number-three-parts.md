# 将数字分成三部分

> 原文:[https://www.geeksforgeeks.org/break-number-three-parts/](https://www.geeksforgeeks.org/break-number-three-parts/)

给定一个非常大的数，把它分解成 3 个整数，这样它们就可以和原来的数相加，并计算出这样做的方法。

**示例:**

```
Input : 3
Output : 10
The possible combinations where the sum
of the numbers is equal to 3 are:
0+0+3 = 3
0+3+0 = 3
3+0+0 = 3
0+1+2 = 3
0+2+1 = 3
1+0+2 = 3
1+2+0 = 3
2+0+1 = 3
2+1+0 = 3
1+1+1 = 3

Input : 6
Output : 28
```

一共 10 种方式，所以回答是 10 种。

**天真方法:**尝试从 0 到给定数字的所有组合，并检查它们是否加到给定数字，如果是，则将计数增加 1 并继续该过程。

## C++

```
// C++ program to count number of ways to break
// a number in three parts.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to count number of ways
// to make the given number n
ll count_of_ways(ll n)
{
    ll count = 0;
    for (int i = 0; i <= n; i++)
        for (int j = 0; j <= n; j++)
            for (int k = 0; k <= n; k++)
                if (i + j + k == n)
                    count++;
    return count;
}

// Driver Function
int main()
{
    ll n = 3;
    cout << count_of_ways(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways to break
// a number in three parts
import java.io.*;

class GFG {
    // Function to count number of ways
    // to make the given number n
    static long count_of_ways(long n)
    {
        long count = 0;
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= n; j++)
                for (int k = 0; k <= n; k++)
                    if (i + j + k == n)
                        count++;
        return count;
    }

    // driver program
    public static void main(String[] args)
    {
        long n = 3;
        System.out.println(count_of_ways(n));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to count number of
# ways to break
# a number in three parts.

# Function to count number of ways
# to make the given number n
def count_of_ways(n):

    count = 0
    for i in range(0, n+1):
        for j in range(0, n+1):
            for k in range(0, n+1):
                if(i + j + k == n):
                    count = count + 1
    return count

# Driver Function
if __name__=='__main__':
    n = 3
    print(count_of_ways(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count number of ways
// to break a number in three parts
using System;

class GFG {

    // Function to count number of ways
    // to make the given number n
    static long count_of_ways(long n)
    {
        long count = 0;
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= n; j++)
                for (int k = 0; k <= n; k++)
                    if (i + j + k == n)
                        count++;
        return count;
    }

    // driver program
    public static void Main()
    {
        long n = 3;
        Console.WriteLine(count_of_ways(n));
    }
}

// This code is Contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of ways to break a number
// in three parts.

// Function to count number of ways
// to make the given number n
function count_of_ways( $n)
{
    $count = 0;
    for ($i = 0; $i <= $n; $i++)
        for ($j = 0; $j <= $n; $j++)
            for ($k = 0; $k <= $n; $k++)
                if ($i + $j + $k == $n)
                    $count++;
    return $count;
}

// Driver Code
$n = 3;
echo count_of_ways($n);

// This code is Contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count
// number of ways to break
// a number in three parts.

// Function to count number of ways
// to make the given number n
function count_of_ways(n)
{
    let count = 0;
    for(let i = 0; i <= n; i++)
        for(let j = 0; j <= n; j++)
            for(let k = 0; k <= n; k++)
                if (i + j + k == n)
                    count++;

    return count;
}

// Driver code
let n = 3;

document.write(count_of_ways(n) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
10
```

**时间复杂度:** O(n <sup>3</sup>

**高效方法:**如果我们仔细观察测试用例，那么我们会意识到将一个数字 n 分成 3 部分的方法数量等于(n+1) * (n+2) / 2。

## C++

```
// C++ program to count number of ways to break
// a number in three parts.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to count number of ways
// to make the given number n
ll count_of_ways(ll n)
{
    ll count;
    count = (n + 1) * (n + 2) / 2;
    return count;
}

// Driver Function
int main()
{
    ll n = 3;
    cout << count_of_ways(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways to break
// a number in three parts
import java.io.*;

class GFG {
    // Function to count number of ways
    // to make the given number n
    static long count_of_ways(long n)
    {
        long count = 0;
        count = (n + 1) * (n + 2) / 2;
        return count;
    }

    // driver program
    public static void main(String[] args)
    {
        long n = 3;
        System.out.println(count_of_ways(n));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to count number of
# ways to break a number in three parts.

# Function to count number of ways
# to make the given number n
def count_of_ways(n):
    count = 0
    count = (n + 1) * (n + 2) // 2
    return count

# Driver code
n = 3
print(count_of_ways(n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to count number of ways to
// break a number in three parts
using System;

class GFG {

    // Function to count number of ways
    // to make the given number n
    static long count_of_ways(long n)
    {
        long count = 0;
        count = (n + 1) * (n + 2) / 2;
        return count;
    }

    // driver program
    public static void Main()
    {
        long n = 3;
        Console.WriteLine(count_of_ways(n));
    }
}

// This code is Contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of ways to break a number
// in three parts.

// Function to count number of ways
// to make the given number n
function count_of_ways( $n)
{
    $count;
    $count = ($n + 1) * ($n + 2) / 2;
    return $count;
}

// Driver Code
$n = 3;
echo count_of_ways($n);

// This code is Contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// javascript program to count number of ways to
// break a number in three parts

    // Function to count number of ways
    // to make the given number n

    function count_of_ways(n)
    {
        var count = 0;
        count = (n + 1) * (n + 2) / 2;
        return count;
    }

    // driver program

        var n = 3;
        document.write(count_of_ways(n));

// This code is contributed by bunnyram19.
</script>
```

**输出:**

```
10
```

**时间复杂度:** O(1)

本文由 [**阿迪蒂亚·古普塔**](https://www.linkedin.com/in/aditya-gupta-437504a7?trk=hp-identity-name) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。