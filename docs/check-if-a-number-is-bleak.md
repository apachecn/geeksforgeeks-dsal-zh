# 检查一个数字是否暗淡

> 原文:[https://www.geeksforgeeks.org/check-if-a-number-is-bleak/](https://www.geeksforgeeks.org/check-if-a-number-is-bleak/)

如果数字“n”不能表示为正数 x 和 x 中的设置位计数之和，即对于任何非负数 x，x + [countSetBits(x)](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/) 不等于 n，则该数字称为“萧瑟”。例如:
:

```
Input : n = 3
Output : false
3 is not Bleak as it can be represented
as 2 + countSetBits(2).

Input : n = 4
Output : true
4 is t Bleak as it cannot be represented 
as sum of a number x and countSetBits(x)
for any number x.
```

**方法 1(简单)**

```
bool isBleak(n)
1) Consider all numbers smaller than n
    a) If x + countSetBits(x) == n
           return false

2) Return true
```

下面是简单方法的实现。

## C++

```
// A simple C++ program to check Bleak Number
#include <bits/stdc++.h>
using namespace std;

/* Function to get no of set bits in binary
   representation of passed binary no. */
int countSetBits(int x)
{
    unsigned int count = 0;
    while (x) {
        x &= (x - 1);
        count++;
    }
    return count;
}

// Returns true if n is Bleak
bool isBleak(int n)
{
    // Check for all numbers 'x' smaller
    // than n.  If x + countSetBits(x)
    // becomes n, then n can't be Bleak
    for (int x = 1; x < n; x++)
        if (x + countSetBits(x) == n)
            return false;

    return true;
}

// Driver code
int main()
{
    isBleak(3) ? cout << "Yes\n" : cout << "No\n";
    isBleak(4) ? cout << "Yes\n" : cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to check Bleak Number
import java.io.*;

class GFG {

    /* Function to get no of set bits in binary
       representation of passed binary no. */
    static int countSetBits(int x)
    {
        int count = 0;
        while (x != 0) {
            x &= (x - 1);
            count++;
        }
        return count;
    }

    // Returns true if n is Bleak
    static boolean isBleak(int n)
    {
        // Check for all numbers 'x' smaller
        // than n.  If x + countSetBits(x)
        // becomes n, then n can't be Bleak
        for (int x = 1; x < n; x++)
            if (x + countSetBits(x) == n)
                return false;

        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        if (isBleak(3))
            System.out.println("Yes");
        else
            System.out.println("No");
        if (isBleak(4))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# A simple Python 3 program
# to check Bleak Number

# Function to get no of set
# bits in binary
# representation of passed
# binary no.
def countSetBits(x) :

    count = 0

    while (x) :
        x = x & (x-1)
        count = count + 1

    return count

# Returns true if n
# is Bleak
def isBleak(n) :

    # Check for all numbers 'x'
    # smaller than n. If x +
    # countSetBits(x) becomes
    # n, then n can't be Bleak.
    for x in range(1, n) :

        if (x + countSetBits(x) == n) :
            return False

    return True

# Driver code
if(isBleak(3)) :
    print( "Yes")
else :
    print("No")

if(isBleak(4)) :
    print("Yes")
else :
    print( "No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A simple C# program to check
// Bleak Number
using System;

class GFG {

    /* Function to get no of set
    bits in binary representation
    of passed binary no. */
    static int countSetBits(int x)
    {
        int count = 0;

        while (x != 0) {
            x &= (x - 1);
            count++;
        }

        return count;
    }

    // Returns true if n is Bleak
    static bool isBleak(int n)
    {

        // Check for all numbers
        // 'x' smaller than n. If
        // x + countSetBits(x)
        // becomes n, then n can't
        // be Bleak
        for (int x = 1; x < n; x++)

            if (x + countSetBits(x)
                              == n)
                return false;

        return true;
    }

    // Driver code
    public static void Main()
    {
        if (isBleak(3))
            Console.Write("Yes");
        else
            Console.WriteLine("No");

        if (isBleak(4))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by
// Nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program
// to check Bleak Number

// Function to get no of
// set bits in binary
// representation of
// passed binary no.
function countSetBits( $x)
{
    $count = 0;
    while ($x)
    {
        $x &= ($x - 1);
        $count++;
    }
    return $count;
}

// Returns true if n is Bleak
function isBleak( $n)
{

    // Check for all numbers 'x' smaller
    // than n. If x + countSetBits(x)
    // becomes n, then n can't be Bleak
    for($x = 1; $x < $n; $x++)
        if ($x + countSetBits($x) == $n)
            return false;

    return true;
}

    // Driver code
    if(isBleak(3))
        echo "Yes\n" ;
    else
        echo "No\n";

    if(isBleak(4))
        echo "Yes\n" ;
    else
        echo "No\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check Bleak Number

    /* Function to get no of set bits in binary
       representation of passed binary no. */
    function countSetBits(x)
    {
        let count = 0;
        while (x != 0) {
            x &= (x - 1);
            count++;
        }
        return count;
    }

    // Returns true if n is Bleak
    function isBleak(n)
    {
        // Check for all numbers 'x' smaller
        // than n.  If x + countSetBits(x)
        // becomes n, then n can't be Bleak
        for (let x = 1; x < n; x++)
            if (x + countSetBits(x) == n)
                return false;

        return true;
    }

// Driver Code

        if (isBleak(3))
            document.write("Yes" + "<br/>");
        else
            document.write("No" + "<br/>");
        if (isBleak(4))
            document.write("Yes" + "<br/>");
        else
            document.write("No" + "<br/>");

</script>
```

**输出:**

```
No
Yes
```

上述解的时间复杂度为 O(n ^ Log n)。

**辅助空间:** O(1)
**方法 2(高效)**
这个想法是基于这样一个事实，即任何小于 n 的数字中的最大设置位数都不能超过 Log 的上限 <sub>2</sub> n。因此我们只需要检查范围从 n–ceilinglog 2(n)到 n 的数字。

```
bool isBleak(n)
1) Consider all numbers n - ceiling(Log<sub>2n) to n-1</sub>
    a) If x + countSetBits(x) == n
           return false

2) Return true
```

下面是这个想法的实现。

## C++

```
// An efficient C++ program to check Bleak Number
#include <bits/stdc++.h>
using namespace std;

/* Function to get no of set bits in binary
   representation of passed binary no. */
int countSetBits(int x)
{
    unsigned int count = 0;
    while (x) {
        x &= (x - 1);
        count++;
    }
    return count;
}

// A function to return ceiling of log x
// in base 2\. For example, it returns 3
// for 8 and 4 for 9.
int ceilLog2(int x)
{
    int count = 0;
    x--;
    while (x > 0) {
        x = x >> 1;
        count++;
    }
    return count;
}

// Returns true if n is Bleak
bool isBleak(int n)
{
    // Check for all numbers 'x' smaller
    // than n.  If x + countSetBits(x)
    // becomes n, then n can't be Bleak
    for (int x = n - ceilLog2(n); x < n; x++)
        if (x + countSetBits(x) == n)
            return false;

    return true;
}

// Driver code
int main()
{
    isBleak(3) ? cout << "Yes\n" : cout << "No\n";
    isBleak(4) ? cout << "Yes\n" : cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to
// check Bleak Number
import java.io.*;

class GFG {

    /* Function to get no of set bits in
    binary representation of passed binary
    no. */
    static int countSetBits(int x)
    {
        int count = 0;
        while (x != 0) {
            x &= (x - 1);
            count++;
        }
        return count;
    }

    // A function to return ceiling of log x
    // in base 2\. For example, it returns 3
    // for 8 and 4 for 9.
    static int ceilLog2(int x)
    {
        int count = 0;
        x--;
        while (x > 0) {
            x = x >> 1;
            count++;
        }
        return count;
    }

    // Returns true if n is Bleak
    static boolean isBleak(int n)
    {
        // Check for all numbers 'x' smaller
        // than n. If x + countSetBits(x)
        // becomes n, then n can't be Bleak
        for (int x = n - ceilLog2(n); x < n; x++)
            if (x + countSetBits(x) == n)
                return false;

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        if (isBleak(3))
            System.out.println("Yes");
        else
            System.out.println("No");

        if (isBleak(4))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# An efficient Python 3 program
# to check Bleak Number
import math

# Function to get no of set
# bits in binary representation
# of passed binary no.
def countSetBits(x) :

    count = 0

    while (x) :
        x = x & (x - 1)
        count = count + 1

    return count

# A function to return ceiling
# of log x in base 2\. For
# example, it returns 3 for 8
# and 4 for 9.
def ceilLog2(x) :

    count = 0
    x = x - 1

    while (x > 0) :
        x = x>>1
        count = count + 1

    return count

# Returns true if n is Bleak
def isBleak(n) :

    # Check for all numbers 'x'
    # smaller than n. If x +
    # countSetBits(x) becomes n,
    # then n can't be Bleak
    for x in range ((n - ceilLog2(n)), n) :

        if (x + countSetBits(x) == n) :
            return False

    return True

# Driver code
if(isBleak(3)) :
    print("Yes")
else :
    print( "No")

if(isBleak(4)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// An efficient C# program to check
// Bleak Number
using System;

class GFG {

    /* Function to get no of set
    bits in binary representation
    of passed binary no. */
    static int countSetBits(int x)
    {
        int count = 0;
        while (x != 0) {
            x &= (x - 1);
            count++;
        }
        return count;
    }

    // A function to return ceiling
    // of log x in base 2\. For
    // example, it returns 3 for 8
    // and 4 for 9.
    static int ceilLog2(int x)
    {
        int count = 0;
        x--;
        while (x > 0) {
            x = x >> 1;
            count++;
        }
        return count;
    }

    // Returns true if n is Bleak
    static bool isBleak(int n)
    {

        // Check for all numbers
        // 'x' smaller than n. If
        // x + countSetBits(x)
        // becomes n, then n
        // can't be Bleak
        for (int x = n - ceilLog2(n);
                          x < n; x++)
            if (x + countSetBits(x)
                               == n)
                return false;

        return true;
    }

    // Driver code
    public static void Main()
    {
        if (isBleak(3))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        if (isBleak(4))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program
// to check Bleak Number

/* Function to get no of set
   bits in binary representation
   of passed binary no. */
function countSetBits( $x)
{
    $count = 0;
    while ($x)
    {
        $x &= ($x - 1);
        $count++;
    }
    return $count;
}

// A function to return ceiling of log x
// in base 2\. For example, it returns 3
// for 8 and 4 for 9.
function ceilLog2( $x)
{

    $count = 0;
    $x--;
    while ($x > 0)
    {
        $x = $x >> 1;
        $count++;
    }
    return $count;
}

// Returns true if n is Bleak
function isBleak( $n)
{

    // Check for all numbers 'x' smaller
    // than n. If x + countSetBits(x)
    // becomes n, then n can't be Bleak
    for ($x = $n - ceilLog2($n); $x < $n; $x++)
        if ($x + countSetBits($x) == $n)
            return false;

    return true;
}

    // Driver code
    if(isBleak(3))
        echo "Yes\n" ;

    else
        echo "No\n";

    if(isBleak(4))
        echo "Yes\n" ;

    else
        echo "No\n";

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>
    // An efficient JavaScript
    // program to check Bleak Number

    /* Function to get no of set
    bits in binary representation
    of passed binary no. */
    function countSetBits(x)
    {
        let count = 0;
        while (x != 0) {
            x &= (x - 1);
            count++;
        }
        return count;
    }

    // A function to return ceiling
    // of log x in base 2\. For
    // example, it returns 3 for 8
    // and 4 for 9.
    function ceilLog2(x)
    {
        let count = 0;
        x--;
        while (x > 0) {
            x = x >> 1;
            count++;
        }
        return count;
    }

    // Returns true if n is Bleak
    function isBleak(n)
    {

        // Check for all numbers
        // 'x' smaller than n. If
        // x + countSetBits(x)
        // becomes n, then n
        // can't be Bleak
        for (let x = n - ceilLog2(n); x < n; x++)
            if (x + countSetBits(x) == n)
                return false;

        return true;
    }

    if (isBleak(3))
      document.write("Yes" + "</br>");
    else
      document.write("No" + "</br>");

    if (isBleak(4))
      document.write("Yes" + "</br>");
    else
      document.write("No" + "</br>");

</script>
```

**输出:**

```
No
Yes
```

时间复杂度:0(对数 n *对数 n)

**辅助空间:** O(1)
**注:**在 GCC 中，我们可以使用 __builtin_popcount()直接对集合位进行计数。因此，我们可以避免使用单独的函数来计算集合位。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate __builtin_popcount()
#include <iostream>
using namespace std;

int main()
{
    cout << __builtin_popcount(4) << endl;
    cout << __builtin_popcount(15);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate Integer.bitCount()
import java.util.*;

class GFG{

public static void main(String[] args)
{
    System.out.print(Integer.bitCount(4) +"\n");
    System.out.print(Integer.bitCount(15));

}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python program to demonstrate Integer.bitCount()

def bitsoncount(i):
    assert 0 <= i < 0x100000000
    i = i - ((i >> 1) & 0x55555555)
    i = (i & 0x33333333) + ((i >> 2) & 0x33333333)
    return (((i + (i >> 4) & 0xF0F0F0F) * 0x1010101) & 0xffffffff) >> 24

# Driver code
if __name__ == '__main__':
    x = 4;
    y = 15;
    print(bitsoncount(x));
    print(bitsoncount(y));

# This code is contributed by umadevi9616
```

## C#

```
// C# program to demonstrate int.bitCount()
using System;

public class GFG{
public static int bitCount (int n) {
      n = n - ((n >> 1) & 0x55555555);
      n = (n & 0x33333333) + ((n >> 2) & 0x33333333);
      return ((n + (n >> 4) & 0xF0F0F0F) * 0x1010101) >> 24;
    }
public static void Main(String[] args)
{
    Console.WriteLine(bitCount(4));
    Console.WriteLine(bitCount(15));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// javascript program to demonstrate int.bitCount()
function bitCount ( n) {
      n = n - ((n >> 1) & 0x55555555);
      n = (n & 0x33333333) + ((n >> 2) & 0x33333333);
      return ((n + (n >> 4) & 0xF0F0F0F) * 0x1010101) >> 24;
    }

     document.write(bitCount(4)+"<br/>");
     document.write(bitCount(15));

// This code is contributed by gauravrajput1
</script>
```

输出:

```
1
4
```

时间复杂度:0(对数 n)

辅助空间:0(1)

本文由**拉华因**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息