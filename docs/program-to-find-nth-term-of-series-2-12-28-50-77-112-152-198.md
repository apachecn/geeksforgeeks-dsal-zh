# 求数列 2、12、28、50、77、112、152、198 的第 n 项的程序…..

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-2-12-28-50-77-112-152-198/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-series-2-12-28-50-77-112-152-198/)

给定一个数字 n，任务是编写一个程序来找到下面系列的第 n 项:

> 2, 12, 28, 50, 77, 112, 152, 198…..(名词)

**例:**

```
Input: N = 4
Output: 50
For N = 4
4th Term = ( 3 * 4 * 4 + 4 - 2) 
         = 50

Input: N = 10
Output: 307
```

**方法:**本系列的广义第 n 项:

下面是需要的实现:

## C++

```
// C++ program to find the N-th term of the series:
// 2, 12, 28, 50, 77, 112, 152, 198, .....
#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return 3 * pow(n, 2) + n - 2;
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
// 2, 12, 28, 50, 77, 112, 152, 198, .....
import java.util.*;

class solution
{

// calculate Nth term of series
static int nthTerm(int n)
{
return 3 *(int)Math.pow(n, 2) + n - 2;
}

//Driver program
public static void main(String arr[])
{

    int N = 4;
    System.out.println(nthTerm(N));
}

}
//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find the
# N-th term of the series:
# 2, 12, 28, 50, 77, 112, 152, 198, .....

# calculate Nth term of series
def nthTerm(n):

    return 3 * pow(n, 2) + n - 2

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
// 2, 12, 28, 50, 77, 112, 152, 198, .....
using System;

class GFG
{

// calculate Nth term of series
static int nthTerm(int n)
{
    return 3 * (int)Math.Pow(n, 2) +
                             n - 2;
}

// Driver Code
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
// 2, 12, 28, 50, 77,
// 112, 152, 198, .....

// calculate Nth term of series
function nthTerm($n)
{
    return 3 * pow($n, 2) + $n - 2;
}

// Driver code
$N = 4;

echo nthTerm($N) ;

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
// JavaScript program to find the N-th term of the series:
// 2, 12, 28, 50, 77, 112, 152, 198, .....

// calculate Nth term of series
function nthTerm( n)
{
    return 3 * Math.pow(n, 2) + n - 2;
}

// Driver code
let N = 4;

   document.write( nthTerm(N) );

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
50
```

**时间复杂度:** O(1)