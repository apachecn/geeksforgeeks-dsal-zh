# 权重为 W 的 N 位整数个数

> 原文:[https://www . geeksforgeeks . org/n 位数整数带权重 w/](https://www.geeksforgeeks.org/number-of-n-digit-integers-with-weight-w/)

给定 N，大于等于 2 的整数的位数和权重 w，任务是找出有 N 位数和权重 w 的整数的个数
**注**:权重定义为一个整数的连续位数之差。

**示例**:

```
Input : N = 2, W = 3
Output : 6

Input : N = 2, W = 4
Output : 5
```

在上面的例子中，权重等于 3 的 2 位整数的总数可能是 6。就像数字 14 的权重是 3 (4-1)，25、36、47、58、69 的权重是 3。如果我们仔细看，我们会发现这样一个逻辑:如果我们把一个 2 位数的权重增加到 5，那么这些数字的总数可能是 5。对于 2 位数的权重 6，可能的总数将是 4，然后是 3，以此类推。另外，如果我们增加位数。假设 n 等于 3，权重为 3，那么 n 等于 4，权重为 3，那么可能的总数将是 60 和 600，以此类推。
**位数|重量— >所有可能的数字**

<figure class="table">

| 2&#124;2 —> 7 | 2&#124;3 —> 6 | 2&#124;4 —> 5 | 2&#124;5 —> 4 | 2&#124;6 —> 3 | 2&#124;7 —> 2 | 2&#124;8 —> 1 |
| 3&#124;2 —> 70 | 3&#124;3 —> 60 | 3&#124;4 —> 50 | 3&#124;5 —> 40 | 3&#124;6 —> 30 | 3&#124;7 —> 20 | 3&#124;8 —> 10 |
| 4&#124;2 —>700 | 4&#124;3 —>600 | 4&#124;4 —>500 | 4&#124;5 —>400 | 4&#124;6 —>300 | 4&#124;7 —>200 | 4&#124;8 —>100 |

从上表中可以看出，随着位数的增加，权重为“w”的数字数量遵循一种模式，即以 10^(n-2 的倍数变化，其中“n”是位数。
下面是解决这个问题的分步算法:

1.  检查给定的重量是正的还是负的。
2.  如果为正，则从 9 中减去重量。
3.  如果权重为负，则将权重增加到 10，然后更新新的权重。
4.  对于 n 位整数，将 10^(n-2)乘以这个更新的权重。
5.  这将给出满足这个权重的整数个数。

下面是上述方法的实现:

## C++

```
// CPP program to find total possible numbers
// with n digits and weight w

#include <iostream>
#include<cmath>

using namespace std;

// Function to find total possible numbers
// with n digits and weight w
int findNumbers(int n, int w)
{
    int x = 0, sum = 0;

    // When Weight of an integer is Positive
    if (w >= 0 && w <= 8) {
        // Subtract the weight from 9
        x = 9 - w;
    }
    // When weight of an integer is negative
    else if (w >= -9 && w <= -1) {
        // add the weight to 10 to make it positive
        x = 10 + w;
    }

    sum = pow(10, n - 2);
    sum = (x * sum);

    return sum;
}

// Driver code
int main()
{
    int n, w;

    // number of digits in an
    // integer and w as weight
    n = 3, w = 4;

    // print the total possible numbers
    // with n digits and weight w
    cout << findNumbers(n, w);;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total
// possible numbers with n
// digits and weight w

class GFG
{

// Function to find total
// possible numbers with n
// digits and weight w
static int findNumbers(int n, int w)
{
    int x = 0, sum = 0;

    // When Weight of an
    // integer is Positive
    if (w >= 0 && w <= 8)
    {
        // Subtract the weight from 9
        x = 9 - w;
    }

    // When weight of an
    // integer is negative
    else if (w >= -9 && w <= -1)
    {
        // add the weight to 10
        // to make it positive
        x = 10 + w;
    }

    sum = (int)Math.pow(10, n - 2);
    sum = (x * sum);

    return sum;
}

// Driver code
public static void main(String args[])
{
    int n, w;

    // number of digits in an
    // integer and w as weight
    n = 3;
    w = 4;

    // print the total possible numbers
    // with n digits and weight w
    System.out.println(findNumbers(n, w));
}
}

// This code is contributed
// by ankita_saini
```

## 蟒蛇 3

```
# Python3 program to find total possible
# numbers with n digits and weight w

# Function to find total possible
# numbers with n digits and weight w
def findNumbers(n, w):

    x = 0;
    sum = 0;

    # When Weight of an integer
    # is Positive
    if (w >= 0 and w <= 8):
        # Subtract the weight from 9
        x = 9 - w;

    # When weight of an integer
    # is negative
    elif (w >= -9 and w <= -1):

        # add the weight to 10 to
        # make it positive
        x = 10 + w;

    sum = pow(10, n - 2);
    sum = (x * sum);

    return sum;

# Driver code

# number of digits in an
# integer and w as weight
n = 3;
w = 4;

# print the total possible numbers
# with n digits and weight w
print(findNumbers(n, w));

# This code is contributed
# by mits
```

## C#

```
// C# program to find total possible
// numbers with n digits and weight w
using System;

class GFG
{

// Function to find total possible
// numbers with n digits and weight w
static int findNumbers(int n, int w)
{
    int x = 0, sum = 0;

    // When Weight of an integer
    // is Positive
    if (w >= 0 && w <= 8)
    {
        // Subtract the weight from 9
        x = 9 - w;
    }

    // When weight of an
    // integer is negative
    else if (w >= -9 && w <= -1)
    {
        // add the weight to 10
        // to make it positive
        x = 10 + w;
    }

    sum = (int)Math.Pow(10, n - 2);
    sum = (x * sum);

    return sum;
}

// Driver code
static public void Main ()
{
    int n, w;

    // number of digits in an
    // integer and w as weight
    n = 3;
    w = 4;

    // print the total possible numbers
    // with n digits and weight w
    Console.WriteLine(findNumbers(n, w));
}
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find total possible
// numbers with n digits and weight w

// Function to find total possible
// numbers with n digits and weight w
function findNumbers($n, $w)
{
    $x = 0; $sum = 0;

    // When Weight of an integer
    // is Positive
    if ($w >= 0 && $w <= 8)
    {
        // Subtract the weight from 9
        $x = 9 - $w;
    }

    // When weight of an integer
    // is negative
    else if ($w >= -9 && $w <= -1)
    {
        // add the weight to 10 to
        // make it positive
        $x = 10 + $w;
    }

    $sum = pow(10, $n - 2);
    $sum = ($x * $sum);

    return $sum;
}

// Driver code

// number of digits in an
// integer and w as weight
$n = 3; $w = 4;

// print the total possible numbers
// with n digits and weight w
echo findNumbers($n, $w);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
    // Javascript program to find total possible
    // numbers with n digits and weight w

    // Function to find total possible
    // numbers with n digits and weight w
    function findNumbers(n, w)
    {
        let x = 0, sum = 0;

        // When Weight of an integer
        // is Positive
        if (w >= 0 && w <= 8)
        {
            // Subtract the weight from 9
            x = 9 - w;
        }

        // When weight of an
        // integer is negative
        else if (w >= -9 && w <= -1)
        {
            // add the weight to 10
            // to make it positive
            x = 10 + w;
        }

        sum = Math.pow(10, n - 2);
        sum = (x * sum);

        return sum;
    }

    let n, w;

    // number of digits in an
    // integer and w as weight
    n = 3;
    w = 4;

    // print the total possible numbers
    // with n digits and weight w
    document.write(findNumbers(n, w));

</script>
```

**Output:** 

```
50
```

</figure>