# 方程 x = b*(sumofdigits(x)^a)+c 的积分解数量

> 原文:[https://www . geeksforgeeks . org/方程式积分解数-x-bsumofdigitsxac/](https://www.geeksforgeeks.org/number-of-integral-solutions-for-equation-x-bsumofdigitsxac/)

给定作为等式 **x = b * ( sumdigits(x) ^ a ) + c** 一部分的 a、b 和 c。
其中 sumdigits(x)确定数字 x 的所有数字的和，任务是找出满足方程的 x 的所有整数解，并按递增顺序打印出来。
鉴于此，1<= x<= 10<sup>9</sup>
**例:**

> **输入:** a = 3，b = 2，c = 8
> **输出:**10 2008 13726
> x 的值为:10 2008 13726。对于 10，s(x)是 1；将 s(x)的值放入方程 b*(s(x)^a)+c，我们得到 10，由于 10 位于范围 0 < x < 1e+9，因此 10 是一个可能的答案，类似于 2008 年和 13726 年。对于给定值 a、b 和 c
> **没有其他 x 值满足方程输入:** a = 2，b = 2，c = -1
> **输出:** 1 31 337 967
> 满足方程的 x 值为:1 31 337 967

**方法:** *sumdigits(x)* 可以在给定的 X 范围内 **1 < =s(X) < =81** ，即 **0 < x < 1e+9。**这是因为 x 的值可以最小为 0，其中 *sumdigits(x)* =0，最大为 999999999，其中 s *umdigits(x)* 为 81。所以首先迭代 1 到 81，从给定的等式中找到 x，然后交叉检查找到的数字的位数总和是否与 sumdigits(x)的值相同。如果两者相同，则增加计数器并将结果存储在数组中。
以下是上述方法的实施:

## C++

```
// C++ program to find the numbers of
// values that satisfy the equation
#include <bits/stdc++.h>
using namespace std;

// This function returns the sum of
// the digits of a number
int getsum(int a)
{
    int r = 0, sum = 0;
    while (a > 0) {
        r = a % 10;
        sum = sum + r;
        a = a / 10;
    }
    return sum;
}

// This function creates
// the array of valid numbers
void value(int a, int b, int c)
{
    int co = 0, p = 0;
    int no, r = 0, x = 0, q = 0, w = 0;
    vector<int> v;

    for (int i = 1; i < 82; i++) {

        // this computes s(x)^a
        no = pow((double)i, double(a));

        // this gives the result of equation
        no = b * no + c;

        if (no > 0 && no < 1000000000) {
            x = getsum(no);

            // checking if the sum same as i
            if (x == i) {

                // counter to keep track of numbers
                q++;

                // resultant array
                v.push_back(no);
                w++;
            }
        }
    }

    // prints the number
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
}

// Driver Code
int main()
{
    int a = 2, b = 2, c = -1;

    // calculate which value
    // of x are possible
    value(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the numbers of
// values that satisfy the equation
import java.util.Vector;

class GFG
{

// This function returns the sum of
// the digits of a number
static int getsum(int a)
{
    int r = 0, sum = 0;
    while (a > 0)
    {
        r = a % 10;
        sum = sum + r;
        a = a / 10;
    }
    return sum;
}

// This function creates
// the array of valid numbers
static void value(int a, int b, int c)
{
    int co = 0, p = 0;
    int no, r = 0, x = 0, q = 0, w = 0;
    Vector<Integer> v = new Vector<Integer>();

    for (int i = 1; i < 82; i++)
    {

        // this computes s(x)^a
        no = (int) Math.pow(i, a);

        // this gives the result of equation
        no = b * no + c;

        if (no > 0 && no < 1000000000)
        {
            x = getsum(no);

            // checking if the sum same as i
            if (x == i)
            {

                // counter to keep track of numbers
                q++;

                // resultant array
                v.add(no);
                w++;
            }
        }
    }

    // prints the number
    for (int i = 0; i < v.size(); i++)
    {
        System.out.print(v.get(i)+" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int a = 2, b = 2, c = -1;

    // calculate which value
    // of x are possible
    value(a, b, c);
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to find the numbers
# of values that satisfy the equation

# This function returns the sum
# of the digits of a number
def getsum(a):

    r = 0
    sum = 0
    while (a > 0) :
        r = a % 10
        sum = sum + r
        a = a // 10

    return sum

# This function creates
# the array of valid numbers
def value(a, b, c):

    x = 0
    q = 0
    w = 0
    v = []

    for i in range(1, 82) :

        # this computes s(x)^a
        no = pow(i, a)

        # this gives the result
        # of equation
        no = b * no + c

        if (no > 0 and no < 1000000000) :
            x = getsum(no)

            # checking if the sum same as i
            if (x == i) :

                # counter to keep track
                # of numbers
                q += 1

                # resultant array
                v.append(no)
                w += 1

    # prints the number
    for i in range(len(v)) :
        print(v[i], end = " ")

# Driver Code
if __name__ == "__main__":

    a = 2
    b = 2
    c = -1

    # calculate which value
    # of x are possible
    value(a, b, c)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the numbers of
// values that satisfy the equation
using System;
using System.Collections.Generic;

class GFG
{

    // This function returns the sum of
    // the digits of a number
    static int getsum(int a)
    {
        int r = 0, sum = 0;
        while (a > 0)
        {
            r = a % 10;
            sum = sum + r;
            a = a / 10;
        }
        return sum;
    }

    // This function creates
    // the array of valid numbers
    static void value(int a, int b, int c)
    {
        int no, x = 0, q = 0, w = 0;
        List<int> v = new List<int>();

        for (int i = 1; i < 82; i++)
        {

            // this computes s(x)^a
            no = (int) Math.Pow(i, a);

            // this gives the result of equation
            no = b * no + c;

            if (no > 0 && no < 1000000000)
            {
                x = getsum(no);

                // checking if the sum same as i
                if (x == i)
                {

                    // counter to keep track of numbers
                    q++;

                    // resultant array
                    v.Add(no);
                    w++;
                }
            }
        }

        // prints the number
        for (int i = 0; i < v.Count; i++)
        {
            Console.Write(v[i]+" ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int a = 2, b = 2, c = -1;

        // calculate which value
        // of x are possible
        value(a, b, c);
    }
}

// This code has been contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the numbers of
// values that satisfy the equation

// This function returns the sum of
// the digits of a number
function getsum($a)
{
    $r = 0;
    $sum = 0;
    while ($a > 0)
    {
        $r = $a % 10;
        $sum = $sum + $r;
        $a = (int)($a / 10);
    }
    return $sum;
}

// This function creates
// the array of valid numbers
function value($a, $b, $c)
{
    $co = 0;
    $p = 0;
    $no;
    $r = 0;
    $x = 0;
    $q = 0;
    $w = 0;
    $v = array();
    $u = 0;

    for ($i = 1; $i < 82; $i++)
    {

        // this computes s(x)^a
        $no = pow($i, $a);

        // this gives the result
        // of equation
        $no = $b * $no + $c;

        if ($no > 0 && $no < 1000000000)
        {
            $x = getsum($no);

            // checking if the
            // sum same as i
            if ($x == $i)
            {

                // counter to keep
                // track of numbers
                $q++;

                // resultant array
                $v[$u++] = $no;
                $w++;
            }
        }
    }

    // prints the number
    for ($i = 0; $i < $u; $i++)
    {
        echo $v[$i] . " ";
    }
}

// Driver Code
$a = 2;
$b = 2;
$c = -1;

// calculate which value
// of x are possible
value($a, $b, $c);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the numbers of
// values that satisfy the equation

    // This function returns the sum of
// the digits of a number
    function getsum(a)
    {
    let r = 0, sum = 0;
    while (a > 0)
    {
        r = a % 10;
        sum = sum + r;
        a = Math.floor(a / 10);
    }
    return sum;
    }

    // This function creates
   // the array of valid numbers
    function value(a,b,c)
    {
        let co = 0, p = 0;
    let no, r = 0, x = 0, q = 0, w = 0;
    let v = [];

    for (let i = 1; i < 82; i++)
    {

        // this computes s(x)^a
        no =  Math.pow(i, a);

        // this gives the result of equation
        no = b * no + c;

        if (no > 0 && no < 1000000000)
        {
            x = getsum(no);

            // checking if the sum same as i
            if (x == i)
            {

                // counter to keep track of numbers
                q++;

                // resultant array
                v.push(no);
                w++;
            }
        }
    }

    // prints the number
    for (let i = 0; i < v.length; i++)
    {
        document.write(v[i]+" ");
    }
    }

    // Driver Code
    let a = 2, b = 2, c = -1;
    // calculate which value
    // of x are possible
    value(a, b, c);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1 31 337 967
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)