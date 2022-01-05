# 山地序列模式

> 原文:[https://www.geeksforgeeks.org/mountain-sequence-pattern/](https://www.geeksforgeeks.org/mountain-sequence-pattern/)

给定一个数字 **N** ，任务是生成一个接一个包含 **N** 金字塔的金字塔序列模式，如下例所示。
**例:**

```
Input: N = 3
Output:
  *    *    *
 ***  ***  ***
***************

Input: N = 4
Output: 
  *    *    *    *
 ***  ***  ***  ***
********************
```

**迭代方法:**为给定编号 **N** 打印**山脉序列模式**的迭代方法步骤:

1.  运行两个**嵌套**循环。
2.  **外部**循环将关注图案的**行**。
3.  **内部**循环将会关心**列**的模式。
4.  取三个变量 **k1、k2** 和**间隙**，这有助于生成模式。
5.  打印完图案行后，将 **k1** 和 **k2** 的值更新为:
    *   **k1 = k1 +间隙**
    *   **k2 = k2 +间隙**

下面是迭代方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to create the mountain
// sequence pattern
void printPatt(int n)
{
    int k1 = 3;
    int k2 = 3;
    int gap = 5;

    // Outer loop to handle the row
    for (int i = 1; i <= 3; i++) {

        // Inner loop to handle the
        // Column
        for (int j = 1;
             j <= (5 * n); j++) {

            if (j > k2 && i < 3) {
                k2 += gap;
                k1 += gap;
            }

            // Condition to print the
            // star in mountain pattern
            if (j >= k1 && j <= k2) {
                cout << "*";
            }
            else {
                cout << " ";
            }
        }

        // Condition to adjust the value of
        // K1 and K2 for printing desire
        // Pattern
        if (i + 1 == 3) {
            k1 = 1;
            k2 = (5 * n);
        }
        else {
            k1 = 3;
            k2 = 3;
            k1--;
            k2++;
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given Number N
    int N = 5;

    // Function call
    printPatt(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to create the mountain
// sequence pattern
static void printPatt(int n)
{
    int k1 = 3;
    int k2 = 3;
    int gap = 5;

    // Outer loop to handle the row
    for(int i = 1; i <= 3; i++)
    {

       // Inner loop to handle the
       // Column
       for(int j = 1; j <= (5 * n); j++)
       {
          if (j > k2 && i < 3)
          {
              k2 += gap;
              k1 += gap;
          }

          // Condition to print the
          // star in mountain pattern
          if (j >= k1 && j <= k2)
          {
              System.out.print("*");
          }
          else
          {
              System.out.print(" ");
          }
       }

       // Condition to adjust the value of
       // K1 and K2 for printing desire
       // Pattern
       if (i + 1 == 3)
       {
           k1 = 1;
           k2 = (5 * n);
       }
       else
       {
           k1 = 3;
           k2 = 3;
           k1--;
           k2++;
       }
       System.out.println();
    }
}

// Driver code
public static void main (String[] args)
{

    // Given Number N
    int N = 5;

    // Function call
    printPatt(N);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to create the mountain
# sequence pattern
def printPatt(n):

    k1 = 3; k2 = 3; gap = 5;

    # Outer loop to handle the row
    for i in range(1, 4):

        # Inner loop to handle the
        # Column
        for j in range(1, (5 * n) + 1):

            if (j > k2 and i < 3):
                k2 += gap;
                k1 += gap;

            # Condition to print the
            # star in mountain pattern
            if (j >= k1 and j <= k2):
                print("*", end = "");
            else:
                print(" ", end = "");
        print("\n", end = "");

        # Condition to adjust the value of
        # K1 and K2 for printing desire
        # Pattern
        if (i + 1 == 3):
            k1 = 1;
            k2 = (5 * n);

        else:
            k1 = 3;
            k2 = 3;
            k1 -= 1;
            k2 += 1;
    print(end = "");

# Driver Code

# Given Number N
N = 5;

# Function call
printPatt(N);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Function to create the mountain
// sequence pattern
static void printPatt(int n)
{
    int k1 = 3;
    int k2 = 3;
    int gap = 5;

    // Outer loop to handle the row
    for(int i = 1; i <= 3; i++)
    {

        // Inner loop to handle the
        // Column
        for(int j = 1; j <= (5 * n); j++)
        {
            if (j > k2 && i < 3)
            {
                k2 += gap;
                k1 += gap;
            }

            // Condition to print the
            // star in mountain pattern
            if (j >= k1 && j <= k2)
            {
                Console.Write("*");
            }
            else
            {
                Console.Write(" ");
            }
        }

        // Condition to adjust the value of
        // K1 and K2 for printing desire
        // Pattern
        if (i + 1 == 3)
        {
            k1 = 1;
            k2 = (5 * n);
        }
        else
        {
            k1 = 3;
            k2 = 3;
            k1--;
            k2++;
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main (String[] args)
{

    // Given Number N
    int N = 5;

    // Function call
    printPatt(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<!--  Javascript program for the above approach. -->

<script>

// Function to create the mountain
// sequence pattern
function printPatt( n)
{
    var k1 = 3;
    var k2 = 3;
    var gap = 5;

    // Outer loop to handle the row
    for(let i = 1; i <= 3; i++)
    {

        // Inner loop to handle the
        // Column
        for(let j = 1; j <= (5 * n); j++)
        {
            if (j > k2 && i < 3)
            {
                k2 += gap;
                k1 += gap;
            }

            // Condition to print the
            // star in mountain pattern
            if (j >= k1 && j <= k2)
            {   document.write("*");
            }
            else
            {
                document.write("  ");
            }
        }

        // Condition to adjust the value of
        // K1 and K2 for printing desire
        // Pattern
        if (i + 1 == 3)
        {
            k1 = 1;
            k2 = (5 * n);
        }
        else
        {
            k1 = 3;
            k2 = 3;
            k1--;
            k2++;
        }
        document.write("<br>");
    }
}

//Driver Code
var N=3;
printPatt(N);

</script>

<!--  This code in contributed by nirajgusain5 -->
```

**Output:** 

```
  *    *    *    *    *  
 ***  ***  ***  ***  *** 
*************************
```