# 检查两个数字是否仅在一个位位置不同

> 原文:[https://www . geesforgeks . org/check-two-numbers-different-one-bit-position/](https://www.geeksforgeeks.org/check-whether-two-numbers-differ-one-bit-position/)

给定两个非负整数 **a** 和 **b** 。问题是检查这两个数字是否仅在一个位位置不同。
示例:

```
Input : a = 13, b = 9
Output : Yes
(13)<sub>10</sub> = (1101)2
(9)<sub>10</sub> = (1001)2
Both the numbers differ at one bit position only, i.e,
differ at the 3rd bit from the right.

Input : a = 15, b = 8
Output : No
```

**进场:**以下为步骤:

1.  计算 **num** = a ^ b。
2.  检查**数**是否为 2 的幂。参考[这篇](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)帖子。

## C++

```
// C++ implementation to check whether the two
// numbers differ at one bit position only
#include <bits/stdc++.h>
using namespace std;

// function to check if x is power of 2
bool isPowerOfTwo(unsigned int x)
{
    // First x in the below expression is
    // for the case when x is 0
    return x && (!(x & (x - 1)));
}

// function to check whether the two numbers
// differ at one bit position only
bool differAtOneBitPos(unsigned int a,
                       unsigned int b)
{
    return isPowerOfTwo(a ^ b);
}

// Driver program to test above
int main()
{
    unsigned int a = 13, b = 9;
    if (differAtOneBitPos(a, b))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether the two 
// numbers differ at one bit position only
import java.io.*;
import java.util.*;

class GFG {
      // function to check if x is power of 2
      static boolean isPowerOfTwo(int x)
      {
             // First x in the below expression is
             // for the case when x is 0
             return x!= 0 && ((x & (x - 1)) == 0);
      }

      // function to check whether the two numbers
      // differ at one bit position only
      static boolean differAtOneBitPos(int a, int b)
      {
             return isPowerOfTwo(a ^ b);
      }
      // Driver code
      public static void main(String args[])
      {
             int a = 13, b = 9;
             if (differAtOneBitPos(a, b) == true)
                 System.out.println("Yes");
             else
                 System.out.println("No");
      }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 implementation to check whether the two
# numbers differ at one bit position only

# function to check if x is power of 2
def isPowerOfTwo( x ):

    # First x in the below expression is
    # for the case when x is 0
    return x and (not(x & (x - 1)))

# function to check whether the two numbers
# differ at one bit position only
def differAtOneBitPos( a , b ):
    return isPowerOfTwo(a ^ b)

# Driver code to test above
a = 13
b = 9
if (differAtOneBitPos(a, b)):
    print("Yes")
else:
    print( "No")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# implementation to check whether the two
// numbers differ at one bit position only
using System;
class GFG
{

    // function to check if x is power of 2
    static bool isPowerOfTwo(int x)
    {
        // First x in the below expression is
        // for the case when x is 0
        return x != 0 && ((x & (x - 1)) == 0);
    }

    // function to check whether the two numbers
    // differ at one bit position only
    static bool differAtOneBitPos(int a, int b)
    {
        return isPowerOfTwo(a ^ b);
    }

    // Driver code
    public static void Main()
    {
        int a = 13, b = 9;
        if (differAtOneBitPos(a, b) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether the two numbers differ
// at one bit position only

    // function to check if x is power of 2
    function isPowerOfTwo($x)
    {
        $y = 0;

        // First x in the below expression is
        // for the case when x is 0
        if($x && (!($x & ($x - 1))))
        $y = 1;
        return $y;
    }

    // function to check whether
    // the two numbers differ at
    // one bit position only
    function differAtOneBitPos($a,$b)
    {
        return isPowerOfTwo($a ^ $b);
    }

        // Driver Code
        $a = 13;
        $b = 9;
        if (differAtOneBitPos($a, $b))
            echo "Yes";
        else
            echo "No";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript program to check whether the two 
// numbers differ at one bit position only

      // function to check if x is power of 2
      function isPowerOfTwo(x)
      {

             // First x in the below expression is
             // for the case when x is 0
             return x!= 0 && ((x & (x - 1)) == 0);
      }

      // function to check whether the two numbers
      // differ at one bit position only
      function differAtOneBitPos(a, b)
      {
             return isPowerOfTwo(a ^ b);
      }

// Driver code         
        let a = 13, b = 9;
             if (differAtOneBitPos(a, b) == true)
                 document.write("Yes");
             else
                 document.write("No");

       // This code is contributed by code_hunt.
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(1)。