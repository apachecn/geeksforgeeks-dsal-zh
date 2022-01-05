# 不使用算术运算符添加两个数字

> 原文:[https://www . geesforgeks . org/add-two-numbers-不使用算术运算符/](https://www.geeksforgeeks.org/add-two-numbers-without-using-arithmetic-operators/)

编写一个返回两个整数之和的函数 Add()。该函数不应使用任何算术运算符(+、++、–、-..等等)。
两个比特的和可以通过对两个比特执行 XOR (^)来获得。进位位可以通过执行两个位的“与”(&)来获得。

上面是简单的[半加法器](http://en.wikipedia.org/wiki/Adder_%28electronics%29#Half_adder)逻辑，可以用来加 2 个单比特。我们可以把这个逻辑推广到整数。如果 x 和 y 在相同位置没有设置位，则 x 和 y 的按位异或(^)得到 x 和 y 的和。为了合并公共设置位，使用按位与(&)。x 和 y 的按位“与”给出所有进位。我们计算(x & y) < < 1，并将其与 x ^ y 相加，得到所需的结果。

## C

```
// C++ Program to add two numbers
// without using arithmetic operator
#include <bits/stdc++.h>
using namespace std;

int Add(int x, int y)
{
    // Iterate till there is no carry
    while (y != 0)
    {
        // carry should be unsigned to
        // deal with -ve numbers
        // carry now contains common
        //set bits of x and y
        unsigned carry = x & y;

        // Sum of bits of x and y where at
        //least one of the bits is not set
        x = x ^ y;

        // Carry is shifted by one so that adding
        // it to x gives the required sum
        y = carry << 1;
    }
    return x;
}

// Driver code
int main()
{
    cout << Add(15, 32);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C Program to add two numbers
// without using arithmetic operator
#include<stdio.h>

int Add(int x, int y)
{
    // Iterate till there is no carry 
    while (y != 0)
    {
        // carry now contains common
        //set bits of x and y
        unsigned carry = x & y; 

        // Sum of bits of x and y where at
        //least one of the bits is not set
        x = x ^ y;

        // Carry is shifted by one so that adding
        // it to x gives the required sum
        y = carry << 1;
    }
    return x;
}

int main()
{
    printf("%d", Add(15, 32));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to add two numbers
// without using arithmetic operator
import java.io.*;

class GFG
{
    static int Add(int x, int y)
    {
        // Iterate till there is no carry
        while (y != 0)
        {
            // carry now contains common
            // set bits of x and y
            int carry = x & y;

            // Sum of bits of x and
            // y where at least one
            // of the bits is not set
            x = x ^ y;

            // Carry is shifted by
            // one so that adding it
            // to x gives the required sum
            y = carry << 1;
        }
        return x;
    }

    // Driver code
    public static void main(String arg[])
    {
        System.out.println(Add(15, 32));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 Program to add two numbers
# without using arithmetic operator
def Add(x, y):

    # Iterate till there is no carry
    while (y != 0):

        # carry now contains common
        # set bits of x and y
        carry = x & y

        # Sum of bits of x and y where at
        # least one of the bits is not set
        x = x ^ y

        # Carry is shifted by one so that  
        # adding it to x gives the required sum
        y = carry << 1

    return x

print(Add(15, 32))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program to add two numbers
// without using arithmetic operator
using System;

class GFG
{
    static int Add(int x, int y)
    {
        // Iterate till there is no carry
        while (y != 0)
        {
            // carry now contains common
            // set bits of x and y
            int carry = x & y;

            // Sum of bits of x and
            // y where at least one
            // of the bits is not set
            x = x ^ y;

            // Carry is shifted by
            // one so that adding it
            // to x gives the required sum
            y = carry << 1;
        }
        return x;
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(Add(15, 32));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to add two numbers
// without using arithmetic operator

function Add( $x, $y)
{

    // Iterate till there is
    // no carry
    while ($y != 0)
    {

        // carry now contains common
        //set bits of x and y
        $carry = $x & $y;

        // Sum of bits of x and y where at
        //least one of the bits is not set
        $x = $x ^ $y;

        // Carry is shifted by one
        // so that adding it to x
        // gives the required sum
        $y = $carry << 1;
    }
    return $x;
}

    // Driver Code
    echo Add(15, 32);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Program to add two numbers
// without using arithmetic operator

    function Add(x, y) {
        // Iterate till there is no carry  
        while (y != 0)
        {
            // carry now contains common 
            //set bits of x and y
            let carry = x & y;  

            // Sum of bits of x and y where at 
            //least one of the bits is not set
            x = x ^ y; 

            // Carry is shifted by one so that adding
            // it to x gives the required sum
            y = carry << 1;
        }
        return x;
    }

     //driver code
    document.write(Add(15, 32));

// This code is contributed by Surbhi Tyagi
</script>
```

**输出:**

```
47
```

***时间复杂度:** O(对数 y)*

***辅助空间:** O(1)*

下面是相同方法的递归实现。

## C++

```
int Add(int x, int y)
{
    if (y == 0)
        return x;
    else
        return Add( x ^ y,(unsigned) (x & y) << 1);
}

// This code is contributed by shubhamsingh10
```

## C

```
int Add(int x, int y)
{
    if (y == 0)
        return x;
    else
        return Add( x ^ y, (unsigned)(x & y) << 1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static int Add(int x, int y)
{
  if (y == 0)
    return x;
  else
    return Add(x ^ y, (x & y) << 1);
}

// This code is contributed by subham348
```

## 蟒蛇 3

```
def Add(x, y):

    if (y == 0):
        return x
    else
        return Add( x ^ y, (x & y) << 1)

# This code is contributed by subhammahato348
```

## C#

```
static int Add(int x, int y)
{
  if (y == 0)
    return x;
  else
    return Add(x ^ y, (x & y) << 1);
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
function Add(x, y)
{
    if (y == 0)
        return x;
    else
        return Add(x ^ y, (x & y) << 1);
}

// This code is contributed by Ankita saini
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。