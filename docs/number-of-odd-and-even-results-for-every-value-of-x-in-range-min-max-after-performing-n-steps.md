# 执行 N 步

后，范围[最小，最大]内每个 x 值的奇数和偶数结果数

> 原文:[https://www . geeksforgeeks . org/执行 n 步后范围内 x 的每个值的奇数和偶数结果数/](https://www.geeksforgeeks.org/number-of-odd-and-even-results-for-every-value-of-x-in-range-min-max-after-performing-n-steps/)

给定一个数字 N 以及最小和最大范围。分别给定 *a* 和 *b* 的 N 值。任务是在执行如下所述的一系列 N 次运算后，计算偶数/奇数结果的数量。
在每一步，计算:

> **y<sub>N</sub>= a<sub>N</sub>y<sub>N-1</sub>+b<sub>N</sub>T9】。**

**说明:**

*   第一步:y<sub>1</sub>= a<sub>1</sub>x+b<sub>1</sub>
*   第二步:y<sub>2</sub>= a<sub>2</sub>y<sub>1</sub>+b<sub>2</sub>T8】=>y<sub>2</sub>= a<sub>2</sub>a<sub>1</sub>x+a<sub>2</sub>b<sub>1</sub>+b<sub>2</sub>
*   第三步:y<sub>3</sub>= a<sub>3</sub>y<sub>2</sub>+b<sub>3</sub>T8】=>y<sub>3</sub>= a<sub>3</sub>a<sub>2</sub>a<sub>1</sub>x+a<sub>3</sub>a<sub>2</sub>b<sub>1</sub>+a
*   第 n 步:y<sub>n</sub>= a<sub>n</sub>y<sub>n-1</sub>+b<sub>n</sub>

要获得最终结果，将 y <sub>0</sub> 的值作为[min，mix]范围内的每个值。为简单起见，我们假设 y <sub>0</sub> 的值为 x，并用最终方程中[最小值，最大值]范围内的所有可能值替换 x 来计算结果。

**示例:**

```
Input: n = 2,  min = 1, max = 4 
       a = 1, b = 2 
       a = 3, b = 4 
Output: even = 2, odd = 2\. 

Step1: y = 1x + 2 = x+2 
Step2: y =  3(x+2) + 4 = 3x + 10 
Putting all values of in range [1, 4], 
2 odd values and 2 even values are obtained. 

Input: n = 1, min = 4, max = 60
       a= 1, b = 2

Output: even = 29, odd = 28
```

A **天真的方法**将 a 和 b 的值存储在一个数组中，并计算指定范围内每个数字的最终结果。如果结果为偶数，则偶数计数递增。否则，奇数计数递增。

这里使用的一种**有效方法**是这样一个基本概念，即两个数的乘积是偶数，否则是奇数，并且只有当两个数都是偶数时，两个数的和才是偶数。这里可以看到，在每一步中，一个数与 x 相乘，另一个常数被加到乘积中。任务是检查结果是偶数还是奇数。在计算的最后一步，检查 a<sub>1</sub>a<sub>2</sub>a<sub>3</sub>…a<sub>n</sub>是否为偶数/奇数，a<sub>2</sub>a<sub>3</sub>…a<sub>n</sub>b<sub>1</sub>+a<sub>3</sub>a<sub>4</sub>a<sub>n</sub>b【T27 检查 a<sub>1</sub>a<sub>2</sub>a<sub>3</sub>…a<sub>n</sub>是否为偶数/奇数:
如果任意 a <sub>i</sub> 为偶数，则积始终为偶数，否则为奇数。检查 a<sub>2</sub>a<sub>3</sub>…a<sub>n</sub>b<sub>1</sub>+a<sub>3</sub>a<sub>4</sub>…a<sub>n</sub>b<sub>2</sub>+…+b<sub>n</sub>是否为偶数/奇数:

下表解释了系数的各种可能性:

<figure class="table">

| a<sub>2</sub>a<sub>3</sub>…a<sub>I-1</sub>b<sub>1</sub>+a<sub>3</sub>a<sub>4</sub>…a<sub>I-1</sub>b<sub>2</sub>+…+b<sub>I-1</sub> | a <sub>i</sub> | b <sub>i</sub> | a<sub>2</sub>a<sub>3</sub>…a<sub>I</sub>b<sub>1</sub>+a<sub>3</sub>a<sub>4</sub>…a<sub>I</sub>b<sub>2</sub>+…+b<sub>I</sub> |
| --- | --- | --- | --- |
| 奇数的 | 奇数的 | 奇数的 | 甚至 |
| 奇数的 | 奇数的 | 甚至 | 奇数的 |
| 奇数的 | 甚至 | 奇数的 | 奇数的 |
| 奇数的 | 甚至 | 甚至 | 甚至 |
| 甚至 | 奇数的 | 奇数的 | 奇数的 |
| 甚至 | 奇数的 | 甚至 | 甚至 |
| 甚至 | 甚至 | 奇数的 | 奇数的 |
| 甚至 | 甚至 | 甚至 | 甚至 |

下表解释了 y = ax + b 的所有各种可能性:

<figure class="table">

| x | a | b | y |
| --- | --- | --- | --- |
| 奇数的 | 奇数的 | 奇数的 | 甚至 |
| 奇数的 | 奇数的 | 甚至 | 奇数的 |
| 奇数的 | 甚至 | 奇数的 | 奇数的 |
| 奇数的 | 甚至 | 甚至 | 甚至 |
| 甚至 | 奇数的 | 奇数的 | 奇数的 |
| 甚至 | 奇数的 | 甚至 | 甚至 |
| 甚至 | 甚至 | 奇数的 | 奇数的 |
| 甚至 | 甚至 | 甚至 | 甚至 |

不要遍历[min，max]范围内的所有数字，而是将其分成两部分，检查该范围内的数字是偶数还是奇数，因为所有偶数输入都有相同的结果，所有奇数输入都有相同的结果。因此，检查一种情况，并将其乘以范围内的偶数和奇数。

进行上述计算，检查最后一步的 x 系数。

*   如果是偶数，则*为真，否则为假。*
*   如果常数为偶数，则*为真，否则为假。*
*   x 的系数是偶数，a 的任何一个值在任何一层都是偶数。
*   最后一层后的常数项如果被执行，则借助于 beven 的值以及当前的 a 和 b 来检查。

借助于上面给出的表格(第一个)，测试每一层的常数，并相应地更新 *beven* 的值。

**假设 x 为偶数，则奇偶的值被初始化。**

1.  如果 x 是偶数，那么 ax 将总是偶数，而不考虑 a。因此，根据常数项的值，结果将是偶数或奇数。
2.  如果常数为偶数，则结果为偶数，因此偶数由给定范围(max/2 –( min-1)/2)内的偶数初始化，奇数由零初始化。
3.  如果常数为奇数，则结果为奇数，因此奇数由给定范围(max/2 –( min-1)/2)内的偶数初始化，偶数由零初始化。

**假设 x 为奇数，则更新奇偶的值。**

1.  如果 a 是奇数，ax 就是奇数。如果 a 是偶数，斧头就是偶数。
2.  如果 ax 和常数都是奇数，或者 ax 和常数都是偶数，那么结果是偶数，因此偶数在给定范围**(max–min+1–偶数)**内增加奇数。
3.  如果 ax 是偶数，常数是奇数，或者 ax 是奇数，常数是奇数，那么结果是奇数，因此奇数的数量在给定的范围内增加奇数的数量**(最大–最小+1–偶数的数量)。**

下面是上述方法的实现:

## C++

```
// C++ program to print
// Number of odd/even results for
// every value of x in range [min, end]
// after performing N steps
#include <bits/stdc++.h>
using namespace std;

// Function that prints the
// number of odd and even results
void count_even_odd(int min, int max, int steps[][2])
{
    int a, b, even, odd;

    // If constant at layer i is even, beven is true,
    // otherwise false. If the coefficient of x at
    // layer i is even, aeven is true, otherwise false.
    bool beven = true, aeven = false;
    int n = 2;
    for (int i = 0; i < n; i++) {

        a = steps[i][0], b = steps[i][1];

        // If any of the coefficients at any layer is found
        // to be even, then the product of all the
        // coefficients will always be even.

        if (!(aeven || a & 1))
            aeven = true;

        // Checking whether the constant added after all
        // layers is even or odd.

        if (beven) {
            if (b & 1)
                beven = false;
        }
        else if (!(a & 1)) {
            if (!(b & 1))
                beven = true;
        }
        else {
            if (b & 1)
                beven = true;
        }
    }

    // Counting the number of even and odd.

    // Assuming input x is even.
    if (beven) {
        even = (int)max / 2 - (int)(min - 1) / 2;
        odd = 0;
    }
    else {
        even = (int)max / 2 - (int)(min - 1) / 2;
        odd = 0;
    }

    // Assuming input x is odd.
    if (!(beven ^ aeven))
        even += max - min + 1 - (int)max / 2
                + (int)(min - 1) / 2;
    else
        odd += max - min + 1 - (int)max / 2
               + (int)(min - 1) / 2;

    // Displaying the counts.
    cout << "even = " << even << ", odd = " << odd << endl;
}

// Driver Code
int main()
{
    int min = 1, max = 4;
    int steps[][2] = { { 1, 2 },
                       { 3, 4 } };

    count_even_odd(min, max, steps);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// Number of odd/even
// results for every value
// of x in range [min, end]
// after performing N steps
import java.io.*;

class GFG
{

// Function that prints
// the number of odd and
// even results
static void count_even_odd(int min,
                           int max,
                           int steps[][])
{
    int a, b, even, odd;

    // If constant at layer i
    // is even, beven is true,
    // otherwise false. If the
    // coefficient of x at layer
    // i is even, aeven is true,
    // otherwise false.
    boolean beven = true,
            aeven = false;
    int n = 2;
    for (int i = 0; i < n; i++)
    {

        a = steps[i][0];
        b = steps[i][1];

        // If any of the coefficients
        // at any layer is found to be
        // even, then the product of
        // all the coefficients will
        // always be even.
        if (!(aeven || (a & 1) > 0))
            aeven = true;

        // Checking whether the
        // constant added after all
        // layers is even or odd.
        if (beven)
        {
            if ((b & 1) > 0)
                beven = false;
        }
        else if (!((a & 1) > 0))
        {
            if (!((b & 1) > 0))
                beven = true;
        }
        else
        {
            if ((b & 1) > 0)
                beven = true;
        }
    }

    // Counting the number
    // of even and odd.

    // Assuming input x is even.
    if (beven)
    {
        even = (int)max / 2 -
               (int)(min - 1) / 2;
        odd = 0;
    }
    else
    {
        even = (int)max / 2 -
               (int)(min - 1) / 2;
        odd = 0;
    }

    // Assuming input x is odd.
    if (!(beven ^ aeven))
        even += max - min + 1 -
                (int)max / 2 +
                (int)(min - 1) / 2;
    else
        odd += max - min + 1 -
               (int)max / 2 +
               (int)(min - 1) / 2;

    // Displaying the counts.
    System.out.print("even = " + even +
                     ", odd = " + odd);
}

// Driver Code
public static void main (String[] args)
{
    int min = 1, max = 4;
    int steps[][] = {{1, 2},
                     {3, 4}};

    count_even_odd(min, max, steps);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to print
# Number of odd/even results
# for every value of x in
# range [min, end] after
# performing N steps

# Function that prints
# the number of odd
# and even results
def count_even_odd(min, max, steps):

    # If constant at layer i
    # is even, beven is True,
    # otherwise False. If
    # the coefficient of x at
    # layer i is even, aeven
    # is True, otherwise False.
    beven = True
    aeven = False
    n = 2
    for i in range(0, n) :
        a = steps[i][0]
        b = steps[i][1]

        # If any of the coefficients
        # at any layer is found to
        # be even, then the product
        # of all the coefficients
        # will always be even.
        if (not(aeven or a & 1)):
            aeven = True

        # Checking whether the
        # constant added after all
        # layers is even or odd.
        if (beven) :
            if (b & 1):
                beven = False

        elif (not(a & 1)) :
            if (not(b & 1)):
                beven = True

        else :
            if (b & 1):
                beven = True

    # Counting the number
    # of even and odd.

    # Assuming input x is even.
    if (beven):
        even = (int(max / 2) -
                int((min - 1) / 2))
        odd = 0

    else :
        even = (int(max / 2) -
                int((min - 1) / 2))
        odd = 0

    # Assuming input x is odd.
    if (not(beven ^ aeven)):
        even += (max - min + 1 -
             int(max / 2) + int((min - 1) / 2))
    else:
        odd += (max - min + 1 -
            int(max / 2) + int((min - 1) / 2))

    # Displaying the counts.
    print("even = " , even ,
          ", odd = " , odd, sep = "")

# Driver Code
min = 1
max = 4
steps = [[1, 2],[3, 4]]
count_even_odd(min, max, steps)

# This code is contributed
# by Smitha
```

## C#

```
// C# program to print
// Number of odd/even
// results for every value
// of x in range [min, end]
// after performing N steps
using System;

class GFG
{

// Function that prints
// the number of odd and
// even results
static void count_even_odd(int min,
                           int max,
                           int [,]steps)
{
    int a, b, even, odd;

    // If constant at layer i
    // is even, beven is true,
    // otherwise false. If the
    // coefficient of x at layer
    // i is even, aeven is true,
    // otherwise false.
    bool beven = true,
         aeven = false;
    int n = 2;
    for (int i = 0; i < n; i++)
    {

        a = steps[i, 0];
        b = steps[i, 1];

        // If any of the coefficients
        // at any layer is found
        // to be even, then the
        // product of all the
        // coefficients will always
        // be even.
        if (!(aeven || (a & 1) > 0))
            aeven = true;

        // Checking whether the
        // constant added after all
        // layers is even or odd.
        if (beven)
        {
            if ((b & 1) > 0)
                beven = false;
        }
        else if (!((a & 1) > 0))
        {
            if (!((b & 1) > 0))
                beven = true;
        }
        else
        {
            if ((b & 1) > 0)
                beven = true;
        }
    }

    // Counting the number
    // of even and odd.

    // Assuming input
    // x is even.
    if (beven)
    {
        even = (int)max / 2 -
               (int)(min - 1) / 2;
        odd = 0;
    }
    else
    {
        even = (int)max / 2 -
            (int)(min - 1) / 2;
        odd = 0;
    }

    // Assuming input
    // x is odd.
    if (!(beven ^ aeven))
        even += max - min + 1 -
                 (int)max / 2 +
                (int)(min - 1) / 2;
    else
        odd += max - min + 1 -
            (int)max / 2 +
            (int)(min - 1) / 2;

    // Displaying the counts.
    Console.Write("even = " + even +
                  ", odd = " + odd);
}

// Driver Code
public static void Main ()
{
    int min = 1, max = 4;
    int [,]steps = {{1, 2},
                    {3, 4}};

    count_even_odd(min, max, steps);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print Number of
// odd/even results for every value
// of x in range [min, end] after
// performing N steps

// Function that prints the
// number of odd and even results
function count_even_odd($min, $max, $steps)
{
    // If constant at layer i is even,
    // beven is true, otherwise false.
    // If the coefficient of x at
    // layer i is even, aeven is true,
    // otherwise false.
    $beven = true;
    $aeven = false;
    $n = 2;
    for ($i = 0; $i < $n; $i++)
    {

        $a = $steps[$i][0];
        $b = $steps[$i][1];

        // If any of the coefficients at
        // any layer is found to be even,
        // then the product of all the
        // coefficients will always be even.
        if (!($aeven || $a & 1))
            $aeven = true;

        // Checking whether the constant
        // added after all layers is even or odd.

        if ($beven)
        {
            if ($b & 1)
                $beven = false;
        }
        else if (!($a & 1))
        {
            if (!($b & 1))
                $beven = true;
        }
        else
        {
            if ($b & 1)
                $beven = true;
        }
    }

    // Counting the number of even and odd.

    // Assuming input x is even.
    if ($beven)
    {
        $even = (int)$max / 2 - (int)($min - 1) / 2;
        $odd = 0;
    }
    else
    {
        $even = (int)$max / 2 - (int)($min - 1) / 2;
        $odd = 0;
    }

    // Assuming input x is odd.
    if (!($beven ^ $aeven))
        $even += $max - $min + 1 - (int)$max / 2 +
                                   (int)($min - 1) / 2;
    else
        $odd += $max - $min + 1 - (int)$max / 2 +
                                  (int)($min - 1) / 2;

    // Displaying the counts.
    echo "even = " , $even,
         ", odd = ", $odd, "\n";
}

// Driver Code
$min = 1;
$max = 4;
$steps = array( array(1, 2 ),
                array(3, 4 ));

count_even_odd($min, $max, $steps);

// This code is contributed
// by Ajit Deshpal
?>
```

## java 描述语言

```
<script>

// Javascript program to print
// Number of odd/even
// results for every value
// of x in range [min, end]
// after performing N steps

// Function that prints
// the number of odd and
// even results
function count_even_odd(min, max, steps)
{
    var a, b, even, odd;

    // If constant at layer i
    // is even, beven is true,
    // otherwise false. If the
    // coefficient of x at layer
    // i is even, aeven is true,
    // otherwise false.
    var beven = true, aeven = false;
    var n = 2;

    for(i = 0; i < n; i++)
    {
        a = steps[i][0];
        b = steps[i][1];

        // If any of the coefficients
        // at any layer is found to be
        // even, then the product of
        // all the coefficients will
        // always be even.
        if (!(aeven || (a & 1) > 0))
            aeven = true;

        // Checking whether the
        // constant added after all
        // layers is even or odd.
        if (beven)
        {
            if ((b & 1) > 0)
                beven = false;
        }
        else if (!((a & 1) > 0))
        {
            if (!((b & 1) > 0))
                beven = true;
        }
        else
        {
            if ((b & 1) > 0)
                beven = true;
        }
    }

    // Counting the number
    // of even and odd.

    // Assuming input x is even.
    if (beven)
    {
        even = parseInt(max / 2) -
               parseInt((min - 1) / 2);
        odd = 0;
    }
    else
    {
        even = parseInt(max / 2) -
               parseInt((min - 1) / 2);
        odd = 0;
    }

    // Assuming input x is odd.
    if (!(beven ^ aeven))
        even += max - min + 1 - parseInt(max / 2) +
                                parseInt((min - 1) / 2);
    else
        odd += max - min + 1 - parseInt(max / 2) +
                               parseInt((min - 1) / 2);

    // Displaying the counts.
    document.write("even = " + even + ", odd = " + odd);
}

// Driver Code
var min = 1, max = 4;
var steps = [ [ 1, 2 ], [ 3, 4 ] ];

count_even_odd(min, max, steps);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
even = 2, odd = 2
```

</figure>

</figure>