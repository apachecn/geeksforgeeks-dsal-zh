# 帕斯卡的三角

> 哎哎哎:# t0]https://www . geeksforgeeks . org/Pascal-triangle/

[帕斯卡三角形](http://en.wikipedia.org/wiki/Pascal's_triangle)是二项式系数的三角形数组。编写一个以整数值 n 为输入的函数，打印帕斯卡三角形的前 n 行。下面是帕斯卡三角形的前 6 行。

```
1  
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1 
1 5 10 10 5 1 
```

**方法 1 ( O(n^3)时间复杂度)**
每行的条目数等于行号。比如第一行有“1”，第二行有“1 1”，第三行有“1 2 1”，..等等。一行中的每个条目都是一个[二项系数](http://en.wikipedia.org/wiki/Binomial_coefficient)的值。第*行*中第 ***i*** 条目的值为 *C(行，i)* 。该值可以使用以下公式计算。

```
C(line, i)   = line! / ( (line-i)! * i! ) 
```

一个简单的方法是运行两个循环，并计算内环中二项式系数的值。

## C++

```
//  C++ code for Pascal's Triangle
#include <iostream>
using namespace std;

// See https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
// for details of this function
int binomialCoeff(int n, int k);

// Function to print first
// n lines of Pascal's
// Triangle
void printPascal(int n)
{
    // Iterate through every line and
    // print entries in it
    for (int line = 0; line < n; line++)
    {
        // Every line has number of
        // integers equal to line
        // number
        for (int i = 0; i <= line; i++)
            cout <<" "<< binomialCoeff(line, i);
        cout <<"\n";
    }
}

// See https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
// for details of this function
int binomialCoeff(int n, int k)
{
    int res = 1;
    if (k > n - k)
    k = n - k;
    for (int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Driver program
int main()
{
    int n = 7;
    printPascal(n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
//  C++ code for Pascal's Triangle
#include <stdio.h>

// See https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
// for details of this function
int binomialCoeff(int n, int k);

// Function to print first
// n lines of Pascal's
// Triangle
void printPascal(int n)
{
    // Iterate through every line and
    // print entries in it
    for (int line = 0; line < n; line++)
    {
        // Every line has number of
        // integers equal to line
        // number
        for (int i = 0; i <= line; i++)
            printf("%d ",
                    binomialCoeff(line, i));
        printf("\n");
    }
}

// See https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
// for details of this function
int binomialCoeff(int n, int k)
{
    int res = 1;
    if (k > n - k)
    k = n - k;
    for (int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Driver program
int main()
{
    int n = 7;
    printPascal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Pascal's Triangle
import java.io.*;

class GFG {

    // Function to print first
    // n lines of Pascal's Triangle
    static void printPascal(int n)
    {

    // Iterate through every line
    // and print entries in it
    for (int line = 0; line < n; line++)
    {
        // Every line has number of
        // integers equal to line number
        for (int i = 0; i <= line; i++)
        System.out.print(binomialCoeff
                        (line, i)+" ");

        System.out.println();
    }
    }

    // Link for details of this function
    // https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
    static int binomialCoeff(int n, int k)
    {
        int res = 1;

        if (k > n - k)
        k = n - k;

        for (int i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }
        return res;
    }

    // Driver code
    public static void main(String args[])
    {
    int n = 7;
    printPascal(n);
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 code for Pascal's Triangle
# A simple O(n^3)
# program for
# Pascal's Triangle

# Function to print
# first n lines of
# Pascal's Triangle
def printPascal(n) :

    # Iterate through every line
    # and print entries in it
    for line in range(0, n) :

        # Every line has number of
        # integers equal to line
        # number
        for i in range(0, line + 1) :
            print(binomialCoeff(line, i),
                " ", end = "")
        print()

# See https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
# for details of this function
def binomialCoeff(n, k) :
    res = 1
    if (k > n - k) :
        k = n - k
    for i in range(0 , k) :
        res = res * (n - i)
        res = res // (i + 1)

    return res

# Driver program
n = 7
printPascal(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code for Pascal's Triangle
using System;

class GFG {

    // Function to print first
    // n lines of Pascal's Triangle
    static void printPascal(int n)
    {

    // Iterate through every line
    // and print entries in it
    for (int line = 0; line < n; line++)
    {
        // Every line has number of
        // integers equal to line number
        for (int i = 0; i <= line; i++)
        Console.Write(binomialCoeff
                        (line, i)+" ");

        Console.WriteLine();
    }
    }

    // Link for details of this function
    // https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
    static int binomialCoeff(int n, int k)
    {
        int res = 1;

        if (k > n - k)
        k = n - k;

        for (int i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
    int n = 7;
    printPascal(n);
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation for
// Pascal's Triangle

// for details of this function
function binomialCoeff($n, $k)
{
    $res = 1;
    if ($k > $n - $k)
    $k = $n - $k;
    for ($i = 0; $i < $k; ++$i)
    {
        $res *= ($n - $i);
        $res /= ($i + 1);
    }
return $res;
}

// Function to print first
// n lines of Pascal's
// Triangle
function printPascal($n)
{
    // Iterate through every line and
    // print entries in it
    for ($line = 0; $line < $n; $line++)
    {
        // Every line has number of
        // integers equal to line
        // number
        for ($i = 0; $i <= $line; $i++)
                echo "".binomialCoeff($line, $i)." ";

        echo "\n";
    }
}

// Driver Code
$n=7;
printPascal($n);

// This code is contributed by Mithun Kumar
?>
```

## java 描述语言

```
<script>

// Javascript code for Pascal's Triangle

    // Function to print first
    // n lines of Pascal's Triangle
    function printPascal(n)
    {

    // Iterate through every line
    // and print entries in it
    for (let line = 0; line < n; line++)
    {
        // Every line has number of
        // integers equal to line number
        for (let i = 0; i <= line; i++)
        document.write(binomialCoeff
                        (line, i)+" ");

        document.write("<br />");
    }
    }

    // Link for details of this function
    // https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/
    function binomialCoeff(n, k)
    {
        let res = 1;

        if (k > n - k)
        k = n - k;

        for (let i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }
        return res;
    }

// Driver Code

    let n = 7;
    printPascal(n);

</script>
```

**输出:**

```
1 
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1 
1 5 10 10 5 1 
1 6 15 20 15 6 1 
```

***辅助空间:** O(1)*

这种方法的时间复杂度是 O(n^3).以下是优化方法。
**方法 2( O(n^2)时间和 O(n^2)额外空间)**
如果我们仔细观察三角形，我们观察到每个条目都是它上面两个值的和。因此，我们可以创建一个存储以前生成的值的 2D 数组。要在一行中生成一个值，我们可以使用数组中先前存储的值。

![](img/de27c3e15c24496f3d5635741c6c6b90.png)

## C++

```
// C++ program for Pascal’s Triangle
// A O(n^2) time and O(n^2) extra space
// method for Pascal's Triangle
#include <bits/stdc++.h>
using namespace std;

void printPascal(int n)
{

    // An auxiliary array to store
    // generated pascal triangle values
    int arr[n][n];

    // Iterate through every line and
    // print integer(s) in it
    for (int line = 0; line < n; line++)
    {
        // Every line has number of integers
        // equal to line number
        for (int i = 0; i <= line; i++)
        {
        // First and last values in every row are 1
        if (line == i || i == 0)
            arr[line][i] = 1;
        // Other values are sum of values just
        // above and left of above
        else
            arr[line][i] = arr[line - 1][i - 1] +
                            arr[line - 1][i];
        cout << arr[line][i] << " ";
        }
        cout << "\n";
    }
}

// Driver code
int main()
{
    int n = 5;
    printPascal(n);
    return 0;
}

// This code is Contributed by Code_Mech.
```

## C

```
// C program for Pascal’s Triangle
// A O(n^2) time and O(n^2) extra space
// method for Pascal's Triangle
void printPascal(int n)
{
// An auxiliary array to store
// generated pascal triangle values
int arr[n][n];

// Iterate through every line and print integer(s) in it
for (int line = 0; line < n; line++)
{
    // Every line has number of integers
    // equal to line number
    for (int i = 0; i <= line; i++)
    {
    // First and last values in every row are 1
    if (line == i || i == 0)
        arr[line][i] = 1;
    // Other values are sum of values just
    // above and left of above
    else
        arr[line][i] = arr[line-1][i-1] + arr[line-1][i];
    printf("%d ", arr[line][i]);
    }
    printf("\n");
}
}
// Driver code
int main()
{
int n = 5;
    printPascal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for Pascal's Triangle
// A O(n^2) time and O(n^2) extra
// space method for Pascal's Triangle
import java.io.*;

class GFG {
    public static void main (String[] args) {
        int n = 5;
        printPascal(n);
    }

public static void printPascal(int n)
{
// An auxiliary array to store generated pascal triangle values
int[][] arr = new int[n][n];

// Iterate through every line and print integer(s) in it
for (int line = 0; line < n; line++)
{
    // Every line has number of integers equal to line number
    for (int i = 0; i <= line; i++)
    {
    // First and last values in every row are 1
    if (line == i || i == 0)
        arr[line][i] = 1;
    else // Other values are sum of values just above and left of above
        arr[line][i] = arr[line-1][i-1] + arr[line-1][i];
    System.out.print(arr[line][i]);
    }
    System.out.println("");
}
}
}
```

## 蟒蛇 3

```
# Python3 program for Pascal's Triangle

# A O(n^2) time and O(n^2) extra
# space method for Pascal's Triangle
def printPascal(n:int):

    # An auxiliary array to store
    # generated pascal triangle values
    arr = [[0 for x in range(n)]
              for y in range(n)]

    # Iterate through every line
    # and print integer(s) in it
    for line in range (0, n):

        # Every line has number of
        # integers equal to line number
        for i in range (0, line + 1):

            # First and last values
            # in every row are 1
            if(i is 0 or i is line):
                arr[line][i] = 1
                print(arr[line][i], end = " ")

            # Other values are sum of values
            # just above and left of above
            else:
                arr[line][i] = (arr[line - 1][i - 1] +
                                arr[line - 1][i])
                print(arr[line][i], end = " ")            
        print("\n", end = "")

# Driver Code
n = 5
printPascal(n)

# This code is contributed
# by Sanju Maderna
```

## C#

```
// C# program for Pascal's Triangle
// A O(n^2) time and O(n^2) extra
// space method for Pascal's Triangle
using System;

class GFG
{
public static void printPascal(int n)
{

// An auxiliary array to store
// generated pascal triangle values
int[,] arr = new int[n, n];

// Iterate through every line
// and print integer(s) in it
for (int line = 0; line < n; line++)
{
    // Every line has number of
    // integers equal to line number
    for (int i = 0; i <= line; i++)
    {

    // First and last values
    // in every row are 1
    if (line == i || i == 0)
        arr[line, i] = 1;
    else // Other values are sum of values
         // just above and left of above
        arr[line, i] = arr[line - 1, i - 1] +
                       arr[line - 1, i];
    Console.Write(arr[line, i]);
    }
Console.WriteLine("");
}
}

// Driver Code
public static void Main ()
{
    int n = 5;
    printPascal(n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Pascal’s Triangle
// A O(n^2) time and O(n^2) extra space
// method for Pascal's Triangle
function printPascal($n)
{
    // An auxiliary array to store
    // generated pascal triangle values
    $arr = array(array());

    // Iterate through every line and
    // print integer(s) in it
    for ($line = 0; $line < $n; $line++)
    {
        // Every line has number of integers
        // equal to line number
        for ($i = 0; $i <= $line; $i++)
        {
            // First and last values in every row are 1
            if ($line == $i || $i == 0)
                $arr[$line][$i] = 1;

            // Other values are sum of values just
            // above and left of above
            else
                $arr[$line][$i] = $arr[$line - 1][$i - 1] +
                                $arr[$line - 1][$i];
            echo $arr[$line][$i] . " ";
        }
        echo "\n";
    }
}

// Driver code
$n = 5;
printPascal($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript program for Pascal's Triangle
// A O(n^2) time and O(n^2) extra
// space method for Pascal's Triangle
var n = 5;
printPascal(n);

function printPascal(n)
{
// An auxiliary array to store generated pascal triangle values
arr = a = Array(n).fill(0).map(x => Array(n).fill(0));

// Iterate through every line and print integer(s) in it
for (line = 0; line < n; line++)
{
    // Every line has number of integers equal to line number
    for (i = 0; i <= line; i++)
    {
    // First and last values in every row are 1
    if (line == i || i == 0)
        arr[line][i] = 1;
    else
    // Other values are sum of values just above and left of above
        arr[line][i] = arr[line-1][i-1] + arr[line-1][i];
    document.write(arr[line][i]);
    }
    document.write("<br>");
}
}

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
1 
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1 
```

这个方法可以优化为使用 O(n)个额外空间，因为我们只需要前一行的值。所以我们可以创建一个大小为 n 的辅助数组并覆盖值。下面是另一种只使用 O(1)个额外空间的方法。
**方法 3 ( O(n^2)时间和 O(1)额外空间)**
这个方法是基于方法 1。我们知道 ***i*** 行号*行*中的第一个条目是二项式系数 *C(行，i)* ，所有行都以值 1 开始。思路是用 *C(线，i-1)* 计算 *C(线，i)* 。可以使用以下公式计算 O(1)时间。

```
C(line, i)   = line! / ( (line-i)! * i! )
C(line, i-1) = line! / ( (line - i + 1)! * (i-1)! )
We can derive following expression from above two expressions.
C(line, i) = C(line, i-1) * (line - i + 1) / i

So C(line, i) can be calculated from C(line, i-1) in O(1) time
```

## C++

```
// C++ program for Pascal’s Triangle
// A O(n^2) time and O(1) extra space
// function for Pascal's Triangle
#include <bits/stdc++.h>

using namespace std;
void printPascal(int n)
{

for (int line = 1; line <= n; line++)
{
    int C = 1; // used to represent C(line, i)
    for (int i = 1; i <= line; i++)
    {

        // The first value in a line is always 1
        cout<< C<<" ";
        C = C * (line - i) / i;
    }
    cout<<"\n";
}
}

// Driver code
int main()
{
    int n = 5;
    printPascal(n);
    return 0;
}

// This code is contributed by Code_Mech
```

## C

```
// C program for Pascal’s Triangle
// A O(n^2) time and O(1) extra space
// function for Pascal's Triangle
void printPascal(int n)
{
for (int line = 1; line <= n; line++)
{
    int C = 1; // used to represent C(line, i)
    for (int i = 1; i <= line; i++)
    {
    printf("%d ", C); // The first value in a line is always 1
    C = C * (line - i) / i;
    }
    printf("\n");
}
}
// Driver code
int main()
{
int n = 5;
    printPascal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Pascal's Triangle
// A O(n^2) time and O(1) extra
// space method for Pascal's Triangle
import java.io.*;
class GFG {

//Pascal function
public static void printPascal(int n)
{
    for(int line = 1; line <= n; line++)
    {

    int C=1;// used to represent C(line, i)
    for(int i = 1; i <= line; i++)
    {
        // The first value in a line is always 1
        System.out.print(C+" ");
        C = C * (line - i) / i;
    }
    System.out.println();
    }
}

// Driver code
public static void main (String[] args) {
    int n = 5;
    printPascal(n);
}
}
// This code is contributed
// by Archit Puri
```

## 蟒蛇 3

```
# Python3 program for Pascal's Triangle
# A O(n^2) time and O(1) extra
# space method for Pascal's Triangle

# Pascal function
def printPascal(n):

    for line in range(1, n + 1):
        C = 1; # used to represent C(line, i)
        for i in range(1, line + 1):

            # The first value in a
            # line is always 1
            print(C, end = " ");
            C = int(C * (line - i) / i);
        print("");

# Driver code
n = 5;
printPascal(n);

# This code is contributed by mits
```

## C#

```
// C# program for Pascal's Triangle
// A O(n^2) time and O(1) extra
// space method for Pascal's Triangle
using System;
class GFG
{

// Pascal function
public static void printPascal(int n)
{
    for(int line = 1;
            line <= n; line++)
    {

    int C = 1;// used to represent C(line, i)
    for(int i = 1; i <= line; i++)
    {
        // The first value in a
        // line is always 1
        Console.Write(C + " ");
        C = C * (line - i) / i;
    }
    Console.Write("\n") ;
    }
}

// Driver code
public static void Main ()
{
    int n = 5;
    printPascal(n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Pascal's Triangle
// A O(n^2) time and O(1) extra
// space method for Pascal's Triangle

// Pascal function
function printPascal($n)
{
    for($line = 1; $line <= $n; $line++)
    {
        $C = 1;// used to represent C(line, i)
        for($i = 1; $i <= $line; $i++)
        {
            // The first value in a
            // line is always 1
            print($C . " ");
            $C = $C * ($line - $i) / $i;
        }
        print("\n");
    }
}

// Driver code
$n = 5;
printPascal($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program for Pascal's Triangle
// A O(n^2) time and O(1) extra
// space method for Pascal's Triangle

//Pascal function
function printPascal(n)
{
    for(line = 1; line <= n; line++)
    {

    var C=1;// used to represent C(line, i)
    for(i = 1; i <= line; i++)
    {
        // The first value in a line is always 1
        document.write(C+" ");
        C = C * (line - i) / i;
    }
    document.write("<br>");
    }
}

// Driver code
var n = 5;
printPascal(n);

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
1 
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1 
```

所以方法 3 是所有方法中最好的方法，但是它可能会导致大 n 值的整数溢出，因为它将两个整数相乘以获得值。

本文由**拉胡尔**编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。