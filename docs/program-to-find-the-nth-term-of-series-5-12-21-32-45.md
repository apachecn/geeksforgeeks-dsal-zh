# 程序寻找系列 5、12、21、32、45 的第 n 项……

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-5-12-21-32-45/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-series-5-12-21-32-45/)

给定一个数字 N，任务是编写一个程序来找到下面系列的第 N 项:

> 5、12、21、32、45……

**例:**

```
Input: N = 2
Output: 12

Input: N = 5
Output: 45
```

**方法:**
本系列的广义第 n 项:

> 第 n 项:n*n + 4*n

下面是需要的实现:

## C++

```
// CPP program to find
// the N-th term of the series:
// 5, 12, 21, 32, 45......

#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return pow(n, 2) + 4 * n;
}

// Driver code
int main()
{

    // Get N
    int N = 4;

    // Get the Nth term
    cout << nthTerm(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find
// the N-th term of the series:
// 5, 12, 21, 32, 45......
import java.io.*;

class GFG {

// calculate Nth term of series
static int nthTerm(int n)
{
    return (int)Math.pow(n, 2) + 4 * n;
}

// Driver code

    public static void main (String[] args) {

    // Get N
    int N = 4;

    // Get the Nth term
    System.out.println( nthTerm(N));

    }
}
// This code is contributed
// by  inder_verma
```

## 蟒蛇 3

```
# Python3 program to find
# the N-th term of the series:
# 5, 12, 21, 32, 45......

# calculate Nth term of series
def nthTerm(n):
    return n ** 2 + 4 * n;

# Driver code

# Get N
N = 4

# Get the Nth term
print(nthTerm(N))

# This code is contributed by Raj
```

## C#

```
// C# program to find the
// N-th term of the series:
// 5, 12, 21, 32, 45......
using System;

class GFG
{

// calculate Nth term of series
static int nthTerm(int n)
{
    return (int)Math.Pow(n, 2) + 4 * n;
}

// Driver code
public static void Main ()
{

    // Get N
    int N = 4;

    // Get the Nth term
    Console.WriteLine(nthTerm(N));
}
}

// This code is contributed
// by sh..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the N-th term of the series:
// 5, 12, 21, 32, 45......

// calculate Nth term of series
function nthTerm($n)
{
    return pow($n, 2) + 4 * $n;
}

// Driver code
$N = 4;

// Get the Nth term
echo nthTerm($N);

// This code is contributed
// by Mahadev99
?>
```

## java 描述语言

```
<script>
// JavaScript program to find
// the N-th term of the series:
// 5, 12, 21, 32, 45......

// calculate Nth term of series
function nthTerm( n)
{
    return Math.pow(n, 2) + 4 * n;
}

// Driver code
    // Get N
    let N = 4;

    // Get the Nth term
    document.write( nthTerm(N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
32
```