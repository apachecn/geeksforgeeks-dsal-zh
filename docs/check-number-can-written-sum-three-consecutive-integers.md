# 检查一个数是否可以写成三个连续整数的和

> 原文:[https://www . geesforgeks . org/check-number-can-writed-sum-三个连续整数/](https://www.geeksforgeeks.org/check-number-can-written-sum-three-consecutive-integers/)

给定一个整数 **n** ，任务是找出 n 是否可以写成三个连续整数之和。如果是，找到连续的三个整数，否则打印“-1”。
示例:

```
Input : n = 6
Output : 1 2 3
6 = 1 + 2 + 3.

Input : n = 7
Output : -1
```

**方法 1:(蛮力):**
想法是运行一个从 i = 0 到 n–2 的循环，检查(i + i+1 + i+2)是否等于 n。此外，检查 n 是正还是负，并相应地将 I 递增或递减 1。
以下是本办法的实施:

## C++

```
// CPP Program to check if a number can
// be written as sum of three consecutive
// integers.
#include <bits/stdc++.h>
using namespace std;

// function to check if a number can be written as sum of
// three consecutive integer.
void checksum(int n)
{
    // if n is 0
    if (n == 0) {
        cout << "-1 0 1" << endl;
        return;
    }

    int inc;

    // if n is positive, increment loop by 1.
    if (n > 0)
        inc = 1;

    // if n is negative, decrement loop by 1.
    else
        inc = -1;

    // Running loop from 0 to n - 2
    for (int i = 0; i <= n - 2; i += inc) {

        // check if sum of three consecutive
        // integer is equal to n.
        if (i + i + 1 + i + 2 == n) {
            cout << i << " " << i + 1
                 << " " << i + 2;
            return;
        }
    }

    cout << "-1";
}

// Driver Program
int main()
{
    int n = 6;
    checksum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to check if a number
// can be written as sum of
// three consecutive integers.
import java.util.*;

class GFG
{
    // function to check if a number
    // can be written as sum of
    // three consecutive integer.
    static void checksum(int n)
    {
        // if n is 0
        if (n == 0) {
            System.out.println("-1 0 1");
            return;
        }

        int inc;

        // if n is positive,
        // increment loop by 1.
        if (n > 0)
            inc = 1;

        // if n is negative,
        // decrement loop by 1.
        else
            inc = -1;

        // Running loop from 0 to n - 2
        for (int i = 0; i <= n - 2; i += inc) {

            // check if sum of three consecutive
            // integer is equal to n.
            if (i + i + 1 + i + 2 == n) {
                System.out.println(i + " " +
                                  (i + 1) +
                                " " + (i + 2));
                return;
            }
        }

        System.out.println("-1");
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 6;
        checksum(n);
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to check if a number
# can be written as sum of three
# consecutive integers.

# function to check if a number
# can be written as sum of three
# consecutive integer.
def checksum(n):

    # if n is 0
    if n == 0:
        print("-1 0 1")
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

    # Running loop from 0 to n - 2
    for i in range(0, n-1, inc):

        # check if sum of three consecutive
        # integer is equal to n.
        if i + i + 1 + i + 2 == n:
            print(i ," ",i + 1, " ", i + 2)
            return 0

    print("-1")

# Driver Code
n = 6
checksum(n)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code to check if a number
// can be written as sum of
// three consecutive integers.
using System;

class GFG
{
    // function to check if a number
    // can be written as sum of
    // three consecutive integer.
    static void checksum(int n)
    {
        // if n is 0
        if (n == 0) {
            Console.WriteLine("-1 0 1");
            return;
        }

        int inc;

        // if n is positive,
        // increment loop by 1.
        if (n > 0)
            inc = 1;

        // if n is negative,
        // decrement loop by 1.
        else
            inc = -1;

        // Running loop from 0 to n - 2
        for (int i = 0; i <= n - 2; i += inc) {

            // check if sum of three consecutive
            // integer is equal to n.
            if (i + i + 1 + i + 2 == n) {
                Console.WriteLine(i + " "
                     + (i + 1) +" " + (i + 2));
                return;
            }
        }

        Console.WriteLine("-1");
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int n = 6;
        checksum(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if a
// number can be written
// as sum of three consecutive
// integers.

// function to check if a number
// can be written as sum of
// three consecutive integer.
function checksum($n)
{

    // if n is 0
    if ($n == 0)
    {
        echo "-1 0 1" ;
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
    // 0 to n - 2
    for ($i = 0; $i <= $n - 2; $i += $inc)
    {

        // check if sum of three consecutive
        // integer is equal to n.
        if ($i + $i + 1 + $i + 2 == $n)
        {
            echo $i , " " , $i + 1
                , " " , $i + 2;
            return;
        }
    }

    echo "-1";
}

    // Driver Code
    $n = 6;
    checksum($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Code to check if a number
// can be written as sum of
// three consecutive integers.

    // function to check if a number
    // can be written as sum of
    // three consecutive integer.
    function checksum(n)
    {

        // if n is 0
        if (n == 0) {
            document.write("-1 0 1");
            return;
        }

        var inc;

        // if n is positive,
        // increment loop by 1.
        if (n > 0)
            inc = 1;

        // if n is negative,
        // decrement loop by 1.
        else
            inc = -1;

        // Running loop from 0 to n - 2
        for (i = 0; i <= n - 2; i += inc)
        {

            // check if sum of three consecutive
            // integer is equal to n.
            if (i + i + 1 + i + 2 == n) {
                document.write(i + " "
                + (i + 1) + " "
                + (i + 2));
                return;
            }
        }
        document.write("-1");
    }

    /* Driver program to test above function */
        var n = 6;
        checksum(n);

// This code is contributed by gauravrajput1

</script>
```

**输出:**

```
1 2 3
```

**方法 2:(有效方法)**
思路是检查 n 是否为 3 的倍数。
设 n 为 k–1，k，k + 1 三个连续整数之和。因此，
k–1+k+k+1 = n
3 * k = n
这三个数字将是 n/3–1，n/3，n/3 + 1。

## C++

```
// CPP Program to check if a number can be
// written as sum of three consecutive integer.
#include <bits/stdc++.h>
using namespace std;

// function to check if a number can be
// written as sum of three consecutive
// integers.
void checksum(int n)
{
    // if n is multiple of 3
    if (n % 3 == 0)
        cout << n / 3 - 1 << " "
             << n / 3 << " " << n / 3 + 1;

    // else print "-1".
    else
        cout << "-1";
}

// Driver Program
int main()
{
    int n = 6;
    checksum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to check if a number
// can be written as sum of three
// consecutive integers.
import java.util.*;

class GFG
{
    // function to check if a number
    // can be written as sum of three
    // consecutive integers.
    static void checksum(int n)
    {
        // if n is multiple of 3
        if (n % 3 == 0)
            System.out.println( n / 3 - 1 + " "
                 + n / 3 + " " + (n / 3 + 1));

        // else print "-1".
        else
            System.out.println("-1");
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 6;
        checksum(n);
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to check if a number
# can be written as sum of three
# consecutive integer.

# function to check if a number
# can be written as sum of three
# consecutive integers.
def checksum(n):
    n = int(n)

    # if n is multiple of 3
    if n % 3 == 0:
        print(int(n / 3 - 1) ," ",
         int(n / 3)," ",int(n / 3 + 1))

    # else print "-1".
    else:
        print("-1")

# Driver Code
n = 6
checksum(n)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code to check if a number
// can be written as sum of three
// consecutive integers.
using System;

class GFG
{
    // function to check if a number
    // can be written as sum of three
    // consecutive integers.
    static void checksum(int n)
    {
        // if n is multiple of 3
        if (n % 3 == 0)
            Console.WriteLine( n / 3 - 1 + " "
                    + n / 3 + " " + (n / 3 + 1));

        // else print "-1".
        else
            Console.WriteLine("-1");
    }

    /* Driver program to
     test above function */
    public static void Main()
    {
        int n = 6;

        checksum(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code to check if a number
// can be written as sum of three
// consecutive integers.

// function to check if
// a number can be written
// as sum of three consecutive
// integers.
function checksum($n)
{

    // if n is multiple of 3
    if ($n % 3 == 0)
        echo $n / 3 - 1, " ",
             $n / 3, " ",
             $n / 3 + 1;

    // else print "-1".
    else
        echo "-1";
}

    // Driver Program
    $n = 6;
    checksum($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// javascript Code to check if a number
// can be written as sum of three
// consecutive integers.
    // function to check if a number
    // can be written as sum of three
    // consecutive integers.
    function checksum(n) {
        // if n is multiple of 3
        if (n % 3 == 0)
            document.write(n / 3 - 1 + " "
            + n / 3 + " "
            + (n / 3 + 1));

        // else prvar "-1".
        else
            document.write("-1");
    }

    /* Driver program to test above function */

        var n = 6;
        checksum(n);

// This code is contributed by todaysgaurav
</script>
```

输出:

```
1 2 3
```