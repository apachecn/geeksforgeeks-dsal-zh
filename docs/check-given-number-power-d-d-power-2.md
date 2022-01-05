# 检查给定的数字是否是 d 的幂，其中 d 是 2 的幂

> 原文:[https://www . geesforgeks . org/check-给定-number-power-d-d-power-2/](https://www.geeksforgeeks.org/check-given-number-power-d-d-power-2/)

给定一个整数 n，求它是否是 d 的幂，其中 d 本身就是 2 的幂。
**例:**

```
Input : n = 256, d = 16
Output : Yes

Input : n = 32, d = 16
Output : No
```

**方法 1** 取给定数在基数 d 上的对数，如果得到一个整数，那么这个数就是 d 的幂。
**方法 2** 继续将这个数除以 d，即迭代做 n = n/d。在任何迭代中，如果 n%d 变成非零且 n 不是 1，则 n 不是 d 的幂，否则 n 是 d 的幂。
**方法 3(按位)**
如果满足以下条件，则数字 n 是 d 的幂。
a)在 n 的二进制表示中只有一个位集(注意:d 是 2 的幂)
b)在(唯一)设置位之前的零位计数是 log 的倍数 <sub>2</sub> (d)。
例如:对于 n = 16 (10000)和 d = 4，16 是 4 的幂，因为只有一个位设置，并且在设置位是 4 之前计数为 0，4 是 log 的倍数 <sub>2</sub> (4)。

## C++

```
// CPP program to find if a number is power
// of d where d is power of 2.
#include<stdio.h>

unsigned int Log2n(unsigned int n)
{
return (n > 1)? 1 + Log2n(n/2): 0;
}

bool isPowerOfd(unsigned int n, unsigned int d)
{
int count = 0;

/* Check if there is only one bit set in n*/
if (n && !(n&(n-1)) )
{
    /* count 0 bits before set bit */
    while (n > 1)
    {
    n >>= 1;
    count += 1;
    }    

    /* If count is a multiple of log2(d)
    then return true else false*/
    return (count%(Log2n(d)) == 0);
}

/* If there are more than 1 bit set
    then n is not a power of 4*/
return false;
}

/* Driver program to test above function*/
int main()
{
int n = 64, d = 8;
if (isPowerOfd(n, d))
    printf("%d is a power of %d", n, d);
else
    printf("%d is not a power of %d", n, d);
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if
// a number is power of d
// where d is power of 2.

class GFG
{
static int Log2n(int n)
{
    return (n > 1)? 1 +
    Log2n(n / 2): 0;
}

static boolean isPowerOfd(int n,
                        int d)
{
int count = 0;

/* Check if there is
only one bit set in n*/
if (n > 0 && (n &
(n - 1)) == 0)
{
    /* count 0 bits
    before set bit */
    while (n > 1)
    {
        n >>= 1;
        count += 1;
    }

    /* If count is a multiple
    of log2(d) then return
    true else false*/
    return (count %
        (Log2n(d)) == 0);
}

/* If there are more
than 1 bit set then
n is not a power of 4*/
return false;
}

// Driver Code
public static void main(String[] args)
{
    int n = 64, d = 8;
    if (isPowerOfd(n, d))
        System.out.println(n +
                    " is a power of " + d);
    else
        System.out.println(n +
                    " is not a power of " + d);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find if a number
# is power of d where d is power of 2.

def Log2n(n):
    return (1 + Log2n(n / 2)) if (n > 1) else 0;

def isPowerOfd(n, d):
    count = 0;

    # Check if there is only
    # one bit set in n

    if (n and (n & (n - 1))==0):
        # count 0 bits
        # before set bit
        while (n > 1):
            n >>= 1;
            count += 1;
        # If count is a multiple of log2(d)
        # then return true else false
        return (count%(Log2n(d)) == 0);

    # If there are more than 1 bit set
    # then n is not a power of 4
    return False;

# Driver Code
n = 64;
d = 8;
if (isPowerOfd(n, d)):
    print(n,"is a power of",d);
else:
    print(n,"is not a power of",d);

# This code is contributed by mits
```

## C#

```
// C# program to find if
// a number is power of d
// where d is power of 2.
using System;

class GFG
{
static int Log2n(int n)
{
    return (n > 1)? 1 +
    Log2n(n / 2): 0;
}

static bool isPowerOfd(int n,
                    int d)
{
int count = 0;

/* Check if there is
only one bit set in n*/
if (n > 0 && (n & (n - 1)) == 0)
{
    /* count 0 bits
    before set bit */
    while (n > 1)
    {
    n >>= 1;
    count += 1;
    }

    /* If count is a multiple
    of log2(d) then return
    true else false*/
    return (count % (Log2n(d)) == 0);
}

/* If there are more than
1 bit set then n is not
a power of 4*/
return false;
}

// Driver Code
static void Main()
{
int n = 64, d = 8;
if (isPowerOfd(n, d))
    Console.WriteLine("{0} is a " +
                    "power of {1}",
                            n, d);
else
    Console.WriteLine("{0} is not a"+
                    " power of {1}",
                            n, d);
}

// This code is contributed by mits
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// is power of d where d is power of 2.

function Log2n($n)
{
    return ($n > 1)? 1 +
    Log2n($n / 2): 0;
}

function isPowerOfd($n, $d)
{
    $count = 0;

// Check if there is only
// one bit set in n
if ($n && !($n & ($n - 1)))
{

    // count 0 bits
    // before set bit
    while ($n > 1)
    {
        $n >>= 1;
        $count += 1;
    }

    /* If count is a multiple of log2(d)
    then return true else false*/
    return ($count%(Log2n($d)) == 0);
}

    /* If there are more than 1 bit set
    then n is not a power of 4*/
    return false;
}

// Driver Code
$n = 64;
$d = 8;
if (isPowerOfd($n, $d))
    echo $n," ","is a power of ", $d;
else
    echo $n," ","is not a power of ", $d;

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to find if
// a number is power of d
// where d is power of 2
function Log2n(n)
{
    return (n > 1) ? 1 +
      Log2n(n / 2) : 0;
}

// Function to count the number
// of ways to paint  N * 3 grid
// based on given conditions
function isPowerOfd(n, d)
{
    var count = 0;

    /* Check if there is
    only one bit set in n*/
    if (n > 0 && (n & (n - 1)) == 0)
    {

        /* count 0 bits
        before set bit */
        while (n > 1)
        {
            n >>= 1;
            count += 1;
        }

        /* If count is a multiple
        of log2(d) then return
        true else false*/
        return (count % (Log2n(d)) == 0);
    }

    /* If there are more
    than 1 bit set then
    n is not a power of 4*/
    return false;
}

// Driver code
var n = 64, d = 8;

if (isPowerOfd(n, d))
    document.write(n +
                " is a power of " + d);
else
    document.write(n +
                " is not a power of " + d);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
64 is a power of 8
```

***时间复杂度:** O(log <sub>2</sub> n)*

***辅助空间:** O(1)*