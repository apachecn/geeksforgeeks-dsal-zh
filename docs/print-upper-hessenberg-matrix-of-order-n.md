# 打印 N 阶上赫森伯格矩阵

> 原文:[https://www . geesforgeks . org/print-upper-hessenberg-matrix-of-order-n/](https://www.geeksforgeeks.org/print-upper-hessenberg-matrix-of-order-n/)

给定一个正整数 **N** ，任务是打印包含任意一个一位数随机正整数作为非零元素的高阶赫森伯格矩阵 **N** 。
[上赫森伯格矩阵](https://en.wikipedia.org/wiki/Hessenberg_matrix)是一个正方形矩阵，其中[次对角线](https://www.geeksforgeeks.org/print-all-the-sub-diagonal-elements-of-the-given-square-matrix/)以下的所有元素都为零。在数学术语**中，mat[i][j] = 0 表示所有 i > j + 1** 。
**举例:**

> **输入:** N = 3
> **输出:**
> 1 2 8
> 1 3 4
> 0 3 4
> **输入:** N = 4
> **输出:**
> 1 2 2 3
> 1 3 4 2
> 0 3 4 2
> 0 1 4

**方法:**为了打印具有一位数正元素的上部赫森伯格矩阵，在[兰德()](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)函数的帮助下，为矩阵中的所有单元打印零，其中 **i > j + 1** 和任何一位数随机数。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the Upper Hessenberg
// matrix of order n
void UpperHessenbergMatrix(int n)
{
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {

            // If element is below sub-diagonal
            // then print 0
            if (i > j + 1)
                cout << '0' << " ";

            // Print a random digit for
            // every non-zero element
            else
                cout << rand() % 10 << " ";
        }
        cout << "\n";
    }
}

// Driver code
int main()
{
    int n = 4;
    UpperHessenbergMatrix(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print the Lower Hessenberg
// matrix of order n
static void UpperHessenbergMatrix(int n)
{
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {

            // If element is above super-diagonal
            // then print 0
            if (i > j + 1)
            {
                System.out.print(0 + " ");
            }

            // Print a random digit for
            // every non-zero element
            else
            {
                System.out.print((int)(Math.random() * 10) + " ");
            }
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 4;
    UpperHessenbergMatrix(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import random

# Function to print the Upper Hessenberg
# matrix of order n
def UpperHessenbergMatrix(n):

    for i in range(1, n + 1):

        for j in range(1, n + 1):

            # If element is below sub-diagonal
            # then pr0
            if (i > j + 1):
                print('0', end = " ")

            # Pra random digit for
            # every non-zero element
            else:
                print(random.randint(1, 10),
                                 end = " ")
        print()

# Driver code
n = 4;
UpperHessenbergMatrix(n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the Lower Hessenberg
    // matrix of order n
    static void UpperHessenbergMatrix(int n)
    {
        Random rand = new Random();

        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= n; j++)
            {

                // If element is above super-diagonal
                // then print 0
                if (i > j + 1)
                    Console.Write(0 + " ");

                // Print a random digit for
                // every non-zero element
                else
                    Console.Write(rand.Next(1, 10) + " ");
            }
            Console.WriteLine();
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 4;
        UpperHessenbergMatrix(n);
    }
}   

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the Upper Hessenberg
// matrix of order n
function UpperHessenbergMatrix( n)
{
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= n; j++) {

            // If element is below sub-diagonal
            // then print 0
            if (i > j + 1)
                document.write( '0' + " ");

            // Print a random digit for
            // every non-zero element
            else
                document.write( Math.floor(Math.random() * 10) + " ");
        }
        document.write("<br>");
    }
}

// Driver code
var n = 4;
UpperHessenbergMatrix(n);

</script>
```

**Output:** 

```
3 6 7 5 
3 5 6 2 
0 9 1 2 
0 0 7 0
```