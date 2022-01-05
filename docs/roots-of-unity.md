# 团结之根

> 原文:[https://www.geeksforgeeks.org/roots-of-unity/](https://www.geeksforgeeks.org/roots-of-unity/)

给定一个小整数 n，打印单位的所有 n 个根，最多 6 个有效数字。我们基本上需要找到方程 x<sup>n</sup>–1 的所有根。

**示例:**

```
Input :  n = 1
Output : 1.000000 + i 0.000000
x - 1 = 0 , has only one root i.e., 1

Input :  2
Output : 1.000000 + i 0.000000
    -1.000000 + i 0.000000
x2 - 1 = 0 has 2 distinct roots, i.e., 1 and -1 
```

任何一个复数，如果加到某个幂时给出 1，则称之为单位根。
单位的第 n 个根是任何复数，当升到 n 的幂时，它给出 1。

```
Mathematically, 
An nth root of unity, where n is a positive integer 
(i.e. n = 1, 2, 3, …) is a number z satisfying the
equation 

z^n  = 1
or , 
z^n - 1 = 0
```

我们可以在这里使用[德莫瓦夫公式](https://en.wikipedia.org/wiki/De_Moivre%27s_formula)，

```
( Cos x + i Sin x )^k = Cos kx + i Sin kx

Setting x = 2*pi/n, we can obtain all the nth roots 
of unity, using the fact that Nth roots are set of 
numbers given by,

Cos (2*pi*k/n) + i Sin(2*pi*k/n)
Where, 0 <= k < n
```

利用上述事实，我们可以很容易地打印出所有的第 n 个统一的根！

下面是同样的程序。

## C++

```
// C++ program to print n'th roots of unity
#include <bits/stdc++.h>
using namespace std;

// This function receives an integer n , and prints
// all the nth roots of unity
void printRoots(int n)
{
    // theta = 2*pi/n
    double theta = M_PI*2/n;

    // print all nth roots with 6 significant digits
    for(int k=0; k<n; k++)
    {
        // calculate the real and imaginary part of root
        double real = cos(k*theta);
        double img = sin(k*theta);

        // Print real and imaginary parts
        printf("%.6f", real);
        img >= 0? printf(" + i "): printf(" - i ");
        printf("%.6f\n", abs(img));
    }
}

// Driver function to check the program
int main()
{
    printRoots(1);
    cout << endl;
    printRoots(2);
    cout << endl;
    printRoots(3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print n'th roots of unity
import java.io.*;

class GFG {

// This function receives an integer n , and prints
// all the nth roots of unity
static void printRoots(int n)
{
    // theta = 2*pi/n
    double theta = 3.14*2/n;

    // print all nth roots with 6 significant digits
    for(int k=0; k<n; k++)
    {
        // calculate the real and imaginary part of root
        double real = Math.cos(k*theta);
        double img = Math.sin(k*theta);

        // Print real and imaginary parts
        System.out.println(real);
        if (img >= 0)
            System.out.println(" + i ");
        else
            System.out.println(" - i ");
        System.out.println(Math.abs(img));
    }
}

// Driver function to check the program
public static void main (String[] args)
{
    printRoots(1);
    //System.out.println();
    printRoots(2);
    //System.out.println();
    printRoots(3);
}
}
// This code is contributed by Raj
```

## 蟒蛇 3

```
# Python3 program to print n'th roots of unity

import math

# This function receives an integer n , and prints
# all the nth roots of unity
def printRoots(n):

    # theta = 2*pi/n
    theta = math.pi * 2 / n

    # print all nth roots with 6 significant digits
    for k in range(0, n):

        # calculate the real and imaginary part of root
        real = math.cos(k * theta)
        img = math.sin(k * theta)

        # Print real and imaginary parts
        print(real, end=" ")
        if(img >= 0):
            print(" + i ", end=" ")
        else:
            print(" - i ", end=" ")
        print(abs(img))

# Driver function to check the program
if __name__=='__main__':
    printRoots(1)
    printRoots(2)
    printRoots(3)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print n'th roots of unity
using System;

class GFG {

// This function receives an integer n , and prints
// all the nth roots of unity
static void printRoots(int n)
{
    // theta = 2*pi/n
    double theta = 3.14*2/n;

    // print all nth roots with 6 significant digits
    for(int k=0; k<n; k++)
    {
        // calculate the real and imaginary part of root
        double real = Math.Cos(k*theta);
        double img = Math.Sin(k*theta);

        // Print real and imaginary parts
        Console.Write(real);
        if (img >= 0)
            Console.Write(" + i ");
        else
            Console.Write(" - i ");
        Console.WriteLine(Math.Abs(img));
    }
}

// Driver function to check the program
static void Main()
{
    printRoots(1);

    printRoots(2);

    printRoots(3);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print n'th roots of unity

// This function receives an integer n,
// and prints all the nth roots of unity
function printRoots($n)
{

    // theta = 2*pi/n
    $theta = pi() * 2 / $n;

    // print all nth roots with 6
    // significant digits
    for($k = 0; $k < $n; $k++)
    {
        // calculate the real and imaginary
        // part of root
        $real = cos($k * $theta);
        $img = sin($k * $theta);

        // Print real and imaginary parts
        print(round($real, 6));
        $img >= 0 ? print(" + i "): print(" - i ");
        printf(round(abs($img), 6) . "\n");
    }
}

// Driver Code
printRoots(1);
printRoots(2);
printRoots(3);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to print n'th roots of unity

// This function receives an integer n , and prints
// all the nth roots of unity
function printRoots(n)
{
    // theta = 2*pi/n
    var theta = (3.14*2/n);

    // print all nth roots with 6 significant digits
    for(k = 0; k < n; k++)
    {
        // calculate the real and imaginary part of root
        var real = Math.cos(k*theta);
        var img = Math.sin(k*theta);

        // Print real and imaginary parts
        document.write(real.toFixed(6));
        if (img >= 0)
            document.write(" + i ");
        else
            document.write(" - i ");
        document.write(Math.abs(img).toFixed(6)+'<br>');
    }
}

// Driver function to check the program
printRoots(1);

//document.write('<br>');
printRoots(2);

//document.write('<br>');
printRoots(3);

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
1.000000 + i 0.000000
1.000000 + i 0.000000
-1.000000 + i 0.000000
1.000000 + i 0.000000
-0.500000 + i 0.866025
-0.500000 - i 0.866025
```

参考文献:[维基百科](http://http://www.wikipedia.org/)

本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。