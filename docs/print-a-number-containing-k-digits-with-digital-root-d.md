# 用数字根 D 打印一个包含 K 位数字的数字

> 原文:[https://www . geesforgeks . org/print-a-number-contain-k-digits-digital-root-d/](https://www.geeksforgeeks.org/print-a-number-containing-k-digits-with-digital-root-d/)

给定一个数字根“D”和数字个数“K”。任务是打印一个包含 K 位数字的数字，该数字的[数字根](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/)等于 d。如果该数字不存在，则打印“-1”。

**示例:**

```
Input: D = 4, K = 4
Output: 4000
No. of digits is 4.
Sum of digits is also 4.

Input:  D = 0, K = 1
Output: 0
```

**方法:**解决这个问题的一个关键观察是，在一个数字上附加任何数量的 0 都不会改变其数字根。因此 **D 后跟(K-1) 0 的**是一个简单的解决方案。

> D 为 0，K 不为 1 的特殊情况没有解决办法，因为数字根为 0 的唯一数字本身就是 0。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a number
void printNumberWithDR(int k, int d)
{

    // If d is 0 k has to be 1
    if (d == 0 && k != 1)
        cout << "-1";

    else {
        cout << d;
        k--;

        // Print k-1 zeroes
        while (k--)
            cout << "0";
    }
}

// Driver code
int main()
{
    int k = 4, d = 4;

    printNumberWithDR(k, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {

// Function to find a number
static void printNumberWithDR(int k, int d)
{

    // If d is 0 k has to be 1
    if (d == 0 && k != 1)
        System.out.print( "-1");

    else {
        System.out.print(d);
        k--;

        // Print k-1 zeroes
        while (k-->0)
            System.out.print( "0");
    }
}

// Driver code

    public static void main (String[] args) {
            int k = 4, d = 4;

    printNumberWithDR(k, d);
    }
}

//This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to find a number
def printNumberWithDR( k, d ) :

    # If d is 0, k has to be 1
    if d == 0 and k != 1 :
        print(-1, end = "")

    else :
        print(d, end = "")
        k -= 1

        # Print k-1 zeroes
        while k :

            print(0,end = "")
            k -= 1

# Driver code    
if __name__ == "__main__" :

    k, d = 4, 4

    # Function call
    printNumberWithDR( k, d )

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

// Function to find a number
static void printNumberWithDR(int k, int d)
{

    // If d is 0 k has to be 1
    if (d == 0 && k != 1)
        Console.Write( "-1");

    else {

        Console.Write(d);
        k--;

        // Print k-1 zeroes
        while (k-->0)
            Console.Write( "0");
    }
}

// Driver code
static public void Main ()
{
    int k = 4, d = 4;

    printNumberWithDR(k, d);
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find a number
function printNumberWithDR($k, $d)
{

    // If d is 0 k has to be 1
    if ($d == 0 && $k != 1)
        echo "-1";

    else
    {
        echo $d;
        $k--;

        // Print k-1 zeroes
        while ($k--)
            echo "0";
    }
}

// Driver code
$k = 4;
$d = 4;

printNumberWithDR($k, $d);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find a number
function printNumberWithDR(k, d)
{

    // If d is 0 k has to be 1
    if (d == 0 && k != 1)
        document.write("-1");

    else
    {
        document.write(d);
        k--;

        // Print k-1 zeroes
        while (k-->0)
            document.write("0");
    }
}

// Driver Code
var k = 4, d = 4;

printNumberWithDR(k, d);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
4000
```

**时间复杂度:** O(K)