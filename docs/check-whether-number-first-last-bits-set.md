# 检查号码是否只设置了第一位和最后一位

> 原文:[https://www . geesforgeks . org/check-when-number-first-last-bits-set/](https://www.geeksforgeeks.org/check-whether-number-first-last-bits-set/)

给定正整数 **n** 。问题是检查在 **n** 的二进制表示中是否只设置了第一位和最后一位。
**例:**

```
Input : 9
Output : Yes
(9)<sub>10</sub> = (1001)2, only the first and
last bits are set.

Input : 15
Output : No
(15)<sub>10</sub> = (1111)2, except first and last
there are other bits also which are set.
```

**进场:**以下为步骤:

1.  如果 n == 1，则返回“是”。
2.  否则检查 n-1 是否是 2 的幂。参考[本](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)岗位。

## C++

```
// C++ to check whether the number has only
// first and last bits set
#include <bits/stdc++.h>

using namespace std;

// function to check whether 'n'
// is a power of 2 or not
bool powerOfTwo(unsigned int n)
{
    return (!(n & n-1));
}

// function to check whether the number has only
// first and last bits set
bool onlyFirstAndLastAreSet(unsigned int n)
{
    if (n == 1)
        return true;
    if (n == 2)
        return false;
    return powerOfTwo(n-1);   
}

// Driver program to test above
int main()
{
    unsigned int n = 9;

    if (onlyFirstAndLastAreSet(n))
        cout << "Yes";
    else
        cout << "No";   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the
// number has only first and last
// bits set
import java.util.*;

class GFG
{
    // function to check whether 'n'
    // is a power of 2 or not
    static boolean powerOfTwo(int n)
    {
        return ((n & n - 1) == 0);
    }

    // function to check whether the number has 
    // only first and last bits set
    static boolean onlyFirstAndLastAreSet(int n)
    {
        if (n == 1)
            return true;

        return powerOfTwo(n-1);
    }

    // Driver program to test above
    public static void main (String[] args) {

       int n = Integer.parseUnsignedInt("9");

        if (onlyFirstAndLastAreSet(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python3 program to check whether number
# has only first and last bits set

# function to check whether 'n'
# is a power of 2 or not
def powerOfTwo (n):
    return (not(n & n-1))

# function to check whether number 
# has only first and last bits set
def onlyFirstAndLastAreSet (n):

    if (n == 1):
        return True
    return powerOfTwo (n-1)

# Driver program to test above
n = 9
if (onlyFirstAndLastAreSet (n)):
    print('Yes')
else:
    print('No')

# This code is contributed by Shariq Raza
```

## C#

```
// C# program to check whether the
// number has only first and last
// bits set
using System;

class GFG {

    // function to check whether 'n'
    // is a power of 2 or not
    static bool powerOfTwo(uint n)
    {
        return ((n & n - 1) == 0);
    }

    // function to check whether the number has
    // only first and last bits set
    static bool onlyFirstAndLastAreSet(uint n)
    {
        if (n == 1)
            return true;

        return powerOfTwo(n - 1);
    }

    // Driver program to test above
    public static void Main()
    {

        uint n = (uint)9;

        if (onlyFirstAndLastAreSet(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to check whether the number
// has only first and last bits set

// function to check whether 'n'
// is a power of 2 or not
function powerOfTwo($n)
{
    return (!($n & $n - 1));
}

// function to check whether
// the number has only first
// and last bits set
function onlyFirstAndLastAreSet($n)
{
    if ($n == 1)
        return true;
    if ($n == 2)
        return false;
    return powerOfTwo($n - 1);    
}

// Driver Code
$n = 9;

if (onlyFirstAndLastAreSet($n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript to check whether the number has only
// first and last bits set

// function to check whether 'n'
// is a power of 2 or not
function powerOfTwo(n)
{
    return (!(n & n-1));
}

// function to check whether the number has only
// first and last bits set
function onlyFirstAndLastAreSet(n)
{
    if (n == 1)
        return true;
    if (n == 2)
        return false;
    return powerOfTwo(n-1);    
}

// Driver program to test above
var n = 9;

if (onlyFirstAndLastAreSet(n))
    document.write("Yes");
else
    document.write("No");    

</script>
```

**输出:**

```
Yes
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。