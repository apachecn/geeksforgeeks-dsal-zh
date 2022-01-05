# 求数列 0、2、4、8、12、18 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n 系列术语-0-2-4-8-12-18/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-0-2-4-8-12-18/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

> **0、2、4、8、12、18……**

**例:**

```
Input: 3
Output: 4
For N = 3
Nth term = ( 3 + ( 3 - 1 ) * 3 ) / 2
         = 4
Input: 5 
Output: 12
```

仔细观察，上述系列中的第 N<sup>项可以概括为:</sup> 

```
Nth term = ( N + ( N - 1 ) * N ) / 2
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 0, 2, 4, 8, 12, 18...
#include <iostream>
using namespace std;

// Calculate Nth term of series
int nthTerm(int N)
{
    return (N + N * (N - 1)) / 2;
}

// Driver Function
int main()
{
    int N = 5;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series:
// 0, 2, 4, 8, 12, 18...
import java.io.*;

// Main class for main method
class GFG {
    public static int nthTerm(int N)
    {
        // By using above formula
        return (N + (N - 1) * N) / 2;
    }  

    // Driver code
    public static void main(String[] args)
    {
        int N = 5; // 5th term is 12

        System.out.println(nthTerm(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find N-th term of the series:
# 0, 2, 4, 8, 12, 18.

# Calculate Nth term of series
def nthTerm(N) :

    return (N + N * (N - 1)) // 2

# Driver Code
if __name__ == "__main__" :

    N = 5

    print(nthTerm(N))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find N-th term of the series:
// 0, 2, 4, 8, 12, 18...
using System;
class gfg
{  
    // Calculate Nth term of series
    public int nthTerm(int N)
    {
        int n = ((N + N * (N - 1)) / 2);
        return n;
    }

    //Driver program
    static void Main(string[] args)
    {
        gfg p = new gfg();
        int a = p.nthTerm(5);
        Console.WriteLine(a);
        Console.Read();
    }
}
//This code is contributed by SoumikMondal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 0, 2, 4, 8, 12, 18...

// Calculate Nth term of series
function nthTerm($N)
{
    return (int)(($N + $N *
                 ($N - 1)) / 2);
}

// Driver Code
$N = 5;

echo nthTerm($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 0, 2, 4, 8, 12, 18...

// Calculate Nth term of series
function nthTerm(N)
{
    return parseInt((N + N * (N - 1)) / 2);
}
// Driver Function

    let N = 5;
    document.write(nthTerm(N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(1)