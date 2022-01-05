# 求模 p |集合 1 下的平方根(当 p 是 4*i + 3 的形式时)

> 原文:[https://www . geeksforgeeks . org/find-求模下平方根-p-set-1-当-p 是-4i-3 的形式时/](https://www.geeksforgeeks.org/find-square-root-under-modulo-p-set-1-when-p-is-in-form-of-4i-3/)

给定一个数“n”和一个素数“p”，求模 p 下 n 的平方根，如果它存在的话。可以给出 p 是 4*i + 3 (OR p % 4 = 3)的形式，其中 I 是整数。这类素数的例子有 7、11、19、23、31、…等
**例子:**

```
Input:  n = 2, p = 7
Output: 3 or 4
3 and 4 both are square roots of 2 under modulo
7 because (3*3) % 7 = 2 and (4*4) % 7 = 2

Input:  n = 2, p = 5
Output: Square root doesn't exist
```

**天真解:**尝试从 2 到 p-1 的所有数字。对于每个数字 x，检查 x 是否是模 p 下 n 的平方根

## C++

```
// A Simple C++ program to find square root under modulo p
// when p is 7, 11, 19, 23, 31, ... etc,
#include <iostream>
using namespace std;

// Returns true if square root of n under modulo p exists
void squareRoot(int n, int p)
{
    n = n % p;

    // One by one check all numbers from 2 to p-1
    for (int x = 2; x < p; x++) {
        if ((x * x) % p == n) {
            cout << "Square root is " << x;
            return;
        }
    }
    cout << "Square root doesn't exist";
}

// Driver program to test
int main()
{
    int p = 7;
    int n = 2;
    squareRoot(n, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program to find square
// root under modulo p when p is 7,
// 11, 19, 23, 31, ... etc,
import java .io.*;

class GFG {

    // Returns true if square root of n
    // under modulo p exists
    static void squareRoot(int n, int p)
    {
        n = n % p;

        // One by one check all numbers
        // from 2 to p-1
        for (int x = 2; x < p; x++) {
            if ((x * x) % p == n) {
                System.out.println("Square "
                    + "root is " + x);
                return;
            }
        }
        System.out.println("Square root "
                + "doesn't exist");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int p = 7;
        int n = 2;
        squareRoot(n, p);
    }
}

// This code is contributed by Anuj_67
```

## 蟒蛇 3

```
# A Simple Python program to find square
# root under modulo p when p is 7, 11,
# 19, 23, 31, ... etc,

# Returns true if square root of n under
# modulo p exists
def squareRoot(n, p):

    n = n % p

    # One by one check all numbers from
    # 2 to p-1
    for x in range (2, p):
        if ((x * x) % p == n) :
            print( "Square root is ", x)
            return

    print( "Square root doesn't exist")

# Driver program to test
p = 7
n = 2
squareRoot(n, p)

# This code is Contributed by Anuj_67
```

## C#

```
// A Simple C# program to find square
// root under modulo p when p is 7,
// 11, 19, 23, 31, ... etc,
using System;

class GFG {

    // Returns true if square root of n
    // under modulo p exists
    static void squareRoot(int n, int p)
    {
        n = n % p;

        // One by one check all numbers
        // from 2 to p-1
        for (int x = 2; x < p; x++) {
            if ((x * x) % p == n) {
                Console.Write("Square "
                     + "root is " + x);
                return;
            }
        }
        Console.Write("Square root "
                   + "doesn't exist");
    }

    // Driver Code
    static void Main()
    {
        int p = 7;
        int n = 2;
        squareRoot(n, p);
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple PHP program to find
// square root under modulo p
// when p is 7, 11, 19, 23, 31,
// ... etc,

// Returns true if square
// root of n under modulo
// p exists
function squareRoot($n, $p)
{
    $n = $n % $p;

    // One by one check all
    // numbers from 2 to p-1
    for ($x = 2; $x < $p; $x++)
    {
        if (($x * $x) % $p == $n)
        {
            echo("Square root is " . $x);
            return;
        }
    }
    echo("Square root doesn't exist");
}

// Driver Code
$p = 7;
$n = 2;
squareRoot($n, $p);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// A Simple Javascript program to find square
// root under modulo p when p is 7,
// 11, 19, 23, 31, ... etc,

    // Returns true if square root of n
    // under modulo p exists
    function squareRoot(n,p)
    {
         n = n % p;

        // One by one check all numbers
        // from 2 to p-1
        for (let x = 2; x < p; x++) {
            if ((x * x) % p == n) {
                document.write("Square "
                    + "root is " + x);
                return;
            }
        }
        document.write("Square root "
                + "doesn't exist");
    }

    // Driver Code
    let p = 7;
    let n = 2;
    squareRoot(n, p);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
Square root is 3
```

这个解的时间复杂度是 O(p)
**直接法:**如果 p 是 4*i + 3 的形式，那么就存在求平方根的快速方法。

```
If n is in the form 4*i + 3 with i >= 1 (OR p % 4 = 3)
And 
If Square root of n exists, then it must be
        ±n<sup>(p + 1)/4</sup>
```

以下是上述思路的实现:

## C++

```
// An efficient C++ program to find square root under
// modulo p when p is 7, 11, 19, 23, 31, ... etc.
#include <iostream>
using namespace std;

// Utility function to do modular exponentiation.
// It returns (x^y) % p.
int power(int x, int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns true if square root of n under modulo p exists
// Assumption: p is of the form 3*i + 4 where i >= 1
void squareRoot(int n, int p)
{
    if (p % 4 != 3) {
        cout << "Invalid Input";
        return;
    }

    // Try "+(n^((p + 1)/4))"
    n = n % p;
    int x = power(n, (p + 1) / 4, p);
    if ((x * x) % p == n) {
        cout << "Square root is " << x;
        return;
    }

    // Try "-(n ^ ((p + 1)/4))"
    x = p - x;
    if ((x * x) % p == n) {
        cout << "Square root is " << x;
        return;
    }

    // If none of the above two work, then
    // square root doesn't exist
    cout << "Square root doesn't exist ";
}

// Driver program to test
int main()
{
    int p = 7;
    int n = 2;
    squareRoot(n, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to find square root under
// modulo p when p is 7, 11, 19, 23, 31, ... etc.
public class GFG {

// Utility function to do modular exponentiation.
// It returns (x^y) % p.
static int power(int x, int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y %2== 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns true if square root of n under modulo p exists
// Assumption: p is of the form 3*i + 4 where i >= 1
static void squareRoot(int n, int p)
{
    if (p % 4 != 3) {
        System.out.print("Invalid Input");
        return;
    }

    // Try "+(n^((p + 1)/4))"
    n = n % p;
    int x = power(n, (p + 1) / 4, p);
    if ((x * x) % p == n) {
        System.out.print("Square root is " + x);
        return;
    }

    // Try "-(n ^ ((p + 1)/4))"
    x = p - x;
    if ((x * x) % p == n) {
        System.out.print("Square root is " + x);
        return;
    }

    // If none of the above two work, then
    // square root doesn't exist
    System.out.print("Square root doesn't exist ");
}

// Driver program to test
   static public void main(String[] args) {
       int p = 7;
    int n = 2;
    squareRoot(n, p);
    }
}
```

## 蟒蛇 3

```
# An efficient python3 program to find square root
# under modulo p when p is 7, 11, 19, 23, 31, ... etc.

# Utility function to do modular exponentiation.
# It returns (x^y) % p.
def power(x, y, p) :

    res = 1 # Initialize result
    x = x % p # Update x if it is more
              # than or equal to p

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Returns true if square root of n under
# modulo p exists. Assumption: p is of the
# form 3*i + 4 where i >= 1
def squareRoot(n, p):

    if (p % 4 != 3) :
        print( "Invalid Input" )
        return

    # Try "+(n^((p + 1)/4))"
    n = n % p
    x = power(n, (p + 1) // 4, p)
    if ((x * x) % p == n):
        print( "Square root is ", x)
        return

    # Try "-(n ^ ((p + 1)/4))"
    x = p - x
    if ((x * x) % p == n):
        print( "Square root is ", x )
        return

    # If none of the above two work, then
    # square root doesn't exist
    print( "Square root doesn't exist " )

# Driver Code
p = 7
n = 2
squareRoot(n, p)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// An efficient C# program to find square root under
// modulo p when p is 7, 11, 19, 23, 31, ... etc.

using System;
public class GFG {

// Utility function to do modular exponentiation.
// It returns (x^y) % p.
static int power(int x, int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y %2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns true if square root of n under modulo p exists
// Assumption: p is of the form 3*i + 4 where i >= 1
static void squareRoot(int n, int p)
{
    if (p % 4 != 3) {
        Console.Write("Invalid Input");
        return;
    }

    // Try "+(n^((p + 1)/4))"
    n = n % p;
    int x = power(n, (p + 1) / 4, p);
    if ((x * x) % p == n) {
        Console.Write("Square root is " + x);
        return;
    }

    // Try "-(n ^ ((p + 1)/4))"
    x = p - x;
    if ((x * x) % p == n) {
        Console.Write("Square root is " + x);
        return;
    }

    // If none of the above two work, then
    // square root doesn't exist
    Console.Write("Square root doesn't exist ");
}

// Driver program to test
   static public void Main() {
       int p = 7;
    int n = 2;
    squareRoot(n, p);
    }
}
// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program
// to find square root under
// modulo p when p is 7, 11,
// 19, 23, 31, ... etc.

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p.
function power($x, $y, $p)
{

    // Initialize result
    $res = 1;    

    // Update x if it
    // is more than or
    // equal to p
    $x = $x % $p;

    while ($y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        // y = y/2
        $y = $y >> 1;
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Returns true if square root
// of n under modulo p exists
// Assumption: p is of the
// form 3*i + 4 where i >= 1
function squareRoot($n, $p)
{
    if ($p % 4 != 3)
    {
        echo "Invalid Input";
        return;
    }

    // Try "+(n^((p + 1)/4))"
    $n = $n % $p;
    $x = power($n, ($p + 1) / 4, $p);
    if (($x * $x) % $p == $n)
    {
        echo "Square root is ", $x;
        return;
    }

    // Try "-(n ^ ((p + 1)/4))"
    $x = $p - $x;
    if (($x * $x) % $p == $n)
    {
        echo "Square root is ", $x;
        return;
    }

    // If none of the above
    // two work, then square
    // root doesn't exist
    echo "Square root doesn't exist ";
}

    // Driver Code
    $p = 7;
    $n = 2;
    squareRoot($n, $p);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// An efficient Javascript program to find square root under
// modulo p when p is 7, 11, 19, 23, 31, ... etc.

    // Utility function to do modular exponentiation.
    // It returns (x^y) % p.
    function power(x,y,p)
    {
        let res = 1; // Initialize result
        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0)
        {

            // If y is odd, multiply x with result
            if (y %2== 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Returns true if square root of n under modulo p exists
    // Assumption: p is of the form 3*i + 4 where i >= 1
    function squareRoot(n, p)
    {
        if (p % 4 != 3)
        {
            document.write("Invalid Input");
            return;
        }

        // Try "+(n^((p + 1)/4))"
        n = n % p;
        let x = power(n, Math.floor((p + 1) / 4), p);
        if ((x * x) % p == n) {
            document.write("Square root is " + x);
            return;
        }

        // Try "-(n ^ ((p + 1)/4))"
        x = p - x;
        if ((x * x) % p == n) {
            document.write("Square root is " + x);
            return;
        }

        // If none of the above two work, then
        // square root doesn't exist
        document.write("Square root doesn't exist ");
    }

    // Driver program to test
    let p = 7;
    let n = 2;
    squareRoot(n, p);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Square root is 4
```

此解决方案的时间复杂度为 O(Log p)
**这是如何工作的？**
我们在之前的帖子里已经讨论过[欧拉准则](https://www.geeksforgeeks.org/eulers-criterion-check-if-square-root-under-modulo-p-exists/)。

```
As per Euler's criterion, if square root exists, then 
following condition is true
 n(p-1)/2 % p = 1

Multiplying both sides with n, we get
 n(p+1)/2 % p = n % p  ------ (1)

Let x be the modulo square root. We can write,
  (x * x) ≡ n mod p
  (x * x) ≡ n(p+1)/2  [Using (1) given above]
  (x * x) ≡ n(2i + 2) [Replacing n = 4*i + 3]
        x ≡ ±n(i + 1)  [Taking Square root of both sides]
        x ≡ ±n(p + 1)/4 [Putting 4*i + 3 = p or i = (p-3)/4]
```

当 p 不是上述形式时，我们将很快讨论方法。
本文由**希瓦姆·古普塔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息