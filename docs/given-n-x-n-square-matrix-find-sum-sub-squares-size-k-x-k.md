# 给定一个`n x n`方阵，求出大小为`k x k`的所有子方和

> 原文： [https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/](https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/)

给定一个`n x n`的正方形矩阵，求出所有大小为`k x k`的子正方形的和，其中`k`小于或等于`n`。

**示例**：

```
Input:
n = 5, k = 3
arr[][] = { {1, 1, 1, 1, 1},
            {2, 2, 2, 2, 2},
            {3, 3, 3, 3, 3},
            {4, 4, 4, 4, 4},
            {5, 5, 5, 5, 5},
         };
Output:
       18  18  18
       27  27  27
       36  36  36

Input:
n = 3, k = 2
arr[][] = { {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9},
         };
Output:
       12  16
       24  28
```

**简单解决方案**是所有可能子正方形的一个接一个拾取起点（最左上角）。 选取起点后，从选取的起点开始计算子平方和。

以下是该想法的实现。

## C++ 

```cpp

// A simple C++ program to find sum of all subsquares of size k x k 
#include <iostream> 
using namespace std; 

// Size of given matrix 
#define n 5 

// A simple function to find sum of all sub-squares of size k x k 
// in a given square matrix of size n x n 
void printSumSimple(int mat[][n], int k) 
{ 
   // k must be smaller than or equal to n 
   if (k > n) return; 

   // row number of first cell in current sub-square of size k x k 
   for (int i=0; i<n-k+1; i++) 
   { 
      // column of first cell in current sub-square of size k x k 
      for (int j=0; j<n-k+1; j++) 
      { 
          // Calculate and print sum of current sub-square 
          int sum = 0; 
          for (int p=i; p<k+i; p++) 
             for (int q=j; q<k+j; q++) 
                 sum += mat[p][q]; 
           cout << sum << "  "; 
      } 

      // Line separator for sub-squares starting with next row 
      cout << endl; 
   } 
} 

// Driver program to test above function 
int main() 
{ 
    int mat[n][n] = {{1, 1, 1, 1, 1}, 
                     {2, 2, 2, 2, 2}, 
                     {3, 3, 3, 3, 3}, 
                     {4, 4, 4, 4, 4}, 
                     {5, 5, 5, 5, 5}, 
                    }; 
    int k = 3; 
    printSumSimple(mat, k); 
    return 0; 
} 

```

## Java

```java
// A simple Java program to find sum of all  
// subsquares of size k x k 
class GFG 
{ 
      
    // Size of given matrix 
    static final int n = 5; 
      
    // A simple function to find sum of all  
    //sub-squares of size k x k in a given  
    // square matrix of size n x n 
    static void printSumSimple(int mat[][], int k) 
    { 
  
        // k must be smaller than or  
        // equal to n 
        if (k > n) return; 
          
        // row number of first cell in  
        // current sub-square of size k x k 
        for (int i = 0; i < n-k+1; i++) 
        { 
              
            // column of first cell in current  
            // sub-square of size k x k 
            for (int j = 0; j < n-k+1; j++) 
            { 
                  
                // Calculate and print sum of  
                // current sub-square 
                int sum = 0; 
                for (int p = i; p < k+i; p++) 
                    for (int q = j; q < k+j; q++) 
                        sum += mat[p][q]; 
  
                System.out.print(sum+ " "); 
            } 
          
            // Line separator for sub-squares  
            // starting with next row 
            System.out.println(); 
        } 
    } 
      
    // Driver Program to test above function 
    public static void main(String arg[]) 
    { 
        int mat[][] = {{1, 1, 1, 1, 1}, 
                       {2, 2, 2, 2, 2}, 
                       {3, 3, 3, 3, 3}, 
                       {4, 4, 4, 4, 4}, 
                       {5, 5, 5, 5, 5}}; 
        int k = 3; 
        printSumSimple(mat, k); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python 3

```
# A simple Python 3 program to find sum  
# of all subsquares of size k x k 
  
# Size of given matrix 
n = 5
  
# A simple function to find sum of all  
# sub-squares of size k x k in a given 
# square matrix of size n x n 
def printSumSimple(mat, k): 
  
    # k must be smaller than or equal to n 
    if (k > n): 
        return
  
    # row number of first cell in current 
    # sub-square of size k x k 
    for i in range(n - k + 1): 
      
        # column of first cell in current  
        # sub-square of size k x k 
        for j in range(n - k + 1): 
              
            # Calculate and print sum of  
            # current sub-square 
            sum = 0
            for p in range(i, k + i): 
                for q in range(j, k + j): 
                    sum += mat[p][q] 
            print(sum, end = " ") 
      
        # Line separator for sub-squares  
        # starting with next row 
        print() 
  
# Driver Code 
if __name__ == "__main__": 
  
    mat = [[1, 1, 1, 1, 1], 
           [2, 2, 2, 2, 2], 
           [3, 3, 3, 3, 3], 
           [4, 4, 4, 4, 4], 
           [5, 5, 5, 5, 5]] 
    k = 3
    printSumSimple(mat, k) 
  
# This code is contributed by ita_c
```

## C#

```cs
// A simple C# program to find sum of all  
// subsquares of size k x k 
using System; 
  
class GFG 
{ 
    // Size of given matrix 
    static int n = 5; 
      
    // A simple function to find sum of all  
    //sub-squares of size k x k in a given  
    // square matrix of size n x n 
    static void printSumSimple(int [,]mat, int k) 
    { 
        // k must be smaller than or  
        // equal to n 
        if (k > n) return; 
          
        // row number of first cell in  
        // current sub-square of size k x k 
        for (int i = 0; i < n-k+1; i++) 
        { 
            // column of first cell in current  
            // sub-square of size k x k 
            for (int j = 0; j < n-k+1; j++) 
            { 
                // Calculate and print sum of  
                // current sub-square 
                int sum = 0; 
                for (int p = i; p < k+i; p++) 
                    for (int q = j; q < k+j; q++) 
                        sum += mat[p,q]; 
  
                Console.Write(sum+ " "); 
            } 
          
            // Line separator for sub-squares  
            // starting with next row 
            Console.WriteLine(); 
        } 
    } 
      
    // Driver Program to test above function 
    public static void Main() 
    { 
        int [,]mat = {{1, 1, 1, 1, 1}, 
                      {2, 2, 2, 2, 2}, 
                      {3, 3, 3, 3, 3}, 
                      {4, 4, 4, 4, 4}, 
                      {5, 5, 5, 5, 5}}; 
        int k = 3; 
        printSumSimple(mat, k); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// A simple PHP program to find  
// sum of all subsquares of size 
// k x k 
  
// Size of given matrix 
$n = 5; 
  
// function to find sum of all sub -  
// squares of size k x k in a given  
// square matrix of size n x n 
function printSumSimple( $mat, $k) 
{ 
    global $n; 
      
    // k must be smaller than 
    // or equal to n 
    if ($k > $n) return; 
      
    // row number of first cell in  
    // current sub-square of size 
    // k x k 
    for($i = 0; $i < $n - $k + 1; $i++) 
    { 
          
        // column of first cell in  
        // current sub-square of size 
        // k x k 
        for($j = 0; $j < $n - $k + 1; $j++) 
        { 
              
            // Calculate and print sum of 
            // current sub-square 
            $sum = 0; 
            for ($p = $i; $p < $k + $i; $p++) 
                for ($q = $j; $q < $k + $j; $q++) 
                    $sum += $mat[$p][$q]; 
            echo $sum , " "; 
        } 
      
        // Line separator for sub-squares 
        // starting with next row 
        echo "\n"; 
    } 
} 
  
    // Driver Code 
    $mat = array(array(1, 1, 1, 1, 1), 
                 array(2, 2, 2, 2, 2,), 
                  array(3, 3, 3, 3, 3,), 
                 array(4, 4, 4, 4, 4,), 
                 array(5, 5, 5, 5, 5)); 
                      
    $k = 3; 
    printSumSimple($mat, $k); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
  18  18  18
  27  27  27
  36  36  36
```

上述解决方案的时间复杂度为`O(k ^ 2 n ^ 2）`。 我们可以使用花式解决方案在`O(n ^ 2)`时间内解决此问题。 这个想法是预处理给定的方阵。 在预处理步骤中，计算临时方阵`stripSum[][]`中大小为`k x 1`的所有垂直条的总和。 一旦我们有了所有垂直条带的总和，我们就可以计算该行中第一个子正方形的总和作为该行中前`k`个条带的总和，对于剩余的子正方形，我们可以在`O(1)`时间内计算总和，通过去除前一个子正方形的最左边的条，并添加新正方形的最右边的条。

以下是该想法的实现。

## C++

```cpp
// An efficient C++ program to find sum of all subsquares of size k x k 
#include <iostream> 
using namespace std; 
  
// Size of given matrix 
#define n 5 
  
// A O(n^2) function to find sum of all sub-squares of size k x k 
// in a given square matrix of size n x n 
void printSumTricky(int mat[][n], int k) 
{ 
   // k must be smaller than or equal to n 
   if (k > n) return; 
  
   // 1: PREPROCESSING 
   // To store sums of all strips of size k x 1 
   int stripSum[n][n]; 
  
   // Go column by column 
   for (int j=0; j<n; j++) 
   { 
       // Calculate sum of first k x 1 rectangle in this column 
       int sum = 0; 
       for (int i=0; i<k; i++) 
          sum += mat[i][j]; 
       stripSum[0][j] = sum; 
  
       // Calculate sum of remaining rectangles 
       for (int i=1; i<n-k+1; i++) 
       { 
            sum += (mat[i+k-1][j] - mat[i-1][j]); 
            stripSum[i][j] = sum; 
       } 
   } 
  
   // 2: CALCULATE SUM of Sub-Squares using stripSum[][] 
   for (int i=0; i<n-k+1; i++) 
   { 
      // Calculate and print sum of first subsquare in this row 
      int sum = 0; 
      for (int j = 0; j<k; j++) 
           sum += stripSum[i][j]; 
      cout << sum << "  "; 
  
      // Calculate sum of remaining squares in current row by 
      // removing the leftmost strip of previous sub-square and 
      // adding a new strip 
      for (int j=1; j<n-k+1; j++) 
      { 
         sum += (stripSum[i][j+k-1] - stripSum[i][j-1]); 
         cout << sum << "  "; 
      } 
  
      cout << endl; 
   } 
} 
  
// Driver program to test above function 
int main() 
{ 
    int mat[n][n] = {{1, 1, 1, 1, 1}, 
                     {2, 2, 2, 2, 2}, 
                     {3, 3, 3, 3, 3}, 
                     {4, 4, 4, 4, 4}, 
                     {5, 5, 5, 5, 5}, 
                    }; 
    int k = 3; 
    printSumTricky(mat, k); 
    return 0; 
}
```

## Java

```java
// An efficient Java program to find 
// sum of all subsquares of size k x k 
import java.io.*; 
  
class GFG { 
      
// Size of given matrix 
static int n = 5; 
  
// A O(n^2) function to find sum of all 
// sub-squares of size k x k in a given 
// square matrix of size n x n 
static void printSumTricky(int mat[][], int k) { 
      
    // k must be smaller than or equal to n 
    if (k > n) 
    return; 
  
    // 1: PREPROCESSING 
    // To store sums of all strips of size k x 1 
    int stripSum[][] = new int[n][n]; 
  
    // Go column by column 
    for (int j = 0; j < n; j++) { 
          
    // Calculate sum of first k x 1 
    // rectangle in this column 
    int sum = 0; 
    for (int i = 0; i < k; i++) 
        sum += mat[i][j]; 
    stripSum[0][j] = sum; 
  
    // Calculate sum of remaining rectangles 
    for (int i = 1; i < n - k + 1; i++) { 
        sum += (mat[i + k - 1][j] - mat[i - 1][j]); 
        stripSum[i][j] = sum; 
    } 
    } 
  
    // 2: CALCULATE SUM of Sub-Squares  
    // using stripSum[][] 
    for (int i = 0; i < n - k + 1; i++) { 
          
    // Calculate and print sum of first  
    // subsquare in this row 
    int sum = 0; 
    for (int j = 0; j < k; j++) 
        sum += stripSum[i][j]; 
    System.out.print(sum + " "); 
  
    // Calculate sum of remaining squares  
    // in current row by removing the 
    // leftmost strip of previous sub-square  
    // and adding a new strip 
    for (int j = 1; j < n - k + 1; j++) { 
        sum += (stripSum[i][j + k - 1] - stripSum[i][j - 1]); 
        System.out.print(sum + " "); 
    } 
    System.out.println(); 
    } 
} 
  
// Driver program to test above function 
public static void main(String[] args) 
{ 
    int mat[][] = {{1, 1, 1, 1, 1}, 
                   {2, 2, 2, 2, 2}, 
                   {3, 3, 3, 3, 3}, 
                   {4, 4, 4, 4, 4},  
                   {5, 5, 5, 5, 5}, 
                  }; 
    int k = 3; 
    printSumTricky(mat, k); 
} 
} 
  
// This code is contributed by vt_m.
```

## Python3

```py
# An efficient Python3 program to find sum  
# of all subsquares of size k x k  
  
# A O(n^2) function to find sum of all   
# sub-squares of size k x k in a given  
# square matrix of size n x n  
def printSumTricky(mat, k): 
    global n 
      
    # k must be smaller than or  
    # equal to n  
    if k > n: 
        return
  
    # 1: PREPROCESSING  
    # To store sums of all strips of size k x 1  
    stripSum = [[None] * n for i in range(n)] 
  
    # Go column by column 
    for j in range(n): 
          
        # Calculate sum of first k x 1  
        # rectangle in this column  
        Sum = 0
        for i in range(k): 
            Sum += mat[i][j]  
        stripSum[0][j] = Sum
  
        # Calculate sum of remaining rectangles 
        for i in range(1, n - k + 1): 
            Sum += (mat[i + k - 1][j] -
                    mat[i - 1][j])  
            stripSum[i][j] = Sum
  
    # 2: CALCULATE SUM of Sub-Squares 
    # using stripSum[][] 
    for i in range(n - k + 1): 
          
        # Calculate and prsum of first  
        # subsquare in this row  
        Sum = 0
        for j in range(k): 
            Sum += stripSum[i][j]  
        print(Sum, end = " ") 
  
        # Calculate sum of remaining squares  
        # in current row by removing the leftmost   
        # strip of previous sub-square and adding 
        # a new strip 
        for j in range(1, n - k + 1): 
            Sum += (stripSum[i][j + k - 1] -
                    stripSum[i][j - 1])  
            print(Sum, end = " ") 
  
        print() 
  
# Driver Code 
n = 5
mat = [[1, 1, 1, 1, 1], 
       [2, 2, 2, 2, 2],  
       [3, 3, 3, 3, 3], 
       [4, 4, 4, 4, 4], 
       [5, 5, 5, 5, 5]]  
k = 3
printSumTricky(mat, k)  
  
# This code is contributed by PranchalK
```

## C#

```cs
// An efficient C# program to find 
// sum of all subsquares of size k x k 
using System; 
class GFG { 
      
    // Size of given matrix 
    static int n = 5; 
      
    // A O(n^2) function to find sum of all 
    // sub-squares of size k x k in a given 
    // square matrix of size n x n 
    static void printSumTricky(int [,]mat, int k)  
    { 
          
        // k must be smaller than or equal to n 
        if (k > n) 
        return; 
      
        // 1: PREPROCESSING 
        // To store sums of all strips of 
        // size k x 1 
        int [,]stripSum = new int[n,n]; 
      
        // Go column by column 
        for (int j = 0; j < n; j++) 
        { 
              
            // Calculate sum of first k x 1 
            // rectangle in this column 
            int sum = 0; 
            for (int i = 0; i < k; i++) 
                sum += mat[i,j]; 
                  
            stripSum[0,j] = sum; 
          
            // Calculate sum of remaining 
            // rectangles 
            for (int i = 1; i < n - k + 1; i++) 
            { 
                sum += (mat[i + k - 1,j]  
                               - mat[i - 1,j]); 
                stripSum[i,j] = sum; 
            } 
        } 
      
        // 2: CALCULATE SUM of Sub-Squares  
        // using stripSum[][] 
        for (int i = 0; i < n - k + 1; i++) 
        { 
              
            // Calculate and print sum of first  
            // subsquare in this row 
            int sum = 0; 
            for (int j = 0; j < k; j++) 
                sum += stripSum[i,j]; 
                  
            Console.Write(sum + " "); 
          
            // Calculate sum of remaining  
            // squares in current row by  
            // removing the leftmost strip 
            // of previous sub-square  
            // and adding a new strip 
            for (int j = 1; j < n - k + 1; j++)  
            { 
                sum += (stripSum[i,j + k - 1]  
                           - stripSum[i,j - 1]); 
                Console.Write(sum + " "); 
            } 
            Console.WriteLine(); 
        } 
    } 
      
    // Driver program to test above function 
    public static void Main() 
    { 
        int [,]mat = {{1, 1, 1, 1, 1}, 
                    {2, 2, 2, 2, 2}, 
                    {3, 3, 3, 3, 3}, 
                    {4, 4, 4, 4, 4},  
                    {5, 5, 5, 5, 5}, 
                    }; 
        int k = 3; 
        printSumTricky(mat, k); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// An efficient PHP program to 
// find sum of all subsquares 
// of size k x k 
  
// Size of given matrix 
$n = 5; 
  
// A O(n^2) function to find  
// sum of all sub-squares of  
// size k x k in a given 
// square matrix of size n x n 
function printSumTricky($mat, $k) 
{ 
global $n; 
  
// k must be smaller  
// than or equal to n 
if ($k > $n) return; 
  
// 1: PREPROCESSING 
// To store sums of all  
// strips of size k x 1 
$stripSum = array(array()); 
  
// Go column by column 
for ($j = 0; $j < $n; $j++) 
{ 
    // Calculate sum of first 
    // k x 1 rectangle in this column 
    $sum = 0; 
    for ($i = 0; $i < $k; $i++) 
        $sum += $mat[$i][$j]; 
    $stripSum[0][$j] = $sum; 
  
    // Calculate sum of  
    // remaining rectangles 
    for ($i = 1; $i < $n - $k + 1; $i++) 
    { 
            $sum += ($mat[$i + $k - 1][$j] -  
                          $mat[$i - 1][$j]); 
            $stripSum[$i][$j] = $sum; 
    } 
} 
  
// 2: CALCULATE SUM of  
// Sub-Squares using stripSum[][] 
for ($i = 0; $i < $n - $k + 1; $i++) 
{ 
    // Calculate and print sum of  
    // first subsquare in this row 
    $sum = 0; 
    for ($j = 0; $j < $k; $j++) 
        $sum += $stripSum[$i][$j]; 
    echo $sum , " "; 
  
    // Calculate sum of remaining  
    // squares in current row by 
    // removing the leftmost strip  
    // of previous sub-square and 
    // adding a new strip 
    for ($j = 1; $j < $n - $k + 1; $j++) 
    { 
        $sum += ($stripSum[$i][$j + $k - 1] -  
                 $stripSum[$i][$j - 1]); 
        echo $sum , " "; 
    } 
  
    echo "\n"; 
} 
} 
  
// Driver Code 
$mat = array(array(1, 1, 1, 1, 1), 
             array(2, 2, 2, 2, 2), 
             array(3, 3, 3, 3, 3), 
             array(4, 4, 4, 4, 4), 
             array(5, 5, 5, 5, 5)); 
$k = 3; 
printSumTricky($mat, $k); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
  18  18  18
  27  27  27
  36  36  36
```

