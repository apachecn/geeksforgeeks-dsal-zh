# Stein 求 GCD 的算法

> 原文:[https://www . geeksforgeeks . org/steins-算法寻找-gcd/](https://www.geeksforgeeks.org/steins-algorithm-for-finding-gcd/)

**Stein 算法**或**二进制 GCD 算法**是计算两个非负整数的最大公约数的算法。Stein 的算法用算术移位、比较和减法代替除法。

**示例:**

```
Input: a = 17, b = 34 
Output : 17

Input: a = 50, b = 49
Output: 1
```

**使用 Stein 算法寻找 GCD 的算法 gcd(a，b)**

1.  如果 a 和 b 都为 0，则 gcd 为零 gcd(0，0) = 0。
2.  gcd(a，0) = a 和 gcd(0，b) = b，因为一切都除以 0。
3.  如果 a 和 b 都是偶数，gcd(a，b) = 2*gcd(a/2，b/2)，因为 2 是公约数。与 2 相乘可以通过按位移位运算符来完成。
4.  如果 a 为偶数，b 为奇数，则 gcd(a，b) = gcd(a/2，b)。同样，如果 a 是奇数，b 是偶数，那么
    gcd(a，b) = gcd(a，b/2)。因为 2 不是公约数。
5.  如果 a 和 b 都是奇数，那么 gcd(a，b) = gcd(|a-b|/2，b)。注意两个奇数的差是偶数
6.  重复步骤 3–5，直到 a = b，或者直到 a = 0。在任一种情况下，GCD 都是幂(2，k) * b，其中幂(2，k)是 2 的幂，k 是在步骤 2 中找到的 2 的公共因子的数量。

**迭代实现**

## C++

```
// Iterative C++ program to
// implement Stein's Algorithm
#include <bits/stdc++.h>
using namespace std;

// Function to implement
// Stein's Algorithm
int gcd(int a, int b)
{
    /* GCD(0, b) == b; GCD(a, 0) == a,
       GCD(0, 0) == 0 */
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    /*Finding K, where K is the
      greatest power of 2
      that divides both a and b. */
    int k;
    for (k = 0; ((a | b) & 1) == 0; ++k)
    {
        a >>= 1;
        b >>= 1;
    }

    /* Dividing a by 2 until a becomes odd */
    while ((a & 1) == 0)
        a >>= 1;

    /* From here on, 'a' is always odd. */
    do
    {
        /* If b is even, remove all factor of 2 in b */
        while ((b & 1) == 0)
            b >>= 1;

        /* Now a and b are both odd.
           Swap if necessary so a <= b,
           then set b = b - a (which is even).*/
        if (a > b)
            swap(a, b); // Swap u and v.

        b = (b - a);
    }while (b != 0);

    /* restore common factors of 2 */
    return a << k;
}

// Driver code
int main()
{
    int a = 34, b = 17;
    printf("Gcd of given numbers is %d\n", gcd(a, b));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to
// implement Stein's Algorithm
import java.io.*;

class GFG {

    // Function to implement Stein's
    // Algorithm
    static int gcd(int a, int b)
    {
        // GCD(0, b) == b; GCD(a, 0) == a,
        // GCD(0, 0) == 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // Finding K, where K is the greatest
        // power of 2 that divides both a and b
        int k;
        for (k = 0; ((a | b) & 1) == 0; ++k)
        {
            a >>= 1;
            b >>= 1;
        }

        // Dividing a by 2 until a becomes odd
        while ((a & 1) == 0)
            a >>= 1;

        // From here on, 'a' is always odd.
        do
        {
            // If b is even, remove
            // all factor of 2 in b
            while ((b & 1) == 0)
                b >>= 1;

            // Now a and b are both odd. Swap
            // if necessary so a <= b, then set
            // b = b - a (which is even)
            if (a > b)
            {
                // Swap u and v.
                int temp = a;
                a = b;
                b = temp;
            }

            b = (b - a);
        } while (b != 0);

        // restore common factors of 2
        return a << k;
    }

    // Driver code
    public static void main(String args[])
    {
        int a = 34, b = 17;

        System.out.println("Gcd of given "
                           + "numbers is " + gcd(a, b));
    }
}

// This code is contributed by Nikita Tiwari
```

## 计算机编程语言

```
# Iterative Python 3 program to
# implement Stein's Algorithm

# Function to implement
# Stein's Algorithm

def gcd(a, b):

    # GCD(0, b) == b; GCD(a, 0) == a,
    # GCD(0, 0) == 0
    if (a == 0):
        return b

    if (b == 0):
        return a

    # Finding K, where K is the
    # greatest power of 2 that
    # divides both a and b.
    k = 0

    while(((a | b) & 1) == 0):
        a = a >> 1
        b = b >> 1
        k = k + 1

    # Dividing a by 2 until a becomes odd
    while ((a & 1) == 0):
        a = a >> 1

    # From here on, 'a' is always odd.
    while(b != 0):

        # If b is even, remove all
        # factor of 2 in b
        while ((b & 1) == 0):
            b = b >> 1

        # Now a and b are both odd. Swap if
        # necessary so a <= b, then set
        # b = b - a (which is even).
        if (a > b):

            # Swap u and v.
            temp = a
            a = b
            b = temp

        b = (b - a)

    # restore common factors of 2
    return (a << k)

# Driver code
a = 34
b = 17

print("Gcd of given numbers is ", gcd(a, b))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Iterative C# program to implement
// Stein's Algorithm
using System;

class GFG {

    // Function to implement Stein's
    // Algorithm
    static int gcd(int a, int b)
    {

        // GCD(0, b) == b; GCD(a, 0) == a,
        // GCD(0, 0) == 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // Finding K, where K is the greatest
        // power of 2 that divides both a and b
        int k;
        for (k = 0; ((a | b) & 1) == 0; ++k)
        {
            a >>= 1;
            b >>= 1;
        }

        // Dividing a by 2 until a becomes odd
        while ((a & 1) == 0)
            a >>= 1;

        // From here on, 'a' is always odd
        do
        {
            // If b is even, remove
            // all factor of 2 in b
            while ((b & 1) == 0)
                b >>= 1;

            /* Now a and b are both odd. Swap
            if necessary so a <= b, then set
            b = b - a (which is even).*/
            if (a > b) {

                // Swap u and v.
                int temp = a;
                a = b;
                b = temp;
            }

            b = (b - a);
        } while (b != 0);

        /* restore common factors of 2 */
        return a << k;
    }

    // Driver code
    public static void Main()
    {
        int a = 34, b = 17;

        Console.Write("Gcd of given "
                      + "numbers is " + gcd(a, b));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative php program to
// implement Stein's Algorithm

// Function to implement
// Stein's Algorithm
function gcd($a, $b)
{
    // GCD(0, b) == b; GCD(a, 0) == a,
    // GCD(0, 0) == 0
    if ($a == 0)
        return $b;
    if ($b == 0)
        return $a;

    // Finding K, where K is the greatest
    // power of 2 that divides both a and b.
    $k;
    for ($k = 0; (($a | $b) & 1) == 0; ++$k)
    {
        $a >>= 1;
        $b >>= 1;
    }

    // Dividing a by 2 until a becomes odd
    while (($a & 1) == 0)
        $a >>= 1;

    // From here on, 'a' is always odd.
    do
    {

        // If b is even, remove
        // all factor of 2 in b
        while (($b & 1) == 0)
            $b >>= 1;

        // Now a and b are both odd. Swap
        // if necessary so a <= b, then set
        // b = b - a (which is even)
        if ($a > $b)
            swap($a, $b); // Swap u and v.

        $b = ($b - $a);
    } while ($b != 0);

    // restore common factors of 2
    return $a << $k;
}

// Driver code
$a = 34; $b = 17;
echo "Gcd of given numbers is " .
                     gcd($a, $b);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Iterative JavaScript program to
// implement Stein's Algorithm

// Function to implement
// Stein's Algorithm
function gcd( a,  b)
{
    /* GCD(0, b) == b; GCD(a, 0) == a,
       GCD(0, 0) == 0 */
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    /*Finding K, where K is the
      greatest power of 2
      that divides both a and b. */
    let k;
    for (k = 0; ((a | b) & 1) == 0; ++k)
    {
        a >>= 1;
        b >>= 1;
    }

    /* Dividing a by 2 until a becomes odd */
    while ((a & 1) == 0)
        a >>= 1;

    /* From here on, 'a' is always odd. */
    do
    {
        /* If b is even, remove all factor of 2 in b */
        while ((b & 1) == 0)
            b >>= 1;

        /* Now a and b are both odd.
           Swap if necessary so a <= b,
           then set b = b - a (which is even).*/
        if (a > b){
        let t = a;
        a = b;
        b = t;
        }

        b = (b - a);
    }while (b != 0);

    /* restore common factors of 2 */
    return a << k;
}

// Driver code

    let a = 34, b = 17;
    document.write("Gcd of given numbers is "+ gcd(a, b));

// This code contributed by gauravrajput1

</script>
```

**Output**

```
Gcd of given numbers is 17
```

**递归实现**

## C++

```
// Recursive C++ program to
// implement Stein's Algorithm
#include <bits/stdc++.h>
using namespace std;

// Function to implement
// Stein's Algorithm
int gcd(int a, int b)
{
    if (a == b)
        return a;

    // GCD(0, b) == b; GCD(a, 0) == a,
    // GCD(0, 0) == 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // look for factors of 2
    if (~a & 1) // a is even
    {
        if (b & 1) // b is odd
            return gcd(a >> 1, b);
        else // both a and b are even
            return gcd(a >> 1, b >> 1) << 1;
    }

    if (~b & 1) // a is odd, b is even
        return gcd(a, b >> 1);

    // reduce larger number
    if (a > b)
        return gcd((a - b) >> 1, b);

    return gcd((b - a) >> 1, a);
}

// Driver code
int main()
{
    int a = 34, b = 17;
    printf("Gcd of given numbers is %d\n", gcd(a, b));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to
// implement Stein's Algorithm
import java.io.*;

class GFG {

    // Function to implement
    // Stein's Algorithm
    static int gcd(int a, int b)
    {
        if (a == b)
            return a;

        // GCD(0, b) == b; GCD(a, 0) == a,
        // GCD(0, 0) == 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // look for factors of 2
        if ((~a & 1) == 1) // a is even
        {
            if ((b & 1) == 1) // b is odd
                return gcd(a >> 1, b);

            else // both a and b are even
                return gcd(a >> 1, b >> 1) << 1;
        }

        // a is odd, b is even
        if ((~b & 1) == 1)
            return gcd(a, b >> 1);

        // reduce larger number
        if (a > b)
            return gcd((a - b) >> 1, b);

        return gcd((b - a) >> 1, a);
    }

    // Driver code
    public static void main(String args[])
    {
        int a = 34, b = 17;
        System.out.println("Gcd of given"
                           + "numbers is " + gcd(a, b));
    }
}

// This code is contributed by Nikita Tiwari
```

## 计算机编程语言

```
# Recursive Python 3 program to
# implement Stein's Algorithm

# Function to implement
# Stein's Algorithm

def gcd(a, b):

    if (a == b):
        return a

    # GCD(0, b) == b; GCD(a, 0) == a,
    # GCD(0, 0) == 0
    if (a == 0):
        return b

    if (b == 0):
        return a

    # look for factors of 2
    # a is even
    if ((~a & 1) == 1):

        # b is odd
        if ((b & 1) == 1):
            return gcd(a >> 1, b)
        else:
            # both a and b are even
            return (gcd(a >> 1, b >> 1) << 1)

    # a is odd, b is even
    if ((~b & 1) == 1):
        return gcd(a, b >> 1)

    # reduce larger number
    if (a > b):
        return gcd((a - b) >> 1, b)

    return gcd((b - a) >> 1, a)

# Driver code
a, b = 34, 17
print("Gcd of given numbers is ",
      gcd(a, b))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// Recursive C# program to
// implement Stein's Algorithm
using System;

class GFG {

    // Function to implement
    // Stein's Algorithm
    static int gcd(int a, int b)
    {
        if (a == b)
            return a;

        // GCD(0, b) == b;
        // GCD(a, 0) == a,
        // GCD(0, 0) == 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // look for factors of 2
        // a is even
        if ((~a & 1) == 1) {

            // b is odd
            if ((b & 1) == 1)
                return gcd(a >> 1, b);

            else

                // both a and b are even
                return gcd(a >> 1, b >> 1) << 1;
        }

        // a is odd, b is even
        if ((~b & 1) == 1)
            return gcd(a, b >> 1);

        // reduce larger number
        if (a > b)
            return gcd((a - b) >> 1, b);

        return gcd((b - a) >> 1, a);
    }

    // Driver code
    public static void Main()
    {
        int a = 34, b = 17;
        Console.Write("Gcd of given"
                      + "numbers is " + gcd(a, b));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to
// implement Stein's Algorithm

// Function to implement
// Stein's Algorithm
function gcd($a, $b)
{
    if ($a == $b)
        return $a;

    /* GCD(0, b) == b; GCD(a, 0) == a,
       GCD(0, 0) == 0 */
    if ($a == 0)
        return $b;
    if ($b == 0)
        return $a;

    // look for factors of 2
    if (~$a & 1) // a is even
    {
        if ($b & 1) // b is odd
            return gcd($a >> 1, $b);
        else // both a and b are even
            return gcd($a >> 1, $b >> 1) << 1;
    }

    if (~$b & 1) // a is odd, b is even
        return gcd($a, $b >> 1);

    // reduce larger number
    if ($a > $b)
        return gcd(($a - $b) >> 1, $b);

    return gcd(($b - $a) >> 1, $a);
}

// Driver code
$a = 34; $b = 17;
echo "Gcd of given numbers is: ",
                     gcd($a, $b);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to
// implement Stein's Algorithm

     // Function to implement
    // Stein's Algorithm
    function gcd(a, b)
    {
        if (a == b)
            return a;

        // GCD(0, b) == b; GCD(a, 0) == a,
        // GCD(0, 0) == 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // look for factors of 2
        if ((~a & 1) == 1) // a is even
        {
            if ((b & 1) == 1) // b is odd
                return gcd(a >> 1, b);

            else // both a and b are even
                return gcd(a >> 1, b >> 1) << 1;
        }

        // a is odd, b is even
        if ((~b & 1) == 1)
            return gcd(a, b >> 1);

        // reduce larger number
        if (a > b)
            return gcd((a - b) >> 1, b);

        return gcd((b - a) >> 1, a);
    }

// Driver Code

        let a = 34, b = 17;
        document.write("Gcd of given "
                           + "numbers is " + gcd(a, b));

</script>
```

**Output**

```
Gcd of given numbers is 17
```

**时间复杂度** : O(N*N)，其中 N 为较大数字中的位数。
您可能还喜欢–[基本和扩展欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)
**参考文献**:

*   https://en.wikipedia.org/wiki/Binary_GCD_algorithm
*   [http://andreinc . net/2010/12/12/binary-gcd-steins-algorithm-in-c/](http://andreinc.net/2010/12/12/binary-gcd-steins-algorithm-in-c/)
*   [http://www . CSE . unt . edu/~ tarau/teaching/PP/numberthetic/GCD/Binary % 20GCD % 20 algorithm . pdf](http://www.cse.unt.edu/~tarau/teaching/PP/NumberTheoretical/GCD/Binary%20GCD%20algorithm.pdf)

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。