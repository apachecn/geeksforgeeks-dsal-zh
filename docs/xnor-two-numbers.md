# XNOR 的两个数字

> 原文:[https://www.geeksforgeeks.org/xnor-two-numbers/](https://www.geeksforgeeks.org/xnor-two-numbers/)

XNOR 给出了二进制位异或的反例。

```
First bit | Second bit | XNOR  
0             0           1
0             1           0
1             0           0
1             1           1
It gives 1 if bits are same else if  
bits are different it gives 0.
```

它与异或相反，但我们不能直接实现它，所以这是实现 XNOR 的程序
示例:

```
Input  : 10 20
Output : 1
Binary of 20 is 10100
Binary of 10 is  1010
So the XNOR is  00001
So output is 1

Input  : 10 10
Output : 15
Binary of 10 is  1010
Binary of 10 is  1010
So the XNOR is   1111
So output is 15
```

**第一种方法:- (O(logn))** 在这个解决方案中，我们一次检查一位。如果两位相同，我们在结果中输入 1，否则输入 0。
下面用代码
来理解一下

## C++

```
// CPP program to find
// XNOR of two numbers
#include <iostream>
using namespace std;

// log(n) solution
int xnor(int a, int b)
{
    // Make sure a is larger
    if (a < b)
        swap(a, b);

    if (a == 0 && b == 0)
        return 1;

    int a_rem = 0; // for last bit of a
    int b_rem = 0; // for last bit of b

    // counter for count bit
    // and set bit  in xnornum
    int count = 0;

    // to make new xnor number
    int xnornum = 0;

    // for set bits in new xnor number
    while (a)
    {
        // get last bit of a
        a_rem = a & 1;

        // get last bit of b
        b_rem = b & 1;

        // Check if current two
        // bits are same
        if (a_rem == b_rem)       
            xnornum |= (1 << count);

        // counter for count bit
        count++;
        a = a >> 1;
        b = b >> 1;
    }
    return xnornum;
}

// Driver code
int main()
{
    int a = 10, b = 50;
    cout << xnor(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// XNOR of two numbers
import java.util.*;
import java.lang.*;

public class GfG {

    public static int xnor(int a, int b)
    {
        // Make sure a is larger
        if (a < b) {
            // swapping a and b;
            int t = a;
            a = b;
            b = t;
        }

        if (a == 0 && b == 0)
            return 1;

        // for last bit of a
        int a_rem = 0;

        // for last bit of b
        int b_rem = 0;

        // counter for count bit
        // and set bit in xnornum
        int count = 0;

        // to make new xnor number
        int xnornum = 0;

        // for set bits in new xnor number
        while (true) {
            // get last bit of a
            a_rem = a & 1;

            // get last bit of b
            b_rem = b & 1;

            // Check if current two bits are same
            if (a_rem == b_rem)
                xnornum |= (1 << count);

            // counter for count bit
            count++;
            a = a >> 1;
            b = b >> 1;
            if (a < 1)
                break;
        }
        return xnornum;
    }

    // Driver function
    public static void main(String argc[])
    {
        int a = 10, b = 50;
        System.out.println(xnor(a, b));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find XNOR
# of two numbers
import math

def swap(a,b):

    temp=a
    a=b
    b=temp

# log(n) solution
def xnor(a, b):

    # Make sure a is larger
    if (a < b):
        swap(a, b)

    if (a == 0 and b == 0) :
        return 1;

    # for last bit of a
    a_rem = 0

    # for last bit of b
    b_rem = 0

    # counter for count bit and
    #  set bit in xnor num
    count = 0

    # for make new xnor number
    xnornum = 0

    # for set bits in new xnor
    # number
    while (a!=0) :

        # get last bit of a
        a_rem = a & 1

        # get last bit of b
        b_rem = b & 1

        # Check if current two
        # bits are same
        if (a_rem == b_rem):    
            xnornum |= (1 << count)

        # counter for count bit
        count=count+1

        a = a >> 1
        b = b >> 1

    return xnornum;

# Driver method
a = 10
b = 50
print(xnor(a, b))

# This code is contributed by Gitanjali
```

## C#

```
// C# program to find
// XNOR of two numbers
using System;

public class GfG {

    public static int xnor(int a, int b)
    {
        // Make sure a is larger
        if (a < b) {
            // swapping a and b;
            int t = a;
            a = b;
            b = t;
        }

        if (a == 0 && b == 0)
            return 1;

        // for last bit of a
        int a_rem = 0;

        // for last bit of b
        int b_rem = 0;

        // counter for count bit
        // and set bit in xnornum
        int count = 0;

        // to make new xnor number
        int xnornum = 0;

        // for set bits in new xnor number
        while (true) {
            // get last bit of a
            a_rem = a & 1;

            // get last bit of b
            b_rem = b & 1;

            // Check if current two bits are same
            if (a_rem == b_rem)
                xnornum |= (1 << count);

            // counter for count bit
            count++;
            a = a >> 1;
            b = b >> 1;
            if (a < 1)
                break;
        }
        return xnornum;
    }

    // Driver function
    public static void Main()
    {
        int a = 10, b = 50;
        Console.WriteLine(xnor(a, b));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// XNOR of two numbers

// log(n) solution
function xnor($a, $b)
{

    // Make sure a is larger
    if ($a < $b)
        list($a, $b) = array($b, $a);

    if ($a == 0 && $b == 0)
        return 1;

    // for last bit of a
    $a_rem = 0;

    // for last bit of b
    $b_rem = 0;

    // counter for count bit
    // and set bit in xnornum
    $count = 0;

    // to make new xnor number
    $xnornum = 0;

    // for set bits in
    // new xnor number
    while ($a)
    {

        // get last bit of a
        $a_rem = $a & 1;

        // get last bit of b
        $b_rem = $b & 1;

        // Check if current two
        // bits are same
        if ($a_rem == $b_rem)
            $xnornum |= (1 << $count);

        // counter for count bit
        $count++;
        $a = $a >> 1;
        $b = $b >> 1;
    }
    return $xnornum;
}

    // Driver code
    $a = 10;
    $b = 50;
    echo xnor($a, $b);

// This code is contributed by mits.    
?>
```

## java 描述语言

```
<script>

// javascript program to find
// XNOR of two numbers
    function xnor(a, b)
    {

        // Make sure a is larger
        if (a < b)
        {

            // swapping a and b;
            let t = a;
            a = b;
            b = t;
        }

        if (a == 0 && b == 0)
            return 1;

        // for last bit of a
        let a_rem = 0;

        // for last bit of b
        let b_rem = 0;

        // counter for count bit
        // and set bit in xnornum
        let count = 0;

        // to make new xnor number
        let xnornum = 0;

        // for set bits in new xnor number
        while (true) {
            // get last bit of a
            a_rem = a & 1;

            // get last bit of b
            b_rem = b & 1;

            // Check if current two bits are same
            if (a_rem == b_rem)
                xnornum |= (1 << count);

            // counter for count bit
            count++;
            a = a >> 1;
            b = b >> 1;
            if (a < 1)
                break;
        }
        return xnornum;
    }

// Driver Function

         let a = 10, b = 50;
        document.write(xnor(a, b));

        // This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
7
```

**第二种方法:- O(1)**
1)求两个给定数的最大值。
2) [切换两个数字中较高的所有位](https://www.geeksforgeeks.org/toggle-bits-significant-bit/)。
3)返回原较小数和修改后较大数的异或。

## C++

```
// CPP program to find XNOR of two numbers.
#include <iostream>
using namespace std;

// Please refer below post for details of this
// function
// https://www.geeksforgeeks.org/toggle-bits-significant-bit/
int togglebit(int n)
{
    if (n == 0)
        return 1;

    // Make a copy of n as we are
    // going to change it.
    int i = n;

    // Below steps set bits after
    // MSB (including MSB)

    // Suppose n is 273 (binary
    // is 100010001). It does following
    // 100010001 | 010001000 = 110011001
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set. It does following
    // 110011001 | 001100110 = 111111111
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    return i ^ n;
}

// Returns XNOR of num1 and num2
int XNOR(int num1, int num2)
{
    // if num2 is greater then
    // we swap this number in num1
    if (num1 < num2)
        swap(num1, num2);
    num1 = togglebit(num1);

    return num1 ^ num2;
}

// Driver code
int main()
{
    int num1 = 10, num2 = 20;
    cout << XNOR(num1, num2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XNOR
// of two numbers
import java.io.*;

class GFG {

    // Please refer below post for
    // details of this function
    // https://www.geeksforgeeks.org/toggle-bits-significant-bit/
    static int togglebit(int n)
    {
        if (n == 0)
            return 1;

        // Make a copy of n as we are
        // going to change it.
        int i = n;

        // Below steps set bits after
        // MSB (including MSB)

        // Suppose n is 273 (binary
        // is 100010001). It does following
        // 100010001 | 010001000 = 110011001
        n |= n >> 1;

        // This makes sure 4 bits
        // (From MSB and including MSB)
        // are set. It does following
        // 110011001 | 001100110 = 111111111
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        return i ^ n;
    }

    // Returns XNOR of num1 and num2
    static int xnor(int num1, int num2)
    {
        // if num2 is greater then
        // we swap this number in num1 
        if (num1 < num2)
        {
            int temp = num1;
            num1 = num2;
            num2 = temp;
        }

        num1 = togglebit(num1);

        return num1 ^ num2;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int a = 10, b = 20;    
        System.out.println(xnor(a, b));
    }
}

// This code is contributed by Gitanjali
```

## 计算机编程语言

```
# python program to find XNOR of two numbers
import math

# Please refer below post for details of this function
# https://www.geeksforgeeks.org/toggle-bits-significant-bit/
def togglebit( n):

    if (n == 0):
        return 1

    # Make a copy of n as we are
    # going to change it.
    i = n

    # Below steps set bits after
    # MSB (including MSB)

    # Suppose n is 273 (binary
    # is 100010001). It does following
    # 100010001 | 010001000 = 110011001
    n = n|(n >> 1)

    # This makes sure 4 bits
    # (From MSB and including MSB)
    # are set. It does following
    # 110011001 | 001100110 = 111111111
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    return i ^ n

# Returns XNOR of num1 and num2
def xnor( num1, num2):

    # Make sure num1 is larger
    if (num1 < num2):
        temp = num1
        num1 = num2
        num2 = temp
    num1 = togglebit(num1)

    return num1 ^ num2

# Driver code
a = 10
b = 20
print (xnor(a, b))

# This code is contributed by 'Gitanjali'.
```

## C#

```
// C# program to find XNOR
// of two numbers
using System;

class GFG {

    // Please refer below post for
    // details of this function
    // https://www.geeksforgeeks.org/toggle-bits-significant-bit/
    static int togglebit(int n)
    {
        if (n == 0)
            return 1;

        // Make a copy of n as we are
        // going to change it.
        int i = n;

        // Below steps set bits after
        // MSB (including MSB)

        // Suppose n is 273 (binary
        // is 100010001). It does following
        // 100010001 | 010001000 = 110011001
        n |= n >> 1;

        // This makes sure 4 bits
        // (From MSB and including MSB)
        // are set. It does following
        // 110011001 | 001100110 = 111111111
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        return i ^ n;
    }

    // Returns XNOR of num1 and num2
    static int xnor(int num1, int num2)
    {
        // if num2 is greater then
        // we swap this number in num1
        if (num1 < num2)
        {
            int temp = num1;
            num1 = num2;
            num2 = temp;
        }

        num1 = togglebit(num1);

        return num1 ^ num2;
    }

    // Driver program
    public static void Main()
    {
        int a = 10, b = 20;
        Console.WriteLine(xnor(a, b));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find XNOR
// of two numbers.

// Please refer below post
// for details of this function
// https://www.geeksforgeeks.org/toggle-bits-significant-bit/

function togglebit($n)
{
    if ($n == 0)
        return 1;

    // Make a copy of n as we are
    // going to change it.
    $i = $n;

    // Below steps set bits after
    // MSB (including MSB)

    // Suppose n is 273 (binary
    // is 100010001). It does following
    // 100010001 | 010001000 = 110011001
    $n |= $n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set. It does following
    // 110011001 | 001100110 = 111111111
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    return $i ^ $n;
}

// Returns XNOR of num1 and num2
function XNOR($num1, $num2)
{

    // if num2 is greater then
    // we swap this number in num1
    if ($num1 < $num2)
        list($num1, $num2)=array($num2, $num1);
    $num1 = togglebit($num1);

    return $num1 ^ $num2;
}

// Driver code
$num1 = 10;
$num2 = 20;
echo XNOR($num1, $num2);

// This code is contributed by Smitha.
?>
```

## java 描述语言

```
<script>
// Javascript program to find XNOR of two numbers.

// Please refer below post for details of this
// function
// https://www.geeksforgeeks.org/toggle-bits-significant-bit/
function togglebit(n)
{
    if (n == 0)
        return 1;

    // Make a copy of n as we are
    // going to change it.
    let i = n;

    // Below steps set bits after
    // MSB (including MSB)

    // Suppose n is 273 (binary
    // is 100010001). It does following
    // 100010001 | 010001000 = 110011001
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set. It does following
    // 110011001 | 001100110 = 111111111
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    return i ^ n;
}

// Returns XNOR of num1 and num2
function XNOR(num1, num2)
{
    // if num2 is greater then
    // we swap this number in num1
    if (num1 < num2) {
        let temp = num1;
        num1 = num2;
        num2 = temp;
    }
    num1 = togglebit(num1);

    return num1 ^ num2;
}

// Driver code
    let num1 = 10, num2 = 20;
    document.write(XNOR(num1, num2));

</script>
```

输出:

```
1
```