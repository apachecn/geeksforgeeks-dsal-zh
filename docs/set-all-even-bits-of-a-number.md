# 设置一个数字的所有偶数位

> 原文:[https://www . geesforgeks . org/set-all-偶数位数字/](https://www.geeksforgeeks.org/set-all-even-bits-of-a-number/)

给定一个数字，任务是设置一个数字的所有偶数位。位的位置从最低有效位计数到最高有效位。LSB 的位置被认为是 1。

**示例:**

```
Input : 20 
Output : 30
Binary representation of 20 is
10100\. After setting
even bits, we get 11110

Input : 10
Output : 10
```

**方法 1:-**
1。首先生成一个包含偶数位置位的数字。
2。用原数取或。注意，1 | 1 = 1，1 | 0 = 1。

让我们用下面的代码来理解这种方法。

## C++

```
// Simple CPP program to set all even
// bits of a number
#include <iostream>
using namespace std;

// Sets even bits of n and returns
// modified number.
int evenbitsetnumber(int n)
{
    // Generate 101010...10 number and
    // store in res.
    int count = 0, res = 0;
    for (int temp = n; temp > 0; temp >>= 1) {

        // if bit is even then generate
        // number and or with res
        if (count % 2 == 1)
            res |= (1 << count);

        count++;
    }

    // return OR number
    return (n | res);
}

int main()
{
    int n = 10;
    cout << evenbitsetnumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to set all even
// bits of a number
class GFG
{
    // Sets even bits of n and returns
    // modified number.
    static int evenbitsetnumber(int n)
    {
        // Generate 101010...10 number and
        // store in res.
        int count = 0, res = 0;
        for (int temp = n; temp > 0; temp >>= 1) {

            // if bit is even then generate
            // number and or with res
            if (count % 2 == 1)
            res |= (1 << count);

        count++;
        }

        // return OR number
        return (n | res);

    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
         System.out.println(evenbitsetnumber(n));
    }
}

// This code is contributed
// by  prerna saini.
```

## 蟒蛇 3

```
# Simple Python program to set all even
# bits of a number

# Sets even bits of n and returns
# modified number.
def evenbitsetnumber(n):

    # Generate 101010...10 number and
    # store in res.
    count = 0
    res = 0
    temp = n
    while(temp > 0):

        # if bit is even then generate
        # number and or with res
        if (count % 2 == 1):
            res |= (1 << count)

        count+=1
        temp >>= 1

    # return OR number
    return (n | res)

n = 10
print(evenbitsetnumber(n))

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// Simple C# program to set
// all even bits of a number
using System;

class GFG
{
    // Sets even bits of n and
    // returns modified number.
    static int evenbitsetnumber(int n) {

        // Generate 101010...10 number
        //  and store in res.
        int count = 0, res = 0;
        for (int temp = n; temp > 0; temp >>= 1) {

            // if bit is even then generate
            // number and or with res
            if (count % 2 == 1)
            res |= (1 << count);

        count++;
        }

        // return OR number
        return (n | res);

    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(evenbitsetnumber(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple php program to set
// all even bits of a number

// Sets even bits of n and
// returns  modified number.
function evenbitsetnumber($n)
{

    // Generate 101010...10 number
    // and store in res.
    $count = 0;
    $res = 0;
    for ($temp = $n; $temp > 0; $temp >>= 1)
    {

        // if bit is even then generate
        // number and or with res
        if ($count % 2 == 1)
            $res |= (1 << $count);

        $count++;
    }

    // return OR number
    return ($n | $res);
}

    //Driver Code
    $n = 10;
    echo evenbitsetnumber($n);

//This Code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to set all even
// bits of a number

// Sets even bits of n and returns
// modified number.
function evenbitsetnumber(n)
{

    // Generate 101010...10 number and
    // store in res.
    let count = 0, res = 0;
    for(let temp = n; temp > 0; temp >>= 1)
    {

        // If bit is even then generate
        // number and or with res
        if (count % 2 == 1)
            res |= (1 << count);

        count++;
    }

    // Return OR number
    return (n | res);
}

// Driver Code
let n = 10;

document.write(evenbitsetnumber(n));

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
10
```

**方法 2(32 位数字的 A0(1)解)**

## C++

```
// Efficient CPP program to set all even
// bits of a number
#include <iostream>
using namespace std;

// return msb set number
int getmsb(int n)
{

    // set all bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // return msb
    // increment n by 1
    // and shift by 1
    return (n + 1) >> 1;
}

// return even seted number
int getevenbits(int n)
{

    // get msb here
    n = getmsb(n);

    // generate even bits like 101010..
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // if bits is odd then shift by 1
    if (n & 1)
        n = n >> 1;

    // return even set bits number
    return n;
}

// set all even bits here
int setallevenbits(int n)
{
    // take or with even set bits number
    return n | getevenbits(n);
}

int main()
{
    int n = 10;
    cout << setallevenbits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to
// set all even bits of a number
import java.io.*;

class GFG
{

// return msb set number
static int getmsb(int n)
{

    // set all bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // return msb
    // increment n by 1
    // and shift by 1
    return (n + 1) >> 1;
}

// return even seted number
static int getevenbits(int n)
{

    // get msb here
    n = getmsb(n);

    // generate even
    // bits like 101010..
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // if bits is odd
    // then shift by 1
    if ((n & 1) == 1)
        n = n >> 1;

    // return even
    // set bits number
    return n;
}

// set all even bits here
static int setallevenbits(int n)
{
    // take or with even
    // set bits number
    return n | getevenbits(n);
}

// Driver Code
public static void main (String[] args)
{
    int n = 10;
    System.out.println(setallevenbits(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Efficient Python 3
# program to set all even
# bits of a number

# return msb set number
def getmsb(n):

    # set all bits
    n |= n >> 1
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    # return msb
    # increment n by 1
    # and shift by 1
    return (n + 1) >> 1

# return even seted number
def getevenbits(n):

    # get msb here
    n = getmsb(n)

    # generate even bits like 101010..
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    # if bits is odd then shift by 1
    if (n & 1):
        n = n >> 1

    # return even set bits number
    return n

# set all even bits here
def setallevenbits(n):

    # take or with even set bits number
    return n | getevenbits(n)

n = 10
print(setallevenbits(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// Efficient C# program to
// set all even bits of a number
using System;

class GFG
{

// return msb set number
static int getmsb(int n)
{

    // set all bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // return msb
    // increment n by 1
    // and shift by 1
    return (n + 1) >> 1;
}

// return even seted number
static int getevenbits(int n)
{

    // get msb here
    n = getmsb(n);

    // generate even
    // bits like 101010..
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // if bits is odd
    // then shift by 1
    if ((n & 1) == 1)
        n = n >> 1;

    // return even
    // set bits number
    return n;
}

// set all even bits here
static int setallevenbits(int n)
{
    // take or with even
    // set bits number
    return n | getevenbits(n);
}

// Driver Code
public static void Main ()
{
    int n = 10;

    Console.WriteLine(setallevenbits(n));
}
}

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient php program to set
// all even bits of a number

// return msb set number
function getmsb($n)
{

    // set all bits
    $n |= $n >> 1;
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // return msb
    // increment n by 1
    // and shift by 1
    return ($n + 1) >> 1;
}

// return even seted number
function getevenbits($n)
{

    // get msb here
    $n = getmsb($n);

    // generate even bits
    // like 101010..
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // if bits is odd then
    // shift by 1
    if ($n & 1)
        $n = $n >> 1;

    // return even set
    // bits number
    return $n;
}

// set all even bits here
function setallevenbits($n)
{
    // take or with even
    // set bits number
    return $n | getevenbits($n);
}

    //Driver code
    $n = 10;
    echo setallevenbits($n);

//This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to
// set all even bits of a number

// Return msb set number
function getmsb(n)
{

    // Set all bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Return msb
    // increment n by 1
    // and shift by 1
    return (n + 1) >> 1;
}

// Return even seted number
function getevenbits(n)
{

    // Get msb here
    n = getmsb(n);

    // Generate even
    // bits like 101010..
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // If bits is odd
    // then shift by 1
    if ((n & 1) == 1)
        n = n >> 1;

    // Return even
    // set bits number
    return n;
}

// Set all even bits here
function setallevenbits(n)
{

    // Take or with even
    // set bits number
    return n | getevenbits(n);
}

// Driver code
let n = 10;

document.write(setallevenbits(n));

// This code is contributed by decode2207 

</script>
```

**Output:** 

```
10
```