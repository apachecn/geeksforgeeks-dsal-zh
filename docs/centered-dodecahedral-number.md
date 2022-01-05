# 居中十二面体数

> 原文:[https://www.geeksforgeeks.org/centered-dodecahedral-number/](https://www.geeksforgeeks.org/centered-dodecahedral-number/)

给定一个数 n，求第 **n 个**中心十二面体数。
一个**中心十二面体数**是一类比喻数。它由一个中心点形成，周围是连续的十二面体(多面体有 12 个平面)层。
前几个居中的十二面体数**(其中 n = 0、1、2、3……)。)**有:
1、33、155、427、909、1661…………
**例:**

```
Input : 5
Output : 1661

Input :1
Output :33
```

**第 n 个**中心十二面体数的数学公式如下:

以下是上述思路的基本实现:

## C++

```
// Program to find nth centered
// dodecahedral number
#include <bits/stdc++.h>
using namespace std;

// Function to find
// centered dodecahedral number
int CenteredDodecahedral_num(long int n)
{
    // Formula to calculate nth
    // centered dodecahedral number
    // and return it into main function.
    return (2 * n + 1) * (5 * n * n + 5 * n + 1);
}
// Driver Code
int main()
{
    long int n = 3;
    // print result
    cout << n << "th Centered Dodecahedral number : ";
    cout << CenteredDodecahedral_num(n) << endl;

    n = 10;
    // print result
    cout << n << "th Centered Dodecahedral number : ";
    cout << CenteredDodecahedral_num(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find nth
// centered dodecahedral number
import java.io.*;

class GFG {

    // Function to find centered
    // dodecahedral number
    static int CenteredDodecahedral_num(int n)
    {

        // Formula to calculate nth
        // centered dodecahedral number
        // and return it into main function.

        return (2 * n + 1) *
                     (5 * n * n + 5 * n + 1);
    }

    // Driver Code
    public static void main (String[] args)
    {

        int n = 3;

        // print result
        System.out.print( n + "th Centered "
                + "Dodecahedral number : ");
        System.out.println (
                CenteredDodecahedral_num(n));

        n = 10;

        // print result
        System.out.print( n + "th Centered "
                + "Dodecahedral number : ");
        System.out.println(
               CenteredDodecahedral_num(n));
    }
}

// This code is contributed by m_kit.
```

## 蟒蛇 3

```
# Program to find nth centered
# dodecahedral number

# Function to find centered
# dodecahedral number
def CenteredDodecahedral_num(n) :

    # Formula to calculate nth
    # centered dodecahedral number
    return (2 * n + 1) * (5 * n * n + 5 * n + 1)

# Driver Code
if __name__ == '__main__' :

    n = 3
    print(n,"rd centered dodecahedral number: ",
                CenteredDodecahedral_num(n))
    n = 10
    print(n,"th centered dodecahedral number : ",
                CenteredDodecahedral_num(n))

# This code is contributed by aj_36
```

## C#

```
// C# Program to find
// nth centered
// dodecahedral number
using System;

class GFG
{

    // Function to find
    // nth centered
    // dodecahedral number
    static int CenteredDodecahedral_num(int n)
    {

        // Formula to calculate
        // nth centered dodecahedral
        // number and return it
        // into main function.
        return (2 * n + 1) *
               (5 * n * n +
                5 * n + 1);
    }

    // Driver Code
    static public void Main ()
    {
        int n = 3;

        // print result
        Console.Write( n + "th Centered " +
                 "Dodecahedral number : ");
        Console.WriteLine(
                CenteredDodecahedral_num(n));

        n = 10;

        // print result
        Console.Write( n + "th Centered " +
                 "Dodecahedral number : ");
        Console.WriteLine(
                CenteredDodecahedral_num(n));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find nth centered
// dodecahedral number

// Function to find
// centered dodecahedral number
function CenteredDodecahedral_num($n)
{
    // Formula to calculate nth
    // centered dodecahedral number
    // and return it into main function.
    return (2 * $n + 1) *
           (5 * $n * $n +
            5 * $n + 1);
}

// Driver Code
$n = 3;
// print result
echo $n, "th Centered Dodecahedral " .
                          "number : ";
echo CenteredDodecahedral_num($n),"\n";

$n = 10;
// print result
echo $n, "th Centered Dodecahedral " .
                          "number : ";
echo CenteredDodecahedral_num($n);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript Program to find nth
// centered dodecahedral number

// Function to find centered
// dodecahedral number
function CenteredDodecahedral_num(n)
{

    // Formula to calculate nth
    // centered dodecahedral number
    // and return it into main function.
    return (2 * n + 1) *
           (5 * n * n + 5 * n + 1);
}

// Driver code
var n = 3;

// print result
document.write(n + "th Centered " +
               "Dodecahedral number : ");
document.write(CenteredDodecahedral_num(n) + "<br>");

n = 10;

// print result
document.write(n + "th Centered " +
               "Dodecahedral number : ");
document.write(CenteredDodecahedral_num(n));

// This code is contributed by Khushboogoyal499

</script>
```

**输出:**

```
3th Centered Dodecahedral number : 427
10th Centered Dodecahedral number : 11571
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

**参考文献:**T2[https://en.wikipedia.org/wiki/Centered_dodecahedral_number](https://en.wikipedia.org/wiki/Centered_dodecahedral_number)T5】