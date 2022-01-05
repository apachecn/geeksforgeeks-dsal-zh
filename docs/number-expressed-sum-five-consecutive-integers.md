# 表示为五个连续整数之和的数

> 原文:[https://www . geesforgeks . org/number-expressed-sum-五个连续整数/](https://www.geeksforgeeks.org/number-expressed-sum-five-consecutive-integers/)

给定一个整数 n，任务是找出 n 是否可以表示为五个连续整数的和。如果是，找到五个连续的整数，否则打印“-1”。
**例:**

```
Input : n = 15
Output : 1 2 3 4 5
15 = 1 + 2 + 3 + 4 + 5

Input : n = 18
Output : -1
```

**方法 1:(蛮力)**
想法是运行一个从 i = 0 到 n–4 的循环，检查(i + i+1 + i+2 + i+3 + i+4)是否等于 n。此外，检查 n 是正还是负，并相应地将 I 递增或递减 1。
以下是本办法的实施:

## C++

```
// CPP Program to check if a number can
// be expressed as sum of five consecutive
// integers.
#include <bits/stdc++.h>
using namespace std;

// function to check if a number can be expressed as
// sum of five consecutive integers.
void checksum(int n)
{
    // if n is 0
    if (n == 0) {
        cout << "-2 -1 0 1 2" << endl;
        return;
    }

    int inc;

    // if n is positive, increment loop by 1.
    if (n > 0)
        inc = 1;

    // if n is negative, decrement loop by 1.
    else
        inc = -1;

    // Running loop from 0 to n - 4
    for (int i = 0; i <= n - 4; i += inc) {

        // check if sum of five consecutive
        // integer is equal to n.
        if (i + i + 1 + i + 2 + i + 3 + i + 4 == n) {
            cout << i << " " << i + 1
                 << " " << i + 2
                 << " " << i + 3
                 << " " << i + 4;
            return;
        }
    }

    cout << "-1";
}

// Driver Program
int main()
{
    int n = 15;
    checksum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a number can
// be expressed as sum of five consecutive
// integers.
import java.io.*;

class GFG {

    // function to check if a number can be
    // expressed as sum of five consecutive
    // integers.
    static void checksum(int n)
    {
        // if n is 0
        if (n == 0) {
            System.out.println("-2 -1 0 1 2");
            return;
        }

        int inc;

        // if n is positive, increment loop by 1.
        if (n > 0)
            inc = 1;

        // if n is negative, decrement loop by 1.
        else
            inc = -1;

        // Running loop from 0 to n - 4
        for (int i = 0; i <= n - 4; i += inc) {

            // check if sum of five consecutive
            // integer is equal to n.
            if (i + i + 1 + i + 2 + i + 3 + i
                                       + 4 == n)
            {
                System.out.print( (i )
                        + " " + (i + 1)
                        + " " + (i + 2)
                        + " " + (i + 3)
                        + " " + (i + 4));
                return;
            }
        }

        System.out.println( "-1");
    }

    // Driver Program
    public static void main (String[] args)
    {
        int n = 15;
        checksum(n);
    }
}

// This code is contributed by anuj_67
```

## 蟒蛇 3

```
# Python3 code to check if a number
# can be expressed as sum of five
# consecutive integers.

# function to check if a number
# can be expressed as sum of five
# consecutive integer.
def checksum(n):

    # if n is 0
    if n == 0:
        print("-2 -1 0 1 2")
        return 0

    inc = 0

    # if n is positive,
    # increment loop by 1.
    if n > 0:
        inc = 1

    # if n is negative,
    # decrement loop by 1.
    else:
        inc = -1

    # Running loop from 0 to n - 4
    for i in range(0, n-3, inc):

        # check if sum of five consecutive
        # integer is equal to n.
        if i + i + 1 + i + 2 + i + 3 + i + 4 == n:
            print(i, " ", i + 1, " ", i + 2, " ", i + 3, " ", i + 4)
            return 0

    print("-1")

# Driver Code
n = 15
checksum(n)
```

## C#

```
// C# Program to check if a number can
// be expressed as sum of five consecutive
// integers.
using System;

class GFG {

    // function to check if a number can be
    // expressed as sum of five consecutive
    // integers.
    static void checksum(int n)
    {
        // if n is 0
        if (n == 0) {
            Console.Write("-2 -1 0 1 2");
            return;
        }

        int inc;

        // if n is positive, increment loop by 1.
        if (n > 0)
            inc = 1;

        // if n is negative, decrement loop by 1.
        else
            inc = -1;

        // Running loop from 0 to n - 4
        for (int i = 0; i <= n - 4; i += inc) {

            // check if sum of five consecutive
            // integer is equal to n.
            if (i + i + 1 + i + 2 + i + 3 + i
                                    + 4 == n)
            {
                Console.Write( (i )
                        + " " + (i + 1)
                        + " " + (i + 2)
                        + " " + (i + 3)
                        + " " + (i + 4));
                return;
            }
        }

        Console.WriteLine( "-1");
    }

    // Driver Program
    public static void Main ()
    {
        int n = 15;
        checksum(n);
    }
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check
// if a number can be
// expressed as sum of
// five consecutive integers.

// function to check if a
// number can be expressed
// as sum of five consecutive
// integers.
function checksum($n)
{
    // if n is 0
    if ($n == 0)
    {
        echo "-2 -1 0 1 2" , "\n";
            return;
    }

    $inc;

    // if n is positive,
    // increment loop by 1.
    if ($n > 0)
        $inc = 1;

    // if n is negative,
    // decrement loop by 1.
    else
        $inc = -1;

    // Running loop from
    // 0 to n - 4
    for ($i = 0;
         $i <= $n - 4; $i += $inc)
    {

        // check if sum of five
        // consecutive integer
        // is equal to n.
        if ($i + $i + 1 + $i + 2 +
            $i + 3 + $i + 4 == $n)
        {
            echo $i , " " , $i + 1,
                      " " , $i + 2,
                      " " , $i + 3,
                      " " , $i + 4;
            return;
        }
    }

    echo "-1";
}

// Driver Code
$n = 15;
checksum($n);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if a number can
// be expressed as sum of five consecutive
// integers.

    // function to check if a number can be
    // expressed as sum of five consecutive
    // integers.
    function checksum(n) {
        // if n is 0
        if (n == 0) {
            document.write("-2 -1 0 1 2");
            return;
        }

        var inc;

        // if n is positive, increment loop by 1.
        if (n > 0)
            inc = 1;

        // if n is negative, decrement loop by 1.
        else
            inc = -1;

        // Running loop from 0 to n - 4
        for (i = 0; i <= n - 4; i += inc) {

            // check if sum of five consecutive
            // integer is equal to n.
            if (i + i + 1 + i + 2 + i + 3 + i + 4 == n) {
                document.write((i) + " "
                + (i + 1) + " "
                + (i + 2) + " "
                + (i + 3) + " "
                + (i + 4));
                return;
            }
        }

        document.write("-1");
    }

    // Driver Program

        var n = 15;
        checksum(n);

// This code contributed by gauravrajput1

</script>
```

**输出:**

```
1 2 3 4 5
```

**方法 2:(有效方法)**
思路是检查 n 是否为 5 的倍数。
设 n 为 k–2，k-1，k，k + 1，k+2 五个连续整数之和。因此，
k-2+k-1+k+1+k+2 = n
5 * k = n
这五个数字将是 n/5–2，n/5–1，n/5，n/5 + 1，n/5 + 2。

以下是本办法的实施:

## C++

```
// CPP Program to check if a number can be
// expressed as sum of five consecutive integer.
#include <bits/stdc++.h>
using namespace std;

// function to check if a number can be
// expressed as sum of five consecutive
// integers.
void checksum(int n)
{
    // if n is multiple of 5
    if (n % 5 == 0)
        cout << n / 5 - 2 << " "
             << n / 5 - 1 << " " << n / 5
             << " " << n / 5 + 1 << " "
             << n / 5 + 2;

    // else print "-1".
    else
        cout << "-1";
}

// Driver Program
int main()
{
    int n = 15;
    checksum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a number can
// be expressed as sum of five consecutive
// integer.
import java.io.*;

class GFG {

    // function to check if a number can
    // be expressed as sum of five
    // consecutive integers.
    static void checksum(int n)
    {
        // if n is multiple of 5
        if (n % 5 == 0)
            System.out.println( (n / 5 - 2)
                  + " " + (n / 5 - 1) + " "
                  + (n / 5) + " " + (n / 5
                + 1 ) + " " + (n / 5 + 2));

        // else print "-1".
        else
            System.out.println( "-1");
    }

    // Driver Program
    public static void main (String[] args)
    {
        int n = 15;
        checksum(n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to check if a number
# can be expressed as sum of five
# consecutive integer.

# function to check if a number
# can be expressed as sum of five
# consecutive integers.
def checksum(n):
    n = int(n)

    # if n is multiple of 5
    if n % 5 == 0:
        print(int(n / 5 - 2), " ",
         int(n / 5 - 1), " ", int(n / 5), " ", int(n / 5 + 1), " ", int(n / 5 + 2))

    # else print "-1".
    else:
        print("-1")

# Driver Code
n = 15
checksum(n)
```

## C#

```
// C# Program to check if a number can
// be expressed as sum of five consecutive
// integer.
using System;

class GFG {

    // function to check if a number can
    // be expressed as sum of five
    // consecutive integers.
    static void checksum(int n)
    {
        // if n is multiple of 5
        if (n % 5 == 0)
            Console.WriteLine( (n / 5 - 2)
                + " " + (n / 5 - 1) + " "
                + (n / 5) + " " + (n / 5
                + 1 ) + " " + (n / 5 + 2));

        // else print "-1".
        else
            Console.WriteLine( "-1");
    }

    // Driver Program
    public static void Main ()
    {
        int n = 15;
        checksum(n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if
// a number can be expressed
// as sum of five consecutive
// integer.

// function to check if a
// number can be expressed
// as sum of five consecutive
// integers.
function checksum( $n)
{
    // if n is multiple of 5
    if ($n % 5 == 0)
        echo $n / 5 - 2 , " " ,
             $n / 5 - 1 , " " ,
             $n / 5 , " " ,
             $n / 5 + 1 , " " ,
             $n / 5 + 2;

    // else print "-1".
    else
        echo "-1";
}

// Driver Code
$n = 15;
checksum($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript Program to check if a number can
// be expressed as sum of five consecutive
// integer.

    // function to check if a number can
    // be expressed as sum of five
    // consecutive integers.
    function checksum(n) {
        // if n is multiple of 5
        if (n % 5 == 0)
            document.write((n / 5 - 2) + " "
            + (n / 5 - 1) + " " + (n / 5)
            + " " + (n / 5 + 1) + " " + (n / 5 + 2));

        // else print "-1".
        else
            document.write("-1");
    }

    // Driver Program

        var n = 15;
        checksum(n);

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
1 2 3 4 5
```