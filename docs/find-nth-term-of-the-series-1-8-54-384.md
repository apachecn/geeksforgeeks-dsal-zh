# 求数列 1，8，54，384 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n 系列术语-1-8-54-384/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-1-8-54-384/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

```
1, 8, 54, 384...
```

**例:**

```
Input : 3
Output : 54
For N = 3
Nth term = ( 3*3) * 3!
         = 54

Input : 2 
Output : 8
```

仔细观察，上述级数中的第 n 项可以概括为:

```
Nth term = ( N*N ) * ( N! )
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 1, 8, 54, 384...
#include <iostream>
using namespace std;

// calculate factorial of N
int fact(int N)
{
    int i, product = 1;
    for (i = 1; i <= N; i++)
        product = product * i;
    return product;
}

// calculate Nth term of series
int nthTerm(int N)
{
    return (N * N) * fact(N);
}

// Driver Function
int main()
{
    int N = 4;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series:
// 1, 8, 54, 384...

import java.io.*;

// Main class for main method
class GFG {
    public static int fact(int N)
    {
        int i, product = 1;
        // Calculate factorial of N
        for (i = 1; i <= N; i++)
            product = product * i;
        return product;
    }
    public static int nthTerm(int N)
    {
        // By using above formula
        return (N * N) * fact(N);
    }

    public static void main(String[] args)
    {
        int N = 4; // 4th term is 384

        System.out.println(nthTerm(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# N-th term of the series:
# 1, 8, 54, 384...

# calculate factorial of N
def fact(N):

    product = 1
    for i in range(1, N + 1):
        product = product * i
    return product

# calculate Nth term of series
def nthTerm(N):
    return (N * N) * fact(N)

# Driver Code
if __name__ =="__main__":
    N = 4
    print(nthTerm(N))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find N-th
// term of the series:
// 1, 8, 54, 384...
using System;

class GFG
{
public static int fact(int N)
{
    int i, product = 1;

    // Calculate factorial of N
    for (i = 1; i <= N; i++)
        product = product * i;
    return product;
}

public static int nthTerm(int N)
{
    // By using above formula
    return (N * N) * fact(N);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4; // 4th term is 384

    Console.WriteLine(nthTerm(N));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find N-th
/// term of the series:
// 1, 8, 54, 384...

// calculate factorial of N
function fact($N)
{
    $product = 1;
    for ($i = 1; $i <= $N; $i++)
        $product = $product * $i;
    return $product;
}

// calculate Nth term of series
function nthTerm($N)
{
    return ($N * $N) * fact($N);
}

// Driver Code
$N = 4;

echo nthTerm($N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 1, 8, 54, 384...

// calculate factorial of N
function fact( N)
{
    let i, product = 1;
    for (i = 1; i <= N; i++)
        product = product * i;
    return product;
}

// calculate Nth term of series
function nthTerm( N)
{
    return (N * N) * fact(N);
}

// Driver Function

    let N = 4;
    document.write(nthTerm(N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
384
```

**时间复杂度:** O(N)