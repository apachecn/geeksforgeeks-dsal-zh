# 中心二十面体数程序

> 原文:[https://www . geesforgeks . org/program-centered-二十面体-number/](https://www.geeksforgeeks.org/program-centered-icosahedral-number/)

给我们一个数 n，我们需要找到第 n 个中心二十面体数。
**描述:**一个中心二十面体数是一个代表一个[二十面体](https://en.wikipedia.org/wiki/Icosahedron)的中心图形数。
**前几个居中的二十面体数**系列是:
1、13、55、147、309、561、923、1415、2057、2869、3871、5083、6525、8217……
第 n 个**中心二十面体数的数学公式:** 

**例:**

```
Input : n = 4
Output : 309

Input : n = 12
Output : 6525
```

下面是上面公式
的实现

## C++

```
// C++ Program to find nth
// Centered icosahedral number
#include <bits/stdc++.h>
using namespace std;

// Function to find
// Centered icosahedral number
int centeredIcosahedralNum(int n)
{
    // Formula to calculate nth
    // Centered icosahedral number
    // and return it into main function.
    return (2 * n + 1) * (5 * n * n + 5 * n + 3) / 3;
}

// Driver Code
int main()
{
    int n = 10;
    cout << centeredIcosahedralNum(n) << endl;

    n = 12;
    cout << centeredIcosahedralNum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find nth
// Centered icosahedral number
// Java Program to find nth Centered
// icosahedral number

import java.io.*;

class GFG {

    // Function to find Centered
    // icosahedral number
    static int centeredIcosahedralNum(int n)
    {

        // Formula to calculate nth Centered
        // icosahedral number and return it
        // into main function.
        return (2 * n + 1) * (5 * n * n +
                             5 * n + 3) / 3;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 10;
        System.out.println(
                   centeredIcosahedralNum(n));

        n = 12;
        System.out.println(
                   centeredIcosahedralNum(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to find nth
# Centered icosahedral number

# Function to calculate
# Centered icosahedral number

def centeredIcosahedralNum(n):

    # Formula to calculate nth
    # Centered icosahedral number
    return ((2 * n + 1) *
            (5 * n * n + 5 * n + 3) // 3)

# Driver Code
n = 10
print(centeredIcosahedralNum(n))

n = 12
print(centeredIcosahedralNum(n))

# This code is contributed by ajit.                
```

## C#

```
// C# Program to find nth
// Centered icosahedral number
// Java Program to find nth Centered
// icosahedral number

using System;

class GFG {

    // Function to find Centered
    // icosahedral number
    static int centeredIcosahedralNum(int n)
    {

        // Formula to calculate nth Centered
        // icosahedral number and return it
        // into main function.
        return (2 * n + 1) * (5 * n * n +
                            5 * n + 3) / 3;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 10;
        Console.WriteLine(
                centeredIcosahedralNum(n));

        n = 12;
        Console.WriteLine(
                centeredIcosahedralNum(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find nth
// Centered icosahedral number

// Function to find
// Centered icosahedral number
function centeredIcosahedralNum($n)
{
    // Formula to calculate nth
    // Centered icosahedral number
    // and return it into main function.
    return (2 * $n + 1) * (5 *
            $n * $n + 5 * $n + 3) / 3;
}

// Driver Code
$n = 10;
echo centeredIcosahedralNum($n),"\n";

$n = 12;
echo centeredIcosahedralNum($n),"\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript Program to find nth
// Centered icosahedral number

// Function to find
// Centered icosahedral number
function centeredIcosahedralNum(n)
{

    // Formula to calculate nth
    // Centered icosahedral number
    // and return it into main function.
    return parseInt((2 * n + 1) * (5 * n * n + 5 * n + 3) / 3);
}

// Driver Code
let n = 10;
document.write(centeredIcosahedralNum(n) + "<br>");

n = 12;
document.write(centeredIcosahedralNum(n));

// This code is contributed by souravmahato348.
</script>
```

**Output :** 

```
3871
6525
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

参考:
T1】https://en.wikipedia.org/wiki/Centered_icosahedral_numberT3】