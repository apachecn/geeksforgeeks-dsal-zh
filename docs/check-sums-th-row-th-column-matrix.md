# 检查矩阵中第`i`行和第`i`列的总和是否相同

> 原文： [https://www.geeksforgeeks.org/check-sums-th-row-th-column-matrix/](https://www.geeksforgeeks.org/check-sums-th-row-th-column-matrix/)

给定矩阵`mat[][]`，我们必须检查第`i`行的总和是否等于第`i`列的总和。

**示例**：

```
Input : 1 2 3 4 
        9 5 3 1
        0 3 5 6 
        0 4 5 6
Output : Yes
Sums of 1st row = 10 and 1st column 
are same, i.e., 10 

```

预期的时间复杂度为`O(m x n)`，其中`m`为行数，`n`为列数。



这个想法真的很简单。 我们使用嵌套循环来计算每一行和每一列的总和，然后检查它们的总和是否相等。

下面给出上述想法的实现。

## C++ 

```cpp

#include <bits/stdc++.h> 
using namespace std; 
const int MAX = 100; 

// Function to check the if sum of a row 
// is same as corresponding column 
bool areSumSame(int a[][MAX], int n, int m) 
{ 
    int sum1 = 0, sum2 = 0; 
    for (int i = 0; i < n; i++) { 
        sum1 = 0, sum2 = 0; 
        for (int j = 0; j < m; j++) { 
            sum1 += a[i][j]; 
            sum2 += a[j][i]; 
        } 
        if (sum1 == sum2) 
            return true; 
    } 
    return false; 
} 

// Driver Code 
int main() 
{ 
    int n = 4; // number of rows 
    int m = 4; // number of columns 
    int M[n][MAX] = { { 1, 2, 3, 4 }, 
                      { 9, 5, 3, 1 },  
                      { 0, 3, 5, 6 }, 
                      { 0, 4, 5, 6 } }; 
    cout << areSumSame(M, n, m) << "n"; 
    return 0; 
} 

```

## Java

```
// java program to check if there are two 
// adjacent set bits. 
public class GFG { 
      
    // Function to check the if sum of a row 
    // is same as corresponding column 
    static boolean areSumSame(int a[][],  
                             int n, int m) 
    { 
        int sum1 = 0, sum2 = 0; 
        for (int i = 0; i < n; i++)  
        { 
            sum1 = 0; 
            sum2 = 0; 
            for (int j = 0; j < m; j++) 
            { 
                sum1 += a[i][j]; 
                sum2 += a[j][i]; 
            } 
              
            if (sum1 == sum2) 
                return true; 
        } 
          
        return false; 
    } 
      
    // Driver code 
    public static void main(String args[]) 
    { 
  
        int n = 4; // number of rows 
        int m = 4; // number of columns 
          
        int M[][] = { { 1, 2, 3, 4 }, 
                      { 9, 5, 3, 1 },  
                      { 0, 3, 5, 6 }, 
                      { 0, 4, 5, 6 } }; 
                          
        if(areSumSame(M, n, m) == true) 
            System.out.print("1\n"); 
        else
            System.out.print("0\n"); 
    } 
} 
  
// This code is contributed by Sam007.
```

## Python3

```
# Python program to check the if 
# sum of a row is same as  
# corresponding column 
MAX = 100; 
  
# Function to check the if sum  
# of a row is same as 
# corresponding column 
def areSumSame(a, n, m): 
    sum1 = 0
    sum2 = 0
    for i in range(0, n): 
        sum1 = 0
        sum2 = 0
        for j in range(0, m): 
            sum1 += a[i][j] 
            sum2 += a[j][i] 
          
        if (sum1 == sum2): 
            return 1
      
    return 0
  
# Driver Code 
n = 4; # number of rows 
m = 4; # number of columns 
M = [ [ 1, 2, 3, 4 ], 
      [ 9, 5, 3, 1 ], 
      [ 0, 3, 5, 6 ], 
      [ 0, 4, 5, 6 ] ] 
        
print(areSumSame(M, n, m)) 
  
# This code is contributed by Sam007.
```

## C#

```
// C# program to check if there are two 
// adjacent set bits. 
using System; 
  
class GFG { 
      
    // Function to check the if sum of a row 
    // is same as corresponding column 
    static bool areSumSame(int [,]a, int n, int m) 
    { 
        int sum1 = 0, sum2 = 0; 
        for (int i = 0; i < n; i++)  
        { 
            sum1 = 0; 
            sum2 = 0; 
            for (int j = 0; j < m; j++) 
            { 
                sum1 += a[i,j]; 
                sum2 += a[j,i]; 
            } 
              
            if (sum1 == sum2) 
                return true; 
        } 
          
        return false; 
    } 
      
    // Driver code     
    public static void Main () 
    { 
        int n = 4; // number of rows 
        int m = 4; // number of columns 
          
        int [,] M = { { 1, 2, 3, 4 }, 
                      { 9, 5, 3, 1 },  
                      { 0, 3, 5, 6 }, 
                      { 0, 4, 5, 6 } }; 
                        
        if(areSumSame(M, n, m) == true) 
            Console.Write("1\n"); 
        else
            Console.Write("0\n"); 
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```
<?php 
// Function to check the if  
// sum of a row is same as 
// corresponding column  
function areSumSame($a, $n, $m) 
{ 
    $sum1 = 0; 
    $sum2 = 0; 
      
    for($i = 0; $i < $n; $i++) 
    { 
        $sum1 = 0; 
        $sum2 = 0; 
        for($j = 0; $j < $m; $j++) 
        { 
            $sum1 += $a[$i][$j]; 
            $sum2 += $a[$j][$i]; 
        } 
          
        if ($sum1 == $sum2) 
            return true ; 
    } 
    return false ; 
} 
  
// Driver code 
$n = 4 ; // number of rows  
$m = 4 ; // number of columns  
$M = array(array(1, 2, 3, 4), 
           array(9, 5, 3, 1), 
           array(0, 3, 5, 6), 
           array(0, 4, 5, 6)); 
  
echo areSumSame($M, $n, $m) ; 
  
// This code is contributed 
// by ANKITRAI1 
?>
```

输出：

```
1
```

