# 使矩阵的每一行和每一列相等所需的最少操作

> 原文： [https://www.geeksforgeeks.org/minimum-operations-required-make-row-column-matrix-equals/](https://www.geeksforgeeks.org/minimum-operations-required-make-row-column-matrix-equals/)

给定大小为`n x n`的方阵。 查找所需的最小操作数，以使每一行和每一列上的元素总数相等。 在一个操作中，将矩阵单元格的任何值加 1。在第一行中，打印所需的最小操作，在接下来的`n`行中，打印`n`个整数，表示操作后的最终矩阵。

**例如**：

```
Input: 
1 2
3 4
Output: 
4
4 3
3 4
Explanation
1\. Increment value of cell(0, 0) by 3
2\. Increment value of cell(0, 1) by 1
Hence total 4 operation are required

Input: 9
1 2 3
4 2 3
3 2 1
Output: 
6
2 4 3 
4 2 3 
3 3 3 

```



方法很简单，假设`maxSum`是所有行和列中的最大和。 我们只需要增加一些单元格，以使任何行或列的总和变为`maxSum`。

假设`X[i]`是使行`i`上的总和等于`maxSum`和`Y[j]`是使列`j`的总和等于`maxSum`所需的操作总数。 由于`X[i] = Y[j]`，因此我们需要根据条件对其中任何一个进行操作。

为了最小化`X[i]`，我们需要从`rowSum[i]`和`colSum[j]`，因为它肯定会导致最低限度的运行。 之后，根据递增后满足的条件递增`i`或`j`。

下面是上述方法的实现。

## C++ 

```cpp

/* C++ Program to Find minimum number of 
operation required such that sum of 
elements on each row and column becomes same*/
#include <bits/stdc++.h> 
using namespace std; 

// Function to find minimum operation required 
// to make sum of each row and column equals 
int findMinOpeartion(int matrix[][2], int n) 
{ 
    // Initialize the sumRow[] and sumCol[] 
    // array to 0 
    int sumRow[n], sumCol[n]; 
    memset(sumRow, 0, sizeof(sumRow)); 
    memset(sumCol, 0, sizeof(sumCol)); 

    // Calculate sumRow[] and sumCol[] array 
    for (int i = 0; i < n; ++i) 
        for (int j = 0; j < n; ++j) { 
            sumRow[i] += matrix[i][j]; 
            sumCol[j] += matrix[i][j]; 
        } 

    // Find maximum sum value in either 
    // row or in column 
    int maxSum = 0; 
    for (int i = 0; i < n; ++i) { 
        maxSum = max(maxSum, sumRow[i]); 
        maxSum = max(maxSum, sumCol[i]); 
    } 

    int count = 0; 
    for (int i = 0, j = 0; i < n && j < n;) { 

        // Find minimum increment required in 
        // either row or column 
        int diff = min(maxSum - sumRow[i], 
                       maxSum - sumCol[j]); 

        // Add difference in corresponding cell, 
        // sumRow[] and sumCol[] array 
        matrix[i][j] += diff; 
        sumRow[i] += diff; 
        sumCol[j] += diff; 

        // Update the count variable 
        count += diff; 

        // If ith row satisfied, increment ith 
        // value for next iteration 
        if (sumRow[i] == maxSum) 
            ++i; 

        // If jth column satisfied, increment 
        // jth value for next iteration 
        if (sumCol[j] == maxSum) 
            ++j; 
    } 
    return count; 
} 

// Utility function to print matrix 
void printMatrix(int matrix[][2], int n) 
{ 
    for (int i = 0; i < n; ++i) { 
        for (int j = 0; j < n; ++j) 
            cout << matrix[i][j] << " "; 
        cout << "\n"; 
    } 
} 

// Driver code 
int main() 
{ 
    int matrix[][2] = { { 1, 2 }, 
                        { 3, 4 } }; 
    cout << findMinOpeartion(matrix, 2) << "\n"; 
    printMatrix(matrix, 2); 
    return 0; 
} 

```

## Java

```java

// Java Program to Find minimum  
// number of operation required  
// such that sum of elements on  
// each row and column becomes same 
import java.io.*; 

class GFG { 

    // Function to find minimum 
    // operation required 
    // to make sum of each row 
    // and column equals 
    static int findMinOpeartion(int matrix[][], 
                                         int n) 
    { 
        // Initialize the sumRow[] 
        // and sumCol[] array to 0 
        int[] sumRow = new int[n]; 
        int[] sumCol = new int[n]; 

        // Calculate sumRow[] and 
        // sumCol[] array 
        for (int i = 0; i < n; ++i) 

            for (int j = 0; j < n; ++j) 
            { 
                sumRow[i] += matrix[i][j]; 
                sumCol[j] += matrix[i][j]; 
            } 

        // Find maximum sum value  
        // in either row or in column 
        int maxSum = 0; 
        for (int i = 0; i < n; ++i)  
        { 
            maxSum = Math.max(maxSum, sumRow[i]); 
            maxSum = Math.max(maxSum, sumCol[i]); 
        } 

        int count = 0; 
        for (int i = 0, j = 0; i < n && j < n;)  
        { 
            // Find minimum increment 
            // required in either row 
            // or column 
            int diff = Math.min(maxSum - sumRow[i], 
                        maxSum - sumCol[j]); 

            // Add difference in  
            // corresponding cell, 
            // sumRow[] and sumCol[] 
            // array 
            matrix[i][j] += diff; 
            sumRow[i] += diff; 
            sumCol[j] += diff; 

            // Update the count  
            // variable 
            count += diff; 

            // If ith row satisfied, 
            // increment ith value  
            // for next iteration 
            if (sumRow[i] == maxSum) 
                ++i; 

            // If jth column satisfied,  
            // increment jth value for 
            // next iteration 
            if (sumCol[j] == maxSum) 
                ++j; 
        } 
        return count; 
    } 

    // Utility function to  
    // print matrix 
    static void printMatrix(int matrix[][], 
                                     int n) 
    { 
        for (int i = 0; i < n; ++i)  
        { 
            for (int j = 0; j < n; ++j) 
                System.out.print(matrix[i][j] + 
                                           " "); 

            System.out.println(); 
        } 
    } 

    /* Driver program */
    public static void main(String[] args) 
    { 
        int matrix[][] = {{1, 2}, 
                          {3, 4}}; 

        System.out.println(findMinOpeartion(matrix, 2)); 
        printMatrix(matrix, 2); 

    } 
} 

// This code is contributed by Gitanjali.  

```

## Python 3

```py

# Python 3 Program to Find minimum  
# number of operation required such  
# that sum of elements on each row 
# and column becomes same  

# Function to find minimum operation  
# required to make sum of each row  
# and column equals 
def findMinOpeartion(matrix, n): 

    # Initialize the sumRow[] and sumCol[] 
    # array to 0 
    sumRow = [0] * n 
    sumCol = [0] * n 

    # Calculate sumRow[] and sumCol[] array 
    for i in range(n): 
        for j in range(n) : 
            sumRow[i] += matrix[i][j] 
            sumCol[j] += matrix[i][j] 

    # Find maximum sum value in  
    # either row or in column 
    maxSum = 0
    for i in range(n) : 
        maxSum = max(maxSum, sumRow[i]) 
        maxSum = max(maxSum, sumCol[i]) 

    count = 0
    i = 0
    j = 0
    while i < n and j < n : 

        # Find minimum increment required  
        # in either row or column 
        diff = min(maxSum - sumRow[i],  
                   maxSum - sumCol[j]) 

        # Add difference in corresponding  
        # cell, sumRow[] and sumCol[] array 
        matrix[i][j] += diff 
        sumRow[i] += diff 
        sumCol[j] += diff 

        # Update the count variable 
        count += diff 

        # If ith row satisfied, increment  
        # ith value for next iteration 
        if (sumRow[i] == maxSum): 
            i += 1

        # If jth column satisfied, increment 
        # jth value for next iteration 
        if (sumCol[j] == maxSum): 
            j += 1

    return count 

# Utility function to print matrix 
def printMatrix(matrix, n): 
    for i in range(n) : 
        for j in range(n): 
            print(matrix[i][j], end = " ") 
        print() 

# Driver code 
if __name__ == "__main__": 
    matrix = [[ 1, 2 ], 
              [ 3, 4 ]] 
    print(findMinOpeartion(matrix, 2)) 
    printMatrix(matrix, 2) 

# This code is contributed 
# by ChitraNayal 

```

## C# 

```cs

// C# Program to Find minimum  
// number of operation required  
// such that sum of elements on  
// each row and column becomes same 
using System; 

class GFG { 

    // Function to find minimum 
    // operation required 
    // to make sum of each row 
    // and column equals 
    static int findMinOpeartion(int [,]matrix, 
                                        int n) 
    { 
        // Initialize the sumRow[] 
        // and sumCol[] array to 0 
        int[] sumRow = new int[n]; 
        int[] sumCol = new int[n]; 

        // Calculate sumRow[] and 
        // sumCol[] array 
        for (int i = 0; i < n; ++i) 

            for (int j = 0; j < n; ++j) 
            { 
                sumRow[i] += matrix[i,j]; 
                sumCol[j] += matrix[i,j]; 
            } 

        // Find maximum sum value  
        // in either row or in column 
        int maxSum = 0; 
        for (int i = 0; i < n; ++i)  
        { 
            maxSum = Math.Max(maxSum, sumRow[i]); 
            maxSum = Math.Max(maxSum, sumCol[i]); 
        } 

        int count = 0; 
        for (int i = 0, j = 0; i < n && j < n;)  
        { 
            // Find minimum increment 
            // required in either row 
            // or column 
            int diff = Math.Min(maxSum - sumRow[i], 
                        maxSum - sumCol[j]); 

            // Add difference in  
            // corresponding cell, 
            // sumRow[] and sumCol[] 
            // array 
            matrix[i,j] += diff; 
            sumRow[i] += diff; 
            sumCol[j] += diff; 

            // Update the count  
            // variable 
            count += diff; 

            // If ith row satisfied, 
            // increment ith value  
            // for next iteration 
            if (sumRow[i] == maxSum) 
                ++i; 

            // If jth column satisfied,  
            // increment jth value for 
            // next iteration 
            if (sumCol[j] == maxSum) 
                ++j; 
        } 
        return count; 
    } 

    // Utility function to  
    // print matrix 
    static void printMatrix(int [,]matrix, 
                                    int n) 
    { 
        for (int i = 0; i < n; ++i)  
        { 
            for (int j = 0; j < n; ++j) 
                Console.Write(matrix[i,j] + 
                                        " "); 

            Console.WriteLine(); 
        } 
    } 

    /* Driver program */
    public static void Main() 
    { 
        int [,]matrix = {{1, 2}, 
                        {3, 4}}; 

        Console.WriteLine(findMinOpeartion(matrix, 2)); 
        printMatrix(matrix, 2); 

    } 
} 

// This code is contributed by Vt_m.  

```

```
Output
4
4 3
3 4

```

**时间复杂度**：`O(n^2)`。

**辅助空间**：`O(n)`。



* * *

* * *



