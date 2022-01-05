# 程序寻找系列 9，23，45，75，113 的第 n 项……

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-9-23-45-75-113/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-series-9-23-45-75-113/)

给定一个数字 N，任务是找到给定数列中的第 N 项:

```
9, 23, 45, 75, 113, 159......
```

**例:**

```
Input: 4
Output: 113
Explanation:
For N = 4
Nth term = ( 2 * N + 3 )*( 2 * N + 3 ) - 2 * N
         = ( 2 * 4 + 3 )*( 2 * 4 + 3 ) - 2 * 4
         = 113

Input: 10
Output: 509
```

**方法:**
给定序列的第 n 项可以概括为:

```
Nth term of the series : ( 2 * N + 3 )*( 2 * N + 3 ) - 2 * N
```

下面是上面问题的实现:
**程序:**

## C++

```
// CPP program to find N-th term of the series:
// 9, 23, 45, 75, 113...

#include <iostream>
using namespace std;

// calculate Nth term of series
int nthTerm(int N)
{
    return (2 * N + 3) * (2 * N + 3) - 2 * N;
}

// Driver Function
int main()
{

    // Get the value of N
    int N = 4;

    // Find the Nth term
    // and print it
    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// N-th term of the series:
// 9, 23, 45, 75, 113...

class GFG
{

// calculate Nth term of series
static int nthTerm(int N)
{
    return (2 * N + 3) *
           (2 * N + 3) - 2 * N;
}

// Driver code
public static void main(String[] args)
{

    // Get the value of N
    int N = 4;

    // Find the Nth term
    // and print it
    System.out.println(nthTerm(N));
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python program to find
# N-th term of the series:
# 9, 23, 45, 75, 113...
def nthTerm(N):

    # calculate Nth term of series
    return ((2 * N + 3) *
            (2 * N + 3) - 2 * N);

# Driver Code

# Get the value of N
n = 4

# Find the Nth term
# and print it
print(nthTerm(n))

# This code is contributed by Bilal
```

## C#

```
// C# program to find
// N-th term of the series:
// 9, 23, 45, 75, 113...
using System;

class GFG
{

// calculate Nth term of series
static int nthTerm(int N)
{
    return (2 * N + 3) *
           (2 * N + 3) - 2 * N;
}

// Driver code
public static void Main()
{

    // Get the value of N
    int N = 4;

    // Find the Nth term
    // and print it
    Console.WriteLine(nthTerm(N));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 9, 23, 45, 75, 113...

// calculate Nth term of series
function nthTerm($N)
{
    return (2 * $N + 3) *
           (2 * $N + 3) - 2 * $N;
}

// Driver Code

// Get the value of N
$N = 4;

// Find the Nth term
// and print it
echo nthTerm($N);

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 9, 23, 45, 75, 113...

// calculate Nth term of series
function nthTerm( N)
{
    return (2 * N + 3) * (2 * N + 3) - 2 * N;
}
// Driver Function

    // get the value of N
    let N = 4;

    // Calculate and print the Nth term
    document.write(  nthTerm(N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
113
```

**时间复杂度:** O(1)