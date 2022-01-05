# 求数列 1，6，15，28，45 的第 n 个数，…..

> 原文:[https://www . geesforgeks . org/find-n-系列号-1-6-15-28-45/](https://www.geeksforgeeks.org/find-nth-number-of-the-series-1-6-15-28-45/)

给定一个数列的前两个数字。任务是找到该系列的第 n 个(n 可能高达 10^18)编号。
**注意:**数组中的每个元素都比它前面和后面的数字的平均值少两个。答案可能非常大，所以在模 10^9+9.下打印答案
T4【示例】T5:

```
Input: N = 3
Output: 15
(1 + 15)/2 - 2 = 6

Input: N = 4
Output: 28
(6 + 28)/2 - 2 = 15
```

**观察:**根据陈述，形成的系列将是 1、6、15、28、45…..所以，第 n 项的公式是:

```
2*n*n - n
```

## C++

```
// CPP program to find Nth term of the series
#include <bits/stdc++.h>
using namespace std;
#define mod 1000000009

// function to return nth term of the series
int NthTerm(long long n)
{
    long long x = (2 * n * n) % mod;
    return (x - n + mod) % mod;
}

// Driver code
int main()
{
    long long N = 4;

    // function call
    cout << NthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// term of the series:

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // function to return nth term of the series
    static long NthTerm(long n)
    {
        long x = (2 * n * n) % 1000000009;
        return (x - n + 1000000009) % 1000000009;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Taking  n as 6
        long N = 4;

        // Printing the nth term
        System.out.println(NthTerm(N));
    }
}
```

## 计算机编程语言

```
# Python 3 program to find 
# N-th term of the series: 

# Function for calculating 
# Nth term of series 
def NthTerm(N) : 

    # return nth term
    x = (2 * N*N)% 1000000009
    return ((x - N + 1000000009)% 1000000009) 

# Driver code 
if __name__ == "__main__" : 

    N = 4

    # Function Calling 
    print(NthTerm(N))
```

## C#

```
// C# program to find N-th
// term of the series:
using System;

class GFG
{

// function to return nth
// term of the series
static long NthTerm(long n)
{
    long x = (2 * n * n) % 1000000009;
    return (x - n + 1000000009) %
                    1000000009;
}

// Driver Code
public static void Main()
{

    // Taking n as 6
    long N = 4;

    // Printing the nth term
    Console.WriteLine(NthTerm(N));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Nth
// term of the series

$mod = 1000000009;

// function to return nth
// term of the series
function NthTerm($n)
{
    global $mod;
    $x = (2 * $n * $n) % $mod;
    return ($x - $n + $mod) % $mod;
}

// Driver code
$N = 4;

// function call
echo NthTerm($N);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to find N-th
// term of the series:

    // function to return nth term of the series
    function NthTerm(n) {
        var x = (2 * n * n) % 1000000009;
        return (x - n + 1000000009) % 1000000009;
    }

    // Driver Code

        // Taking n as 6
        var N = 4;

        // Printing the nth term
        document.write(NthTerm(N));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
28
```