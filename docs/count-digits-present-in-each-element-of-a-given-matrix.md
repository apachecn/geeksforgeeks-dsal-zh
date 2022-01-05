# 计算给定矩阵每个元素中出现的位数

> 原文:[https://www . geeksforgeeks . org/count-digits-给定矩阵的每个元素中存在的位数/](https://www.geeksforgeeks.org/count-digits-present-in-each-element-of-a-given-matrix/)

给定维度为 **M * N** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，任务是计算给定矩阵中每个元素的位数。

**示例:**

> **输入:** arr[][] = { { 27，173，5 }，{ 21，6，624 }，{ 5，321，49 } }
> **输出:**
> 2 3 1
> 2 1 3
> 1 3 2
> 
> **输入:** arr[][] = { {11，12，33 }，{ 64，57，61 }，{ 74，88，39 } }
> **输出:**
> 2 2 2
> 2 2
> 2 2 2

**方法:**解决这个问题的思路是[遍历给定的矩阵](https://www.geeksforgeeks.org/print-a-2d-array-or-matrix-using-single-loop/)，对于矩阵的每个索引，[使用以下表达式计算该索引处出现的数字的位数](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/):

> **任何数值 **X** 中出现的位数**由**楼层(log10(X))+1** 给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int M = 3;
const int N = 3;

// Function to count the number of digits
// in each element of the given matrix
void countDigit(int arr[M][N])
{

    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++) {

        // Traverse each column of arr[][]
        for (int j = 0; j < N; j++) {

            // Store the current matrix element
            int X = arr[i][j];

            // Count the number of digits
            int d = floor(log10(X) * 1.0) + 1;

            // Print the result
            cout << d << " ";
        }

        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given matrix
    int arr[][3] = { { 27, 173, 5 },
                     { 21, 6, 624 },
                     { 5, 321, 49 } };

    countDigit(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

static int M = 3;
static int N = 3;

// Function to count the number of digits
// in each element of the given matrix
static void countDigit(int arr[][])
{

    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for (int j = 0; j < N; j++)
        {

            // Store the current matrix element
            int X = arr[i][j];

            // Count the number of digits
            int d = (int) (Math.floor(Math.log10(X) * 1.0) + 1);

            // Print the result
            System.out.print(d+ " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given matrix
    int arr[][] = { { 27, 173, 5 },
                     { 21, 6, 624 },
                     { 5, 321, 49 } };
    countDigit(arr);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import floor, log10

M = 3
N = 3

# Function to count the number of digits
# in each element of the given matrix
def countDigit(arr):

    # Traverse each row of arr[][]
    for i in range(M):

        # Traverse each column of arr[][]
        for j in range(N):

            # Store the current matrix element
            X = arr[i][j]

            # Count the number of digits
            d = floor(log10(X) * 1.0) + 1

            # Print the result
            print(d, end = " ")

        print()

# Driver Code
if __name__ == '__main__':

    # Given matrix
    arr = [ [ 27, 173, 5 ],
            [ 21, 6, 624 ],
            [ 5, 321, 49 ] ]

    countDigit(arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

static int M = 3;
static int N = 3;

// Function to count the number of digits
// in each element of the given matrix
static void countDigit(int[,] arr)
{

    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for (int j = 0; j < N; j++)
        {

            // Store the current matrix element
            int X = arr[i, j];

            // Count the number of digits
            int d = (int) (Math.Floor(Math.Log10(X) * 1.0) + 1);

            // Print the result
            Console.Write(d + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main()
{

    // Given matrix
    int[,] arr = { { 27, 173, 5 },
                     { 21, 6, 624 },
                     { 5, 321, 49 } };
    countDigit(arr);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

let M = 3;
let N = 3;

// Function to count the number of digits
// in each element of the given matrix
function countDigit(arr)
{

    // Traverse each row of arr[][]
    for (let i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for (let j = 0; j < N; j++)
        {

            // Store the current matrix element
            let X = arr[i][j];

            // Count the number of digits
            let d =  (Math.floor(Math.log10(X) * 1.0) + 1);

            // Prlet the result
            document.write(d+ " ");
        }
        document.write("<br/>");
    }
}

// Driver code

    // Given matrix
    let arr = [[ 27, 173, 5 ],
                     [ 21, 6, 624 ],
                     [ 5, 321, 49 ]];
    countDigit(arr);

</script>
```

**Output:** 

```
2 3 1 
2 1 3 
1 3 2
```

***时间复杂度:*** O(M * N)
***辅助空间:*** O(1)