# 大于或等于 n 的 2 的最小幂

> 原文:[https://www . geesforgeks . org/2 的最小幂大于或等于 n/](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/)

写一个函数，对于给定的 n，求一个大于或等于 n 并且是 2 的最小幂的数 p。

**示例:**

```
    Input : n = 5
    Output: 8     

    Input  : n = 17
    Output : 32     

    Input  : n = 32
    Output : 32     
```

对此有很多解决方案。让我们以 17 为例来解释其中的一些。

**方法 1(使用对数)**

```
    1\.  Calculate Position of set bit in p(next power of 2):
        pos =  ceil(lgn)  (ceiling of log n with base 2)
    2\.  Now calculate p:
        p   = pow(2, pos) 
```

**示例:**

```
    Let us try for 17
            pos = 5
            p   = 32    
```

**方法 2(通过获取结果中唯一设置位的位置)**

```
    /* If n is a power of 2 then return n */
    1  If (n & !(n&(n-1))) then return n 
    2  Else keep right shifting n until it becomes zero 
        and count no of shifts
        a. Initialize: count = 0
        b. While n ! = 0
                n = n>>1
                count = count + 1

     /* Now count has the position of set bit in result */
    3  Return (1 << count)  
```

**示例:**

```
    Let us try for 17
                 count = 5
                 p     = 32   
```

## C++

```
// C++ program to find
// smallest power of 2
// greater than or equal to n
#include <bits/stdc++.h>
using namespace std;

unsigned int nextPowerOf2(unsigned int n)
{
    unsigned count = 0;

    // First n in the below condition
    // is for the case where n is 0
    if (n && !(n & (n - 1)))
        return n;

    while( n != 0)
    {
        n >>= 1;
        count += 1;
    }

    return 1 << count;
}

// Driver Code
int main()
{
    unsigned int n = 0;
    cout << nextPowerOf2(n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>

unsigned int nextPowerOf2(unsigned int n)
{
unsigned count = 0;

// First n in the below condition
// is for the case where n is 0
if (n && !(n & (n - 1)))
    return n;

while( n != 0)
{
    n >>= 1;
    count += 1;
}

return 1 << count;
}

// Driver Code
int main()
{
unsigned int n = 0;
printf("%d", nextPowerOf2(n));
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// smallest power of 2
// greater than or equal to n
import java.io.*;

class GFG
{
    static int nextPowerOf2(int n)
    {
        int count = 0;

        // First n in the below
        // condition is for the
        // case where n is 0
        if (n > 0 && (n & (n - 1)) == 0)
            return n;

        while(n != 0)
        {
            n >>= 1;
            count += 1;
        }

        return 1 << count;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 0;
        System.out.println(nextPowerOf2(n));
    }
}

// This article is contributed
// by Anshika Goyal.
```

## 蟒蛇 3

```
def nextPowerOf2(n):
    count = 0

    # First n in the below
    # condition is for the
    # case where n is 0
    if (n and not(n & (n - 1))):
        return n

    while( n != 0):
        n >>= 1
        count += 1

    return 1 << count

# Driver Code
n = 0
print(nextPowerOf2(n))
# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// C# program to find smallest
// power of 2 greater than
// or equal to n
using System;

class GFG
{
    static int nextPowerOf2(int n)
    {
        int count = 0;

        // First n in the below
        // condition is for the
        // case where n is 0
        if (n > 0 && (n & (n - 1)) == 0)
            return n;

        while(n != 0)
        {
            n >>= 1;
            count += 1;
        }

        return 1 << count;
    }

    // Driver Code
    public static void Main()
    {
        int n = 0;
        Console.WriteLine(nextPowerOf2(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest
// power of 2 greater than or
// equal to n

function nextPowerOf2($n)
{
$count = 0;

// First n in the below condition
// is for the case where n is 0
if ($n && !($n&($n - 1)))
    return $n;

while($n != 0)
{
    $n >>= 1;
    $count += 1;
}

return 1 << $count;
}

// Driver Code
$n = 0;
echo (nextPowerOf2($n));

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>

// JavaScript program to find
// smallest power of 2
// greater than or equal to n

function nextPowerOf2(n)
{
    var count = 0;

    // First n in the below condition
    // is for the case where n is 0
    if (n && !(n & (n - 1)))
        return n;

    while( n != 0)
    {
        n >>= 1;
        count += 1;
    }

    return 1 << count;
}

// Driver Code
var n = 0;
document.write(nextPowerOf2(n));

</script>
```

**输出:**

```
1
```

**时间复杂度:** O(对数 n)

**辅助空间:** O(1)
**方法 3(逐个移位结果)**
感谢 coderyogi 提出这个方法。这个方法是方法 2 的一个变体，我们不是获取计数，而是在一个循环中一个接一个地移动结果。

## C++

```
// C++ program to find smallest
// power of 2 greater than or
// equal to n
#include<bits/stdc++.h>
using namespace std;
unsigned int nextPowerOf2(unsigned int n)
{
    unsigned int p = 1;
    if (n && !(n & (n - 1)))
        return n;

    while (p < n)
        p <<= 1;

    return p;
}

// Driver Code
int main()
{
    unsigned int n = 5;
    cout << nextPowerOf2(n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
unsigned int nextPowerOf2(unsigned int n)
{
    unsigned int p = 1;
    if (n && !(n & (n - 1)))
        return n;

    while (p < n)
        p <<= 1;

    return p;
}

// Driver Code
int main()
{
unsigned int n = 5;
printf("%d", nextPowerOf2(n));
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest
// power of 2 greater than or
// equal to n
import java.io.*;

class GFG
{
    static int nextPowerOf2(int n)
    {
        int p = 1;
        if (n > 0 && (n & (n - 1)) == 0)
            return n;

        while (p < n)
            p <<= 1;

        return p;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(nextPowerOf2(n));
    }
}

// This article is contributed
// by Anshika Goyal.
```

## 蟒蛇 3

```
def nextPowerOf2(n):

    p = 1
    if (n and not(n & (n - 1))):
        return n

    while (p < n) :
        p <<= 1

    return p;

# Driver Code
n = 5
print(nextPowerOf2(n));

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find smallest
// power of 2 greater than or
// equal to n
using System;

class GFG
{

    static int nextPowerOf2(int n)
    {
        int p = 1;
        if (n > 0 && (n & (n - 1)) == 0)
            return n;

        while (p < n)
            p <<= 1;

        return p;
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        Console.Write(nextPowerOf2(n));
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

function nextPowerOf2($n)
{
    $p = 1;
    if ($n && !($n & ($n - 1)))
        return $n;

    while ($p < $n)
        $p <<= 1;

    return $p;
}

// Driver Code
$n = 5;
echo ( nextPowerOf2($n));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// Program to find smallest
// power of 2 greater than or
// equal to n

function  nextPowerOf2( n)
{
    p = 1;
    if (n && !(n & (n - 1)))
        return n;

    while (p < n)
        p <<= 1;

    return p;
}

// Driver Code

     n = 5;
    document.write (nextPowerOf2(n));

    //This code is contributed by simranarora5sos
</script>
```

**输出:**

```
8
```

**时间复杂度:** O(lgn)

**辅助空间:** O(1)

**方法 4(定制和快速)**

```
    1\. Subtract n by 1
       n = n -1

    2\. Set all bits after the leftmost set bit.

    /* Below solution works only if integer is 32 bits */
                n = n | (n >> 1);
                n = n | (n >> 2);
                n = n | (n >> 4);
                n = n | (n >> 8);
                n = n | (n >> 16);
    3\. Return n + 1
```

**示例:**

```
Steps 1 & 3 of above algorithm are to handle cases 
of power of 2 numbers e.g., 1, 2, 4, 8, 16,

    Let us try for 17(10001)
    step 1
       n = n - 1 = 16 (10000)  
    step 2
       n = n | n >> 1
       n = 10000 | 01000
       n = 11000
       n = n | n >> 2
       n = 11000 | 00110
       n = 11110
       n = n | n >> 4
       n = 11110 | 00001
       n = 11111
       n = n | n >> 8
       n = 11111 | 00000
       n = 11111
       n = n | n >> 16
       n = 11110 | 00000
       n = 11111    

    step 3: Return n+1
     We get n + 1 as 100000 (32)
```

**程序:**

## C++

```
// C++ program to 
// Finds next power of two
// for n. If n itself is a
// power of two then returns n
#include <bits/stdc++.h>
using namespace std;

unsigned int nextPowerOf2(unsigned int n) 
{
    n--;
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;
    n++;
    return n;
}

// Driver Code 
int main() 
{ 
    unsigned int n = 5; 
    cout << nextPowerOf2(n); 
    return 0; 
} 

// This code is contributed by SHUBHAMSINGH10
```

## C

```
#include <stdio.h>
// Finds next power of two
// for n. If n itself is a
// power of two then returns n
unsigned int nextPowerOf2(unsigned int n)
{
    n--;
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;
    n++;
    return n;
}

// Driver Code
int main()
{
    unsigned int n = 5;
    printf("%d", nextPowerOf2(n));
    return 0;
}    
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest
// power of 2 greater than or
// equal to n
import java.io.*;

class GFG
{
    // Finds next power of two
    // for n. If n itself is a
    // power of two then returns n
    static int nextPowerOf2(int n)
    {
        n--;
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;
        n++;

        return n;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(nextPowerOf2(n));
    }
}

// This article is contributed
// by Anshika Goyal.
```

## 蟒蛇 3

```
# Finds next power of two
# for n. If n itself is a
# power of two then returns n
def nextPowerOf2(n):

    n -= 1
    n |= n >> 1
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16
    n += 1
    return n

# Driver program to test
# above function
n = 5
print(nextPowerOf2(n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find smallest
// power of 2 greater than or
// equal to n
using System;

class GFG
{

    // Finds next power of two
    // for n. If n itself is a
    // power of two then returns n
    static int nextPowerOf2(int n)
    {
        n--;
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;
        n++;

        return n;
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(nextPowerOf2(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest
// power of 2 greater than or
// equal to n

// Finds next power of
// two for n. If n itself
// is a power of two then
// returns n
function nextPowerOf2($n)
{
    $n--;
    $n |= $n >> 1;
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;
    $n++;
    return $n;
}

    // Driver Code
    $n = 5;
    echo nextPowerOf2($n);

// This code contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find smallest
// power of 2 greater than or
// equal to n

// Finds next power of
// two for n. If n itself
// is a power of two then
// returns n
function nextPowerOf2(n)
{
    n -= 1
    n |= n >> 1
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16
    n += 1
    return n
}

// Driver Code
n = 5;
document.write (nextPowerOf2(n));

// This code is contributed by bunnyram19

</script>
```

**输出:**

```
8
```

**时间复杂度:** O(lgn)

**辅助空间:** O(1)
**相关岗位:**
[最高 2 次方小于等于给定数](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)
**参考文献:**
[http://en.wikipedia.org/wiki/Power_of_2](http://en.wikipedia.org/wiki/Power_of_2)