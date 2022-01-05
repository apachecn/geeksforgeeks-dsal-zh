# 程序寻找数列 3，5，21，51，95 的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-3-5-21-51-95/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-the-series-3-5-21-51-95/)

给定一个数字 N，任务是找到这个数列的第 N 项:

> 3, 5, 21, 51, 95, ….

**例:**

```
Input: N = 4
Output: 51
Explanation:
Nth term = (7 * pow(N, 2) - 19 * N + 15)
         = (7 * pow(4, 2) - 19 * 4 + 15)
         = 51

Input: N = 10
Output: 525
```

**方法:**
给定序列的第 n 项可以概括为:

```
[Tex] [/Tex]
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 3, 5, 21, 51, 95,...

#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int getNthTerm(long long int N)
{
    // Return Nth term
    return (7 * pow(N, 2) - 19 * N + 15);
}

// driver code
int main()
{
    // declaration of number of terms
    long long int N = 4;

    // Get the Nth term
    cout << getNthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series:
// 3, 5, 21, 51, 95,...
import java.util.*;

class solution
{
static long getNthTerm(long N)
{
// Return Nth term
    return (7 *(int) Math.pow(N, 2) - 19 * N + 15);
}

//Driver program
public static void main(String arr[])
{
// declaration of number of terms
    long N = 4;

    // Get the Nth term
     System.out.println(getNthTerm(N));
}
}
```

## 蟒蛇 3

```
# Python3 program to find N-th term
# of the series:
# 3, 5, 21, 51, 95,...

# calculate Nth term of series
def getNthTerm(N):

    #Return Nth term
    return (7 * pow(N, 2) - 19 * N + 15)

#Driver code
if __name__=='__main__':

#declaration of number of terms
    N = 4

#Get the Nth term
    print(getNthTerm(N))

#this code is contributed by Shashank_Sharma
```

## C#

```
// C# program to find
// N-th term of the series:
// 3, 5, 21, 51, 95,...
using System;

class GFG
{
static long getNthTerm(long N)
{
    // Return Nth term
    return (7 *(int) Math.Pow(N, 2) -
                       19 * N + 15);
}

// Driver Code
static public void Main ()
{

    // declaration of number
    // of terms
    long N = 4;

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
// 3, 5, 21, 51, 95,...

// calculate Nth term of series
function getNthTerm($N)
{
    // Return Nth term
    return (7 * pow($N, 2) -
            19 * $N + 15);
}

// Driver code

// declaration of number
// of terms
$N = 4;

// Get the Nth term
echo getNthTerm($N);

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>

// JavaScript  program to find N-th term of the series:
// 3, 5, 21, 51, 95,...

// calculate Nth term of series
function getNthTerm(N)
{
    // Return Nth term
    return (7 * Math.pow(N, 2) - 19 * N + 15);
}

// driver code
  // declaration of number of terms
   let N = 4;
   document.write( getNthTerm(N) );

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
51
```

**时间复杂度:** O(1)