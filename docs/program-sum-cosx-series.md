# cos(x)系列之和程序

> 原文:[https://www.geeksforgeeks.org/program-sum-cosx-series/](https://www.geeksforgeeks.org/program-sum-cosx-series/)

给定 n 和 x，其中 n 是级数中的项数，x 是角度的度数。
用级数展开公式计算 x 的余弦值，并与库函数的输出进行比较的程序。

**所用公式:**
cos x = 1 –( x<sup>2</sup>/2！)+ (x <sup>4</sup> / 4！)–(x<sup>6</sup>/6！) +…

**示例:**

```
Input : n = 3
        x = 90
Output : Sum of the cosine series is =  -0.23
The value using library function is = -0.000204

Input : n = 4
        x = 45
Output : 
Sum of the cosine series is = 0.71
The value using library function is = 0.707035
```

## C++

```
// CPP program to find the
// sum of cos(x) series
#include <bits/stdc++.h>
using namespace std;

const double PI = 3.142;

double cosXSertiesSum(double x, int n)
{
    // here x is in degree.
    // we have to convert it to radian
    // for using it with series formula,
    // as in series expansion angle is in radian

    x = x * (PI / 180.0);

    double res = 1;
    double sign = 1, fact = 1, pow = 1;
    for (int i = 1; i < 5; i++) {
        sign = sign * -1;
        fact = fact * (2 * i - 1) * (2 * i);
        pow = pow * x * x;
        res = res + sign * pow / fact;
    }

    return res;
}

// Driver Code
int main()
{
    float x = 50;
    int n = 5;
    cout << cosXSertiesSum(x, 5);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the sum of cos(x) series
import java.lang.Math.*;

class GFG
{
    static final double PI = 3.142;

    static double cosXSertiesSum(double x,
                                 int n)
    {
          // here x is in degree.
        // we have to convert it to radian
        // for using it with series formula,
        // as in series expansion angle is in radian

        x = x * (PI / 180.0);

        double res = 1;
        double sign = 1, fact = 1,
                         pow = 1;
        for (int i = 1; i < 5; i++)
        {
            sign = sign * -1;
            fact = fact * (2 * i - 1) *
                               (2 * i);
            pow = pow * x * x;
            res = res + sign * pow / fact;
        }

        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        float x = 50;
        int n = 5;
        System.out.println((float)(
            cosXSertiesSum(x, 5) * 1000000) /
                                 1000000.00);
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python3 program to find the
# sum of cos(x) series

PI = 3.142;

def cosXSertiesSum(x, n):

    # here x is in degree.
    # we have to convert it to radian
    # for using it with series formula,
    # as in series expansion angle is in radian

    x = x * (PI / 180.0);

    res = 1;
    sign = 1;
    fact = 1;
    pow = 1;

    for i in range(1,5):
        sign = sign * (-1);
        fact = fact * (2 * i - 1) * (2 * i);
        pow = pow * x * x;
        res = res + sign * pow / fact;

    return res;

# Driver Code
x = 50;
n = 5;
print(round(cosXSertiesSum(x, 5), 6));

# This code is contributed by mits
```

## C#

```
// C# program to find the
// sum of cos(x) series
using System;

class GFG
{
    static double PI = 3.142;

    static double cosXSertiesSum(double x,
                                 int n)
    {
          // here x is in degree.
        // we have to convert it to radian
        // for using it with series formula,
        // as in series expansion angle is in radian

          x = x * (PI / 180.0);

        double res = 1;
        double sign = 1, fact = 1,
                         pow = 1;
        for (int i = 1; i < 5; i++)
        {
            sign = sign * -1;
            fact = fact * (2 * i - 1) *
                               (2 * i);
            pow = pow * x * x;
            res = res + sign * pow / fact;
        }

        return res;
    }

    // Driver Code
    public static void Main()
    {
        float x = 50;
        int n = 5;
        Console.Write((float)(cosXSertiesSum(x, n) *
                             1000000) / 1000000.00);
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// sum of cos(x) series

$PI = 3.142;

function cosXSertiesSum($x, $n)
{
    global $PI;

    // here x is in degree.
    // we have to convert it to radian
    // for using it with series formula,
    // as in series expansion angle is in radian

    $x = $x * ($PI / 180.0);

    $res = 1;
    $sign = 1; $fact = 1;
               $pow = 1;
    for ( $i = 1; $i < 5; $i++)
    {
        $sign = $sign * -1;
        $fact = $fact * (2 * $i - 1) *
                             (2 * $i);
        $pow = $pow * $x * $x;
        $res = $res + $sign * $pow /
                              $fact;
    }

    return $res;
}

// Driver Code
$x = 50;
$n = 5;
echo cosXSertiesSum($x, 5);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the sum of cos(x) series

const  PI = 3.142;

    function cosXSertiesSum( x, n) {
        // here x is in degree.
        // we have to convert it to radian
        // for using it with series formula,
        // as in series expansion angle is in radian

        x = x * (PI / 180.0);

        let res = 1;
        let sign = 1, fact = 1, pow = 1,i;
        for ( i = 1; i < 5; i++) {
            sign = sign * -1;
            fact = fact * (2 * i - 1) * (2 * i);
            pow = pow * x * x;
            res = res + sign * pow / fact;
        }

        return res;
    }

    // Driver Code

        let x = 50;
        let n = 5;
        document.write( ((cosXSertiesSum(x, 5) * 1000000) / 1000000.00).toFixed(6));

// This code is contributed by shikhasingrajput

</script>
```

**Output :** 

```
0.642701
```

请注意，我们也可以使用库函数找到 cos(x)。

## C++

```
// C++ code to illustrate
// the use of cos function
#include <bits/stdc++.h>
using namespace std;

#define PI 3.14159265

int main ()
{
    double x, ret, val;

    x = 60.0;
    val = PI / 180.0;
    ret = cos(x * val);
    cout << "The cosine of " << fixed
         << setprecision(6) << x << " is ";
    cout << fixed << setprecision(6)
         << ret << " degrees" << endl;

    x = 90.0;
    val = PI / 180.0;
    ret = cos(x * val);
    cout << "The cosine of " << fixed
         << setprecision(6) << x << " is ";
    cout << fixed << setprecision(6)
         << ret << " degrees" << endl;

    return(0);
}

// This code is contributed by shubhamsingh10
```

## C

```
// C code to illustrate
// the use of cos function
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
double x, ret, val;

x = 60.0;
val = PI / 180.0;
ret = cos( x * val );
printf("The cosine of %lf is ", x);
printf("%lf degrees\n", ret);

x = 90.0;
val = PI / 180.0;
ret = cos( x*val );
printf("The cosine of %lf is ", x);
printf("%lf degrees\n", ret);

return(0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to illustrate
// the use of cos function
import java.io.*;

class GFG
{
static final double PI = 3.142;
public static void main (String[] args)
{
    double x, ret, val;

    x = 60.0;
    val =(int)PI / 180.0;
    ret = Math.cos(x * val);
    System.out.print("The cosine of " +
                           x + " is ");
    System.out.print(ret);
    System.out.println(" degrees");

    x = 90.0;
    val = (int)PI / 180.0;
    ret = Math.cos( x*val );
    System.out.print("The cosine of " +
                           x + " is ");
    System.out.print(ret);
    System.out.println(" degrees");
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 code to illustrate
# the use of cos function
import math

if __name__=='__main__':
    PI = 3.14159265

    x = 60.0
    val = PI / 180.0
    ret = math.cos(x * val)
    print("The cosine of is ", x, end=" ")
    print(" degrees", ret)

    x = 90.0
    val = PI / 180.0
    ret = math.cos(x * val)
    print("The cosine of is ", x, end=" ")
    print("degrees", ret)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# code to illustrate
// the use of cos function
using System;

class GFG
{

// Constant PI Declaration
static double PI = 3.142;

// Driver Code
static public void Main ()
{
    double x, ret, val;

    x = 60.0;
    val = (int)PI / 180.0;
    ret = Math.Cos(x * val);
    Console.Write("The cosine of " +
                        x + " is ");
    Console.Write(ret);
    Console.WriteLine(" degrees");

    x = 90.0;
    val = (int)PI / 180.0;
    ret = Math.Cos(x * val);
    Console.Write("The cosine of " +
                        x + " is ");
    Console.Write(ret);
    Console.WriteLine(" degrees");
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP code to illustrate
// the use of cos function

$PI =3.14159265;

$x; $ret; $val;

$x = 60.0;
$val = $PI / 180.0;
$ret = cos( $x * $val );
echo "The cosine of is ", $x;
echo "degrees", $ret;
echo "\n";

$x = 90.0;
$val = $PI / 180.0;
$ret = cos( $x * $val );
echo "The cosine of is ", $x;
echo "degrees ", $ret;

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// javascript code to illustrate
// the use of cos function
    var PI = 3.142;

    var x, ret, val;

    x = 60.0;
    val = PI / 180.0;
    ret = Math.cos(x * val);
    document.write("The cosine of " +
                           x + " is ");
    document.write(ret.toFixed(5));
    document.write(" degrees");
    document.write("<br>") 

    x = 90.0;
    val = PI / 180.0;
    ret = parseInt(Math.cos( x*val ));
    document.write("The cosine of " +
                           x + " is ");
    document.write(ret.toFixed(5));
    document.write(" degrees");

// This code contributed by shikhasingrajput

</script>
```

**Output :** 

```
The cosine of 60.000000 is 0.500000 degrees
The cosine of 90.000000 is 0.000000 degrees
```