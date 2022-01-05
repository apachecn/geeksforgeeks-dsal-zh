# 求 N 阶乘之和的单位位数

> 原文:[https://www . geeksforgeeks . org/find-the-unit-place-digit-of-n-factories/](https://www.geeksforgeeks.org/find-the-unit-place-digit-of-sum-of-n-factorials/)

给定一个数字 N，任务是找到单位第一个 N 个自然数阶乘的位置数字，即 1！+2!+3!+….n！其中 N <=10e18.
**例:**

```
Input: n = 2 
Output: 3
1! + 2! = 3
Last digit is 3

Input: n = 3
Output: 9
1! + 2! + 3! = 9
Last digit is 9
```

**天真法:**在这种方法中，只需计算每个数的阶乘，并求出这些数的和。最后得到和的单位位数。这将花费大量时间和不必要的计算。
**有效方法:**在这种方法中，只有单位的数字 N 要在范围[1，5]内计算，因为:
1！= 1
2！= 2
3！= 6
4！= 24
5！= 120
6！= 720
7！= 5040
以此类推。
As 5！=120，大于 5 的阶乘有尾随零。所以，N > =5 在做求和的时候不在单位位置做贡献。
因此:

```
if (n < 5)
    ans = (1 ! + 2 ! +..+ n !) % 10;
else
    ans = (1 ! + 2 ! + 3 ! + 4 !) % 10;

Note : We know (1! + 2! + 3! + 4!) % 10 = 3
So we always return 3 when n is greater 
than 4.
```

下面是高效方法的实现:

## C++

```
// C++ program to find the unit place digit
// of the first N natural numbers factorials
#include <iostream>
using namespace std;

// Function to find the unit's place digit
int get_unit_digit(long long int N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 4.
    if (N == 0 || N == 1)
       return 1;
    else if (N == 2)
       return 3;
    else  if (N == 3)
       return 9;

    // We know following
    // (1! + 2! + 3! + 4!) % 10 = 3
    else // (N >= 4)
       return 3;
}

// Driver code
int main()
{
    long long int N = 1;

    for (N = 0; N <= 10; N++)
        cout << "For N = " << N
             << " : " << get_unit_digit(N)
             << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find the unit place digit
// of the first N natural numbers factorials

import java.io.*;

class GFG {

// Function to find the unit's place digit
static int get_unit_digit(  int N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 4.
    if (N == 0 || N == 1)
    return 1;
    else if (N == 2)
    return 3;
    else if (N == 3)
    return 9;

    // We know following
    // (1! + 2! + 3! + 4!) % 10 = 3
    else // (N >= 4)
    return 3;
}

// Driver code

    public static void main (String[] args) {

      int N = 1;

    for (N = 0; N <= 10; N++)
            System.out.println ("For N = " + N
            + " : " + get_unit_digit(N));
    }
}
//This Code is Contributed by ajit
```

## 蟒蛇 3

```
# Python3 program to find the unit
# place digit of the first N natural
# numbers factorials

# Function to find the unit's place digit
def get_unit_digit(N):

    # Let us write for cases when
    # N is smaller than or equal
    # to 4.
    if (N == 0 or N == 1):
        return 1
    elif (N == 2):
        return 3
    elif(N == 3):
        return 9

    # We know following
    # (1! + 2! + 3! + 4!) % 10 = 3
    else:
        return 3

# Driver code
N = 1
for N in range(11):
    print("For N = ", N, ":",
        get_unit_digit(N), sep = ' ')

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find the unit
// place digit of the first N
// natural numbers factorials
using System;

class GFG
{

// Function to find the unit's
// place digit
static int get_unit_digit( int N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 4.
    if (N == 0 || N == 1)
    return 1;
    else if (N == 2)
    return 3;
    else if (N == 3)
    return 9;

    // We know following
    // (1! + 2! + 3! + 4!) % 10 = 3
    else // (N >= 4)
    return 3;
}

// Driver code
static public void Main ()
{
    int N = 1;

    for (N = 0; N <= 10; N++)
        Console.WriteLine ("For N = " + N +
                " : " + get_unit_digit(N));
}
}

// This Code is Contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the unit place digit
// of the first N natural numbers factorials

// Function to find the unit's place digit
function get_unit_digit($N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 4.
    if ($N == 0 || $N == 1)
        return 1;
    else if ($N == 2)
        return 3;
    else if ($N == 3)
        return 9;

    // We know following
    // (1! + 2! + 3! + 4!) % 10 = 3
    else // (N >= 4)
        return 3;
}

// Driver code
$N = 1;

for ($N = 0; $N <= 10; $N++)
    echo "For N = " . $N.
         " : " . get_unit_digit($N) . "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find the unit place digit
// of the first N natural numbers factorials

// Function to find the unit's place digit
function get_unit_digit(N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 4.
    if (N == 0 || N == 1)
      return 1;
    else if (N == 2)
      return 3;
    else if (N == 3)
      return 9;
    // We know following
    // (1! + 2! + 3! + 4!) % 10 = 3
    else // (N >= 4)
      return 3;
}

// Driver code
var N = 1;
for (N = 0; N <= 10; N++)
    document.write( "For N = " + N
        + " : " + get_unit_digit(N)+"<br>")

</script>
```

**Output:** 

```
For N = 0 : 1
For N = 1 : 1
For N = 2 : 3
For N = 3 : 9
For N = 4 : 3
For N = 5 : 3
For N = 6 : 3
For N = 7 : 3
For N = 8 : 3
For N = 9 : 3
For N = 10 : 3
```