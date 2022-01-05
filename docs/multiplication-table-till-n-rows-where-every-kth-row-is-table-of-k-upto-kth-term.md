# 乘法表直到 N 行，其中每第 K 行是 K 到第 K 项的表

> 原文:[https://www . geeksforgeeks . org/乘法表-直到-n-row-其中-每-kth-row-是-k-up-kth-term/](https://www.geeksforgeeks.org/multiplication-table-till-n-rows-where-every-kth-row-is-table-of-k-upto-kth-term/)

给定一个数字 **N** ，任务是打印 **N** 行，其中每一个 **K <sup>第</sup>T7】行由 **K** 到 **K <sup>第</sup>T13】项的乘法表组成。
**举例:****** 

> **输入:** N = 3
> **输出:**
> 1
> 2 4
> 3 6 9
> **说明:**
> 在上述系列中，每 K 个<sup>第</sup>行，打印 K 个最多 K 个术语的乘法表。
> **输入:** N = 5
> **输出:**
> 1
> 2 4
> 3 6 9
> 4 8 12 16
> 5 10 15 20 25

**方法:**思路是用两个[作循环](https://www.geeksforgeeks.org/loops-in-java/)打印[乘法表](https://www.geeksforgeeks.org/program-to-print-multiplication-table-of-a-number/)。“I”中的外循环用作“K”的值，“j”中的内循环用作每个“I”的乘法表的项。“I”表中的每一项都可以用公式“i * j”得到。
以下是上述方法的实现:

## C++

```
// C++ program to print multiplication table
// till N rows where every Kth row
// is the table of K up to Kth term
#include <iostream>
using namespace std;

// Function to print the multiplication table
// upto K-th term
void printMultiples(int N)
{
    // For loop to iterate from 1 to N
    // where i serves as the value of K
    for (int i = 1; i <= N; i++)
    {

        // Inner loop which at every
        // iteration goes till i
        for (int j = 1; j <= i; j++)
        {

            // Printing the table value for i
            cout << (i * j) << " ";
        }

        // New line after every row
        cout << endl;
    }
}

// Driver code
int main()
{
    int N = 5;

    printMultiples(N);

    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print multiplication table
// till N rows where every Kth row
// is the table of K up to Kth term

class GFG {

    // Function to print the multiplication table
    // upto K-th term
    public static void printMultiples(int N)
    {
        // For loop to iterate from 1 to N
        // where i serves as the value of K
        for (int i = 1; i <= N; i++) {

            // Inner loop which at every
            // iteration goes till i
            for (int j = 1; j <= i; j++) {

                // Printing the table value for i
                System.out.print((i * j) + " ");
            }

            // New line after every row
            System.out.println();
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 5;

        printMultiples(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to pr multiplication table
# till N rows where every Kth row
# is the table of K up to Kth term

# Function to pr the multiplication table
# upto K-th term
def prMultiples(N):

    # For loop to iterate from 1 to N
    # where i serves as the value of K
    for i in range(1, N + 1):

        # Inner loop which at every
        # iteration goes till i
        for j in range(1, i + 1):

            # Printing the table value for i
            print((i * j), end = " ")

        # New line after every row
        print()

# Driver code
if __name__ == '__main__':
    N = 5

    prMultiples(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print multiplication table
// till N rows where every Kth row
// is the table of K up to Kth term
using System;

class GFG
{

    // Function to print the multiplication table
    // upto K-th term
    public static void printMultiples(int N)
    {
        // For loop to iterate from 1 to N
        // where i serves as the value of K
        for (int i = 1; i <= N; i++) {

            // Inner loop which at every
            // iteration goes till i
            for (int j = 1; j <= i; j++) {

                // Printing the table value for i
                Console.Write((i * j) + " ");
            }

            // New line after every row
            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        int N = 5;

        printMultiples(N);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// javascript program to print multiplication table
// till N rows where every Kth row
// is the table of K up to Kth term

// Function to print the multiplication table
// upto K-th term
function printMultiples( N)
{
    // For loop to iterate from 1 to N
    // where i serves as the value of K
    for (let i = 1; i <= N; i++)
    {

        // Inner loop which at every
        // iteration goes till i
        for (let j = 1; j <= i; j++)
        {

            // Printing the table value for i
           document.write((i * j) + " ");
        }

        // New line after every row
       document.write("<br/>");
    }
}

// Driver code

    let N = 5;

    printMultiples(N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
1 
2 4 
3 6 9 
4 8 12 16 
5 10 15 20 25
```