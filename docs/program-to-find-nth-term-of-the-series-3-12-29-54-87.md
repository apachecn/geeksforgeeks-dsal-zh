# 程序寻找系列 3，12，29，54，87 的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-3-12-29-54-87/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-the-series-3-12-29-54-87/)

给定一个数字 N，任务是找到这个数列的第 N 项:

> 3, 12, 29, 54, 87, ………….

**例:**

```
Input: N = 4
Output: 54
Explanation:
Nth term = 4 * pow(n, 2) - 3 * n + 2
         = 4 * pow(4, 2) - 3 * 4 + 2
         = 54

Input: N = 10
Output: 372
```

**方法:**
给定系列的第 n 项是:

```
Nth term of the series [Tex] [/Tex]
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 3, 12, 29, 54, 87, ...

#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int getNthTerm(long long int N)
{
    // Return Nth term
    return 4 * pow(N, 2) - 3 * N + 2;
}

// driver code
int main()
{
    // declaration of number of terms
    long long int N = 10;

    // Get the Nth term
    cout << getNthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series:
// 3, 12, 29, 54, 87, ...

import java.util.*;
class solution
{

static long getNthTerm(long N)
{
    // Return Nth term
    return 4 *(long)Math.pow(N, 2) - 3 * N + 2;
}

//Driver code
public static void main(String arr[])
{
// declaration of number of terms
    long N = 10;

    // Get the Nth term
    System.out.println(getNthTerm(N));

}
}
```

## 蟒蛇 3

```
# Python3 program to find N-th term of the series:
# 3, 12, 29, 54, 87, ...

# calculate Nth term of series
def getNthTerm(N):

    # Return Nth term
    return 4 * pow(N, 2) - 3 * N + 2

# driver code
if __name__=='__main__':

    # declaration of number of terms
    N = 10

    # Get the Nth term
    print(getNthTerm(N))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find
// N-th term of the series:
// 3, 12, 29, 54, 87, ...
using System;

class GFG
{
static long getNthTerm(long N)
{
    // Return Nth term
    return 4 * (long)Math.Pow(N, 2) -
                         3 * N + 2;
}

// Driver code
static public void Main ()
{

    // declaration of number
    // of terms
    long N = 10;

    // Get the Nth term
    Console.Write(getNthTerm(N));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 3, 12, 29, 54, 87, ...

// calculate Nth term of series
function getNthTerm($N)
{
    // Return Nth term
    return 4 * pow($N, 2) -
           3 * $N + 2;
}

// Driver code

// declaration of number of terms
$N = 10;

// Get the Nth term
echo getNthTerm($N);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// javascript program to find N-th term of the series:
// 3, 12, 29, 54, 87, ...

// calculate Nth term of series
function getNthTerm( N)
{
    // Return Nth term
    return 4 * Math.pow(N, 2) - 3 * N + 2;
}

// driver code

    // declaration of number of terms
    let N = 10;

    // Get the Nth term
    document.write( getNthTerm(N));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
372
```

**时间复杂度:** O(1)