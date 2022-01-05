# 程序寻找数列 0，4，14，30，51，80，114，154，200 的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-0-4-14-30-51-80-114-154-200/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-series-0-4-14-30-51-80-114-154-200/)

给定一个数字 n，任务是编写一个程序来找到下面系列的第 n 项:

> 0、4、14、30、51、80、114、154、200……(N 项)

**例:**

```
Input: N = 4
Output: 82
For N = 4
4th Term = ( 4 * 4 - 2 * 4 + 2) 
         = 10

Input: N = 10
Output: 122
```

**方法:**本系列的广义第 n 项:

下面是需要的实现:

## C++

```
// CPP program to find the N-th term of the series:
// 5, 10, 17, 26, 37, 50, 65, 82, ...
#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return pow(n, 2) - 2 * n + 2;
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
// Java program to find the N-th term of the series:
// 5, 10, 17, 26, 37, 50, 65, 82, ...
import java.util.*;

class solution
{

// calculate Nth term of series
static int nthTerm(int n)
{

    //return the total sum
    return (int)Math.pow(n, 2) - 2 * n + 2;
}

//Driver function
public static void main(String arr[])
{
    int N = 4;

    System.out.println(nthTerm(N));

}

}
```

## 蟒蛇 3

```
# Python3 program to find the N-th
# term of the series:
# 0, 4, 14, 30, 51, 80, 114, 154, 200, …

# from math lib. import everything
from math import *

# calculate Nth term of series
def nthTerm(n) :

    return pow(n, 2) - 2 * n + 2

# Driver code    
if __name__ == "__main__" :

    N = 4
    print(nthTerm(N))

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program to find the
// N-th term of the series:
// 5, 10, 17, 26, 37, 50, 65, 82, ...
using System;

class GFG
{

// calculate Nth term of series
public static int nthTerm(int n)
{

    // return the total sum
    return (int)Math.Pow(n, 2) -
                    2 * n + 2;
}

// Driver Code
public static void Main(string[] arr)
{
    int N = 4;

    Console.WriteLine(nthTerm(N));
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// N-th term of the series:
// 5, 10, 17, 26, 37, 50, 65, 82, ...

// calculate Nth term of series
function nthTerm($n)
{
    return pow($n, 2) - 2 * $n + 2;
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
// JavaScript program to find the N-th term of the series:
// 5, 10, 17, 26, 37, 50, 65, 82, ...

// calculate Nth term of series
function nthTerm( n)
{
    return Math.pow(n, 2) - 2 * n + 2;
}
// Driver code

    let N = 4;
   document.write( nthTerm(N) );

// This code contributed by aashish1995

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(1)