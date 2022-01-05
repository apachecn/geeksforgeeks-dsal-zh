# 求数列 3、7、13、21、31 的第 n 项的程序…..

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-3-7-13-21-31/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-the-series-3-7-13-21-31/)

给定一个数字 N，任务是找到这个系列的第 N 项:

> 3, 7, 13, 21, 31, …….

**示例:**

```
Input: N = 4
Output: 21
Explanation:
Nth term = (pow(N, 2) + N + 1)
         = (pow(4, 2) + 4 + 1)
         = 21

Input: N = 11
Output: 133
```

**方法:**
![Sum = 0+3+7+13+21+31+........+a_{n-1} + a_n\\ Sum = 3+7+13+21+31+...+a_{n-2}+a_{n-1}+a_n      ](img/e14f5c51e2b20007d7c039d50fe108ea.png "Rendered by QuickLaTeX.com")
减去这两个方程我们得到
![ 0=3+\left \{\frac{n-1}{2}\right \}[2*4 + (n-2)*2]-a_n\\ =3+\left \{\frac{n-1}{2}\right \}[8 + 2n-4]-a_n\\ =3+\left \{\frac{n-1}{2}\right \}[2n+4]-a_n\\ a_n=3+(n-1)(n+2)\\ a_n=n^2+n+1     ](img/b466bd8d534a5397614c7095eba122fc.png "Rendered by QuickLaTeX.com")
因此，给定级数的第 n 项是:

下面是上述方法的实现:

## C++

```
// CPP program to find the Nth term of given series.
#include <iostream>
#include <math.h>
using namespace std;

// Function to calculate sum
long long int getNthTerm(long long int N)
{
    // Return Nth term
    return (pow(N, 2) + N + 1);
}

// driver code
int main()
{
    // declaration of number of terms
    long long int N = 11;

    // Get the Nth term
    cout << getNthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the Nth term of given series.
import java.util.*;

class solution
{

// Function to calculate sum
static long getNthTerm(long N)
{

   // Return Nth term
    return ((int)Math.pow(N, 2) + N + 1);
}

//Driver program
public static void main(String arr[])
{

   // declaration of number of terms
    long N = 11;

    // Get the Nth term
    System.out.println(getNthTerm(N));

}
}
//THis code is contributed by
//Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 Code to find the
# Nth term of given series.

# Function to calculate sum
def getNthTerm(N):

    # Return Nth term
    return (pow(N, 2) + N + 1)

# driver code
if __name__=='__main__':

# declaration of number of terms
    N = 11

# Get the Nth term
    print(getNthTerm(N))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# code to find the Nth
// term of given series.
using System;

class GFG
{

// Function to calculate sum
static long getNthTerm(long N)
{

// Return Nth term
    return ((int)Math.Pow(N, 2) + N + 1);
}

// Driver Code
static public void Main ()
{

    // declaration of number
    // of terms
    long N = 11;

    // Get the Nth term
    Console.Write(getNthTerm(N));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// Nth term of given series

// Function to calculate sum
function getNthTerm($N)
{
    // Return Nth term
    return (pow($N, 2) + $N + 1);
}

// Driver code

// declaration of number of terms
$N = 11;

// Get the Nth term
echo getNthTerm($N);

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>
// JavaScript program to find the Nth term of given series.

// Function to calculate sum
function getNthTerm(N)
{
    // Return Nth term
    return (Math.pow(N, 2) + N + 1);
}

// driver code

   // declaration of number of terms
   let N = 11;

   // Get the Nth term
   document.write(getNthTerm(N));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
133
```

**时间复杂度:** O(1)