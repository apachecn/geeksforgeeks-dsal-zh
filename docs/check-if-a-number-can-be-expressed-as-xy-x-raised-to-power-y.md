# 检查一个数字是否可以表示为 x^y (x 的幂为 y)

> 原文:[https://www . geesforgeks . org/check-if-a-number-can-express-as-xy-x-raid-to-power-y/](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-xy-x-raised-to-power-y/)

给定一个正整数 n，求它是否可以表示为 x <sup>y</sup> ，其中 y > 1 和 x > 0。x 和 y 都是整数。

**示例:**

```
Input:  n = 8
Output: true
8 can be expressed as 23

Input:  n = 49
Output: true
49 can be expressed as 72

Input:  n = 48
Output: false
48 can't be expressed as xy
```

想法很简单，尝试从 2 到 n(给定数字)的平方根的所有数字 x。对于每个 x，尝试 x^y，其中 y 从 2 开始，一个接一个地增加，直到 x^y 变成 n 或大于 n。

以下是上述想法的实现。

## C++

```
// C++ program to check if a given number can be expressed
// as power
#include <bits/stdc++.h>
using namespace std;

// Returns true if n can be written as x^y
bool isPower(unsigned n)
{
    if (n==1)  return true;

    // Try all numbers from 2 to sqrt(n) as base
    for (int x=2; x<=sqrt(n); x++)
    {
        unsigned y = 2;
        unsigned p = pow(x, y);

        // Keep increasing y while power 'p' is smaller
        // than n.
        while (p<=n && p>0)
        {
            if (p==n)
                return true;
            y++;
            p = pow(x, y);
         }
    }
    return false;
}

// Driver Program
int main()
{
    for (int i =2; i<100; i++)
        if (isPower(i))
           cout << i << "  ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a number can be expressed
// as x^y (x raised to power y)
class GFG {

    // Returns true if n can be written as x^y
    static boolean isPower(int n)
    {
        for (int x = 2; x <= Math.sqrt(n); x++) {
            int y = 2;

            double p = Math.pow(x, y);

            while (p <= n && p > 0) {
                if (p == n)
                    return true;
                y++;
                p = Math.pow(x, y);
            }
        }
        return false;
    }

    // Driver function
    public static void main(String[] args)
    {
        for (int i = 2; i < 100; i++)
            if (isPower(i))
                System.out.print(i + " ");
    }
}

// This code is submitted by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to check if
# a given number can be expressed
# as power
import math

# Returns true if n can be written as x^y
def isPower(n) :
    if (n==1)  :
        return True

    # Try all numbers from 2 to sqrt(n) as base
    for x in range(2,(int)(math.sqrt(n))+1) :
        y = 2
        p = (int)(math.pow(x, y))

        # Keep increasing y while power 'p' is smaller
        # than n.
        while (p<=n and p>0) :
            if (p==n) :
                return True

            y = y + 1
            p = math.pow(x, y)

    return False

# Driver Program
for i in range(2,100 ) :
    if (isPower(i)) :
        print(i,end=" ")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to check if a number
// can be expressed as x^y
// (x raised to power y)
using System;

class GFG
{
    // Returns true if n can
    // be written as x^y
    static bool isPower(int n)
    {
        for (int x = 2; x <= Math.Sqrt(n); x++)
        {
            int y = 2;

            double p = Math.Pow(x, y);

            while (p <= n && p > 0)
            {
                if (p == n)
                    return true;
                y++;
                p = Math.Pow(x, y);
            }
        }
        return false;
    }

    // Driver Code
    static public void Main ()
    {
        for (int i = 2; i < 100; i++)
            if (isPower(i))
                Console.Write(i + " ");
    }
}

// This code is submitted by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given
// number can be expressed as power

// Returns true if n can
// be written as x^y
function isPower($n)
{
    if ($n == 1) return true;

    // Try all numbers from 2
    // to sqrt(n) as base
    for ($x = 2; $x <= sqrt($n); $x++)
    {
        $y = 2;
        $p = pow($x, $y);

        // Keep increasing y while
        // power 'p' is smaller than n.
        while ($p <= $n && $p > 0)
        {
            if ($p == $n)
                return true;
            $y++;
            $p = pow($x, $y);
        }
    }
    return false;
}

// Driver Code
for ($i = 2; $i < 100; $i++)
    if (isPower($i))
    echo $i , " ";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// javascript code to check if a number can be expressed
// as x^y (x raised to power y)   
// Returns true if n can be written as x^y
    function isPower(n)
    {
        for (x = 2; x <= Math.sqrt(n); x++) {
            var y = 2;

            var p = Math.pow(x, y);

            while (p <= n && p > 0) {
                if (p == n)
                    return true;
                y++;
                p = Math.pow(x, y);
            }
        }
        return false;
    }

    // Driver function
        for (i = 2; i < 100; i++)
            if (isPower(i))
                document.write(i + " ");

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
4 8 9 16 25 27 32 36 49 64 81 
```

上述解决方案中的一个优化是通过将 p 与 x 一一相乘来避免调用 power()。

## C++

```
// C++ program to check if a given number can be expressed
// as power
#include <bits/stdc++.h>
using namespace std;

// Returns true if n can be written as x^y
bool isPower(unsigned int n)
{
    // Base case
    if (n <= 1) return true;

    // Try all numbers from 2 to sqrt(n) as base
    for (int x=2; x<=sqrt(n); x++)
    {
        unsigned  p = x;

        // Keep multiplying p with x while is smaller
        // than or equal to x
        while (p <= n)
        {
            p *= x;
            if (p == n)
                return true;
        }
    }
    return false;
}

// Driver Program
int main()
{
    for (int i =2; i<100; i++)
        if (isPower(i))
           cout << i << "  ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a number can be expressed
// as x^y (x raised to power y)
class GFG {

    // Returns true if n can be written as x^y
    static boolean isPower(int n)
    {
        for (int x = 2; x <= Math.sqrt(n); x++) {
            int p = x;

            while (p <= n) {
                p = p * x;
                if (p == n)
                    return true;
            }
        }
        return false;
    }

    // Driver function
    public static void main(String[] args)
    {
        for (int i = 2; i < 100; i++)
            if (isPower(i))
                System.out.print(i + " ");
    }
}

// This code is submitted by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to check if
# a given number can be expressed
# as power
import math

# Returns true if n can be written
# as x ^ y
def isPower(n) :

    # Base case
    if (n <= 1) :
        return True

    # Try all numbers from 2 to sqrt(n)
    # as base
    for x in range(2, (int)(math.sqrt(n)) + 1) :
        p = x

        # Keep multiplying p with x while
        # is smaller than or equal to x
        while (p <= n) :
            p = p * x

            if (p == n) :
                return True

    return False

# Driver Program
for i in range(2, 100) :

    if (isPower(i)) :
        print( i, end =" ")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to check if a number
// can be expressed as x^y (x
// raised to power y)
using System;

class GFG
{

    // Returns true if n can
    // be written as x^y
    static bool isPower(int n)
    {
        for (int x = 2;
                 x <= Math.Sqrt(n); x++)
        {
            int p = x;

            while (p <= n)
            {
                p = p * x;
                if (p == n)
                    return true;
            }
        }
        return false;
    }

    // Driver Code
    public static void Main()
    {
        for (int i = 2; i < 100; i++)
            if (isPower(i))
                Console.Write(i + " ");
    }
}

// This code is submitted by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// given number can be expressed
// as power

// Returns true if n can
// be written as x^y
function isPower($n)
{
    // Base case
    if ($n <= 1) return true;

    // Try all numbers from 2
    // to sqrt(n) as base
    for ($x = 2; $x <= sqrt($n); $x++)
    {
        $p = $x;

        // Keep multiplying p with
        // x while is smaller
        // than or equal to x
        while ($p <= $n)
        {
            $p *= $x;
            if ($p == $n)
                return true;
        }
    }
    return false;
}

    // Driver Code
    for ($i = 2; $i < 100; $i++)
        if (isPower($i))
        echo $i , " ";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript code to check if a number
    // can be expressed as x^y (x
    // raised to power y)

    // Returns true if n can
    // be written as x^y
    function isPower(n)
    {
        for (let x = 2; x <= parseInt(Math.sqrt(n), 10); x++)
        {
            let p = x;

            while (p <= n)
            {
                p = p * x;
                if (p == n)
                    return true;
            }
        }
        return false;
    }

    for (let i = 2; i < 100; i++)
            if (isPower(i))
                document.write(i + " ");

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
4  8  9  16  25  27  32  36  49  64  81
```

**替代实施:**

## C++

```
// C++ program to check if a given number can be expressed
// as power
#include <bits/stdc++.h>
using namespace std;

// Returns true if n can be written as x^y
bool isPower(unsigned n)
{
    float p;
    if (n <= 1)
        return 1;
    for (int i = 2; i <= sqrt(n); i++) {
        p = log2(n) / log2(i);
        if ((ceil(p) == floor(p)) && p > 1)
            return true;
    }
    return false;
}

// Driver Program
int main()
{
    for (int i = 2; i < 100; i++)
        if (isPower(i))
            cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// number can be expressed as power
import java.io.*;
import java.lang.Math;

class GFG {

// Returns true if n can be written as x^y
static boolean isPower(int n)
{
    double p;
    if (n <= 1)
    {
        return true;
    }
    for(int i = 2; i <= Math.sqrt(n); i++)
    {
       p = Math.log(n) / Math.log(i);

       if ((Math.ceil(p) == Math.floor(p)) && p > 1)
       {
           return true;
       }
    }
    return false;
}

// Driver Code
public static void main (String[] args)
{
    for(int i = 2; i < 100; i++)
    {
       if (isPower(i))
           System.out.print(i + " ");
    }
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program to check if a given
# number can be expressed as power
import math

# Returns true if n can be
# written as x^y
def isPower(n):

    p = 0

    if (n <= 1):
        return 1

    for i in range(2, (int)(math.sqrt(n)) + 1):
        p = math.log2(n) / math.log2(i)

        if ((math.ceil(p) ==
            math.floor(p)) and p > 1):
            return 1

    return 0

# Driver code
for i in range(2, 100):
    if isPower(i):
        print(i, end = " ")

# This code is contributed by sallagondaavinashreddy7
```

## C#

```
// C# program to check if a given
// number can be expressed as power
using System;

class GFG{

// Returns true if n can be written as x^y
static bool isPower(int n)
{
    double p;
    if (n <= 1)
    {
        return true;
    }

    for(int i = 2; i <= Math.Sqrt(n); i++)
    {
       p = Math.Log(n) / Math.Log(i);

       if ((Math.Ceiling(p) == Math.Floor(p)) && p > 1)
       {
           return true;
       }
    }
    return false;
}

// Driver code
static public void Main ()
{
    for(int i = 2; i < 100; i++)
    {
       if (isPower(i))
           Console.Write(i + " ");
    }
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

    // Javascript program to check if a given
    // number can be expressed as power

    // Returns true if n can be written as x^y
    function isPower(n)
    {
        let p;
        if (n <= 1)
        {
            return true;
        }

        for(let i = 2; i <= parseInt(Math.sqrt(n), 10); i++)
        {
           p = (Math.log(n) / Math.log(i)).toFixed(14);
           if ((Math.ceil(p) == Math.floor(p)) && (p > 1))
           {
               return true;
           }
        }
        return false;
    }

    for(let i = 2; i < 100; i++)
    {
       if (isPower(i))
           document.write(i + " ");
    }

</script>
```

**Output:** 

```
4 8 9 16 25 27 32 36 49 64 81
```

**高效求解:** [检查一个数是否可以表示为 a^b |集合 2](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-ab-set-2/)
本文由 **Vaibhav Gupta** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息