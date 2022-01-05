# 两个数字中最右边公共位的位置

> 原文:[https://www . geesforgeks . org/position-最右侧-common-bit-two-numbers/](https://www.geeksforgeeks.org/position-rightmost-common-bit-two-numbers/)

给定两个非负数 **m** 和 **n** 。找到数字的二进制表示中最右边相同位的位置。

示例:

```
Input : m = 10, n = 9
Output : 3
(10)<sub>10</sub> = (1010)2
(9)<sub>10</sub> = (1001)2
It can be seen that the 3rd bit
from the right is same.

Input : m = 16, n = 7
Output : 4
(16)<sub>10</sub> = (10000)2
(7)<sub>10</sub> = (111)2, can also be written as
     = (00111)2
It can be seen that the 4th bit
from the right is same.
```

**方法:**对 **m** 和 **n** 进行逐位异或运算。让它成为 **xor_value** = m ^ n .现在，[获取 **xor_value** 中最右边未置位位](https://www.geeksforgeeks.org/get-position-rightmost-unset-bit/)的位置。

**说明:**按位异或运算产生的数字只有在 **m** 和 **n** 的位相同的位置才有未置位的位。因此， **xor_value** 中最右边未设置位的位置给出了最右边相同位的位置。

## C++

```
// C++ implementation to find the position
// of rightmost same bit
#include <bits/stdc++.h>

using namespace std;

// Function to find the position of
// rightmost set bit in 'n'
int getRightMostSetBit(unsigned int n)
{
    return log2(n & -n) + 1;
}

// Function to find the position of
// rightmost same bit in the
// binary representations of 'm' and 'n'
int posOfRightMostSameBit(unsigned int m,
                          unsigned int n)
{
    // position of rightmost same bit
    return getRightMostSetBit(~(m ^ n));
}

// Driver program to test above
int main()
{
    int m = 16, n = 7;
    cout << "Position = "
         << posOfRightMostSameBit(m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the position
// of rightmost same bit
class GFG {

    // Function to find the position of
    // rightmost set bit in 'n'
    static int getRightMostSetBit(int n)
    {
        return (int)((Math.log(n & -n))/(Math.log(2)))
                                                  + 1;
    }

    // Function to find the position of
    // rightmost same bit in the
    // binary representations of 'm' and 'n'
    static int posOfRightMostSameBit(int m,int n)
    {

        // position of rightmost same bit
        return getRightMostSetBit(~(m ^ n));
    }

    //Driver code
    public static void main (String[] args)
    {
        int m = 16, n = 7;

        System.out.print("Position = "
            + posOfRightMostSameBit(m, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to find the
# position of rightmost same bit
import math

# Function to find the position
# of rightmost set bit in 'n'
def getRightMostSetBit(n):

    return int(math.log2(n & -n)) + 1

# Function to find the position of
# rightmost same bit in the binary
# representations of 'm' and 'n'
def posOfRightMostSameBit(m, n):

    # position of rightmost same bit
    return getRightMostSetBit(~(m ^ n))

# Driver Code
m, n = 16, 7
print("Position = ", posOfRightMostSameBit(m, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to find the position
// of rightmost same bit
using System;

class GFG
{
    // Function to find the position of
    // rightmost set bit in 'n'
    static int getRightMostSetBit(int n)
    {
        return (int)((Math.Log(n & -n)) / (Math.Log(2))) + 1;
    }

    // Function to find the position of
    // rightmost same bit in the
    // binary representations of 'm' and 'n'
    static int posOfRightMostSameBit(int m,int n)
    {
        // position of rightmost same bit
        return getRightMostSetBit(~(m ^ n));
    }

    //Driver code
    public static void Main ()
    {
        int m = 16, n = 7;
        Console.Write("Position = "
              + posOfRightMostSameBit(m, n));
    }
}
//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find the position
// of rightmost same bit

// Function to find the position of
// rightmost set bit in 'n'
function getRightMostSetBit($n)
{
    return log($n & -$n) + 1;
}

// Function to find the position of
// rightmost same bit in the
// binary representations of 'm' and 'n'
function posOfRightMostSameBit($m,
                               $n)
{

    // position of rightmost same bit
    return getRightMostSetBit(~($m ^ $n));
}

    // Driver Code
    $m = 16; $n = 7;
    echo "Position = "
        , ceil(posOfRightMostSameBit($m, $n));

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript implementation to find the position
// of rightmost same bit

// Function to find the position of
// rightmost set bit in 'n'
function getRightMostSetBit(n)
{
    return Math.log2(n & -n) + 1;
}

// Function to find the position of
// rightmost same bit in the
// binary representations of 'm' and 'n'
function posOfRightMostSameBit(m, n)
{

    // position of rightmost same bit
    return getRightMostSetBit(~(m ^ n));
}

// Driver program to test above
    let m = 16, n = 7;
    document.write("Position = "
        + posOfRightMostSameBit(m, n));

// This code is contributed by Manoj.
</script>
```

**输出:**

```
Position = 4
```

**替代方法:**直到两个值都变为零，检查两个数字的最后一位并右移。任何时候，两个位都是相同的，返回计数器。

**说明:**两个值 **m** 和 **n** 的最右位只有在两个值为奇数或偶数时才相等。

## C++

```
// C++ implementation to find the position
// of rightmost same bit
#include <iostream>
using namespace std;

// Function to find the position of
// rightmost same bit in the binary
// representations of 'm' and 'n'
static int posOfRightMostSameBit(int m, int n)
{

    // Initialize loop counter
    int loopCounter = 1;

    while (m > 0 || n > 0)
    {

        // Check whether the value 'm' is odd
        bool a = m % 2 == 1;

        // Check whether the value 'n' is odd
        bool b = n % 2 == 1;

        // Below 'if' checks for both
        // values to be odd or even
        if (!(a ^ b))
        {
            return loopCounter;
        }

        // Right shift value of m
        m = m >> 1;

        // Right shift value of n
        n = n >> 1;
        loopCounter++;
    }

    // When no common set is found
    return -1;
}

// Driver code
int main()
{
    int m = 16, n = 7;

    cout << "Position = "
         <<  posOfRightMostSameBit(m, n);
}

// This code is contributed by shivanisinghss2110
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the position
// of rightmost same bit
class GFG {

    // Function to find the position of
    // rightmost same bit in the
    // binary representations of 'm' and 'n'
    static int posOfRightMostSameBit(int m,int n)
    {
        int loopCounter = 1; // Initialize loop counter
        while (m > 0 || n > 0){

            boolean a = m%2 == 1; //Check whether the value 'm' is odd
            boolean b = n%2 == 1; //Check whether the value 'n' is odd

            // Below 'if' checks for both values to be odd or even
            if (!(a ^ b)){
                return loopCounter;}

            m = m >> 1; //Right shift value of m
            n = n >> 1; //Right shift value of n
            loopCounter++;
        }
        return -1; //When no common set is found
    }

    //Driver code
    public static void main (String[] args)
    {
        int m = 16, n = 7;

        System.out.print("Position = "
            + posOfRightMostSameBit(m, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the position
# of rightmost same bit

# Function to find the position of
# rightmost same bit in the
# binary representations of 'm' and 'n'
def posOfRightMostSameBit(m, n):

    # Initialize loop counter
    loopCounter = 1

    while (m > 0 or n > 0):

        # Check whether the value 'm' is odd
        a = m % 2 == 1

        # Check whether the value 'n' is odd
        b = n % 2 == 1

        # Below 'if' checks for both
        # values to be odd or even
        if (not (a ^ b)):
            return loopCounter

        # Right shift value of m
        m = m >> 1

        # Right shift value of n
        n = n >> 1
        loopCounter += 1

    # When no common set is found
    return -1

# Driver code
if __name__ == '__main__':

    m, n = 16, 7

    print("Position = ",
    posOfRightMostSameBit(m, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the position
// of rightmost same bit
using System;
class GFG
{

  // Function to find the position of
  // rightmost same bit in the
  // binary representations of 'm' and 'n'
  static int posOfRightMostSameBit(int m, int n)
  {
    int loopCounter = 1; // Initialize loop counter
    while (m > 0 || n > 0)
    {

      Boolean a = m % 2 == 1; // Check whether the value 'm' is odd
      Boolean b = n % 2 == 1; // Check whether the value 'n' is odd

      // Below 'if' checks for both values to be odd or even
      if (!(a ^ b))
      {
        return loopCounter;
      }

      m = m >> 1; // Right shift value of m
      n = n >> 1; // Right shift value of n
      loopCounter++;
    }
    return -1; // When no common set is found
  }

  // Driver code
  public static void Main (String[] args)
  {
    int m = 16, n = 7;        
    Console.Write("Position = "
                  + posOfRightMostSameBit(m, n));
  }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript implementation to find the position
// of rightmost same bit

// Function to find the position of
// rightmost same bit in the binary
// representations of 'm' and 'n'
function posOfRightMostSameBit(m, n)
{

    // Initialize loop counter
    let loopCounter = 1;

    while (m > 0 || n > 0)
    {

        // Check whether the value 'm' is odd
        let a = m % 2 == 1;

        // Check whether the value 'n' is odd
        let b = n % 2 == 1;

        // Below 'if' checks for both
        // values to be odd or even
        if (!(a ^ b))
        {
            return loopCounter;
        }

        // Right shift value of m
        m = m >> 1;

        // Right shift value of n
        n = n >> 1;
        loopCounter++;
    }

    // When no common set is found
    return -1;
}

// Driver code
    let m = 16, n = 7;

    document.write("Position = "
        + posOfRightMostSameBit(m, n));

// This code is contributed by Manoj.
</script>
```

**输出:**

```
Position = 4
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。