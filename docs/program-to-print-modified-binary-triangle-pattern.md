# 打印修改后的二进制三角形图案的程序

> 原文:[https://www . geesforgeks . org/program-to-print-modified-binary-triangle-pattern/](https://www.geeksforgeeks.org/program-to-print-modified-binary-triangle-pattern/)

给定一个整数 **N** ，任务是打印修改后的二叉树模式。

> 在**修改的二元三角形模式**中，第 N 行的第一个和最后一个元素是 1，中间(N–2)个元素是 0。

**例:**

> **输入:** N = 6
> **输出:**
> 1
> 11
> 101
> 1001
> 10001
> 100001
> **输入:** N = 3
> **输出:**
> 1
> 11
> 101

**方法:**从上面的例子可以观察到，对于每一行 N:

*   第一个和第 n 个元素是 1
*   元素 2 到(N-1)是 0

因此，可以开发一种算法来打印如下图案:

*   使用循环变量 I 运行从 1 到 N 的[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，I 表示三角形模式的行号。
*   对于每一行 I，运行一个从 1 到 I 的循环，使用循环变量 j，表示每行中的数字。
*   在 j 的每次迭代中，检查 j 是 1 还是 I。如果两者都为真，则打印 1。
*   如果 j 的情况都不成立，则打印 0
*   [每次](https://www.geeksforgeeks.org/difference-between-increment-and-decrement-operators/)[迭代](https://www.geeksforgeeks.org/difference-between-recursion-and-iteration/)后，将 j 的值增加 1
*   当 j 循环成功完成时，我们已经打印了一行图案。因此，通过打印下一行来将输出更改为下一行。
*   增加 I 的值，重复整个过程，直到成功打印出 N 行。

以下是上述方法的实现:

## C++

```
// C++ implementation to print the
// modified binary triangle pattern

#include <bits/stdc++.h>
using namespace std;

// Function to print the modified
// binary pattern
void modifiedBinaryPattern(int n)
{

    // Loop to traverse the rows
    for (int i = 1; i <= n; i++) {

        // Loop to traverse the
        // numbers in each row
        for (int j = 1; j <= i; j++) {

            // Check if j is 1 or i
            // In either case print 1
            if (j == 1 || j == i)
                cout << 1;

            // Else print 0
            else
                cout << 0;
        }

        // Change the cursor to next
        // line after each row
        cout << endl;
    }
}

// Driver Code
int main()
{
    int n = 7;

    // Function Call
    modifiedBinaryPattern(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the
// modified binary triangle pattern
import java.io.*;

class GFG{

// Function to print the modified
// binary pattern
static void modifiedBinaryPattern(int n)
{

    // Loop to traverse the rows
    for(int i = 1; i <= n; i++)
    {

       // Loop to traverse the
       // numbers in each row
       for(int j = 1; j <= i; j++)
       {

           // Check if j is 1 or i
           // In either case print 1
           if (j == 1 || j == i)
               System.out.print(1);

           // Else print 0
           else
               System.out.print(0);
        }

        // Change the cursor to next
        // line after each row
        System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{
    int n = 7;

    // Function call
    modifiedBinaryPattern(n);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# python3 implementation to print the
# modified binary triangle pattern

# Function to print the modified
# binary pattern
def modifiedBinaryPattern(n):

    # Loop to traverse the rows
    for i in range(1, n + 1, 1):

        # Loop to traverse the
        # numbers in each row
        for j in range(1, i + 1, 1):

            # Check if j is 1 or i
            # In either case print 1
            if (j == 1 or j == i):
                print(1, end = "")

            # Else print 0
            else:
                print(0, end = "")

        # Change the cursor to next
        # line after each row
        print('\n', end = "")

# Driver Code
if __name__ == '__main__':

    n = 7

    # Function Call
    modifiedBinaryPattern(n)

# This code is contributed by Samarth
```

## C#

```
// C# implementation to print the
// modified binary triangle pattern
using System;
class GFG{

// Function to print the modified
// binary pattern
static void modifiedBinaryPattern(int n)
{

    // Loop to traverse the rows
    for(int i = 1; i <= n; i++)
    {

        // Loop to traverse the
        // numbers in each row
        for(int j = 1; j <= i; j++)
        {

            // Check if j is 1 or i
            // In either case print 1
            if (j == 1 || j == i)
                Console.Write(1);

            // Else print 0
            else
                Console.Write(0);
        }

        // Change the cursor to next
        // line after each row
        Console.WriteLine();
    }
}

// Driver Code
public static void Main()
{
    int n = 7;

    // Function call
    modifiedBinaryPattern(n);
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// Javascript implementation to print the
// modified binary triangle pattern

// Function to print the modified
// binary pattern
function modifiedBinaryPattern(n)
{

    // Loop to traverse the rows
    for(let i = 1; i <= n; i++)
    {

       // Loop to traverse the
       // numbers in each row
       for(let j = 1; j <= i; j++)
       {

           // Check if j is 1 or i
           // In either case print 1
           if (j == 1 || j == i)
               document.write(1);

           // Else print 0
           else
               document.write(0);
        }

        // Change the cursor to next
        // line after each row
        document.write("<br/>");
    }
}

// Driver code
    let n = 7;

    // Function call
    modifiedBinaryPattern(n);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1
11
101
1001
10001
100001
1000001
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:0(1)