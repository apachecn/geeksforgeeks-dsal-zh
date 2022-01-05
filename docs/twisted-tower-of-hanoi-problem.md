# 扭曲的河内塔问题

> 原文:[https://www . geesforgeks . org/twisted-of-tower-of-Hanoi-problem/](https://www.geeksforgeeks.org/twisted-tower-of-hanoi-problem/)

河内[塔](https://www.geeksforgeeks.org/c-program-for-tower-of-hanoi/)的基本版本可以在这里找到。
这是一个扭曲的河内塔问题。其中，所有规则都是一样的，只是增加了一条规则:
**你不能直接将任何盘面从第一根杆移动到最后一根杆**，也就是说，如果你想将盘面从第一根杆移动到最后一根杆，那么你必须先将第一根杆移动到中间杆，然后再移动到最后一根杆。

**进场:**

*   **基本情况:**如果盘片数为 1，那么先移到中间棒，再移到最后棒。
*   **递归情况:**在递归情况下，以下步骤将产生最优解:(所有这些移动都遵循河内问题的扭曲塔的规则)
    1.  我们将首先把第一个 n-1 个磁盘移到最后一个棒上。
    2.  然后将最大的圆盘移到中间的杆上。
    3.  将第一个 n-1 盘从最后一个杆移动到第一个杆。
    4.  将最大的圆盘从中间杆移到最后一根杆上。
    5.  将所有 n-1 个磁盘从第一个棒移动到最后一个棒。

下面是上述方法的实现:

## C++

```
// C++ implementation
#include <iostream>
using namespace std;

// Function to print the moves
void twistedTOH(int n, char first,
                char middle, char last)
{
    // Base case
    if (n == 1) {

        cout << "Move disk " << n
             << " from rod " << first
             << " to " << middle
             << " and then to "
             << last << endl;

        return;
    }

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);

    // Move largest disk from first to middle
    cout << "Move disk " << n
         << " from rod " << first
         << " to " << middle << endl;

    // Move n-1 disks from last to first
    twistedTOH(n - 1, last, middle, first);

    // Move nth disk from middle to last
    cout << "Move disk " << n
         << " from rod " << middle
         << " to " << last << endl;

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);
}

// Driver's Code
int main()
{
    // Number of disks
    int n = 2;

    // Rods are in order
    // first(A), middle(B), last(C)
    twistedTOH(n, 'A', 'B', 'C');

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to print the moves
static void twistedTOH(int n, char first,
                char middle, char last)
{
    // Base case
    if (n == 1)
    {

        System.out.println("Move disk " + n + " from rod " +
                                   first + " to " + middle +
                                    " and then to " + last);

        return;
    }

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);

    // Move largest disk from first to middle
    System.out.println("Move disk " + n +
                       " from rod " + first +
                       " to " + middle);

    // Move n-1 disks from last to first
    twistedTOH(n - 1, last, middle, first);

    // Move nth disk from middle to last
    System.out.println("Move disk " + n +
                       " from rod " + middle +
                       " to " + last);

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);
}

// Driver Code
public static void main(String[] args)
{
    // Number of disks
    int n = 2;

    // Rods are in order
    // first(A), middle(B), last(C)
    twistedTOH(n, 'A', 'B', 'C');
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to print the moves
def twistedTOH(n, first, middle, last):

    # Base case
    if (n == 1):

        print("Move disk", n, "from rod", first,
              "to", middle, "and then to", last)

        return

    # Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last)

    # Move largest disk from first to middle
    print("Move disk", n, "from rod",
                 first, "to", middle)

    # Move n-1 disks from last to first
    twistedTOH(n - 1, last, middle, first)

    # Move nth disk from middle to last
    print("Move disk", n, "from rod",
                 middle, "to", last)

    # Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last)

# Driver Code

# Number of disks
n = 2

# Rods are in order
# first(A), middle(B), last(C)
twistedTOH(n, 'A', 'B', 'C')

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the moves
static void twistedTOH(int n, char first,
                       char middle, char last)
{
    // Base case
    if (n == 1)
    {
        Console.WriteLine("Move disk " + n + " from rod " +
                                  first + " to " + middle +
                                   " and then to " + last);

        return;
    }

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);

    // Move largest disk from first to middle
    Console.WriteLine("Move disk " + n +
                      " from rod " + first +
                      " to " + middle);

    // Move n-1 disks from last to first
    twistedTOH(n - 1, last, middle, first);

    // Move nth disk from middle to last
    Console.WriteLine("Move disk " + n +
                      " from rod " + middle +
                      " to " + last);

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);
}

// Driver Code
public static void Main(String[] args)
{
    // Number of disks
    int n = 2;

    // Rods are in order
    // first(A), middle(B), last(C)
    twistedTOH(n, 'A', 'B', 'C');
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program
// Function to print the moves
function twistedTOH(n, first, middle, last)
{
    // Base case
    if (n == 1) {

        document.write("Move disk " + n
             + " from rod " + first
             + " to " + middle
             + " and then to "
             + last + "<br>");

        return;
    }

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);

    // Move largest disk from first to middle
    document.write("Move disk " + n
         + " from rod " + first
         + " to " + middle + "<br>");

    // Move n-1 disks from last to first
    twistedTOH(n - 1, last, middle, first);

    // Move nth disk from middle to last
    document.write("Move disk " + n
         + " from rod " + middle
         + " to " + last + "<br>");

    // Move n-1 disks from first to last
    twistedTOH(n - 1, first, middle, last);
}

// driver code
// Number of disks
var n = 2;

// Rods are in order
// first(A), middle(B), last(C)
twistedTOH(n, 'A', 'B', 'C');

// This code contributed by shivani
</script>
```

**Output:** 

```
Move disk 1 from rod A to B and then to C
Move disk 2 from rod A to B
Move disk 1 from rod C to B and then to A
Move disk 2 from rod B to C
Move disk 1 from rod A to B and then to C
```

重复公式:

```
T(n) = T(n-1) + 1 + T(n-1) + 1 + T(n-1)
     = 3 * T(n-1) + 2

where n is the number of disks.
```

通过求解这个递归，**时间复杂度为 O(3 <sup>n</sup> )** 。
**辅助空间** : O(n)。