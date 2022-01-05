# 前三位和后三位

> 原文:[https://www.geeksforgeeks.org/first-and-last-three-bits/](https://www.geeksforgeeks.org/first-and-last-three-bits/)

给定一个整数 **N** 。任务是在 **N** 的**二进制表示**中打印**前三位**和**后三位**的**十进制等价物**。
**示例:**

> **输入:**86
> T3】输出:5 6
> 86 的二进制表示为 1010110。
> 前三位(101)的十进制等效值为 5。
> 最后三位(110)的十进制等效值是 6。
> 因此输出为 5 6。
> **输入:** 7
> **输出:** 7 7

**简单方法:**

*   将 **N** 转换为二进制，并将这些位存储在一个数组中。
*   将数组中的前三个值转换为十进制等效值并打印出来。
*   同样，将数组中的最后三个值转换为十进制等效值并打印出来。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the first
// and last 3 bits equivalent decimal number
void binToDecimal3(int n)
{
    // Converting n to binary
    int a[64] = { 0 };
    int x = 0, i;
    for (i = 0; n > 0; i++) {
        a[i] = n % 2;
        n /= 2;
    }

    // Length of the array has to be at least 3
    x = (i < 3) ? 3 : i;

    // Convert first three bits to decimal
    int d = 0, p = 0;
    for (int i = x - 3; i < x; i++)
        d += a[i] * pow(2, p++);

    // Print the decimal
    cout << d << " ";

    // Convert last three bits to decimal
    d = 0;
    p = 0;
    for (int i = 0; i < 3; i++)
        d += a[i] * pow(2, p++);

    // Print the decimal
    cout << d;
}

// Driver code
int main()
{
    int n = 86;

    binToDecimal3(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach

import java.math.*;
public class GFG {

    //Function to print the first
    //and last 3 bits equivalent decimal number
    static void binToDecimal3(int n)
    {
     // Converting n to binary
     int a[] = new int[64] ;
     int x = 0, i;
     for (i = 0; n > 0; i++) {
         a[i] = n % 2;
         n /= 2;
     }

     // Length of the array has to be at least 3
     x = (i < 3) ? 3 : i;

     // Convert first three bits to decimal
     int d = 0, p = 0;
     for (int j = x - 3; j < x; j++)
         d += a[j] * Math.pow(2, p++);

     // Print the decimal
     System.out.print( d + " ");

     // Convert last three bits to decimal
     d = 0;
     p = 0;
     for (int k = 0; k < 3; k++)
         d += a[k] * Math.pow(2, p++);

     // Print the decimal
     System.out.print(d);
    }

    //Driver code
    public static void main(String[] args) {

        int n = 86;

         binToDecimal3(n);

    }

}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import pow

# Function to print the first and last 3
# bits equivalent decimal number
def binToDecimal3(n):

    # Converting n to binary
    a = [0 for i in range(64)]
    x = 0
    i = 0
    while(n > 0):
        a[i] = n % 2
        n = int(n / 2)
        i += 1

    # Length of the array has to
    # be at least 3
    if (i < 3):
        x = 3
    else:
        x = i

    # Convert first three bits to decimal
    d = 0
    p = 0
    for i in range(x - 3, x, 1):
        d += a[i] * pow(2, p)
        p += 1

    # Print the decimal
    print(int(d), end =" ")

    # Convert last three bits to decimal
    d = 0
    p = 0
    for i in range(0, 3, 1):
        d += a[i] * pow(2, p)
        p += 1

    # Print the decimal
    print(int(d),end = " ")

# Driver code
if __name__ == '__main__':
    n = 86

    binToDecimal3(n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the first and last
// 3 bits equivalent decimal number
static void binToDecimal3(int n)
{

    // Converting n to binary
    int [] a= new int[64] ;
    int x = 0, i;
    for (i = 0; n > 0; i++)
    {
        a[i] = n % 2;
        n /= 2;
    }

    // Length of the array has to be
    // at least 3
    x = (i < 3) ? 3 : i;

    // Convert first three bits to decimal
    int d = 0, p = 0;
    for (int j = x - 3; j < x; j++)
        d += a[j] *(int)Math.Pow(2, p++);

    // Print the decimal
    int d1 = d;

    // Convert last three bits to decimal
    d = 0;
    p = 0;
    for (int k = 0; k < 3; k++)
        d += a[k] * (int)Math.Pow(2, p++);

    // Print the decimal
    Console.WriteLine(d1 + " " + d);
}

// Driver code
static void Main()
{
    int n = 86;

    binToDecimal3(n);
}
}

// This code is contributed by Mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the first
// and last 3 bits equivalent decimal number
function binToDecimal3(n)
{
    // Converting n to binary
    var a = Array(64).fill(0);
    var x = 0, i;
    for (i = 0; n > 0; i++) {
        a[i] = n % 2;
        n = parseInt(n/2);
    }

    // Length of the array has to be at least 3
    x = (i < 3) ? 3 : i;

    // Convert first three bits to decimal
    var d = 0, p = 0;
    for (var i = x - 3; i < x; i++)
        d += a[i] * parseInt(Math.pow(2, p++));

    // Print the decimal
    document.write(d + " ");

    // Convert last three bits to decimal
    d = 0;
    p = 0;
    for (var i = 0; i < 3; i++)
        d += a[i] * parseInt(Math.pow(2, p++));

    // Print the decimal
    document.write(d);
}

// Driver code
var n = 86;
binToDecimal3(n);

</script>
```

**Output:** 

```
5 6
```

**高效方法:**
我们可以使用[按位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)来查找所需的数字。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the first
// and last 3 bits equivalent decimal
// number
void binToDecimal3(int n)
{
    // Number formed from last three
    // bits
    int last_3 = ((n & 4) + (n & 2) + (n & 1));

    // Let us get first three bits in n
    n = n >> 3;
    while (n > 7)
        n = n >> 1;

    // Number formed from first three
    // bits
    int first_3 = ((n & 4) + (n & 2) + (n & 1));

    // Printing result
    cout << first_3 << " " << last_3;
}

// Driver code
int main()
{
    int n = 86;
    binToDecimal3(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to print the first
// and last 3 bits equivalent
// decimal number
static void binToDecimal3(int n)
{
    // Number formed from last three
    // bits
    int last_3 = ((n & 4) +
                  (n & 2) + (n & 1));

    // Let us get first three bits in n
    n = n >> 3;
    while (n > 7)
        n = n >> 1;

    // Number formed from first
    // three bits
    int first_3 = ((n & 4) +
                   (n & 2) + (n & 1));

    // Printing result
    System.out.println(first_3 + " " + last_3);
}

// Driver code
public static void main(String args[])
{
    int n = 86;
    binToDecimal3(n);
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the first and
# last 3 bits equivalent decimal
# number
def binToDecimal3(n) :

    # Number formed from last three
    # bits
    last_3 = ((n & 4) + (n & 2) + (n & 1));

    # Let us get first three bits in n
    n = n >> 3
    while (n > 7) :
        n = n >> 1

    # Number formed from first three
    # bits
    first_3 = ((n & 4) + (n & 2) + (n & 1))

    # Printing result
    print(first_3,last_3)

# Driver code
if __name__ == "__main__" :

    n = 86
    binToDecimal3(n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the first
// and last 3 bits equivalent
// decimal number
static void binToDecimal3(int n)
{
    // Number formed from last three
    // bits
    int last_3 = ((n & 4) +
                (n & 2) + (n & 1));

    // Let us get first three bits in n
    n = n >> 3;
    while (n > 7)
        n = n >> 1;

    // Number formed from first
    // three bits
    int first_3 = ((n & 4) +
                (n & 2) + (n & 1));

    // Printing result
    Console.WriteLine(first_3 + " " + last_3);
}

// Driver code
static public void Main ()
{
    int n = 86;
    binToDecimal3(n);
}
}

// This code is contributed by akt_mit..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the first and last
// 3 bits equivalent decimal number
function binToDecimal3($n)
{
    // Number formed from last three
    // bits
    $last_3 = (($n & 4) + ($n & 2) + ($n & 1));

    // Let us get first three bits in n
    $n = $n >> 3;
    while ($n > 7)
        $n = $n >> 1;

    // Number formed from first three
    // bits
    $first_3 = (($n & 4) + ($n & 2) + ($n & 1));

    // Printing result
    echo($first_3);
    echo(" ");
    echo($last_3);
}

// Driver code
$n = 86;
binToDecimal3($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
  <script>

    // Javascript implementation of the approach

    // Function to print the first
    // and last 3 bits equivalent decimal
    // number
    function binToDecimal3(n)
    {

      // Number formed from last three
      // bits
      var last_3 = ((n & 4) + (n & 2) + (n & 1));

      // Let us get first three bits in n
      n = n >> 3;
      while (n > 7)
        n = n >> 1;

      // Number formed from first three
      // bits
      var first_3 = ((n & 4) + (n & 2) + (n & 1));

      // Printing result
      document.write(first_3 + " " + last_3);
    }

    // Driver code
    var n = 86;
    binToDecimal3(n);

// This code is contributed by rrrtnx.
  </script>
```

**Output:** 

```
5 6
```