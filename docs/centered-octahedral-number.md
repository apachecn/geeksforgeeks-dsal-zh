# 中心八面体数

> 原文:[https://www.geeksforgeeks.org/centered-octahedral-number/](https://www.geeksforgeeks.org/centered-octahedral-number/)

给我们一个数 n，我们需要找到第 n 个中心八面体数。
**描述:**一个居中的八面体数是一个具象数。它计算位于以原点为中心的八面体内部的三维整数点阵的点数。相同的数字是[德拉诺尼数字](https://www.geeksforgeeks.org/delannoy-number/)的特例，它计算某些二维点阵路径。
前几个居中的八面体数**(其中 n = 0、1、2、3……)。)**是:
1，7，25，63，129，231，377，575，833，1159……………。
第 n 个**中心八面体数的数学公式:** 

**例:**

```
Input : n = 6
Output : 377

Input : n = 15
Output : 4991
```

## C++

```
// C++ Program to find nth
// Centered octahedral number
#include <bits/stdc++.h>
using namespace std;

// Function to find
// Centered octahedral number

int centeredOctahedral(int n)
{
    // Formula to calculate nth
    // Centered octahedral number
    // and return it into main function.
    return (2 * n + 1) * (2 * n * n + 2 * n + 3) / 3;
}

// Driver Code
int main()
{
    int n = 3;
    cout << centeredOctahedral(n) << endl;

    n = 9;
    cout << centeredOctahedral(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find nth
// Centered octahedral number
import java.io.*;

class GFG
{
    // Function to find
    // Centered octahedral number
    static int centeredOctahedral(int n)
    {

    // Formula to calculate nth
    // Centered octahedral number
    // and return it into main function.

    return (2 * n + 1) *
           (2 * n * n + 2 * n + 3) / 3;
    }

    // Driver Code
    public static void main (String[] args)
    {
    int n = 3;
    System.out.print( centeredOctahedral(n));
    System.out.println();
    n = 9;
    System.out.print(centeredOctahedral(n));
    }
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# Python 3 Program to find nth
# Centered octahedral number

# Centered octahedral
# number function
def centeredOctahedral(n) :

    # Formula to calculate nth
    # Centered octahedral number
    # return it into main function.
    return (2 * n + 1) * (
            2 * n * n +
            2 * n + 3) // 3

# Driver Code
if __name__ == '__main__' :

    n = 3
    print(centeredOctahedral(n))
    n = 9
    print(centeredOctahedral(n))

# This code is contributed ajit
```

## C#

```
// C# Program to find nth
// Centered octahedral number
using System;

public class GFG {

    // Function to find
    // Centered octahedral number
    static int centeredOctahedral(int n)
    {

        // Formula to calculate nth
        // Centered octahedral number
        // and return it into main function.

        return (2 * n + 1) *
            (2 * n * n + 2 * n + 3) / 3;
    }

    // Driver Code
    static public void Main ()
    {
        int n = 3;
        Console.WriteLine(
               centeredOctahedral(n));

        n = 9;
        Console.WriteLine(
              centeredOctahedral(n));
    }
}

// This code is contributed by m_kit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find nth
// Centered octahedral number

// Function to find
// Centered octahedral number
function centeredOctahedral($n)
{
    // Formula to calculate
    // nth Centered octahedral
    // number and return it
    // into main function.
    return (2 * $n + 1) *
           (2 * $n * $n +
            2 * $n + 3) / 3;
}

// Driver Code
$n = 3;
echo centeredOctahedral($n), "\n";

$n = 9;
echo centeredOctahedral($n), "\n";

// This code is contributed ajit
?>
```

## java 描述语言

```
<script>

// Javascript Program to find nth
// Centered octahedral number

// Function to find
// Centered octahedral number
function centeredOctahedral(n)
{

    // Formula to calculate nth
    // Centered octahedral number
    // and return it into main function.

    return (2 * n + 1) *
           (2 * n * n + 2 * n + 3) / 3;
}

// Driver Code

var n = 3;
document.write(centeredOctahedral(n));
document.write("<br>");

n = 9;
document.write(centeredOctahedral(n));

// This code is contributed by Kirti

</script>
```

**Output :** 

```
63
1159
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

参考:
T1】https://en.wikipedia.org/wiki/Centered_octahedral_numberT3】