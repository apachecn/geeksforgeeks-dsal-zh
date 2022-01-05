# 程序查找所有类型的矩阵

> 原文:[https://www . geesforgeks . org/program-to-find-all-type-matrix/](https://www.geeksforgeeks.org/program-to-find-all-types-of-matrix/)

给定矩阵 R(行)* C(列)的维数，任务是找出给定维数代表哪种类型的矩阵。
示例:

```
Input : R = 1 C = 0
Output : Row Matrix 

Input : R = 4 C = 5
Output : Horizontal Matrix 
```

> *   **Row matrix:** When R = 1 and C = 0, this matrix represents the row matrix.
> *   **Column matrix:** When C = 1 and R = 0, this matrix represents the column matrix.
> *   **Horizontal matrix:** A matrix with fewer rows than columns is called horizontal matrix (r < c).
> *   **Vertical matrix:** A matrix with more rows than columns is called a horizontal matrix (r > c).
> *   **Square matrix:** A matrix with the number of rows equal to the number of columns is called a square matrix (R = C).

## C++

```
// C++ program to check
// types of Matrix
#include <bits/stdc++.h>
using namespace std;

// Function to display which
// type of matrix
void check(int r, int c)
{
    if (r == 0 && c == 1)
        cout << "Column Matrix " << endl;
    else if (r == 1 && c == 0)
        cout << "Row Matrix " << endl;
    else if (r < c)
        cout << "Horizontal Matrix " << endl;
    else if (r > c)
        cout << "Vertical Matrix " << endl;
    else if (r == c)
        cout << "Square Matrix " << endl;
}

// Driver code
int main()
{
    // input for r and c
    // function calling
    check(1, 0);
    check(0, 1);
    check(4, 5);
    check(5, 4);
    check(3, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// types of Matrix
import java.io.*;
import java.util.*;
import java.math.*;
import java.util.regex.*;

public class GFG {

    // Function to display which type of matrix
    static void check(int r, int c)
    {
        if (r == 0 && c == 1)
            System.out.println("Column Matrix ");
        else if (r == 1 && c == 0)
            System.out.println("Row Matrix ");
        else if (r < c)
            System.out.println("Horizontal Matrix ");
        else if (r > c)
            System.out.println("Vertical Matrix ");
        else if (r == c)
            System.out.println("Square Matrix ");
    }

    // Driver code
    public static void main(String[] args)
    {

        // static input for r and c
        // function calling
        check(1, 0);
        check(0, 1);
        check(4, 5);
        check(5, 4);
        check(3, 3);
    }
}
```

## 蟒蛇 3

```
# Python3 program to check
# types of Matrix

# Function to display which
# type of matrix
def check(r, c) :

    if r == 0 and c == 1:
        print ("Column Matrix ")

    elif r == 1 and c == 0:
        print ("Row Matrix ")

    elif r < c:
        print ("Horizontal Matrix ")

    elif r > c:
        print ("Vertical Matrix ")

    elif r == c:
        print ("Square Matrix ")

# Driver code
check(1, 0)
check(0, 1)
check(4, 5)
check(5, 4)
check(3, 3)

# This code is contributed by Sam007.

```

## C#

```
// C# program to check types of Matrix
using System;

class GFG
{
    // Function to display which type of matrix
    static void check(int r, int c)
    {
        if (r == 0 && c == 1)
            Console.WriteLine("Column Matrix ");
        else if (r == 1 && c == 0)
            Console.WriteLine("Row Matrix ");
        else if (r < c)
            Console.WriteLine("Horizontal Matrix ");
        else if (r > c)
            Console.WriteLine("Vertical Matrix ");
        else if (r == c)
            Console.WriteLine("Square Matrix ");
    }

    // Driver code
    static void Main()
    {

        // static input for r and c
        // function calling
        check(1, 0);
        check(0, 1);
        check(4, 5);
        check(5, 4);
        check(3, 3);
    }

}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// types of Matrix

// Function to display which
// type of matrix
function check($r, $c)
{
    if ($r == 0 && $c == 1)
        echo "Column Matrix "."\n";
    else if ($r == 1 && $c == 0)
        echo "Row Matrix "."\n";
    else if ($r < $c)
        echo "Horizontal Matrix "."\n";
    else if ($r > $c)
        echo "Vertical Matrix "."\n";
    else if ($r == $c)
        echo "Square Matrix "."\n";
}

    // Driver code

    // input for r and c
    // function calling
    check(1, 0);
    check(0, 1);
    check(4, 5);
    check(5, 4);
    check(3, 3);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to check types of Matrix

    // Function to display which type of matrix
    function check(r, c)
    {
        if (r == 0 && c == 1)
            document.write("Column Matrix " + "</br>");
        else if (r == 1 && c == 0)
            document.write("Row Matrix " + "</br>");
        else if (r < c)
            document.write("Horizontal Matrix " + "</br>");
        else if (r > c)
            document.write("Vertical Matrix " + "</br>");
        else if (r == c)
            document.write("Square Matrix " + "</br>");
    }

    // static input for r and c
    // function calling
    check(1, 0);
    check(0, 1);
    check(4, 5);
    check(5, 4);
    check(3, 3);

</script>
```

输出:

```
Row Matrix 
Column Matrix 
Horizontal Matrix 
Vertical Matrix 
Square Matrix
```