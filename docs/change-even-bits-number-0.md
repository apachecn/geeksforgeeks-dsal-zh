# 将一个数字中的所有偶数位改为 0

> 原文:[https://www.geeksforgeeks.org/change-even-bits-number-0/](https://www.geeksforgeeks.org/change-even-bits-number-0/)

给定一个数字，将偶数位置的所有位都改为 0。

**示例:**

```
Input : 30
Output : 10
Binary representation of 11110. 
Bits at Even positions are highlighted. 
After making all of them 0, we get 01010

Input :  10
Output :  10
```

**方法 1(位遍历)**

这个想法是遍历所有偶数比特。我们把一个数的 2 的所有幂累加起来相减。最后我们从 n 中减去累加值得到结果。

## C++

```
// C++ program to change even
// bits to 0.
#include <bits/stdc++.h>
using namespace std;

// Returns modified number with
// all even bits 0.
int changeEvenBits(int n)
{
    // To store sum of bits
    // at even positions.
    int to_subtract = 0;

    // To store bits to shift
    int m = 0;

    // One by one put all even
    // bits to end
    for (int x = n; x; x >>= 2) {
        // If current last bit
        // is set, add it to ans
        if (x & 1)
            to_subtract += (1 << m);

        // Next shift position
        m += 2;
    }

    return n - to_subtract;
}

// Driver code
int main()
{
    int n = 30;
    cout << changeEvenBits(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change even
// bits to 0.
import java.util.*;
class GFG {
    // Returns modified number with
    // all even bits 0.
    static int changeEvenBits(int n)
    {
        // To store sum of bits
        // at even positions.
        int to_subtract = 0;

        // To store bits to shift
        int m = 0;

        // One by one put all even
        // bits to end
        for (int x = n; x > 0; x >>= 2) {
            // If current last bit
            // is set, add it to ans
            if ((x & 1) > 0)
                to_subtract += (1 << m);

            // Next shift position
            m += 2;
        }

        return n - to_subtract;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 30;
        System.out.println(changeEvenBits(n));
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 计算机编程语言

```
# Python program to change even
# bits to 0.

# Returns modified number with
# all even bits 0.

def changeEvenBits(n):

    # To store sum of bits
    # at even positions.
    to_subtract = 0

    # To store bits to shift
    m = 0

    # One by one put all even
    # bits to end
    x = n
    while(x):

        # If current last bit
        # is set, add it to ans
        if (x & 1):
            to_subtract += (1 << m)

        # Next shift position
        m += 2
        x >>= 2

    return n - to_subtract

# Driver code
n = 30
print changeEvenBits(n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to change even
// bits to 0.
using System;

class GFG {

    // Returns modified number with
    // all even bits 0.
    static int changeEvenBits(int n)
    {

        // To store sum of bits
        // at even positions.
        int to_subtract = 0;

        // To store bits to shift
        int m = 0;

        // One by one put all even
        // bits to end
        for (int x = n; x > 0; x >>= 2)
        {

            // If current last bit
            // is set, add it to ans
            if ((x & 1) > 0)
            to_subtract += (1 << m);

            // Next shift position
            m += 2;
        }

        return n - to_subtract;
    }

    // Driver code
    public static void Main()
    {
        int n = 30;

        Console.Write(changeEvenBits(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to change even
// bits to 0.

// Returns modified number with
// all even bits 0.
function changeEvenBits($n)
{

    // To store sum of bits
    // at even positions.
    $to_subtract = 0;

    // To store bits to shift
    $m = 0;

    // One by one put all even
    // bits to end
    for ($x = $n; $x; $x >>= 2)
    {

        // If current last bit
        // is set, add it to ans
        if ($x & 1)
        $to_subtract += (1 << $m);

        // Next shift position
        $m += 2;
    }

    return $n - $to_subtract;
}

    // Driver code
    $n = 30;
    echo changeEvenBits($n) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// js program to change even
// bits to 0.

// Returns modified number with
// all even bits 0.
function changeEvenBits(n)
{

    // To store sum of bits
    // at even positions.
    let to_subtract = 0;

    // To store bits to shift
    let m = 0;

    // One by one put all even
    // bits to end
    for (x = n; x; x >>= 2)
    {

        // If current last bit
        // is set, add it to ans
        if (x & 1)
        to_subtract += (1 << m);

        // Next shift position
        m += 2;
    }

    return n - to_subtract;
}

    // Driver code
    n = 30;
    document.write( changeEvenBits(n) );

// This code is contributed by sravan kumar

</script>
```

**Output**

```
10
```

**方法 2:(位屏蔽)**

## C++

```
#include <bits/stdc++.h>
using namespace std;

int convertEvenBitToOne(int n) { return (n & 0xaaaaaaaa); }

int main()
{
    int n = 30;
    cout << convertEvenBitToOne(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program using Bitmask to
// Change all even bits in a
// number to 0
import java.io.*;

class GFG {

    static int convertEvenBitToOne(int n)
    {
        return (n & 0xaaaaaaaa);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 30;
        System.out.println(convertEvenBitToOne(n));
    }
}

// This code is contributed by anuj_67.
```

## 计算机编程语言

```
def convertEvenBitToOne(n):
    return (n & 0xaaaaaaaa)

# Driver code
n = 30
print convertEvenBitToOne(n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program using Bitmask to
// Change all even bits in a
// number to 0
using System;

class GFG {

    static long convertEvenBitToOne(int n)
    {
        return (n & 0xaaaaaaaa);
    }

    // Driver code
    public static void Main()
    {
        int n = 30;
        Console.WriteLine(convertEvenBitToOne(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program using Bitmask to
// Change all even bits in a
// number to 0

function convertEvenBitToOne($n)
{
    return ($n & 0xaaaaaaaa);
}

// Driver Code
$n = 30;
echo convertEvenBitToOne($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// java script program using Bitmask to
// Change all even bits in a
// number to 0

function convertEvenBitToOne(n)
{
    return (n & 0xaaaaaaaa);
}

// Driver Code
n = 30;
document.write(convertEvenBitToOne(n));
// This code is contributed by sravan kumar

</script>
```

**Output**

```
10
```

本文由**里沙布·拉杰·JHA**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。