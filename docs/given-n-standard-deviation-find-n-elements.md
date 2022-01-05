# 给定 N 和标准差，找到 N 个元素

> 原文:[https://www . geesforgeks . org/given-n-标准差-find-n-elements/](https://www.geeksforgeeks.org/given-n-standard-deviation-find-n-elements/)

给定 N 和[标准差](https://en.wikipedia.org/wiki/Standard_deviation)求 N 个元素。

> 平均值是元素的平均值。
> **表示 arr【0】的**..n-1]=σ(arr[I])/n
> 其中 0 < = i < n
> 方差是平均值除以元素数的平方差之和。
> **方差**=σ(arr[I]–均值) <sup>2</sup> / n
> 标准差为方差的平方根
> **标准差**=σ(方差)
> 详见[均值、方差和标准差](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)。

**示例:**

```
Input: 6 0 
Output: 0 0 0 0 0 0  
Explanation: 
The standard deviation of 0, 0, 0, 0, 0, 0 is 0\. 
Also the standard deviation of 4, 4, 4, 4, 4, 4 
is 0, we print any of the possible N elements.

Input: 3 3
Output: 0 -3.67423 3.67423 
Explanation: 
On calculating SD of these N elements,
we get standard deviation to be 3\. 

```

**进场:**
如果我们看公式，我们有两个未知项一个是 xi，另一个是均值。主要动机是使平均值为 0，这样我们就可以得到 X 元素的公式。会有两种情况，一种是偶数，一种是奇数。

**当 N 为偶数时:**
要使 N 元素的平均值为 0，最好的方法是将 N 元素表示为-X +X -X +X。公式将是 sqrt(x^2)/n、x2+x^2+x^2+………N 项之和)，所以公式原来是 sqrt (N*(x^2)/N).n 相互抵消，所以 sqrt (x^2)变成了 SD。所以，我们得到 N 元素为 **-SD +SD -SD +SD……** 得到平均值 0。我们需要打印-标清+标清-标清+标清……

**N 为奇数时:**
N 元素的平均值为 0。所以，一个元素是 0，其他 N-1 个元素是-X +X -X。公式将是 sqrt(x^2)/n、x2+x^2+x^2+………N-1 项之和，所以公式原来是 sqrt((N-1)*(x^2)/N)，所以
X= SD * sqrt(n/(n-1))。n 个元素是 0-X+X-X+X……
当 SD 为 0 时，那么所有元素都是相同的，所以我们可以为其打印 0。

下面是上述方法的实现:

## C++

```
// CPP program to find n elements
#include <bits/stdc++.h>
using namespace std;

// function to print series of n elements
void series(int n, int d)
{

    // if S.D. is 0 then print all
    // elements as 0.
    if (d == 0) {

        // print n 0's
        for (int i = 0; i < n; i++)
            cout << "0 ";

        cout << endl;
        return;
    }

    // if S.D. is even
    if (n % 2 == 0) {

        // print -SD, +SD, -SD, +SD
        for (int i = 1; i <= n; i++) {
            cout << pow(-1, i) * d << " ";
        }
        cout << endl;
    }
    else // if odd
    {
        // convert n to a float integer
        float m = n;
        float r = (m / (m - 1));
        float g = (float)(d * (float)sqrtf(r));

        // print one element to be 0
        cout << "0 ";

        // print (n-1) elements as xi derived
        // from the formula
        for (int i = 1; i < n; i++) {
            cout << pow(-1, i) * g << " ";
        }
        cout << endl;
    }
}

// driver program to test the above function
int main()
{
    int n = 3, d = 3;
    series(n, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n elements
import java.util.*;
import java.lang.*;

public class GfG {

    // function to print series of n elements
    public static void series(int n, int d)
    {

        // if S.D. is 0 then print all
        // elements as 0.
        if (d == 0) {

            // print n 0's
            for (int i = 0; i < n; i++)
                System.out.print("0 ");
            System.out.println();
            return;
        }

        // if S.D. is even
        if (n % 2 == 0) {

            // print -SD, +SD, -SD, +SD
            for (int i = 1; i <= n; i++) {
                System.out.print(Math.pow(-1, i) * d + " ");
            }
            System.out.println();
        }
        else // if odd
        {
            // convert n to a float integer
            float m = n;
            float r = (m / (m - 1));
            float g = (float)(d * (float)(Math.sqrt(r)));

            // print one element to be 0
            System.out.print("0 ");

            // print (n-1) elements as xi
            // derived from the formula
            for (int i = 1; i < n; i++) {
                System.out.print(Math.pow(-1, i) * g + " ");
            }
            System.out.println();
        }
    }

    // driver function
    public static void main(String args[])
    {
        int n = 3, d = 3;
        series(n, d);
    }
}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python program to find n elements
import math

# function to print series of n elements
def series( n, d):

    # if S.D. is 0 then print all
    # elements as 0.
    if d == 0:

        # print n 0's
        for i in range(n):
            print("0", end = ' ')
        return 1

    # if S.D. is even
    if n % 2 == 0:

        # print -SD, +SD, -SD, +SD
        i = 1
        while i <= n:
            print("%.5f"%((math.pow(-1, i) * d)),
                  end =' ')
            i += 1
    else:
        # if odd
        # convert n to a float integer
        m = n
        r = (m / (m - 1))
        g = (float)(d * float(math.sqrt(r)))

        # print one element to be 0
        print("0 ", end = ' ')

        # print (n-1) elements as xi derived
        # from the formula
        i = 1
        while i < n:
            print("%.5f"%(math.pow(-1, i) * g),
                  end = ' ')
            i = i + 1
    print("\n")

# driver code to test the above function
n = 3
d = 3
series(n, d)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find n elements
using System;

public class GfG {

    // function to print series of n
    // elements
    public static void series(int n, int d)
    {

        // if S.D. is 0 then print all
        // elements as 0.
        if (d == 0) {

            // print n 0's
            for (int i = 0; i < n; i++)
                Console.Write("0");

            Console.WriteLine();

            return;
        }

        // if S.D. is even
        if (n % 2 == 0) {

            // print -SD, +SD, -SD, +SD
            for (int i = 1; i <= n; i++) {
                Console.Write(Math.Pow(-1, i)
                                   * d + " ");
            }

            Console.WriteLine();
        }
        else // if odd
        {

            // convert n to a float integer
            float m = n;
            float r = (m / (m - 1));
            float g = (float)(d *
                       (float)(Math.Sqrt(r)));

            // print one element to be 0
            Console.Write("0 ");

            // print (n-1) elements as xi
            // derived from the formula
            for (int i = 1; i < n; i++) {
                Console.Write(Math.Pow(-1, i)
                                   * g + " ");
            }

            Console.WriteLine();
        }
    }

    // driver function
    public static void Main()
    {
        int n = 3, d = 3;

        series(n, d);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n elements

// function to print
// series of n elements
function series( $n, $d)
{

    // if S.D. is 0 then print all
    // elements as 0.
    if ($d == 0)
    {

        // print n 0's
        for ($i = 0; $i < $n;$i++)
            echo "0 ";

        echo "\n";
        return;
    }

    // if S.D. is even
    if ($n % 2 == 0)
    {

        // print -SD, +SD, -SD, +SD
        for ( $i = 1; $i <= $n; $i++)
        {
            echo pow(-1, $i) * $d , " ";
        }
        echo"\n";
    }

    // if odd
    else
    {

        // convert n to a
        // float integer
        $m = $n;
        $r = ($m / ($m - 1));
        $g = ($d * sqrt($r));

        // print one element
        // to be 0
        echo "0 ";

        // print (n-1) elements
        // as xi derived
        // from the formula
        for ($i = 1; $i < $n; $i++)
        {
            echo pow(-1, $i) * $g , " ";
        }
        echo"\n";
    }
}

    // Driver Code
    $n = 3; $d = 3;
    series($n, $d);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find n elements

// Function to print series of n elements
function series(n, d)
{

    // If S.D. is 0 then print all
    // elements as 0.
    if (d == 0)
    {

        // Print n 0's
        for(let i = 0; i < n; i++)
            document.write("0 ");

        document.write();
        return;
    }

    // If S.D. is even
    if (n % 2 == 0)
    {

        // Print -SD, +SD, -SD, +SD
        for(let i = 1; i <= n; i++)
        {
            document.write(Math.pow(-1, i) * d + "  ");
        }
        document.write();
    }

    // If odd
    else
    {

        // Convert n to a float integer
        let m = n;
        let r = (m / (m - 1));
        let g = (d * (Math.sqrt(r)));

        // Print one element to be 0
        document.write("0 ");

        // Print (n-1) elements as xi
        // derived from the formula
        for(let i = 1; i < n; i++)
        {
            document.write(Math.pow(-1, i) * g + "  ");
        }
        document.write();
    }
}

// Driver Code
let n = 3, d = 3;

series(n, d);

// This code is contributed by susmitakundugoaldanga

</script>
```

输出:

```
0 -3.67423 3.67423 
```