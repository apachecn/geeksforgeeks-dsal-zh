# 寻找奇偶性的程序

> 原文:[https://www.geeksforgeeks.org/program-to-find-parity/](https://www.geeksforgeeks.org/program-to-find-parity/)

**奇偶性:**一个数的奇偶性是指它是包含奇数还是偶数个 1 位。如果该数包含奇数个 1 位，则该数具有“奇数奇偶校验”，如果该数包含偶数个 1 位，则该数具有“偶数奇偶校验”。
以下解决方案的主要思想是–当 n 不为 0 时循环，并在循环中取消设置一个设置位并反转奇偶校验。

```
Algorithm: getParity(n)
1\. Initialize parity = 0
2\. Loop while n != 0      
      a. Invert parity 
             parity = !parity
      b. Unset rightmost set bit
             n = n & (n-1)
3\. return parity

Example:
 Initialize: n = 13 (1101)   parity = 0

n = 13 & 12  = 12 (1100)   parity = 1
n = 12 & 11 = 8  (1000)   parity = 0
n = 8 & 7 = 0  (0000)    parity = 1
```

**节目:**

## C++

```
// C++ program to find parity
// of an integer
# include<bits/stdc++.h>
# define bool int
using namespace std;

// Function to get parity of number n. It returns 1
// if n has odd parity, and returns 0 if n has even
// parity
bool getParity(unsigned int n)
{
    bool parity = 0;
    while (n)
    {
        parity = !parity;
        n     = n & (n - 1);
    }    
    return parity;
}

/* Driver program to test getParity() */
int main()
{
    unsigned int n = 7;
    cout<<"Parity of no "<<n<<" = "<<(getParity(n)? "odd": "even");

    getchar();
    return 0;
}
```

## C

```
// C program to find parity
// of an integer
# include <stdio.h>
# define  bool int

/* Function to get parity of number n. It returns 1
   if n has odd parity, and returns 0 if n has even
   parity */
bool getParity(unsigned int n)
{
    bool parity = 0;
    while (n)
    {
        parity = !parity;
        n      = n & (n - 1);
    }       
    return parity;
}

/* Driver program to test getParity() */
int main()
{
    unsigned int n = 7;
    printf("Parity of no %d = %s",  n,
             (getParity(n)? "odd": "even"));

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find parity
// of an integer
import java.util.*;
import java.lang.*;
import java.io.*;
import java.math.BigInteger;

class GFG
 {
    /* Function to get parity of number n.
    It returns 1 if n has odd parity, and
    returns 0 if n has even parity */
    static boolean getParity(int n)
    {
        boolean parity = false;
        while(n != 0)
        {
            parity = !parity;
            n = n & (n-1);
        }
        return parity;

    }

    /* Driver program to test getParity() */
    public static void main (String[] args)
    {
        int n = 12;
        System.out.println("Parity of no " + n + " = " +
                         (getParity(n)? "odd": "even"));
    }
}
/* This code is contributed by Amit khandelwal*/
```

## 蟒蛇 3

```
# Python3 code to get parity.

# Function to get parity of number n.
# It returns 1 if n has odd parity,
# and returns 0 if n has even parity
def getParity( n ):
    parity = 0
    while n:
        parity = ~parity
        n = n & (n - 1)
    return parity

# Driver program to test getParity()
n = 7
print ("Parity of no ", n," = ",
     ( "odd" if getParity(n) else "even"))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find parity of an integer
using System;

class GFG {

    /* Function to get parity of number n.
    It returns 1 if n has odd parity, and
    returns 0 if n has even parity */
    static bool getParity(int n)
    {
        bool parity = false;
        while(n != 0)
        {
            parity = !parity;
            n = n & (n-1);
        }
        return parity;

    }

    // Driver code
    public static void Main ()
    {
        int n = 7;
        Console.Write("Parity of no " + n
                 + " = " + (getParity(n)?
                          "odd": "even"));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the parity
// of an unsigned integer

// Function to get parity of
// number n. It returns 1
// if n has odd parity, and
// returns 0 if n has even
// parity
function getParity( $n)
{
    $parity = 0;
    while ($n)
    {
        $parity = !$parity;
        $n = $n & ($n - 1);
    }
    return $parity;
}

    // Driver Code
    $n = 7;
    echo "Parity of no ",$n ," = " ,
          getParity($n)? "odd": "even";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find parity
// of an integer

// Function to get parity of number n.
// It returns 1 if n has odd parity, and
// returns 0 if n has even parity
function getParity(n)
{
    var parity = false;
    while(n != 0)
    {
        parity = !parity;
        n = n & (n - 1);
    }
    return parity;
}

// Driver code
var n = 7;
document.write("Parity of no " + n + " = " +
              (getParity(n) ? "odd": "even"));

// This code is contributed by Kirti

</script>
```

**输出:**

```
Parity of no 7 = odd
```

上述解决方案可以通过使用查找表来优化。详情请参考比特旋转黑客[第一参考]。
**时间复杂度:**上述算法花费的时间与设置的位数成正比。最坏的情况是复杂度为 0(对数 n)。

**辅助空间:** O(1)
**用途:**奇偶校验用于错误检测和密码学。
[**使用 XOR 和查表计算一个数的奇偶性**](https://www.geeksforgeeks.org/compute-parity-number-using-xor-table-look/)
**参考文献:**
[http://graphics . Stanford . edu/~ seander/bithacks . html # parity naive](http://graphics.stanford.edu/~seander/bithacks.html#ParityNaive)–上次检查是 2009 年 5 月 30 日。