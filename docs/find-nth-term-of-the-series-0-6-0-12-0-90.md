# 求数列 0，6，0，12，0，90…的第 n 项

> 原文:[https://www . geesforgeks . org/find-n 系列术语-0-6-0-12-0-90/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-0-6-0-12-0-90/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

> **0，6，0，12，0，90…**

**例:**

```
Input : N = 4
Output : 12
For N = 4
Nth term = abs( 4 * ((4-1) * (4-3) * (4-5)) );
         = 12
Input : N = 6 
Output : 90
```

我们可以将上述级数的第 n 项推广为:

```
Nth term = abs( N * ((N-1) * (N-3) * (N-5)) )
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series
// 0, 6, 0, 12, 0, 90...

#include <iostream>
using namespace std;

// Function to return the Nth term
int nthTerm(int N)
{
    return abs(N * ((N - 1) * (N - 3) * (N - 5)));
}

// Driver code
int main()
{
    int N = 6;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series
// 0, 6, 0, 12, 0, 90...

import java.io.*;
import java.lang.*;

class GFG {
    // Function to calculate Nth term of
    // the series
    public static int nthTerm(int N)
    {
        // By using above formula
        return Math.abs(N * ((N - 1) * (N - 3) * (N - 5)));
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 6; // Nth term is 6

        System.out.println(nthTerm(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find N-th
# term of the series
# 0, 6, 0, 12, 0, 90...

# Function to return the Nth term
def nthTerm(N) :

    return (abs(N * ((N - 1) * (N - 3)
           * (N - 5))))

# Driver code    
if __name__ == "__main__" :

    N = 6

    # Function calling
    print(nthTerm(N))

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program to find N-th term of the series
// 0, 6, 0, 12, 0, 90...

using System;

class GFG {
    // Function to calculate Nth term of
    // the series
    public static int nthTerm(int N)
    {
        // By using above formula
        return Math.Abs(N * ((N - 1) * (N - 3) * (N - 5)));
    }

    // Driver code
    public static void Main()
    {
        int N = 6; // Nth term is 6

        Console.WriteLine(nthTerm(N));
    }
}
// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series
// 0, 6, 0, 12, 0, 90...

// Function to return the Nth term
function nthTerm( $N)
{
    return abs($N * (($N - 1) *
              ($N - 3) * ($N - 5)));
}

// Driver code
$N = 6;

echo nthTerm($N);

// This code is contributed
// by inder_verma..
?>
```

## java 描述语言

```
<script>
// JavaScript  program to find N-th term of the series
// 0, 6, 0, 12, 0, 90...

// Function to return the Nth term
function nthTerm( N)
{
    return Math.abs(N * ((N - 1) * (N - 3) * (N - 5)));
}

// Driver code

    let N = 6;
   document.write( nthTerm(N) );

// This code contributed by aashish1995

</script>
```

**Output:** 

```
90
```

**时间复杂度** : O(1)