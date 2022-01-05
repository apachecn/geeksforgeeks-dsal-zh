# 程序求数列 4，14，28，46，68，94，124，158 的第 n 项，…..

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-4-14-28-46-68-94-124-158/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-series-4-14-28-46-68-94-124-158/)

给定一个数字 n，任务是编写一个程序来找到下面系列的第 n 项:

> 4, 14, 28, 46, 68, 94, 124, 158…..(名词)

**例:**

```
Input: N = 4
Output: 46
For N = 4
4th Term = ( 2 * 4 * 4 + 4 * 4 - 2) 
         = 46

Input: N = 10
Output: 237
```

**方法:**本系列的广义第 n 项:

下面是需要的实现:

## C++

```
// CPP program to find the N-th term of the series:
// 4, 14, 28, 46, 68, 94, 124, 158, .....
#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return 2 * pow(n, 2) + 4 * n - 2;
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
// 4, 14, 28, 46, 68, 94, 124, 158, .....
import java.util.*;

class solution
{

// calculate Nth term of series
static int nthTerm(int n)
{

    return 2 *(int)Math.pow(n, 2) + 4 * n - 2;

}

//Driver code
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
# 4, 14, 28, 46, 68, 94, 124, 158, .....

# calculate Nth term of series
def nthTerm(n):

    return 2 * pow(n, 2) + 4 * n - 2

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
// 4, 14, 28, 46, 68, 94, 124, 158, .....
using System;

class GFG
{

// calculate Nth term of series
static int nthTerm(int n)
{
    return 2 * (int)Math.Pow(n, 2) +
                             4 * n - 2;
}

// Driver Code
public static void Main()
{
    int N = 4;
    Console.Write(nthTerm(N));
}
}

// This code is contributed
// by Sanjit_Prasad
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// N-th term of the series:
// 4, 14, 28, 46, 68, 94, 124, 158, .....

// calculate Nth term of series
function nthTerm($n)
{
    return 2 * pow($n, 2) + 4 * $n - 2;
}

// Driver code
$N = 4;

echo nthTerm($N) . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// JavaScript program to find the N-th term of the series:
// 4, 14, 28, 46, 68, 94, 124, 158, .....

// calculate Nth term of series
function nthTerm( n)
{
    return 2 * Math.pow(n, 2) + 4 * n - 2;
}

// Driver code
let N = 4;

   document.write( nthTerm(N) );

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
46
```

**时间复杂度:** O(1)