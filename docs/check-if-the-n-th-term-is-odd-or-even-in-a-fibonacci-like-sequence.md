# 检查第 n 项在斐波那契数列中是奇数还是偶数

> 原文:[https://www . geeksforgeeks . org/check-n-term-in-n-Fibonacci-like-sequence 是奇数还是偶数/](https://www.geeksforgeeks.org/check-if-the-n-th-term-is-odd-or-even-in-a-fibonacci-like-sequence/)

考虑一个序列 a <sub>0</sub> ，a <sub>1</sub> ，a【】n，其中 a<sub>I</sub>= a<sub>I-1</sub>+a<sub>I-2</sub>。给定 **a <sub>0</sub> ，a <sub>1</sub>** ，以及正整数 **n** 。任务是找出一个 <sub>n</sub> 是奇数还是偶数。
注意，给定的序列类似[斐波那契](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，区别在于前两项可以是任何东西，而不是 0 或 1。
**举例:**

```
Input : a0 = 2, a1 = 4, n =3
Output : Even 
a2 = 6, a3 = 10
And a3 is even.

Input : a0 = 1, a1 = 9, n = 2
Output : Even
```

**方法 1:** 思路是利用数组找到序列，检查第 n 个元素是偶数还是奇数。

## C++

```
// CPP Program to check if the nth is odd or even in a
// sequence where each term is sum of previous two term
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Return if the nth term is even or odd.
bool findNature(int a, int b, int n)
{
    int seq[MAX] = { 0 };

    seq[0] = a;
    seq[1] = b;

    for (int i = 2; i <= n; i++)
        seq[i] = seq[i - 1] + seq[i - 2];

    // Return true if odd
    return (seq[n] & 1);
}

// Driven Program
int main()
{
    int a = 2, b = 4;
    int n = 3;

    (findNature(a, b, n) ? (cout << "Odd"
                                 << " ")
                         : (cout << "Even"
                                 << " "));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if
// the nth is odd or even
// in a sequence where each
// term is sum of previous
// two term

// Return if the nth
// term is even or odd.
class GFG
{
public static int findNature(int a,
                             int b, int n)
{
    int[] seq = new int[100];

    seq[0] = a;
    seq[1] = b;

    for (int i = 2; i <= n; i++)
        seq[i] = seq[i - 1] + seq[i - 2];

    // Return true if odd
    if((seq[n] & 1) != 0)
    return 1;
    else
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int a = 2, b = 4;
    int n = 3;
    if(findNature(a, b, n) == 1)
    System.out.println("Odd ");
    else
    System.out.println("Even ");
}
}

// This code is contributed
// by mits
```

## 蟒蛇 3

```
# Python3 Program to check if
# the nth is odd or even in a
# sequence where each term is
# sum of previous two term
MAX = 100;

# Return if the nth
# term is even or odd.
def findNature(a, b, n):
    seq = [0] * MAX;
    seq[0] = a;
    seq[1] = b;

    for i in range(2, n + 1):
        seq[i] = seq[i - 1] + seq[i - 2];

    # Return true if odd
    return (seq[n] & 1);

# Driver Code
a = 2;
b = 4;
n = 3;

if(findNature(a, b, n)):
    print("Odd");
else:
    print("Even");

# This code is contributed by mits
```

## C#

```
// C# Program to check if the
// nth is odd or even in a
// sequence where each term
// is sum of previous two term
using System;

// Return if the nth term
// is even or odd.
class GFG
{
public static int findNature(int a,
                             int b, int n)
{
    int[] seq = new int[100];

    seq[0] = a;
    seq[1] = b;

    for (int i = 2; i <= n; i++)
        seq[i] = seq[i - 1] +
                 seq[i - 2];

    // Return true if odd
    if((seq[n] & 1)!=0)
    return 1;
    else
    return 0;
}

// Driver Code
public static void Main()
{
    int a = 2, b = 4;
    int n = 3;
    if(findNature(a, b, n) == 1)
    Console.Write("Odd ");
    else
    Console.Write("Even ");
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if the
// nth is odd or even in a
// sequence where each term is
// sum of previous two term
$MAX = 100;

// Return if the nth
// term is even or odd.
function findNature($a, $b, $n)
{
    global $MAX;
    $seq = array_fill(0,$MAX, 0);

    $seq[0] = $a;
    $seq[1] = $b;

    for ($i = 2; $i <= $n; $i++)
        $seq[$i] = $seq[$i - 1] +
                   $seq[$i - 2];

    // Return true if odd
    return ($seq[$n] & 1);
}

// Driver Code
$a = 2;
$b = 4;
$n = 3;

if(findNature($a, $b, $n))
echo "Odd";
else
echo "Even";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to check if the
// nth is odd or even in a
// sequence where each term is sum
// of previous two term
var MAX = 100;

// Return if the nth term is even or odd.
function findNature(a, b, n)
{
    var seq = Array(MAX).fill(0);

    seq[0] = a;
    seq[1] = b;

    for (var i = 2; i <= n; i++)
        seq[i] = seq[i - 1] + seq[i - 2];

    // Return true if odd
    return (seq[n] & 1);
}

// Driven Program
var a = 2, b = 4;
var n = 3;
(findNature(a, b, n) ? (document.write( "Odd"
                             + " "))
                     : (document.write( "Even"
                             + " ")));

</script>
```

**Output:** 

```
Even
```

**方法二(高效):**
观察，第 n 项的性质(奇数或偶数)取决于前几项，前几项的性质取决于它们的前几项，最后取决于初始值即 a <sub>0</sub> 和 a <sub>1</sub> 。
那么，我们有四种可能的情况，一个 <sub>0</sub> 和一个 <sub>1</sub> :
**情况 1:当一个 <sub>0</sub> 和一个 <sub>1</sub> 为偶数时**
在这种情况下，序列中的每个值只会为偶数。
**案例二:当一个 <sub>0</sub> 一个 <sub>1</sub> 为奇数**
这种情况下，观察一个 <sub>2</sub> 为偶数，一个 <sub>3</sub> 为奇数，一个 <sub>4</sub> 为奇数等等。所以，我们可以说一个 <sub>i</sub> 是偶数，如果我是 3 * k–1 的形式，那么就是奇数。
**案例三:当一个 <sub>0</sub> 为偶数，一个 <sub>1</sub> 为奇数**
这种情况下，观察一个 <sub>2</sub> 为奇数，一个 <sub>3</sub> 为偶数，一个 <sub>4</sub> 和一个 <sub>5</sub> 为奇数，一个 <sub>6</sub> 为偶数等等。所以，我们可以说，一个 <sub>i</sub> 就算我是 3 的倍数也是偶数，否则就是奇数
**情况 4:当一个 <sub>0</sub> 是奇数，一个 <sub>1</sub> 是偶数**
这种情况下，观察一个 <sub>2</sub> 和一个 <sub>3</sub> 是奇数，一个 <sub>4</sub> 是偶数，一个【T75 所以，我们可以说，一个 <sub>i</sub> 就是即使我是 3*k + 1 的形式，k > = 0，否则奇数。
以下是本办法的实施:

## C++

```
// CPP Program to check if the nth is odd or even in a
// sequence where each term is sum of previous two term
#include <bits/stdc++.h>
using namespace std;

// Return if the nth term is even or odd.
bool findNature(int a, int b, int n)
{
    if (n == 0)
        return (a & 1);

    if (n == 1)
        return (b & 1);

    // If a is even
    if (!(a & 1)) {

        // If b is even
        if (!(b & 1))
            return false;

        // If b is odd
        else
            return (n % 3 != 0);
    }

    // If a is odd
    else {
        // If b is odd
        if (!(b & 1))
            return ((n - 1) % 3 != 0);

        // If b is eve
        else
            return ((n + 1) % 3 != 0);
    }
}

// Driven Program
int main()
{
    int a = 2, b = 4;
    int n = 3;

    (findNature(a, b, n) ? (cout << "Odd"
                                 << " ")
                         : (cout << "Even"
                                 << " "));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if the nth is odd or even in a
// sequence where each term is sum of previous two term

class GFG{
// Return if the nth term is even or odd.
static boolean findNature(int a, int b, int n)
{
    if (n == 0)
        return (a & 1)==1?true:false;

    if (n == 1)
        return (b & 1)==1?true:false;

    // If a is even
    if ((a & 1)==0) {

        // If b is even
        if ((b & 1)==0)
            return false;

        // If b is odd
        else
            return (n % 3 != 0);
    }

    // If a is odd
    else {
        // If b is odd
        if ((b & 1)==0)
            return ((n - 1) % 3 != 0);

        // If b is eve
        else
            return ((n + 1) % 3 != 0);
    }
}

// Driven Program
public static void main(String[] args)
{
    int a = 2, b = 4;
    int n = 3;

    if(findNature(a, b, n))
    System.out.println("Odd");
    else
    System.out.println("Even");

}
}
// This Code is contributed by mits
```

## 蟒蛇 3

```
# Python3 Program to check if the
# nth is odd or even in a
# sequence where each term is
# sum of previous two term

# Return if the nth
# term is even or odd.
def findNature(a, b, n):
    if (n == 0):
        return (a & 1);

    if (n == 1):
        return (b & 1);

    # If a is even
    if ((a & 1) == 0):

        # If b is even
        if ((b & 1) == 0):
            return False;

        # If b is odd
        else:
            return True if(n % 3 != 0) else False;

    # If a is odd
    else:
        # If b is odd
        if ((b & 1) == 0):
            return True if((n - 1) % 3 != 0) else False;

        # If b is eve
        else:
            return True if((n + 1) % 3 != 0) else False;

# Driver Code
a = 2;
b = 4;
n = 3;

if (findNature(a, b, n) == True):
    print("Odd", end = " ");
else:
    print("Even", end = " ");

# This code is contributed by mits
```

## C#

```
// C# Program to check if the nth is odd or even in a
// sequence where each term is sum of previous two term

class GFG{
// Return if the nth term is even or odd.
static bool findNature(int a, int b, int n)
{
    if (n == 0)
        return (a & 1)==1?true:false;

    if (n == 1)
        return (b & 1)==1?true:false;

    // If a is even
    if ((a & 1)==0) {

        // If b is even
        if ((b & 1)==0)
            return false;

        // If b is odd
        else
            return (n % 3 != 0);
    }

    // If a is odd
    else {
        // If b is odd
        if ((b & 1)==0)
            return ((n - 1) % 3 != 0);

        // If b is eve
        else
            return ((n + 1) % 3 != 0);
    }
}

// Driven Program
static void Main()
{
    int a = 2, b = 4;
    int n = 3;

    if(findNature(a, b, n))
    System.Console.WriteLine("Odd");
    else
    System.Console.WriteLine("Even");

}
}
// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if the
// nth is odd or even in a
// sequence where each term is
// sum of previous two term

// Return if the nth
// term is even or odd.
function findNature($a, $b, $n)
{
    if ($n == 0)
        return ($a & 1);

    if ($n == 1)
        return ($b & 1);

    // If a is even
    if (!($a & 1))
    {

        // If b is even
        if (!($b & 1))
            return false;

        // If b is odd
        else
            return ($n % 3 != 0);
    }

    // If a is odd
    else
    {
        // If b is odd
        if (!($b & 1))
            return (($n - 1) % 3 != 0);

        // If b is eve
        else
            return (($n + 1) % 3 != 0);
    }
}

// Driver Code
$a = 2; $b = 4;
$n = 3;

if (findNature($a, $b, $n) == true)
    echo "Odd"," ";
else
    echo "Even"," ";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Program to check if the nth is odd or even in a
    // sequence where each term is sum of previous two term

    // Return if the nth term is even or odd.
    function findNature(a, b, n)
    {
        if (n == 0)
            return (a & 1)==1?true:false;

        if (n == 1)
            return (b & 1)==1?true:false;

        // If a is even
        if ((a & 1)==0) {

            // If b is even
            if ((b & 1)==0)
                return false;

            // If b is odd
            else
                return (n % 3 != 0);
        }

        // If a is odd
        else {
            // If b is odd
            if ((b & 1)==0)
                return ((n - 1) % 3 != 0);

            // If b is eve
            else
                return ((n + 1) % 3 != 0);
        }
    }

    let a = 2, b = 4;
    let n = 3;

    if(findNature(a, b, n))
        document.write("Odd");
    else
        document.write("Even");

// This code is contributed by suresh07.
</script>
```

**Output :** 

```
Even
```