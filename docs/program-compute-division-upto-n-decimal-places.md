# 计算除法至小数位数的程序

> 原文:[https://www . geesforgeks . org/program-compute-division-up-n-小数位数/](https://www.geeksforgeeks.org/program-compute-division-upto-n-decimal-places/)

给定 3 个数字 x，y 和 n，计算到小数点后 n 位的除法(x/y)。
**例:**

```
Input  : x = 22, y = 7, n = 10
Output : 3.1428571428
Explanation :
Since n = 10, division (x / y) is taken till
10 decimal places.

Input  : x = 22, y = 7, n = 20
Output : 3.14285714285714285714
```

**进场:**

1.  求余数，用被除数减去余数，乘以 10，进行下一次迭代。
2.  如果我们达到了完整的结果，我们可能不需要继续，直到达到预定义的迭代次数。

## C++

```
// CPP program to compute division upto n
// decimal places.
#include <bits/stdc++.h>
using namespace std;

void precisionCompute(int x, int y, int n)
{
    // Base cases
    if (y == 0) {
        cout << "Infinite" << endl;
        return;
    }
    if (x == 0) {
        cout << 0 << endl;
        return;
    }
    if (n <= 0) {
        // Since n <= 0, don't compute after
        // the decimal
        cout << x / y << endl;
        return;
    }

    // Handling negative numbers
    if (((x > 0) && (y < 0)) || ((x < 0) && (y > 0))) {
        cout << "-";
        x = x > 0 ? x : -x;
        y = y > 0 ? y : -y;
    }

    // Integral division
    int d = x / y;

    // Now one by print digits after dot
    // using school division method.
    for (int i = 0; i <= n; i++) {
        cout << d;
        x = x - (y * d);
        if (x == 0)
            break;
        x = x * 10;
        d = x / y;
        if (i == 0)
            cout << ".";
    }
}

// Driver Program
int main()
{
    int x = 22, y = 7, n = 15;
    precisionCompute(x, y, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute division upto n
// decimal places.
import java.util.*;

class Eulerian {
    public static void precisionCompute(int x, int y, int n)
    {
        // Base cases
        if (y == 0) {
            System.out.print("Infinite");
            return;
        }
        if (x == 0) {
            System.out.print("0");
            return;
        }
        if (n <= 0) {
            // Since n <= 0, don't compute after
            // the decimal
            System.out.print(x / y);
            return;
        }

        // Handling negative numbers
        if (((x > 0) && (y < 0)) || ((x < 0) && (y > 0))) {
            System.out.print("-");
            x = x > 0 ? x : -x;
            y = y > 0 ? y : -y;
        }

        // Integral division
        int d = x / y;

        // Now one by print digits after dot
        // using school division method.
        for (int i = 0; i <= n; i++) {
            System.out.print(d);
            x = x - (y * d);
            if (x == 0)
                break;
            x = x * 10;
            d = x / y;
            if (i == 0)
                System.out.print(".");
        }
    }

    public static void main(String[] args)
    {
        int x = 22, y = 7, n = 15;
        precisionCompute(x, y, n);
    }
}

// This code is contributed by rishabh_jain
```

## C#

```
// C# program to compute division
// upto n decimal places.
using System;

class Eulerian {

    public static void precisionCompute(int x, int y,
                                        int n)
    {
        // Base cases
        if (y == 0) {
            Console.WriteLine("Infinite");
            return;
        }
        if (x == 0) {
            Console.WriteLine("0");
            return;
        }
        if (n <= 0) {

            // Since n <= 0, don't compute after
            // the decimal
            Console.WriteLine(x / y);
            return;
        }

        // Handling negative numbers
        if (((x > 0) && (y < 0)) || ((x < 0) && (y > 0))) {
            Console.WriteLine("-");
            x = x > 0 ? x : -x;
            y = y > 0 ? y : -y;
        }

        // Integral division
        int d = x / y;

        // Now one by print digits after dot
        // using school division method.
        for (int i = 0; i <= n; i++) {
            Console.Write(d);
            x = x - (y * d);
            if (x == 0)
                break;
            x = x * 10;
            d = x / y;
            if (i == 0)
                Console.Write(".");
        }
    }

    // Driver code
    public static void Main()
    {
        int x = 22, y = 7, n = 15;
        precisionCompute(x, y, n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute
// division upto n decimal
// places.

function precisionCompute($x, $y, $n)
{
    // Base cases
    if ($y == 0)
    {
        echo "Infinite", "\n";
        return;
    }
    if ($x == 0)
    {
        echo 0, "\n";
        return;
    }
    if ($n <= 0)
    {
        // Since n <= 0, don't 
        // compute after the decimal
        echo $x / $y, "\n";
        return;
    }

    // Handling negative numbers
    if ((($x > 0) && ($y < 0)) ||
        (($x < 0) && ($y > 0)))
    {
        echo "-";
        $x = $x > 0 ? $x : -$x;
        $y = $y > 0 ? $y : -$y;
    }

    // Integral division
    $d = $x / $y;

    // Now one by print digits after dot
    // using school division method.
    for ($i = 0; $i <= $n; $i++)
    {
        echo $d;
        $x = $x - ($y * $d);
        if ($x == 0)
            break;
        $x = $x * 10;
        $d = $x / $y;
        if ($i == 0)
            echo ".";
    }
}

// Driver Code
$x = 22; $y = 7; $n = 15;

precisionCompute($x, $y, $n);

// This code is contributed by aj_36
?>
```

## 蟒蛇 3

```
# Python3 program to compute
# division upto n decimal places.

def precisionCompute(x, y, n):

    # Base cases
    if y == 0:
        print("Infinite");
        return;
    if x == 0:
        print(0);
        return;
    if n <= 0:

        # Since n <= 0, don't
        # compute after the decimal
        print(x / y);
        return;

    # Handling negative numbers
    if (((x > 0) and (y < 0)) or
        ((x < 0) and (y > 0))):
        print("-", end = "");
        if x < 0:
            x = -x;
        if y < 0:
            y = -y;

    # Integral division
    d = x / y;

    # Now one by print digits
    # after dot using school
    # division method.
    for i in range(0, n + 1):
        print(d);
        x = x - (y * d);
        if x == 0:
            break;
        x = x * 10;
        d = x / y;
        if (i == 0):
            print(".", end = "");

# Driver Code
x = 22;
y = 7;
n = 15;
precisionCompute(x, y, n);

# This code is contributed by mits
```

## java 描述语言

```
<script>

// JavaScript program to compute division upto n
// decimal places.

    function precisionCompute(x, y, n)
    {
        // Base cases
        if (y == 0) {
            document.write("Infinite");
            return;
        }
        if (x == 0) {
            document.write("0");
            return;
        }
        if (n <= 0) {
            // Since n <= 0, don't compute after
            // the decimal
            document.write(x / y);
            return;
        }

        // Handling negative numbers
        if (((x > 0) && (y < 0)) || ((x < 0) && (y > 0))) {
            document.write("-");
            x = x > 0 ? x : -x;
            y = y > 0 ? y : -y;
        }

        // Integral division
        let d = x / y;

        // Now one by print digits after dot
        // using school division method.
        for (let i = 0; i <= n; i++) {
            document.write(d);
            x = x - (y * d);
            if (x == 0)
                break;
            x = x * 10;
            d = x / y;
            if (i == 0)
                document.write(".");
        }
    }

// Driver code

        let x = 22, y = 7, n = 15;
        precisionCompute(x, y, n);

</script>
```

**输出:**

```
3.142857142857142
```