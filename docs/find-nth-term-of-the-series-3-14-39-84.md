# 求数列 3、14、39、84 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n 系列术语-3-14-39-84/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-3-14-39-84/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

> 3, 14, 39, 84…

**例:**

```
Input: 3
Output: 39
For N = 3
Nth term = ( 3*3*3 ) + ( 3*3 ) + 3
         = 39

Input: 4
Output: 84
```

计算级数第 n 项的公式:

```
Nth term = ( N*N*N ) + ( N*N ) + N 
```

下面是需要的实现:

## C++

```
// CPP program to find N-th term of the series:
// 3, 14, 38, 84...
#include <iostream>
using namespace std;

// calculate Nth term of series
int nthTerm(int N)
{
    return (N * N * N) + (N * N) + N;
}

// Driver Function
int main()
{
    int N = 3;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Nth number
import java.io.*;

// calculate Nth term of this series
class GFG
{
public int nthTerm(int N)
{
    // By using above formula
    return (N * N * N) + (N * N) + N;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    GFG a = new GFG();

    // call and print Nth term
    System.out.println(a.nthTerm(N));
}
}
```

## 蟒蛇 3

```
# Python 3 program to find  N-th
# term of the series:
# 3, 14, 38, 84...

# Function to calculate Nth term of series 
def nthTerm(n) :

    return (N * N * N) + (N * N) + N

# Driver code
if __name__ == "__main__" :

     N = 3

     # function calling
     print(nthTerm(N))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find Nth number
using System;

// calculate Nth term of this series
class GFG
{
public int nthTerm(int N)
{
    // By using above formula
    return (N * N * N) + (N * N) + N;
}

// Driver Code
public static void Main()
{
    int N = 3;
    GFG a = new GFG();

    // call and print Nth term
    Console.WriteLine(a.nthTerm(N));
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find N-th term 
// of the series: 3, 14, 38, 84...

// calculate Nth term of series
function nthTerm($N)
{
    return ($N * $N * $N) +
           ($N * $N) + $N;
}

// Driver Code
$N = 3;

echo nthTerm($N);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScriptprogram to find N-th term of the series:
// 3, 14, 38, 84...

// calculate Nth term of series
function nthTerm( N)
{
    return (N * N * N) + (N * N) + N;
}

// Driver Function

    let N = 3;
    document.write(nthTerm(N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
39
```