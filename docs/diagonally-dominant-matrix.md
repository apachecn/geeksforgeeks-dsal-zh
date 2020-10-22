# 对角占优矩阵

> 原文： [https://www.geeksforgeeks.org/diagonally-dominant-matrix/](https://www.geeksforgeeks.org/diagonally-dominant-matrix/)

在数学中，如果对于矩阵的每一行，一行中对角线条目的大小大于或等于，则称方阵为[**对角线优势**](https://en.wikipedia.org/wiki/Diagonally_dominant_matrix#Applications_and_properties)。 该行中所有其他（非对角线）条目的大小。 更准确地说，如果，

![](img/1e586dd1c7115555c3c38bafcde7fba2.png)

矩阵`A`对角占优势，例如，由于，

```
|a11| ≥ |a12| + |a13| since |+3| ≥ |-2| + |+1|
|a22| ≥ |a21| + |a23| since |-3| ≥ |+1| + |+2|
|a33| ≥ |a31| + |a32| since |+4| ≥ |-1| + |+2|
```

矩阵对角占优：

![](img/5211dc2ff64f8483c9b96e8f8cd1b2f1.png)

给定`n`行和`n`列的矩阵。 任务是检查矩阵`A`是否对角占优。

**示例**：

```
Input : A = { { 3, -2, 1 },
              { 1, -3, 2 },
              { -1, 2, 4 } };
Output : YES
Given matrix is diagonally dominant
because absolute value of every diagonal
element is more than sum of absolute values
of corresponding row.

Input : A = { { -2, 2, 1 },
              { 1, 3, 2 },
              { 1, -2, 0 } };
Output : NO

```



这个想法是对行数从`i = 0`到`n-1`运行一个循环，对于每行，运行`j = 0`到`n-1`的循环，找到非对角元素的总和，即`i != j`。 并检查对角线元素是否大于或等于和。 如果任何一行为`false`，则返回`false`或打印`No`。 否则打印`Yes`。

## C++ 

```cpp

// CPP Program to check whether given matrix 
// is Diagonally Dominant Matrix. 
#include <bits/stdc++.h> 
#define N 3 
using namespace std; 

// check the given given matrix is Diagonally 
// Dominant Matrix or not. 
bool isDDM(int m[N][N], int n) 
{ 
    // for each row 
    for (int i = 0; i < n; i++) 
   {         

        // for each column, finding sum of each row. 
        int sum = 0; 
        for (int j = 0; j < n; j++)              
            sum += abs(m[i][j]);         

        // removing the diagonal element. 
        sum -= abs(m[i][i]); 

        // checking if diagonal element is less  
        // than sum of non-diagonal element. 
        if (abs(m[i][i]) < sum)  
            return false;  

    } 

    return true; 
} 

// Driven Program 
int main() 
{ 
    int n = 3; 
    int m[N][N] = { { 3, -2, 1 }, 
                    { 1, -3, 2 }, 
                    { -1, 2, 4 } }; 

    (isDDM(m, n)) ? (cout << "YES") : (cout << "NO"); 

    return 0; 
} 

```

## Java

```java
// JAVA Program to check whether given matrix 
// is Diagonally Dominant Matrix. 
import java.util.*; 
  
class GFG { 
      
    // check the given given matrix is Diagonally 
    // Dominant Matrix or not. 
    static boolean isDDM(int m[][], int n) 
    { 
        // for each row 
        for (int i = 0; i < n; i++) 
        {         
       
            // for each column, finding  
            //sum of each row. 
            int sum = 0; 
            for (int j = 0; j < n; j++)              
                sum += Math.abs(m[i][j]);         
       
            // removing the diagonal element. 
            sum -= Math.abs(m[i][i]); 
       
            // checking if diagonal element is less  
            // than sum of non-diagonal element. 
            if (Math.abs(m[i][i]) < sum)  
                return false;  
         
        } 
  
        return true; 
    } 
  
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int n = 3; 
        int m[][] = { { 3, -2, 1 }, 
                      { 1, -3, 2 }, 
                      { -1, 2, 4 } }; 
       
        if (isDDM(m, n)) 
             System.out.println("YES") ; 
        else  
            System.out.println("NO"); 
      
    } 
} 
  
// This code is contributed by  Arnav Kr. Mandal.
```

## Python3

```py
# Python Program to check 
# whether given matrix is  
# Diagonally Dominant Matrix. 
  
# check the given given  
# matrix is Diagonally  
# Dominant Matrix or not. 
def isDDM(m, n) : 
  
    # for each row 
    for i in range(0, n) :          
      
        # for each column, finding 
        # sum of each row. 
        sum = 0
        for j in range(0, n) : 
            sum = sum + abs(m[i][j])      
  
        # removing the  
        # diagonal element. 
        sum = sum - abs(m[i][i]) 
  
        # checking if diagonal  
        # element is less than  
        # sum of non-diagonal 
        # element. 
        if (abs(m[i][i]) < sum) : 
            return False
  
    return True
  
# Driver Code 
n = 3
m = [[ 3, -2, 1 ], 
    [ 1, -3, 2 ], 
    [ -1, 2, 4 ]] 
  
if((isDDM(m, n))) : 
    print ("YES") 
else : 
    print ("NO") 
  
# This code is contributed by  
# Manish Shaw(manishshaw1)
```

## C#

```cs
// C# Program to check whether given matrix 
// is Diagonally Dominant Matrix. 
using System; 
  
class GFG { 
      
    // check the given given matrix is Diagonally 
    // Dominant Matrix or not. 
    static bool isDDM(int [,]m, int n) 
    { 
        // for each row 
        for (int i = 0; i < n; i++) 
        {  
      
            // for each column, finding  
            //sum of each row. 
            int sum = 0; 
            for (int j = 0; j < n; j++)          
                sum += Math.Abs(m[i, j]);      
      
            // removing the diagonal element. 
            sum -= Math.Abs(m[i, i]); 
      
            // checking if diagonal element is less  
            // than sum of non-diagonal element. 
            if (Math.Abs(m[i,i]) < sum)  
                return false;  
          
        } 
  
        return true; 
    } 
  
    // Driver program  
    public static void Main()  
    { 
        int n = 3; 
        int [,]m = { { 3, -2, 1 }, 
                    { 1, -3, 2 }, 
                    { -1, 2, 4 } }; 
      
        if (isDDM(m, n)) 
            Console.WriteLine("YES") ; 
        else
            Console.WriteLine("NO"); 
      
    } 
} 
  
// This code is contributed by Vt_m.
```

## PHP

```php
<?php 
// PHP Program to check whether  
// given matrix is Diagonally 
// Dominant Matrix. 
  
// check the given given matrix  
// is Diagonally Dominant Matrix or not. 
function isDDM( $m, $n) 
{ 
    // for each row 
    for ($i = 0; $i < $n; $i++) 
          
    { 
        // for each column, finding 
        // sum of each row. 
        $sum = 0; 
        for ( $j = 0; $j < $n; $j++)              
            $sum += abs($m[$i][$j]);      
  
        // removing the diagonal element. 
        $sum -= abs($m[$i][$i]); 
  
        // checking if diagonal element  
        // is less than sum of non-diagonal 
        // element. 
        if (abs($m[$i][$i]) < $sum)  
            return false;  
    } 
  
    return true; 
} 
  
// Driver Code 
$n = 3; 
$m = array(array( 3, -2, 1 ), 
           array( 1, -3, 2 ), 
           array( -1, 2, 4 )); 
  
if((isDDM($m, $n)))  
echo "YES";  
else
echo"NO"; 
  
// This code is contributed by SanjuTomar 
?>
```

输出：

```
YES
```

