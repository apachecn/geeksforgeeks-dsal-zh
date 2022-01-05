# 居中非正交数程序

> 原文:[https://www . geesforgeks . org/program-for-centered-non-gonal-number/](https://www.geeksforgeeks.org/program-for-centered-nonagonal-number/)

居中的非正交数是一个居中的图形数，它代表一个在中心有一个点的非多边形，以及在连续的非正交层中围绕中心点的所有其他点。
n 的中心非正交数由
中心非正交数=(3 * n–2)*(3 * n–1)/2 给出；
[https://en.wikipedia.org/wiki/Centered_nonagonal_number](https://en.wikipedia.org/wiki/Centered_nonagonal_number)
**例:**

```
Input : n = 10
Output : 406

Input : n = 8
Output : 253
```

## C++

```
// CPP Program to find
// nth centered nonagonal number.
#include <bits/stdc++.h>
using namespace std;

// Function to find nth
// centered nonagonal number.
int centeredNonagonal(int n)
{
    // Formula to find nth centered
    // nonagonal number.
    return (3 * n - 2) * (3 * n - 1) / 2;
}

// Driver function.
int main()
{
    int n = 10;
    cout << centeredNonagonal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// nth centered nonagonal number.
import java.io.*;

class GFG {

    // Function to find nth
    // centered nonagonal number.
    static int centeredNonagonal(int n)
    {
        // Formula to find nth centered
        // nonagonal number.
        return (3 * n - 2) * (3 * n - 1) / 2;
    }

    // Driver function.
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(centeredNonagonal(n));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 Program to find
# nth centered nonagonal number.

# Function to find nth
# centered nonagonal number
def centeredNonagonal(n) :

    # Formula to find nth centered
    # nonagonal number.
    return (3 * n - 2) * (3 * n - 1) // 2

# Driver function.
n = 10
print(centeredNonagonal(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# Program to find nth
// centered nonagonal number.
using System;

class GFG {

    // Function to find nth
    // centered nonagonal number.
    static int centeredNonagonal(int n)
    {
        // Formula to find nth centered
        // nonagonal number.
        return (3 * n - 2) * (3 * n - 1) / 2;
    }

    // Driver function.
    public static void Main()
    {
        int n = 10;
        Console.Write(centeredNonagonal(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find nth
// centered nonagonal number.

// Function to find nth
// centered nonagonal number.
function centeredNonagonal( $n)
{

    // Formula to find nth centered
    // nonagonal number.
    return (3 * $n - 2) *
           (3 * $n - 1) / 2;
}

    // Driver Code
    $n = 10;
    echo centeredNonagonal($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript Program to find
// nth centered nonagonal number.

// Function to find nth
// centered nonagonal number.
function centeredNonagonal(n)
{
    // Formula to find nth centered
    // nonagonal number.
    return parseInt((3 * n - 2) * (3 * n - 1) / 2);
}

// Driver function.
let n = 10;
document.write(centeredNonagonal(n));

// This code is contributed by souravmahato348.
</script>
```

输出:

```
406
```

**给定一个数 n，求居中的九次数列直到 n.**
我们也可以求居中的九次数列。中心非正交数列包含中心非正交数列上的点。
居中非正交数:1、10、28、55、91、136、190、253、325、406、496、595、703、820、946。。。

## C++

```
// CPP Program find first
// n centered nonagonal number.
#include <bits/stdc++.h>
using namespace std;

// Function to find centered
// nonagonal number series.
int centeredNonagonal(int n)
{
    for (int i = 1; i <= n; i++) {
        cout << (3 * i - 2) * (3 * i - 1) / 2;
        cout << " ";
    }
}

// Driver function.
int main()
{
    int n = 10;
    centeredNonagonal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program find first
// n centered nonagonal number.
import java.io.*;

class GFG {

    // Function to find centered
    // nonagonal number series.
    static void centeredNonagonal(int n)
    {
        for (int i = 1; i <= n; i++)
        {
            System.out.print((3 * i - 2) *
                             (3 * i - 1) / 2);
            System.out.print(" ");
        }
    }

    // Driver function.
    public static void main(String args[])
    {
        int n = 10;
        centeredNonagonal(n);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 Program find first
# n centered nonagonal number

# Function to find centered
# nonagonal number series
def centeredNonagonal(n) :

    for i in range(1, n + 1) :
        print( (3 * i - 2) * (3 * i - 1) // 2, end=" ")

# Driver function
n = 10
centeredNonagonal(n)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# Program find first
// n centered nonagonal number.
using System;

class GFG {

    // Function to find centered
    // nonagonal number series.
    static void centeredNonagonal(int n)
    {
        for (int i = 1; i <= n; i++)
        {
            Console.Write((3 * i - 2) *
                            (3 * i - 1) / 2);

            Console.Write(" ");
        }
    }

    // Driver function.
    public static void Main()
    {
        int n = 10;
        centeredNonagonal(n);
    }
}

// This code is contributed by
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program find first
// n centered nonagonal number.

// Function to find centered
// nonagonal number series.
function centeredNonagonal( $n)
{
    for ( $i = 1; $i <= $n; $i++)
    {
        echo (3 * $i - 2) *
             (3 * $i - 1) / 2;
        echo " ";
    }
}

// Driver Code
$n = 10;
centeredNonagonal($n);

// This code is contributed anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript Program find first
// n centered nonagonal number.

// Function to find centered
    // nonagonal number series.
    function centeredNonagonal(n)
    {
        for (let i = 1; i <= n; i++)
        {
            document.write((3 * i - 2) *
                             (3 * i - 1) / 2);
            document.write(" ");
        }
    }

// Driver code
    let n = 10;
    centeredNonagonal(n);

// This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
1  10  28  55  91  136  190  253  325  406
```