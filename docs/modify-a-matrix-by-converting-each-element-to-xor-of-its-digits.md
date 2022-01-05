# 通过将每个元素转换为其数字的异或来修改矩阵

> 原文:[https://www . geeksforgeeks . org/通过将其数字的每个元素转换为异或来修改矩阵/](https://www.geeksforgeeks.org/modify-a-matrix-by-converting-each-element-to-xor-of-its-digits/)

给定维度为 **M*N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**arr【】【】【】**，任务是将每个矩阵元素转换为元素中数字的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[][] = {{27，173}，{5，21}}
> **输出:**
> 5 5
> 5 3
> t8】解释:
> arr[0][0](= 27)的数字按位异或是 5 (2^7).
> arr[0][1](= 173)的数字按位异或值为 5 (1 ^ 7 ^ 3)。
> arr[1][0](= 5)位数的按位异或值为 5。
> arr[1][1](= 21)的数字按位异或值为 3(1 ^ 2)。
> 
> **输入:** arr[][] = {{11，12，33}，{64，57，61}，{74，88，39}}
> **输出:**
> 0 3 0
> 2 2 7
> 3 0 10

**逼近:**为了解决这个问题，逼近思想是[遍历给定的矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)，对于每个矩阵元素，打印其数字的[按位异或。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int M = 3;
const int N = 3;

// Function to calculate Bitwise
// XOR of digits present in X
int findXOR(int X)
{

    // Stores the Bitwise XOR
    int ans = 0;

    // While X is true
    while (X) {

        // Update Bitwise
        // XOR of its digits
        ans ^= (X % 10);
        X /= 10;
    }

    // Return the result
    return ans;
}

// Function to print matrix after
// converting each matrix element
// to XOR of its digits
void printXORmatrix(int arr[M][N])
{
    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++) {

        // Traverse each column of arr[][]
        for (int j = 0; j < N; j++) {
            cout << arr[i][j] << " ";
        }
        cout << "\n";
    }
}

// Function to convert the given
// matrix to required XOR matrix
void convertXOR(int arr[M][N])
{
    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++) {

        // Traverse each column of arr[][]
        for (int j = 0; j < N; j++) {

            // Store the current
            // matrix element
            int X = arr[i][j];

            // Find the xor of
            // digits present in X
            int temp = findXOR(X);

            // Stores the XOR value
            arr[i][j] = temp;
        }
    }

    // Print resultant matrix
    printXORmatrix(arr);
}

// Driver Code
int main()
{
    int arr[][3] = { { 27, 173, 5 },
                     { 21, 6, 624 },
                     { 5, 321, 49 } };

    convertXOR(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

static int M = 3;
static int N = 3;

// Function to calculate Bitwise
// XOR of digits present in X
static int findXOR(int X)
{

    // Stores the Bitwise XOR
    int ans = 0;

    // While X is true
    while (X != 0)
    {

        // Update Bitwise
        // XOR of its digits
        ans ^= (X % 10);
        X /= 10;
    }

    // Return the result
    return ans;
}

// Function to print matrix after
// converting each matrix element
// to XOR of its digits
static void printXORmatrix(int arr[][])
{

    // Traverse each row of arr[][]
    for(int i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for(int j = 0; j < N; j++)
        {
            System.out.print(arr[i][j] + " ");
        }
        System.out.println();
    }
}

// Function to convert the given
// matrix to required XOR matrix
static void convertXOR(int arr[][])
{

    // Traverse each row of arr[][]
    for(int i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for(int j = 0; j < N; j++)
        {

            // Store the current
            // matrix element
            int X = arr[i][j];

            // Find the xor of
            // digits present in X
            int temp = findXOR(X);

            // Stores the XOR value
            arr[i][j] = temp;
        }
    }

    // Print resultant matrix
    printXORmatrix(arr);
}

// Driver Code
public static void main (String[] args)
{
    int arr[][] = { { 27, 173, 5 },
                    { 21, 6, 624 },
                    { 5, 321, 49 } };

    convertXOR(arr);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
M = 3
N = 3

# Function to calculate Bitwise
# XOR of digits present in X
def findXOR(X):

    # Stores the Bitwise XOR
    ans = 0

    # While X is true
    while (X):

        # Update Bitwise
        # XOR of its digits
        ans ^= (X % 10)
        X //= 10

    # Return the result
    return ans

# Function to print matrix after
# converting each matrix element
# to XOR of its digits
def printXORmatrix(arr):

    # Traverse each row of arr[][]
    for i in range(3):

        # Traverse each column of arr[][]
        for j in range(3):
            print(arr[i][j], end = " ")
        print()

# Function to convert the given
# matrix to required XOR matrix
def convertXOR(arr):

    # Traverse each row of arr[][]
    for i in range(3):

        # Traverse each column of arr[][]
        for j in range(3):

            # Store the current
            # matrix element
            X = arr[i][j]

            # Find the xor of
            # digits present in X
            temp = findXOR(X)

            # Stores the XOR value
            arr[i][j] = temp

    # Print resultant matrix
    printXORmatrix(arr)

# Driver Code
if __name__ == '__main__':
    arr=[[27, 173, 5],
        [ 21, 6, 624 ],
        [ 5, 321, 49 ]]

    convertXOR(arr)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int M = 3;
static int N = 3;

// Function to calculate Bitwise
// XOR of digits present in X
static int findXOR(int X)
{

    // Stores the Bitwise XOR
    int ans = 0;

    // While X is true
    while (X != 0)
    {

        // Update Bitwise
        // XOR of its digits
        ans ^= (X % 10);
        X /= 10;
    }

    // Return the result
    return ans;
}

// Function to print matrix after
// converting each matrix element
// to XOR of its digits
static void printXORmatrix(int[,] arr)
{

    // Traverse each row of arr[][]
    for(int i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for(int j = 0; j < N; j++)
        {
            Console.Write(arr[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Function to convert the given
// matrix to required XOR matrix
static void convertXOR(int[,] arr)
{

    // Traverse each row of arr[][]
    for(int i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for(int j = 0; j < N; j++)
        {

            // Store the current
            // matrix element
            int X = arr[i, j];

            // Find the xor of
            // digits present in X
            int temp = findXOR(X);

            // Stores the XOR value
            arr[i, j] = temp;
        }
    }

    // Print resultant matrix
    printXORmatrix(arr);
}

// Driver Code
static public void Main()
{
    int[,] arr = { { 27, 173, 5 },
                   { 21, 6, 624 },
                   { 5, 321, 49 } };

    convertXOR(arr);
}
}

// This code is contributed by splevel62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

let M = 3;
let N = 3;

// Function to calculate Bitwise
// XOR of digits present in X
function findXOR(X)
{

    // Stores the Bitwise XOR
    let ans = 0;

    // While X is true
    while (X != 0)
    {

        // Update Bitwise
        // XOR of its digits
        ans ^= (X % 10);
        X /= 10;
    }

    // Return the result
    return ans;
}

// Function to print matrix after
// converting each matrix element
// to XOR of its digits
function printXORmatrix(arr)
{

    // Traverse each row of arr[][]
    for(let i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for(let j = 0; j < N; j++)
        {
            document.write(arr[i][j] + " ");
        }
        document.write("<br/>");
    }
}

// Function to convert the given
// matrix to required XOR matrix
function convertXOR(arr)
{

    // Traverse each row of arr[][]
    for(let i = 0; i < M; i++)
    {

        // Traverse each column of arr[][]
        for(let j = 0; j < N; j++)
        {

            // Store the current
            // matrix element
            let X = arr[i][j];

            // Find the xor of
            // digits present in X
            let temp = findXOR(X);

            // Stores the XOR value
            arr[i][j] = temp;
        }
    }

    // Print resultant matrix
    prletXORmatrix(arr);
}

// Driver code
    let arr = [[ 27, 173, 5 ],
                    [ 21, 6, 624 ],
                    [ 5, 321, 49 ]];

    convertXOR(arr);;

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
5 5 5 
3 6 0 
5 0 13
```

***时间复杂度:** O(M*N*log <sub>10</sub> K)其中 K 是* [*矩阵中存在的最大元素*](https://www.geeksforgeeks.org/program-to-find-the-maximum-element-in-a-matrix/) *。*
***辅助空间:** O(1)*