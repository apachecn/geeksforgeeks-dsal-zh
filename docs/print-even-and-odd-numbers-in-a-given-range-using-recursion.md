# 使用递归打印给定范围内的偶数和奇数

> 原文:[https://www . geeksforgeeks . org/print-给定范围内的偶数和奇数-使用递归/](https://www.geeksforgeeks.org/print-even-and-odd-numbers-in-a-given-range-using-recursion/)

给定两个整数 **L** 和 **R** ，任务是使用[递归](https://www.geeksforgeeks.org/recursion/)打印从 **L** 到 **R** 的所有偶数和奇数。

**示例:**

> **输入:** L = 1，R = 10
> **输出:**
> 偶数:2 4 6 8 10
> 奇数:1 3 5 7 9
> 
> **输入:** L = 10，R = 25
> **输出:**
> 偶数:10 12 14 16 18 20 22 24
> 奇数:11 13 15 17 19 21 23 25

**方法:**按照以下步骤使用[递归](https://www.geeksforgeeks.org/recursion/)解决问题:

*   遍历**【R，L】**范围。
*   使用以下递归关系，使用[递归](https://www.geeksforgeeks.org/recursion/)打印范围内的奇数元素:

> 奇数(L，R) = R % 2 == 1？奇数(左，右–2):奇数(左，右–1)

*   使用以下[递归关系](https://www.geeksforgeeks.org/algorithms-gq/analysis-of-algorithms-recurrences-gq/)使用递归打印范围内的偶数元素:

> 偶数(L，R) = R % 2 == 0？偶数(L，R–2):偶数(L，R–1)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the
// even numbers from L to R
void Even(int L, int R)
{

    // Base case
    if (R < L) {
        return;
    }

    // Recurrence relation
    R % 2 == 0 ? Even(L, R - 2)
               : Even(L, R - 1);

    // Check if R is even
    if (R % 2 == 0) {
        cout << R << " ";
    }
}

// Function to print all the
// odd numbers from L to R
void Odd(int L, int R)
{

    // Base case
    if (R < L) {
        return;
    }

    // Recurrence relation
    R % 2 == 1 ? Odd(L, R - 2)
               : Odd(L, R - 1);

    // Check if R is even
    if (R % 2 == 1) {
        cout << R << " ";
    }
}

// Driver Code
int main()
{
    int L = 10, R = 25;
    cout << "Even numbers:";

    // Print all the
    // even numbers
    Even(L, R);
    cout << endl;

    // Print all the
    // odd numbers
    cout << "Odd numbers:";
    Odd(L, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to print
// all the even numbers
// from L to R
static void Even(int L,
                 int R)
{
  // Base case
  if (R < L)
  {
    return;
  }

  // Recurrence relation
  if(R % 2 == 0 )
    Even(L, R - 2);
  else
    Even(L, R - 1);

  // Check if R is even
  if (R % 2 == 0)
  {
    System.out.print(R + " ");
  }
}

// Function to print
// all the odd numbers
// from L to R
static void Odd(int L,
                int R)
{
  // Base case
  if (R < L)
  {
    return;
  }

  // Recurrence relation
  if(R % 2 == 1 )
    Odd(L, R - 2);
  else
    Odd(L, R - 1);

  // Check if R is even
  if (R % 2 == 1)
  {
    System.out.print(R + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  int L = 10, R = 25;
  System.out.print("Even numbers:");

  // Print all the
  // even numbers
  Even(L, R);
  System.out.println();

  // Print all the
  // odd numbers
  System.out.print("Odd numbers:");
  Odd(L, R);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print all the
# even numbers from L to R
def Even(L, R):

    # Base case
    if (R < L):
        return

    # Recurrence relation
    if (R % 2 == 0):
        Even(L, R - 2)
    else:
        Even(L, R - 1)

    # Check if R is even
    if (R % 2 == 0):
        print(R, end = " ")

# Function to print all the
# odd numbers from L to R
def Odd(L, R):

    # Base case
    if (R < L):
        return

    # Recurrence relation
    if (R % 2 == 1):
        Odd(L, R - 2)
    else:
        Odd(L, R - 1)

    # Check if R is even
    if (R % 2 == 1):
        print(R, end = " ")

# Driver Code
if __name__ == '__main__':

    L = 10
    R = 25

    print("Even numbers:")

    # Print all the
    # even numbers
    Even(L, R)
    print()

    # Print all the
    # odd numbers
    print("Odd numbers:")
    Odd(L, R)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to print
// all the even numbers
// from L to R
static void Even(int L,
                 int R)
{
  // Base case
  if (R < L)
  {
    return;
  }

  // Recurrence relation
  if(R % 2 == 0 )
    Even(L, R - 2);
  else
    Even(L, R - 1);

  // Check if R is even
  if (R % 2 == 0)
  {
    Console.Write(R + " ");
  }
}

// Function to print
// all the odd numbers
// from L to R
static void Odd(int L,
                int R)
{
  // Base case
  if (R < L)
  {
    return;
  }

  // Recurrence relation
  if(R % 2 == 1 )
    Odd(L, R - 2);
  else
    Odd(L, R - 1);

  // Check if R is even
  if (R % 2 == 1)
  {
    Console.Write(R + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  int L = 10, R = 25;
  Console.Write("Even numbers:");

  // Print all the
  // even numbers
  Even(L, R);
  Console.WriteLine();

  // Print all the
  // odd numbers
  Console.Write("Odd numbers:");
  Odd(L, R);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Java script program to implement
// the above approach

// Function to print
// all the even numbers
// from L to R
function Even(L, R)
{

    // Base case
    if (R < L)
    {
        return;
    }

    // Recurrence relation
    if (R % 2 == 0 )
    {
        Even(L, R - 2);
    }
    else
    {
        Even(L, R - 1);
    }

    // Check if R is even
    if (R % 2 == 0)
    {
        document.write(R + " ");
    }
}

// Function to print
// all the odd numbers
// from L to R
function Odd(L, R)
{

    // Base case
    if (R < L)
    {
        return;
    }

    // Recurrence relation
    if (R % 2 == 1 )
    {
        Odd(L, R - 2);
    }
    else
    {
        Odd(L, R - 1);
    }

    // Check if R is even
    if (R % 2 == 1)
    {
        document.write(R + " ");
    }
}

// Driver Code
let L = 10;
let R = 25;
document.write("Even numbers:");

// Print all the
// even numbers
Even(L, R);
document.write("<br>");

// Print all the
// odd numbers
document.write("Odd numbers:");
Odd(L, R);

// This code is contributed by sravan kumar G

</script>
```

**Output:** 

```
Even numbers:10 12 14 16 18 20 22 24 
Odd numbers:11 13 15 17 19 21 23 25
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)