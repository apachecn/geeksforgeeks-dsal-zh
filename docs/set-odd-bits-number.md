# 设置一个数字的所有奇数位

> 原文:[https://www.geeksforgeeks.org/set-odd-bits-number/](https://www.geeksforgeeks.org/set-odd-bits-number/)

给定一个数，任务是设置一个数的所有奇数位。位的位置从最低有效位计数到最高有效位。LSB 的位置被认为是 1。

**示例:**

```
Input : 20
Output : 21
Explanation : Binary representation of 20
is 10100. Setting all odd
bits make the number 10101 which is binary
representation of 21.

Input : 10
Output : 15
```

**方法 1(使用 OR)**
1。首先生成一个包含奇数位的数字。
2。用原数取或。注意，1 | 1 = 1，1 | 0 = 1。

让我们用下面的代码来理解这种方法。

## C++

```
// CPP code Set all odd bits
// of a number
#include <iostream>
using namespace std;

// set all odd bit
int oddbitsetnumber(int n)
{
    int count = 0;

    // res for store 010101.. number
    int res = 0;

    // generate number form of 010101.....till
    // temp size
    for (int temp = n; temp > 0; temp >>= 1) {

        // if bit is odd, then generate
        // number and or with res
        if (count % 2 == 0)
            res |= (1 << count);

        count++;
    }

    return (n | res);
}

// Driver code
int main()
{
    int n = 10;
    cout << oddbitsetnumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Set all odd
// bits of a number

class GFG
{

    // set all odd bit
    static int oddbitsetnumber(int n)
    {
        int count = 0;

        // res for store 010101.. number
        int res = 0;

        // generate number form of
        // 010101.....till temp size
        for (int temp = n; temp > 0; temp >>= 1)
        {

            // if bit is odd, then generate
            // number and or with res
            if (count % 2 == 0)
                res |= (1 << count);

            count++;
        }

        return (n | res);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10;
        System.out.println(oddbitsetnumber(n));
    }
}

// This code is contributed
// by prerna saini
```

## 蟒蛇 3

```
''' Python3 code Set all odd bits
   of a number'''

# set all odd bit
def oddbitsetnumber(n):
    count = 0
    # res for store 010101.. number
    res = 0

    # generate number form of 010101.....till
    # temp size
    temp = n
    while temp > 0:

        # if bit is odd, then generate
        # number and or with res
        if count % 2 == 0:
            res |= (1 << count)

        count += 1
        temp >>= 1

    return (n | res)

n = 10
print (oddbitsetnumber(n))

#This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# code to Set all odd
// bits of a number
using System;

class GFG
{
    static int oddbitsetnumber(int n)
    {
        int count = 0;

        // res for store 010101.. number
        int res = 0;

        // generate number form of
        // 010101.....till temp size
        for (int temp = n; temp > 0;
                           temp >>= 1)
        {

            // if bit is odd, then
            // generate number and
            // or with res
            if (count % 2 == 0)
                res |= (1 << count);

            count++;
        }

        return (n | res);
    }

    // Driver Code
    static public void Main ()
    {
        int n = 10;
        Console.WriteLine(oddbitsetnumber(n));
    }
}

// This code is contributed
// by prerna ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php code Set all odd
// bits  of a number

// set all odd bit
function oddbitsetnumber($n)
{
    $count = 0;

    // res for store 010101..
    // number
    $res = 0;

    // generate number form of
    // 010101... till temp size
    for ($temp = $n; $temp > 0; $temp >>= 1)
    {

        // if bit is odd, then generate
        // number and or with res
        if ($count % 2 == 0)
            $res |= (1 << $count);

        $count++;
    }

    return ($n | $res);
}

    // Driver code
    $n = 10;
    echo oddbitsetnumber($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript Program to Set all odd
// bits of a number

    // set all odd bit
    function oddbitsetnumber(n)
    {
        let count = 0;

        // res for store 010101.. number
        let res = 0;

        // generate number form of
        // 010101.....till temp size
        for (let temp = n; temp > 0; temp >>= 1)
        {

            // if bit is odd, then generate
            // number and or with res
            if (count % 2 == 0)
                res |= (1 << count);

            count++;
        }
        return (n | res);
    }

// Driver Code
        let n = 10;
        document.write(oddbitsetnumber(n));

       // This code is contributed by chinmoy1997pal.
</script>
```

输出:

```
15
```

**方法 2(32 位数字的 A0(1)解)**

## C++

```
// Efficient CPP program to set all
// odd bits number
#include <iostream>
using namespace std;

// return MSB set number
int getmsb(int n)
{
    // set all bits including MSB.
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // return MSB
    return (n + 1) >> 1;
}

// Returns a number of same size (MSB at
// same position) as n and all odd bits
// set.
int getevenbits(int n)
{
    n = getmsb(n);

    // generate odd bits like 010101..
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // if bits is even then shift by 1
    if ((n&1) == 0)
        n = n >> 1;

    // return odd set bits number
    return n; 
}

// set all odd bits here
int setalloddbits(int n)
{   
    // take OR with odd set bits number
    return n | getevenbits(n);   
}

// Driver code
int main()
{
    int n = 10;
    cout << setalloddbits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to set
// all odd bits number
class GFG {

    // return MSB set number
    static int getmsb(int n)
    {
        // set all bits including MSB.
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // return MSB
        return (n + 1) >> 1;
    }

    // Returns a number of same
    // size (MSB at same position)
    // as n and all odd bits set.
    static int getevenbits(int n)
    {
        n = getmsb(n);

        // generate odd bits
        // like 010101..
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // if bits is even
        // then shift by 1
        if ((n & 1) == 0)
            n = n >> 1;

        // return odd set bits number
        return n;
    }

    // set all odd bits here
    static int setalloddbits(int n)
    {
        // take OR with odd
        // set bits number
        return n | getevenbits(n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10;
        System.out.println(setalloddbits(n));
    }
}

// This code is contributed
// by prerna saini
```

## 蟒蛇 3

```
# Efficient python3 program to 
# set all odd bits number
import math

# return MSB set number
def getmsb( n):

    # set all bits including MSB.
    n |= n >> 1
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    # return MSB
    return (n + 1) >> 1

# Returns a number of same
# size (MSB at same position)
# as n and all odd bits set.
def getevenbits(n):

    n = getmsb(n)

    # generate odd bits
    # like 010101..
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    # if bits is even
    # then shift by 1
    if ((n & 1) == 0):
        n = n >> 1

    # return odd set bits number
    return n

# set all odd bits here
def setalloddbits( n):

    # take OR with odd
    # set bits number
    return n | getevenbits(n)

# Driver Program
n = 10
print(setalloddbits(n))

# This code is contributed
# by Gitanjali.
```

## C#

```
// Efficient C# program to
// set all odd bits number
using System;

class GFG
{

    // return MSB set number
    static int getmsb(int n)
    {
        // set all bits
        // including MSB.
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // return MSB
        return (n + 1) >> 1;
    }

    // Returns a number of same
    // size (MSB at same position)
    // as n and all odd bits set.
    static int getevenbits(int n)
    {
        n = getmsb(n);

        // generate odd bits
        // like 010101..
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // if bits is even
        // then shift by 1
        if ((n & 1) == 0)
            n = n >> 1;

        // return odd
        // set bits number
        return n;
    }

    // set all odd bits here
    static int setalloddbits(int n)
    {
        // take OR with odd
        // set bits number
        return n | getevenbits(n);
    }

    // Driver Code
    static public void Main ()
    {
        int n = 10;
        Console.WriteLine(setalloddbits(n));
    }
}

// This code is contributed ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient php program to
// set all  odd bits number

// return MSB set number
function getmsb($n)
{

    // set all bits
    // including MSB.
    $n |= $n >> 1;
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // return MSB
    return ($n + 1) >> 1;
}

// Returns a number of
// same size (MSB at
// same position) as n
// and all odd bits set
function getevenbits($n)
{
    $n = getmsb($n);

    // generate odd bits
    // like 010101..
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // if bits is even
    // then shift by 1
    if (($n&1) == 0)
        $n = $n >> 1;

    // return odd set
    // bits number
    return $n;
}

// set all odd bits here
function setalloddbits($n)
{

    // take OR with odd
    // set bits number
    return $n | getevenbits($n);
}

    // Driver code
    $n = 10;
    echo setalloddbits($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to
// set all odd bits number

// Return MSB set number
function getmsb(n)
{

    // Set all bits
    // including MSB.
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Return MSB
    return (n + 1) >> 1;
}

// Returns a number of same
// size (MSB at same position)
// as n and all odd bits set.
function getevenbits(n)
{
    n = getmsb(n);

    // Generate odd bits
    // like 010101..
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // If bits is even
    // then shift by 1
    if ((n & 1) == 0)
        n = n >> 1;

    // Return odd
    // set bits number
    return n;
}

// Set all odd bits here
function setalloddbits(n)
{

    // Take OR with odd
    // set bits number
    return n | getevenbits(n);
}

// Driver Code
let n = 10;
document.write(setalloddbits(n));

// This code is contributed by decode2207 

</script>
```

输出:

```
15
```