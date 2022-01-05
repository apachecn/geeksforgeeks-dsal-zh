# 使用从 1 到 N 的数字模式打印“N”字母的程序

> 原文:[https://www . geesforgeks . org/program-to-print-n-alphabet-使用从 1 到 n 的数字模式/](https://www.geeksforgeeks.org/program-to-print-n-alphabet-using-the-number-pattern-from-1-to-n/)

给定一个整数 **N** ，任务是打印字母 N 图案，如下所示:

```
1           1
2 2         2
3   3       3
*    *      *
*      *    *
*        *  *
N           N
```

**例:**

```
Input: N = 6
Output:
1           1
2  2        2
3    3      3
4      4    4
5        5  5
6           6

Input: N = 5
Output:
1         1
2  2      2
3    3    3
4      4  4
5         5
```

**进场:**除第一排和最后一排外，每隔一排跟随如下:

*   将第一个值打印为**索引+ 1** ，其中**索引**是该行的索引。
*   然后打印空格 **2 *索引**次。
*   再次打印数值**索引+ 1** 作为当前行的对角线元素。
*   然后打印剩余的**2 *(N–index–1)**空格，后面跟着结束元素，也是 **index + 1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to print the desired Alphabet N Pattern
void Alphabet_N_Pattern(int N)
{

    int index, side_index, size;

    // Declaring the values of Right, Left and Diagonal values
    int Right = 1, Left = 1, Diagonal = 2;

    // Main Loop for the rows
    for (index = 0; index < N; index++) {

        // For the left Values
        cout << Left++;

        // Spaces for the diagonals
        for (side_index = 0; side_index < 2 * (index); side_index++)
            cout << " ";

        // Condition for the diagonals
        if (index != 0 && index != N - 1)
            cout << Diagonal++;
        else
            cout << " ";

        // Spaces for the Right Values
        for (side_index = 0; side_index < 2 * (N - index - 1); side_index++)
            cout << " ";

        // For the right values
        cout << Right++;

        cout << endl;
    }
}

// Driver Code
int main(int argc, char** argv)
{
    // Size of the Pattern
    int Size = 6;

    // Calling the function to print the desired Pattern
    Alphabet_N_Pattern(Size);
}
```

## C

```
// C implementation of the approach
#include <stdio.h>

// Function to print the desired Alphabet N Pattern
void Alphabet_N_Pattern(int N)
{

    int index, side_index, size;

    // Declaring the values of Right, Left and Diagonal values
    int Right = 1, Left = 1, Diagonal = 2;

    // Main Loop for the rows
    for (index = 0; index < N; index++) {

        // For the left Values
        printf("%d", Left++);

        // Spaces for the diagonals
        for (side_index = 0; side_index < 2 * (index); side_index++)
            printf(" ");

        // Condition for the diagonals
        if (index != 0 && index != N - 1)
            printf("%d", Diagonal++);
        else
            printf(" ");

        // Spaces for the Right Values
        for (side_index = 0; side_index < 2 * (N - index - 1); side_index++)
            printf(" ");

        // For the right values
        printf("%d", Right++);

        printf("\n");
    }
}

// Driver Code
int main(int argc, char** argv)
{
    // Size of the Pattern
    int Size = 6;

    // Calling the function to print the desired Pattern
    Alphabet_N_Pattern(Size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// Function to print the desired Alphabet N Pattern
static void Alphabet_N_Pattern(int N)
{

    int index, side_index, size;

    // Declaring the values of Right, Left and Diagonal values
    int Right = 1, Left = 1, Diagonal = 2;

    // Main Loop for the rows
    for (index = 0; index < N; index++) {

        // For the left Values
        System.out.print(Left++);

        // Spaces for the diagonals
        for (side_index = 0; side_index < 2 * (index); side_index++)
            System.out.print(" ");

        // Condition for the diagonals
        if (index != 0 && index != N - 1)
            System.out.print(Diagonal++);
        else
            System.out.print(" ");

        // Spaces for the Right Values
        for (side_index = 0; side_index < 2 * (N - index - 1); side_index++)
            System.out.print(" ");

        // For the right values
        System.out.print(Right++);

        System.out.println();
    }
}

// Driver Code
public static void main(String args[])
{
    // Size of the Pattern
    int Size = 6;

    // Calling the function to print the desired Pattern
    Alphabet_N_Pattern(Size);
}

}

// This code is contributed by
// Surendra_Gagwar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print the desired
# Alphabet N Pattern
def Alphabet_N_Pattern(N):

    # Declaring the values of Right, Left
    # and Diagonal values
    Right = 1
    Left = 1
    Diagonal = 2

    # Main Loop for the rows
    for index in range(N):

        # For the left Values
        print(Left, end = "")
        Left += 1

        # Spaces for the diagonals
        for side_index in range(0, 2 * (index), 1):
            print(" ", end = "")

        # Condition for the diagonals
        if (index != 0 and index != N - 1):
            print(Diagonal, end = "")
            Diagonal += 1
        else:
            print(" ", end = "")

        # Spaces for the Right Values
        for side_index in range(0, 2 * (N - index - 1), 1):
            print(" ", end = "")

        # For the right values
        print(Right, end = "")
        Right += 1

        print("\n", end = "")

# Driver Code
if __name__ == '__main__':

    # Size of the Pattern
    Size = 6

    # Calling the function to print
    # the desired Pattern
    Alphabet_N_Pattern(Size)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the desired Alphabet N Pattern
public static void Alphabet_N_Pattern(int N)
{

    int index, side_index;

    // Declaring the values of Right,
    // Left and Diagonal values
    int Right = 1, Left = 1, Diagonal = 2;

    // Main Loop for the rows
    for (index = 0; index < N; index++)
    {

        // For the left Values
        Console.Write(Left++);

        // Spaces for the diagonals
        for (side_index = 0;
             side_index < 2 * (index); side_index++)
            Console.Write(" ");

        // Condition for the diagonals
        if (index != 0 && index != N - 1)
            Console.Write(Diagonal++);
        else
            Console.Write(" ");

        // Spaces for the Right Values
        for (side_index = 0;
             side_index < 2 * (N - index - 1);
             side_index++)
            Console.Write(" ");

        // For the right values
        Console.Write(Right++);

        Console.Write("\n");
    }
}

// Driver Code
static void Main()
{
    // Size of the Pattern
    int Size = 6;

    // Calling the function to print
    // the desired Pattern
    Alphabet_N_Pattern(Size);
}
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the desired
// Alphabet N Pattern
function Alphabet_N_Pattern($N)
{
    $index;
    $side_index;
    $size;

    // Declaring the values of Right,
    // Left and Diagonal values
    $Right = 1;
    $Left = 1;
    $Diagonal = 2;

    // Main Loop for the rows
    for ($index = 0; $index < $N; $index++)
    {

        // For the left Values
        echo $Left++;

        // Spaces for the diagonals
        for ($side_index = 0;
             $side_index < 2 * ($index);
             $side_index++)
            echo " ";

        // Condition for the diagonals
        if ($index != 0 && $index != $N - 1)
            echo $Diagonal++;
        else
            echo " ";

        // Spaces for the Right Values
        for ($side_index = 0;
             $side_index < 2 * ($N - $index - 1);
             $side_index++)
            echo " ";

        // For the right values
        echo $Right++;

        echo "\n";
    }
}

// Driver Code

// Size of the Pattern
$Size = 6;

// Calling the function to
// print the desired Pattern
Alphabet_N_Pattern($Size);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach

      // Function to print the desired
      // Alphabet N Pattern
      function Alphabet_N_Pattern(N) {
        var index, side_index, size;

        // Declaring the values of Right,
        // Left and Diagonal values
        var Right = 1,
          Left = 1,
          Diagonal = 2;

        // Main Loop for the rows
        for (index = 0; index < N; index++) {
          // For the left Values
          document.write(Left++);

          // Spaces for the diagonals
          for (side_index = 0;
          side_index < 2 * index; side_index++)
            document.write("  ");

          // Condition for the diagonals
          if (index != 0 && index != N - 1)
          document.write(Diagonal++);
          else
          document.write("  ");

          // Spaces for the Right Values
          for (side_index = 0;
          side_index < 2 * (N - index - 1); side_index++)
            document.write("  ");

          // For the right values
          document.write(Right++);
          document.write("<br>");
        }
      }

      // Driver Code
      // Size of the Pattern
      var Size = 6;
      // Calling the function to print
      // the desired Pattern
      Alphabet_N_Pattern(Size);

</script>
```

**Output:** 

```
1           1
2  2        2
3    3      3
4      4    4
5        5  5
6           6
```