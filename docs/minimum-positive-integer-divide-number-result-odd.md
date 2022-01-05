# 最小正整数除以一个数，结果为奇数

> 原文:[https://www . geesforgeks . org/minimum-正整数-除数-结果-奇数/](https://www.geeksforgeeks.org/minimum-positive-integer-divide-number-result-odd/)

给定一个数 n。打印最小正整数，除以该整数，结果为奇数。
**例:**

```
Input : 36
Output : 4
36 must be divided by 4 or 12 to make it odd.
We take minimum of 4 and 12 i.e. 4

Input : 8
Output : 8
8 must be divided by 8 to make it an odd number.
```

**方法 1:**

```
Find the minimum number that makes the given number 
odd  by dividing it one by one from 2(i) to N
If (N/i) is odd then return i.
```

## C++

```
// C++ program to make a number odd
#include <iostream>
using namespace std;

int makeOdd(int n)
{
    // Return 1 if already odd
    if (n % 2 != 0)
        return 1;

    // Check on dividing with a number when
    // the result becomes odd Return that number
    for (int i = 2 ; i <= n ; i++)

        // If n is divided by i and n/i is odd
        // then return i
        if ((n % i == 0) && ((n / i) % 2 == 1))
            return i;

}

// Driver code
int main()
{
    int n = 36;
    cout << makeOdd(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make a number odd
import java.io.*;

class GFG
{
    static int makeOdd(int n)
    {
        // Return 1 if already odd
        if (n % 2 != 0)
            return 1;

        // Check on dividing with a number when
        // the result becomes odd Return that number
        int i;
        for (i = 2 ; i <= n ; i++)

            // If n is divided by i and n/i is odd
            // then return i
            if ((n % i  == 0) && ((n / i) % 2 == 1))
                break;

        return i;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 36;
        int res = makeOdd(n);
        System.out.println(res);
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to
# make a number odd

def makeOdd(n):

    # Return 1 if
    # already odd
    if n % 2 != 0:
        return 1;

    # Check on dividing
    # with a number when
    # the result becomes
    # odd Return that number
    for i in range(2, n):

        # If n is divided by
        # i and n/i is odd
        # then return i
        if (n % i == 0 and
           (int)(n / i) % 2 == 1):
            return i;

# Driver code
n = 36;
print(makeOdd(n));

# This code is contributed
# by mits
```

## C#

```
// C# program to make a number odd
using System;

class GFG
{
    static int makeOdd(int n)
    {
        // Return 1 if already odd
        if (n % 2 != 0)
            return 1;

        // Check on dividing with a number when
        // the result becomes odd Return that number
        int i;
        for (i = 2 ; i <= n ; i++)

            // If n is divided by i and n/i is odd
            // then return i
            if ((n % i == 0) && ((n / i) % 2 == 1))
                break;

        return i;
    }

    // Driver code
    public static void Main ()
    {
        int n = 36;
        int res = makeOdd(n);
        Console.Write(res);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to make
// a number odd

function makeOdd($n)
{

    // Return 1 if already odd
    if ($n % 2 != 0)
        return 1;

    // Check on dividing with
    // a number when the result
    // becomes odd Return that
    // number
    for ($i = 2 ; $i <= $n ; $i++)

        // If n is divided by i and
        // n/i is odd then return i
        if (($n % $i == 0) &&
           (($n / $i) % 2 == 1))
            return $i;

}

    // Driver code
    $n = 36;
    echo makeOdd($n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// javascript program to make a number odd
function makeOdd(n)
{
        // Return 1 if already odd
    if (n % 2 != 0)
        return 1;

    // Check on dividing with a number when
    // the result becomes odd Return that number
    var i;
    for (i = 2 ; i <= n ; i++)

        // If n is divided by i and n/i is odd
        // then return i
        if ((n % i  == 0) && ((n / i) % 2 == 1))
            break;

    return i;
}

// Driver code
   var n = 36;
   var res = makeOdd(n);
   document.write(res);

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
4
```

**方法二:**

```
 As there is only one case to make a number odd i.e.
It is an even number i.e. divisible by 2.
So, the point is to find the smallest multiple of 2 
that can make the given number odd.
```

## C++

```
// C++ program to make a number odd
#include <iostream>
using namespace std;

// Function to find the value
int makeOdd(int n)
{
    // Return 1 if already odd
    if (n%2 != 0)
        return 1;

    // Check how many times it is divided by 2
    int resul = 1;
    while (n%2 == 0)
    {
        n /= 2;
        resul *= 2;
    }

    return resul;
}

// Driver code
int main()
{
    int n = 36;
    cout << makeOdd(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make a number odd
import java.io.*;

class GFG
{
    // Function to find the value
    static int makeOdd(int n)
    {
        // Return 1 if already odd
        if (n % 2 != 0)
            return 1;

        // Check how many times it is divided by 2
        int ans = 1;
        while (n % 2 == 0)
        {
            n /= 2;
            ans *= 2;
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 36;
        int res = makeOdd(n);
        System.out.println(res);
    }
}
// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to
# make a number odd

# Function to find
# the value
def makeOdd(n):

    # Return 1 if
    # already odd
    if (n % 2 != 0):
        return 1;

    # Check how many times
    # it is divided by 2
    resul = 1;
    while (n % 2 == 0):
        n = n/ 2;
        resul = resul * 2;
    return resul;

# Driver code
n = 36;
print(makeOdd(n));

# This code is contributed
# by mits
```

## C#

```
// C# program to make a number odd
using System;

class GFG {

    // Function to find the value
    static int makeOdd(int n)
    {
        // Return 1 if already odd
        if (n % 2 != 0)
            return 1;

        // Check how many times it
        // is divided by 2
        int ans = 1;
        while (n % 2 == 0)
        {
            n /= 2;
            ans *= 2;
        }
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int n = 36;
        int res = makeOdd(n);
        Console.Write(res);
    }
}

// This code is contributed by
// nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to make
// a number odd

// Function to find the value
function makeOdd( $n)
{
    // Return 1 if already odd
    if ($n % 2 != 0)
        return 1;

    // Check how many times
    // it is divided by 2
    $resul = 1;
    while ($n % 2 == 0)
    {
        $n /= 2;
        $resul *= 2;
    }

    return $resul;
}

// Driver code
$n = 36;
echo makeOdd($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// javascript program to make a number odd
    // Function to find the value
    function makeOdd( n) {
        // Return 1 if already odd
        if (n % 2 != 0)
            return 1;

        // Check how many times it is divided by 2
        var ans = 1;
        while (n % 2 == 0) {
            n = parseInt(n/2);
            ans *= 2;
        }
        return ans;
    }

    // Driver code

        var n = 36;
        var res = makeOdd(n);
        document.write(res);

// This code contributed by Princi Singh
</script>
```

**输出:**

```
4
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。