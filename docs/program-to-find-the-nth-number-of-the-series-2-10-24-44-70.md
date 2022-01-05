# 程序求数列 2，10，24，44，70 的第 n 个数…..

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-number-the-series-2-10-24-44-70/](https://www.geeksforgeeks.org/program-to-find-the-nth-number-of-the-series-2-10-24-44-70/)

给定一个数字 n，任务是找到这个数列的第 n 个(n 可以是 10^18)项:

> 2, 10, 24, 44, 70…..

答案可能非常大，所以在模 10^9+9.下打印答案

**示例:**

```
Input: N = 2
Output: 10

Input: N = 5
Output: 70
```

**方法:**第 n 项的公式为:

> 第 n 项= 3 * n * n–n

下面是上述方法的实现:

## C++

```
// CPP program to find
// the Nth term of the series
// 2, 10, 24, 44, 70.....

#include <bits/stdc++.h>
using namespace std;

#define mod 1000000009

// function to return nth term of the series
int NthTerm(long long n)
{
    long long x = (3 * n * n) % mod;
    return (x - n + mod) % mod;
}

// Driver code
int main()
{

// Get N
    long long N = 4;

    // Get Nth term
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
        long x = (3 * n * n) % 1000000009;
        return (x - n + 1000000009) % 1000000009;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Taking  n as 4
        long N = 4;

        // Printing the nth term
        System.out.println(NthTerm(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find  
# N-th term of the series:  

# Function for calculating  
# Nth term of series  
def NthTerm(N) :  

    # return nth term
    x = (3 * N*N)% 1000000009
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
    long x = (3 * n * n) % 1000000009;
    return (x - n + 1000000009) % 1000000009;
}

// Driver Code
public static void Main()
{

    // Taking n as 4
    long N = 4;

    // Printing the nth term
    Console.Write(NthTerm(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the Nth term of the series
// 2, 10, 24, 44, 70.....

// function to return Nth
// term of the series
function NthTerm($n)
{
    $mod = 1000000009;

    $x = (3 * $n * $n) % $mod;
    return ($x - $n + $mod) % $mod;
}

// Driver code
$N = 4;

// Get Nth term
echo NthTerm($N);

// This code is contributed
// by Mahadev99
?>
```

## java 描述语言

```
<script>

// Javascript program to find N-th
// term of the series:

    // function to return nth term of the series
    function NthTerm( n) {
        let x = (3 * n * n) % 1000000009;
        return (x - n + 1000000009) % 1000000009;
    }

    // Driver Code

        // Taking n as 4
        let N = 4;

        // Printing the nth term
        document.write(NthTerm(N));

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
44
```