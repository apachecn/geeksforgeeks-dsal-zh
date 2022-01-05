# 检查一个数是否是 8 的幂

> 原文:[https://www.geeksforgeeks.org/check-number-power-8-not/](https://www.geeksforgeeks.org/check-number-power-8-not/)

给定一个数，检查它是否是 8 的幂。

**示例:**

```
Input : n = 64
Output : Yes

Input : 75
Output : No
```

**首解**

我们计算数的 log8(n)，如果它是整数，那么 n 是 8 的幂。我们使用 trunc(n)函数来为双精度值找到最接近的整数。

## C++

```
// C++ program to check if a number is power of 8
#include <cmath>
#include <iostream>
using namespace std;

/* function to check if power of 8 */
bool checkPowerof8(int n)
{
    /* calculate log8(n) */
    double i = log(n) / log(8);

    /* check if i is an integer or not */
    return (i - trunc(i) < 0.000001);
}

/* driver function */
int main()
{
    int n = 65;
    checkPowerof8(n) ? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a number is power of 8

class GFG {

    // function to check
    // if power of 8
    static boolean checkPowerof8(int n)
    {
        /* calculate log8(n) */
        double i = Math.log(n) / Math.log(8);

        /* check if i is an integer or not */
        return (i - Math.floor(i) < 0.000001);
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 65;
        if (checkPowerof8(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to check
# if a number is power of 8
from math import log,trunc

# function to check if power of 8
def checkPowerof8(n):

    # calculate log8(n)
    i = log(n, 8)

    # check if i is an integer or not
    return (i - trunc(i) < 0.000001);

# Driver Code
n = 65
if checkPowerof8(n):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C#  program to check if
// a number is power of 8
using System;

class GFG {

    // function to check
    // if power of 8
    static bool checkPowerof8(int n)
    {

        // calculate log8(n) */
        double i = Math.Log(n) / Math.Log(8);

        // check if i is an integer or not */
        return (i - Math.Floor(i) < 0.000001);
    }

    // Driver Code
    static public void Main()
    {
        int n = 65;

        if (checkPowerof8(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is power of 8

// function to check
// if power of 8
function checkPowerof8($n)
{
    /* calculate log8(n) */
    $i = log($n) / log(8);

    /* check if i is an integer or not */
    return ($i - floor($i) < 0.000001);
}

// Driver Code
$n = 65;
if(checkPowerof8($n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

    // Javascript program to check if
    // a number is power of 8

    // function to check
    // if power of 8
    function checkPowerof8(n)
    {

        // calculate log8(n) */
        let i = Math.log(n) / Math.log(8);

        // check if i is an integer or not */
        return (i - Math.floor(i) < 0.000001);
    }

    let n = 65;

    if (checkPowerof8(n))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**输出:**

```
No
```

**第二个解**
如果满足以下条件，一个数是 8 的幂。

1.  [这个数字是](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) [二](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)的幂。如果一个数只有一个设置位，即 n 和 n-1 的按位“与”为 0，则该数为 2 的幂。
2.  这个数字在 0、3、6 或…位置只有一位。30[对于 32 位数字]。要检查其设置位的位置，我们可以使用掩码(0xb6 db 6 db 6)<sub>16</sub>=(10110110110110110110110110110110)<sub>2</sub>。

以下是上述想法的实现。

## C++

```
// C++ program to check if a number is power of 8
// using bit mask.
#include <bits/stdc++.h>
using namespace std;

/*function to check if power of 8*/
bool checkPowerof8(int n)
{
    return (n && !(n & (n - 1)) && !(n & 0xB6DB6DB6));
}

/*driver function*/
int main()
{
    int n = 65;
    checkPowerof8(n) ? cout << "Yes" : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// number is power of 8 using
// bit mask.
import java.util.*;
class GFG{

// function to check if
// power of 8
static boolean checkPowerof8(int n)
{
  return (n > 0 && (n & (n - 1)) > 0 &&
         (n & 0xB6DB6DB6) > 0);
}

// Driver code
public static void main(String[] args)
{
  int n = 65;
  if (checkPowerof8(n) == true)
    System.out.print("Yes" );
  else
    System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if a number
# is power of 8

# function to check if power of 8
def checkPowerof8(n):

    return (n and not (n & (n - 1)) and
                  not (n & 0xB6DB6DB6))

# Driver Code
if __name__ == "__main__":

    n = 65

if checkPowerof8(n):
    print ("Yes") 
else:
    print ("No")

# This code is contributed by ita_c
```

## C#

```
// C# program to check if a
// number is power of 8 using
// bit mask.
using System;

class GFG{

// Function to check if
// power of 8
static bool checkPowerof8(int n)
{
    return (n > 0 && (n & (n - 1)) > 0 &&
           (n & 0xB6DB6DB6) > 0);
}

// Driver code
static public void Main()
{
    int n = 65;

    if (checkPowerof8(n) == true)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by avanitrachhadiya2155
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is power of 8 using bit mask.

// function to check if power of 8
function checkPowerof8($n)
{
    $t = ($n && !($n & ($n - 1)) &&
                !($n & 0xB6DB6DB6));
    return $t;
}

// Driver Code
$n = 65;
if(checkPowerof8($n))
    echo "Yes" ;
else
    echo "No";

// This code is contributed by Sach
?>
```

## java 描述语言

```
<script>

/*function to check if power of 8*/
function checkPowerof8( n)
{
    return (n && !(n & (n - 1)) && !(n & 0xB6DB6DB6));
}

var n = 65;
    if(checkPowerof8(n))
    document.write("Yes" );
    else
    document.write("No");

</script>
```

**输出:**

```
No
```

这里可以做的一个简单的观察是，如果一个数是 8 的幂，那么它只有一个一位集，并且该位在位置 1、4、7、10、…
因此，我们可以只检查该数中唯一的一个位集是否在这些位置之一，那么它是 8 的幂，否则不是。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if n is power of 8
bool checkPowerof8(int n)
{
    // Variable i will denote the bit
    // that we are currently at
    int i = 0;
    unsigned long long l = 1;
    while (i <= 63) {
        l <<= i;

        // If only set bit in n
        // is at position i
        if (l == n)
            return true;

        // Get to next valid bit position
        i += 3;
        l = 1;
    }
    return false;
}

// Driver code
int main()
{
    int n = 65;
    if (checkPowerof8(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to check if n is power of 8
static boolean checkPowerof8(int n)
{
    // Variable i will denote the bit
    // that we are currently at
    int i = 0;
    long l = 1;
    while (i <= 63)
    {
        l <<= i;

        // If only set bit in n
        // is at position i
        if (l == n)
            return true;

        // Get to next valid bit position
        i += 3;
        l = 1;
    }
    return false;
}

// Driver code
public static void main (String[] args)
{

    int n = 65;
    if (checkPowerof8(n))
        System.out.println ("Yes");
    else
        System.out.println( "No");
}
}

// This code is contributed by Tushil.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check if n is power of 8
def checkPowerof8(n):

    # Variable i will denote the bit
    # that we are currently at
    i = 0
    l = 1

    while (i <= 63):
        l <<= i

        # If only set bit in n
        # is at position i
        if (l == n):
            return True

        # Get to next valid bit position
        i += 3
        l = 1

    return False

# Driver code
if __name__ == '__main__':

    n = 65
    if (checkPowerof8(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by math_lover
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to check if n is power of 8
static bool checkPowerof8(int n)
{
    // Variable i will denote the bit
    // that we are currently at
    int i = 0;
    long l = 1;
    while (i <= 63)
    {
        l <<= i;

        // If only set bit in n
        // is at position i
        if (l == n)
            return true;

        // Get to next valid bit position
        i += 3;
        l = 1;
    }
    return false;
}

// Driver code
static public void Main ()
{
    int n = 65;
    if (checkPowerof8(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine( "No");
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Function to check if n is power of 8
function checkPowerof8( n)
{
    // Variable i will denote the bit
    // that we are currently at
    var i = 0;
    var l= 1;
    while (i <= 63) {
        l<<=i;

        // If only set bit in n
        // is at position i
        if (l == n)
            return 1;

        // Get to next valid bit position
        i += 3;
        l = 1;
    }
    return 0;
}

var n = 65;
    if (checkPowerof8(n))
        document.write( "Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
No
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。