# 打印给定中心的矩形图案

> 原文:[https://www . geesforgeks . org/print-矩形-带给定中心的图案/](https://www.geeksforgeeks.org/print-rectangular-pattern-with-given-center/)

给定 **3** 正整数 **c1，c2** 和 **n，**其中 **n** 是[二维正方形矩阵的大小。](https://www.geeksforgeeks.org/how-to-access-elements-of-a-square-matrix/)任务是打印填充有矩形图案的矩阵，该矩形图案具有中心坐标 **c1、c2** ，使得 **0 < = c1、c2 < n.**

**示例:**

> **输入** : c1 = 2，c2 = 2，n = 5
> **输出**:
> 2 2 2 2 2 2 2
> 2 1 1 2
> 2 1 0 1 2
> 2 1 1 2
> 2 2 2 2 2 2 2 2 2
> 
> **输入:** c1 = 3，c2 = 4，n = 7
> T3】输出:T5】4 3 3 3 3 3 3 3 3
> 4 3 2 2 2 2
> 4 3 2 1 1 1 2
> 4 3 2 1 0 1 2
> 4 3 2 1 1 2
> 4 3 2 2 2 2 2 2
> 4 3 3 3 3 3 3 3 3 3

**方法:**这个问题可以通过使用两个嵌套循环来解决。按照以下步骤解决此问题:

*   使用变量 I 在[0，N-1]范围内迭代，并执行以下步骤:
    *   使用变量 j 在[0，N-1]范围内迭代，并执行以下步骤:
        *   打印 ABS(C1–I)和 ABS(C2–j)的最大值。
    *   打印新行。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to print the matrix filled
// with rectangle pattern having center
// coordinates are c1, c2

void printRectPattern(int c1, int c2, int n)
{

    // Iterate in the range[0, n-1]
    for (int i = 0; i < n; i++) {
        // Iterate in the range[0, n-1]
        for (int j = 0; j < n; j++) {
            cout << (max(abs(c1 - i), abs(c2 - j))) << " ";
        }
        cout << endl;
    }
}
// Driver Code

int main()
{

    // Given Input
    int c1 = 2;
    int c2 = 2;
    int n = 5;

    // Function Call
    printRectPattern(c1, c2, n);
    // This code is contributed by Potta Lokesh
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to print the matrix filled
// with rectangle pattern having center
// coordinates are c1, c2
static void printRectPattern(int c1, int c2, int n)
{

    // Iterate in the range[0, n-1]
    for(int i = 0; i < n; i++)
    {

        // Iterate in the range[0, n-1]
        for(int j = 0; j < n; j++)
        {
            System.out.print((Math.max(Math.abs(c1 - i),
                              Math.abs(c2 - j))) + " ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int c1 = 2;
    int c2 = 2;
    int n = 5;

    // Function Call
    printRectPattern(c1, c2, n);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the matrix filled
# with rectangle pattern having center
# coordinates are c1, c2

def printRectPattern(c1, c2, n):

    # Iterate in the range[0, n-1]
    for i in range(n):
        # Iterate in the range[0, n-1]
        for j in range(n):
            print(max(abs(c1 - i), abs(c2 - j)), end = " ")
        print("")

# Driver Code

# Given Input
c1 = 2
c2 = 2
n = 5

# Function Call
printRectPattern(c1, c2, n)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print the matrix filled
// with rectangle pattern having center
// coordinates are c1, c2
static void printRectPattern(int c1, int c2, int n)
{

    // Iterate in the range[0, n-1]
    for(int i = 0; i < n; i++)
    {

        // Iterate in the range[0, n-1]
        for(int j = 0; j < n; j++)
        {
            Console.Write((Math.Max(Math.Abs(c1 - i),
                           Math.Abs(c2 - j))) + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int c1 = 2;
    int c2 = 2;
    int n = 5;

    // Function Call
    printRectPattern(c1, c2, n);
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the matrix filled
// with rectangle pattern having center
// coordinates are c1, c2
function printRectPattern(c1, c2, n) {

    // Iterate in the range[0, n-1]
    for (let i = 0; i < n; i++)
    {

        // Iterate in the range[0, n-1]
        for (let j = 0; j < n; j++) {
            document.write(Math.max(Math.abs(c1 - i), Math.abs(c2 - j)) + " ");
        }
        document.write("<br>");
    }
}

// Driver Code

// Given Input
let c1 = 2;
let c2 = 2;
let n = 5;

// Function Call
printRectPattern(c1, c2, n);

    // This code is contributed by gfgking
</script>
```

**Output:** 

```
2 2 2 2 2 
2 1 1 1 2 
2 1 0 1 2 
2 1 1 1 2 
2 2 2 2 2
```

***时间复杂度:** O(N ^2)*
***辅助空间:** O(1)*