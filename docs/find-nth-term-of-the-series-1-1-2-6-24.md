# 求数列 1、1、2、6、24 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n 系列术语-1-1-2-6-24/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-1-1-2-6-24/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

> 1, 1, 2, 6, 24…

**例:**

```
Input: 3
Output: 2
For N = 3
Nth term = (N-1)!
         = 2
Input: 5
Output: 24
```

级数的第 n 项由下式给出:

```
Nth term = ( N-1)! 
```

下面是需要的实现:

## C++

```
// CPP program to find N-th term of the series:
// 1, 1, 2, 6, 24...
#include <iostream>
using namespace std;

// calculate Nth term of series
int nthTerm(int N)
{
    if (N <= 1)
        return 1;

    int i, fact = 1;
    for (i = 1; i < N; i++)
        fact = fact * i;

    return fact;
}

// Driver Function
int main()
{
    int N = 3;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Nth term
import java.io.*;

// calculate Nth term of this series
// 1, 1, 2, 6, 24...
class Nth {
    public int nthTerm(int N)
    {
        // By using above formula
        if (N <= 1)
            return 1;

        int i, fact = 1;
        for (i = 1; i < N; i++)
            fact = fact * i;

        return fact;
    }
}
// Main class for main method
class GFG {

    public static void main(String[] args)
    {

        int N = 3;

        // create object of Class Nth
        Nth a = new Nth();

        // call and print Nth term
        System.out.println(a.nthTerm(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# N-th term of the series:
# 1, 1, 2, 6, 24...

# Function to calculate
# Nth term of series
def nthTerm(n) :

    if n <= 1 :
        return 1

    fact = 1
    for i in range(1, N) :
        fact = fact * i

    return fact

# Driver code
if __name__ == "__main__" :

    N = 3

    # function calling
    print(nthTerm(N))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to find the
// Nth term of the series
// 1, 1, 2, 6, 24...
using System;

// calculate Nth term
class GFG
{
public int nthTerm(int N)
{
    // By using above formula
    if (N <= 1)
        return 1;

    int i, fact = 1;
    for (i = 1; i < N; i++)
        fact = fact * i;

    return fact;
}

// Driver Code
public static void Main()
{
    int N = 3;

    // create object of Class GFG
    GFG a = new GFG();

    // call and print Nth term
    Console.Write(a.nthTerm(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find N-th
// term of the series:
// 1, 1, 2, 6, 24...

// calculate Nth term of series
function nthTerm($N)
{
    if ($N <= 1)
        return 1;

    $fact = 1;
    for ($i = 1; $i < $N; $i++)
        $fact = $fact * $i;

    return $fact;
}

// Driver Code
$N = 3;

echo nthTerm($N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 1, 1, 2, 6, 24...

// calculate Nth term of series
function nthTerm( N)
{
    if (N <= 1)
        return 1;

    let i, fact = 1;
    for (i = 1; i < N; i++)
        fact = fact * i;

    return fact;
}

// Driver Function
    let N = 3;

    document.write(nthTerm(N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```