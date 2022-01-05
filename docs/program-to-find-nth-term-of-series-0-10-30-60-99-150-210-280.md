# 求数列 0、10、30、60、99、150、210、280 的第 n 项的程序……..

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-0-10-30-60-99-150-210-280/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-series-0-10-30-60-99-150-210-280/)

给定一个数字 n，任务是编写一个程序来找到下面系列的第 n 项:

> 0, 10, 30, 60, 99, 150, 210, 280…..(名词)

**例:**

```
Input: N = 4
Output: 60
For N = 4
4th Term = ( 5 * 4 * 4 - 5 * 4) 
         = 60

Input: N = 10
Output: 449
```

**方法:**本系列的广义第 n 项:

下面是需要的实现:

## C++

```
// C++ program to find the N-th term of the series:
// 0, 10, 30, 60, 99, 150, 210, .....
#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return 5 * pow(n, 2) - 5 * n;
}

// Driver code
int main()
{
    int N = 4;

    cout << nthTerm(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th term of the series:
// 0, 10, 30, 60, 99, 150, 210, .....
import java.util.*;

class solution
{

// calculate Nth term of series
static int nthTerm(int n)
{
    return 5 * (int)Math.pow(n, 2) - 5 * n;
}

//Driver code
public static void main(String arr[])
{

     int N = 4;
     System.out.println(nthTerm(N) );

}
}

//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find the
# N-th term of the series:
# 0, 10, 30, 60, 99, 150, 210, .....

# calculate Nth term of series
def nthTerm(n):

    return 5 * pow(n, 2) - 5 * n

# Driver code
N = 4
print(nthTerm(N))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find the
// N-th term of the series:
// 0, 10, 30, 60, 99, 150, 210, .....
using System;

class GFG
{

// calculate Nth term of series
static int nthTerm(int n)
{
    return 5 * (int)Math.Pow(n, 2) - 5 * n;
}

// Driver code
public static void Main()
{
    int N = 4;
    Console.Write(nthTerm(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// N-th term of the series:
// 0, 10, 30, 60, 99, 150, 210,...

// calculate Nth term of series
function nthTerm($n)
{
    return 5 * pow($n, 2) - 5 * $n;
}

// Driver code
$N = 4;

echo nthTerm($N);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the N-th term of the series:
// 0, 10, 30, 60, 99, 150, 210, .....

// calculate Nth term of series
function nthTerm( n)
{
    return 5 * Math.pow(n, 2) - 5 * n;
}

// Driver code

let N = 4;

   document.write( nthTerm(N) );

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
60
```

**时间复杂度:** O(1)