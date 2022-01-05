# 程序寻找数列 3，20，63，144，230 的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-3-20-63-144-230/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-the-series-3-20-63-144-230/)

给定一个数列和一个数字 n，任务是找到给定数列的第 n 项:

> 3, 20, 63, 144, 230 … ..

**例:**

```
Input: N = 4
Output: 144
When n = 4
nth term = 2 ( n * n * n ) + n * n
         = 2 ( 4 * 4 * 4 ) + 4 * 4
         = 144

Input: N = 10
Output: 2100
```

**逼近:**我们可以求出给定级数的通项(Tn)。
![series\: can\: be\: written\: in\: the\: following\: way\: also:\\ (3 * 1^2), (5 * 2^2), (7 * 3^2), (9 * 4^2), .......up t n terms\\ Tn = (\:General\; term\; of \;series\; 3, 5, 7, 9 ....\;)\; X\; (\;General\; term\; of\; series\; 1^2, 2^2, 3^2, 4^2 ....\;)\\ Tn = (3 + (n-1) * 2) X ( n^2 )\\ Tn = 2*n^3 + n^2   ](img/b0c20954b0c0fe1154c5cad80b8408af.png "Rendered by QuickLaTeX.com")
以下是所需实现:

## C++

```
// CPP program to find N-th term of the series:
// 3, 20, 63, 144, 230 .....
#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return 2 * pow(n, 3) + pow(n, 2);
}

// Driver code
int main()
{
    int N = 3;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series:
// 3, 20, 63, 144, 230 .....
import java.util.*;

class solution
{

// calculate Nth term of series
static int nthTerm(int n)
{
    //return final sum
    return 2 *(int)Math.pow(n, 3) + (int)Math.pow(n, 2);
}

// Driver code
public static void main(String arr[])
{
    int N = 3;

System.out.println(nthTerm(N));

}

}
//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python program to find
# N-th term of the series:
# 3, 20, 63, 144, 230 .....

# calculate Nth term of series
def nthTerm(n) :

    return 2 * pow(n, 3) + pow(n, 2)

# Driver code
if __name__ == "__main__" :

    N = 3
    print(nthTerm(N))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to find N-th term of the series:
// 3, 20, 63, 144, 230 .....
using System;

class solution
{

// calculate Nth term of series
static int nthTerm(int n)
{
    //return final sum
    return 2 *(int)Math.Pow(n, 3) + (int)Math.Pow(n, 2);
}

// Driver code
public static void Main()
{
    int N = 3;

Console.WriteLine(nthTerm(N));

}

}
//This code is contributed by  Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 3, 20, 63, 144, 230 .....

// calculate Nth term of series
function nthTerm($n)
{
    return 2 * pow($n, 3) +
               pow($n, 2);
}

// Driver code
$N = 3;
echo nthTerm($N);

//This code is contributed by Shashank
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 3, 20, 63, 144, 230 .....

// calculate Nth term of series
function nthTerm( n)
{
    return 2 * Math.pow(n, 3) + Math.pow(n, 2);
}

// Driver code

    let N = 3;
   document.write( nthTerm(N) );

// This code contributed by aashish1995

</script>
```

**Output:** 

```
63
```

**时间复杂度:** O(1)