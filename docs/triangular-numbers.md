# 三角数字

> 原文:[https://www.geeksforgeeks.org/triangular-numbers/](https://www.geeksforgeeks.org/triangular-numbers/)

如果我们能以点的三角形网格的形式来表示一个数，使得这些点形成一个等边三角形，并且每行包含与行号一样多的点，即第一行有一个点，第二行有两个点，第三行有三个点，以此类推，那么这个数被称为三角形数。开始的三角数是 1，3 (1+2)，6 (1+2+3)，10 (1+2+3+4)。

![triangular](img/2066515b53bcf816c6b7102565a7a68e.png)

**如何检查一个数字是否为三角形？**
这个想法是基于第 n 个三角数可以写成 n 个自然数的和，也就是 n*(n+1)/2。原因很简单，三角形网格的基线有 n 个点，基线以上的线有(n-1)个点等等。

**方法 1(简单)**
我们从 1 开始，检查数字是否等于 1。如果不是，我们加 2 使其为 3，并用数字重新检查。我们重复这个过程，直到总和小于或等于要检查是否为三角形的数字。
下面是检查一个数是否是三角数的实现。

## C++

```
// C++ program to check if a number is a triangular number
// using simple approach.
#include <iostream>
using namespace std;

// Returns true if 'num' is triangular, else false
bool isTriangular(int num)
{
    // Base case
    if (num < 0)
        return false;

    // A Triangular number must be sum of first n
    // natural numbers
    int sum = 0;
    for (int n=1; sum<=num; n++)
    {
        sum = sum + n;
        if (sum==num)
            return true;
    }

    return false;
}

// Driver code
int main()
{
    int n = 55;
    if (isTriangular(n))
        cout << "The number is a triangular number";
    else
        cout << "The number is NOT a triangular number";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// number is a triangular number
// using simple approach
class GFG
{

    // Returns true if 'num' is
    // triangular, else false
    static boolean isTriangular(int num)
    {
        // Base case
        if (num < 0)
            return false;

        // A Triangular number must be
        // sum of first n natural numbers
        int sum = 0;

        for (int n = 1; sum <= num; n++)
        {
            sum = sum + n;
            if (sum == num)
                return true;
        }

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 55;
        if (isTriangular(n))
            System.out.print("The number "
                + "is a triangular number");
        else
            System.out.print("The number"
             + " is NOT a triangular number");
    }
}

// This code is contributed
// by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check if a number is a
# triangular number using simple approach.

# Returns True if 'num' is triangular, else False
def isTriangular(num):

    # Base case
    if (num < 0):
        return False

    # A Triangular number must be
    # sum of first n natural numbers
    sum, n = 0, 1

    while(sum <= num):

        sum = sum + n
        if (sum == num):
            return True
        n += 1

    return False

# Driver code
n = 55
if (isTriangular(n)):
    print("The number is a triangular number")
else:
    print("The number is NOT a triangular number")

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to check if a number is a
// triangular number using simple approach
using System;

class GFG {

    // Returns true if 'num' is
    // triangular, else false
    static bool isTriangular(int num)
    {
        // Base case
        if (num < 0)
            return false;

        // A Triangular number must be
        // sum of first n natural numbers
        int sum = 0;

        for (int n = 1; sum <= num; n++)
        {
            sum = sum + n;
            if (sum == num)
                return true;
        }

        return false;
    }

    // Driver code
    public static void Main ()
    {
        int n = 55;

        if (isTriangular(n))
            Console.WriteLine("The number "
                + "is a triangular number");
        else
            Console.WriteLine("The number"
            + " is NOT a triangular number");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number is a
// triangular number using simple approach.

// Returns true if 'num' is triangular,
// else false
function isTriangular( $num)
{

    // Base case
    if ($num < 0)
        return false;

    // A Triangular number must be
    // sum of first n natural numbers
    $sum = 0;
    for ($n = 1; $sum <= $num; $n++)
    {
        $sum = $sum + $n;
        if ($sum == $num)
            return true;
    }

    return false;
}

// Driver code
$n = 55;
if (isTriangular($n))
    echo "The number is a triangular number";
else
    echo "The number is NOT a triangular number";

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
// javascript program to check if a number is a triangular number
// using simple approach.

// Returns true if 'num' is triangular, else false
function isTriangular(num)
{

    // Base case
    if (num < 0)
        return false;

    // A Triangular number must be sum of first n
    // natural numbers
    let sum = 0;
    for (let n = 1; sum <= num; n++)
    {
        sum = sum + n;
        if (sum == num)
            return true;
    }

    return false;
}

// Driver code
let n = 55;
    if (isTriangular(n))
       document.write( "The number is a triangular number");
    else
       document.write( "The number is NOT a triangular number");

// This code is contributed by aashish1995

</script>
```

**输出:**

```
 The number is a triangular number 
```

**方法 2(使用二次方程根公式)**
我们通过将数与第一个‘n’个自然数的和的公式相等来形成二次方程，如果我们得到至少一个‘n’的值，那就是自然数，我们说这个数是一个三角数。

```
Let the input number be 'num'. We consider,

n*(n+1) = num

as,

 n2 + n + (-2 * num) = 0 
```

以下是上述想法的实现。

## C++

```
// C++ program to check if a number is a triangular number
// using quadratic equation.
#include <bits/stdc++.h>
using namespace std;

// Returns true if num is triangular
bool isTriangular(int num)
{
    if (num < 0)
        return false;

    // Considering the equation n*(n+1)/2 = num
    // The equation is  : a(n^2) + bn + c = 0";
    int c = (-2 * num);
    int b = 1, a = 1;
    int d = (b * b) - (4 * a * c);

    if (d < 0)
        return false;

    // Find roots of equation
    float root1 = ( -b + sqrt(d)) / (2 * a);
    float root2 = ( -b - sqrt(d)) / (2 * a);

    // checking if root1 is natural
    if (root1 > 0 && floor(root1) == root1)
        return true;

    // checking if root2 is natural
    if (root2 > 0 && floor(root2) == root2)
        return true;

    return false;
}

// Driver code
int main()
{
    int num = 55;
    if (isTriangular(num))
        cout << "The number is a triangular number";
    else
        cout << "The number is NOT a triangular number";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is a
// triangular number using quadratic equation.
import java.io.*;

class GFG {

    // Returns true if num is triangular
    static boolean isTriangular(int num)
    {
        if (num < 0)
            return false;

        // Considering the equation
        // n*(n+1)/2 = num
        // The equation is :
        // a(n^2) + bn + c = 0";
        int c = (-2 * num);
        int b = 1, a = 1;
        int d = (b * b) - (4 * a * c);

        if (d < 0)
            return false;

        // Find roots of equation
        float root1 = ( -b +
           (float)Math.sqrt(d)) / (2 * a);

        float root2 = ( -b -
           (float)Math.sqrt(d)) / (2 * a);

        // checking if root1 is natural
        if (root1 > 0 && Math.floor(root1)
                                  == root1)
            return true;

        // checking if root2 is natural
        if (root2 > 0 && Math.floor(root2)
                                  == root2)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args) {
        int num = 55;
        if (isTriangular(num))
            System.out.println("The number is"
                    + " a triangular number");
        else
            System.out.println ("The number "
              + "is NOT a triangular number");
    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to check if a number is a
# triangular number using quadratic equation.
import math

# Returns True if num is triangular
def isTriangular(num):

    if (num < 0):
        return False

    # Considering the equation n*(n+1)/2 = num
    # The equation is : a(n^2) + bn + c = 0
    c = (-2 * num)
    b, a = 1, 1
    d = (b * b) - (4 * a * c)

    if (d < 0):
        return False

    # Find roots of equation
    root1 = ( -b + math.sqrt(d)) / (2 * a)
    root2 = ( -b - math.sqrt(d)) / (2 * a)

    # checking if root1 is natural
    if (root1 > 0 and math.floor(root1) == root1):
        return True

    # checking if root2 is natural
    if (root2 > 0 and math.floor(root2) == root2):
        return True

    return False

# Driver code
n = 55
if (isTriangular(n)):
    print("The number is a triangular number")
else:
    print("The number is NOT a triangular number")

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to check if a number is a triangular
// number using quadratic equation.
using System;

class GFG {

    // Returns true if num is triangular
    static bool isTriangular(int num)
    {
        if (num < 0)
            return false;

        // Considering the equation n*(n+1)/2 = num
        // The equation is : a(n^2) + bn + c = 0";
        int c = (-2 * num);
        int b = 1, a = 1;
        int d = (b * b) - (4 * a * c);

        if (d < 0)
            return false;

        // Find roots of equation
        float root1 = ( -b + (float)Math.Sqrt(d))
                                        / (2 * a);

        float root2 = ( -b - (float)Math.Sqrt(d)) 
                                        / (2 * a);

        // checking if root1 is natural
        if (root1 > 0 && Math.Floor(root1) == root1)
            return true;

        // checking if root2 is natural
        if (root2 > 0 && Math.Floor(root2) == root2)
            return true;

        return false;
    }

    // Driver code
    public static void Main () {

        int num = 55;
        if (isTriangular(num))
            Console.WriteLine("The number is a "
                            + "triangular number");
        else
            Console.WriteLine ("The number is NOT "
                          + "a triangular number");
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number is a
// triangular number using quadratic equation.

// Returns true if num is triangular
function isTriangular($num)
{
    if ($num < 0)
        return false;

    // Considering the equation
    // n*(n+1)/2 = num
    // The equation is :
    // a(n^2) + bn + c = 0";
    $c = (-2 * $num);
    $b = 1; $a = 1;
    $d = ($b * $b) - (4 * $a * $c);

    if ($d < 0)
        return false;

    // Find roots of equation
    $root1 = (-$b + (float)sqrt($d)) / (2 * $a);

    $root2 = (-$b - (float)sqrt($d)) / (2 * $a);

    // checking if root1 is natural
    if ($root1 > 0 && floor($root1) == $root1)
        return true;

    // checking if root2 is natural
    if ($root2 > 0 && floor($root2) == $root2)
        return true;

    return false;
}

// Driver code
$num = 55;
if (isTriangular($num))
    echo("The number is" .
         " a triangular number");
else
    echo ("The number " .
          "is NOT a triangular number");

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>
// javascript program to check if a number is a
// triangular number using quadratic equation.

    // Returns true if num is triangular
    function isTriangular(num)
    {
        if (num < 0)
            return false;

        // Considering the equation
        // n*(n+1)/2 = num
        // The equation is :
        // a(n^2) + bn + c = 0";
        var c = (-2 * num);
        var b = 1, a = 1;
        var d = (b * b) - (4 * a * c);

        if (d < 0)
            return false;

        // Find roots of equation
        var root1 = (-b +  Math.sqrt(d)) / (2 * a);

        var root2 = (-b -  Math.sqrt(d)) / (2 * a);

        // checking if root1 is natural
        if (root1 > 0 && Math.floor(root1) == root1)
            return true;

        // checking if root2 is natural
        if (root2 > 0 && Math.floor(root2) == root2)
            return true;

        return false;
    }

    // Driver code

    var num = 55;
    if (isTriangular(num))
        document.write("The number is" + " a triangular number");
    else
        document.write("The number " + "is NOT a triangular number");

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
 The number is a triangular number 
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息