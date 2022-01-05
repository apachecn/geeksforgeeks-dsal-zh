# 求数列 1、4、15、72、420 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n 系列术语-1-4-15-72-420/](https://www.geeksforgeeks.org/find-nth-term-of-series-1-4-15-72-420/)

给定一个数字 N。任务是编写一个程序来查找下面系列中的第 N 个<sup>项:</sup>

> **1、4、15、72、420……**

**示例:**

```
Input: 3
Output: 15
For N = 3, we know that the factorial of 3 is 6
Nth term = 6*(3+2)/2
         = 15

Input: 6
Output: 2880
For N = 6, we know that the factorial of 6 is 720
Nth term = 620*(6+2)/2
         = 2880
```

想法是先求给定数 N 的阶乘，也就是 N！。现在，上述系列中的第 N 项将是:

> **第 N 项** = N！* (N + 2)/2

下面是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 1, 4, 15, 72, 420…
#include <iostream>
using namespace std;

// Function to find factorial of N
int factorial(int N)
{
    int fact = 1;

    for (int i = 1; i <= N; i++)
        fact = fact * i;

    // return factorial of N        
    return fact;
}

// calculate Nth term of series
int nthTerm(int N)
{
    return (factorial(N) * (N + 2) / 2);
}

// Driver Function
int main()
{
    int N = 6;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// term of the series:
// 1, 4, 15, 72, 420
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to find factorial of N
static int factorial(int N)
{
    int fact = 1;

    for (int i = 1; i <= N; i++)
        fact = fact * i;

    // return factorial of N    
    return fact;
}

// calculate Nth term of series
static int nthTerm(int N)
{
    return (factorial(N) * (N + 2) / 2);
}

// Driver Code
public static void main(String args[])
{
    int N = 6;

    System.out.println(nthTerm(N));
}
}

// This code is contributed by Subhadeep
```

## 蟒蛇 3

```
# Python 3 program to find
# N-th term of the series:
# 1, 4, 15, 72, 420…

# Function for finding
# factorial of N
def factorial(N) :
    fact = 1
    for i in range(1, N + 1) :
        fact = fact * i

    # return factorial of N
    return fact

# Function for calculating
# Nth term of series
def nthTerm(N) :

    # return nth term
    return (factorial(N) * (N + 2) // 2)

# Driver code
if __name__ == "__main__" :

    N = 6

    # Function Calling
    print(nthTerm(N))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to find N-th
// term of the series:
// 1, 4, 15, 72, 420
using System;

class GFG
{

// Function to find factorial of N
static int factorial(int N)
{
    int fact = 1;

    for (int i = 1; i <= N; i++)
        fact = fact * i;

    // return factorial of N    
    return fact;
}

// calculate Nth term of series
static int nthTerm(int N)
{
    return (factorial(N) * (N + 2) / 2);
}

// Driver Code
public static void Main()
{
    int N = 6;

    Console.Write(nthTerm(N));
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 1, 4, 15, 72, 420…

// Function for finding
// factorial of N
function factorial($N)
{
    $fact = 1;
    for($i = 1; $i <= $N; $i++)
        $fact = $fact * $i;

    // return factorial of N
    return $fact;
}

// Function for calculating
// Nth term of series
function nthTerm($N)
{

    // return nth term
    return (factorial($N) *
           ($N + 2) / 2);
}

// Driver code
$N = 6;

// Function Calling
echo nthTerm($N);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 1, 4, 15, 72, 420…

// Function to find factorial of N
function factorial( N)
{
    let fact = 1;

    for (let i = 1; i <= N; i++)
        fact = fact * i;

    // return factorial of N        
    return fact;
}

// calculate Nth term of series
function nthTerm(N)
{
    return (factorial(N) * (N + 2) / 2);
}
// Driver code

    let N = 6;
   document.write( nthTerm(N) );

// This code contributed by aashish1995

</script>
```

**Output:** 

```
2880
```

**另一种方法:**(使用递归)

## C++

```
// CPP program to find N-th term of the series:
// 1, 4, 15, 72, 420…
// Using recursion
#include <iostream>
using namespace std;

// Function to find factorial of N
// with recursion
int factorial(int N)
{
    // base condition
    if( N == 0 || N == 1 )
        return 1;
    // use recursion
    return N * factorial( N - 1 );
}

// calculate Nth term of series
int nthTerm(int N)
{
    return (factorial(N) * (N + 2) / 2);
}

// Driver Function
int main()
{
    int N = 6;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// term of the series:
// 1, 4, 15, 72, 420
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to find factorial of N
static int factorial(int N)
{
    // base condition
    if( N == 0 || N == 1 )
        return 1;
    // use recursion
    return N * factorial( N - 1 );
}

// calculate Nth term of series
static int nthTerm(int N)
{
    return (factorial(N) * (N + 2) / 2);
}

// Driver Code
public static void main(String args[])
{
    int N = 6;

    System.out.println(nthTerm(N));
}
}
```

## 蟒蛇 3

```
# Python3 program to find
# N-th term of the series:
# 1, 4, 15, 72, 420…
# Using recursion

# Function to find factorial
# of N with recursion
def factorial(N):

    # base condition
    if N == 0 or N == 1:
        return 1

    # use recursion
    return N * factorial(N - 1)

def nthTerm(N):

    # calculate Nth term of series
    return (factorial(N) * (N + 2) // 2)

# Driver code
N = 6
print(nthTerm(N))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# program to find N-th
// term of the series:
// 1, 4, 15, 72, 420
using System;

class GFG
{

// Function to find factorial of N
static int factorial(int N)
{
    // base condition
    if( N == 0 || N == 1 )
        return 1;
    // use recursion
    return N * factorial( N - 1 );
}

// calculate Nth term of series
static int nthTerm(int N)
{
    return (factorial(N) * (N + 2) / 2);
}

// Driver Code
public static void Main()
{
    int N = 6;

    Console.Write(nthTerm(N));
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 1, 4, 15, 72, 420…

// Function to find factorial
// of N with recursion
function factorial($N)
{
    // base condition
    if($N == 0 or $N == 1)
        return 1;

    // use recursion
    return $N * factorial($N - 1);
}

// calculate Nth term of series
function nthTerm($N)
{
    return (factorial($N) *
           ($N + 2) / 2);
}

// Driver Code
$N = 6;

echo nthTerm($N);

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

// Javascript program to find N-th
// term of the series:
// 1, 4, 15, 72, 420

// Function to find factorial of N
function factorial(N)
{

    // Base condition
    if (N == 0 || N == 1)
        return 1;

    // Use recursion
    return N * factorial(N - 1);
}

// Calculate Nth term of series
function nthTerm(N)
{
    return(factorial(N) * (N + 2) / 2);
}

// Driver Code
let N = 6;

document.write(nthTerm(N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2880
```

**时间复杂度** : O(N)
**注意:**上面的代码对大 N 值不起作用，要找到大 N 的值，对大数使用[阶乘的概念。](https://www.geeksforgeeks.org/factorial-large-number/)