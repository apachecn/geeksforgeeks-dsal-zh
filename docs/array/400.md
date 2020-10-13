# 矩阵中偶数和奇数的频率

> 原文： [https://www.geeksforgeeks.org/find-frequency-even-odd-numbers-matrix/](https://www.geeksforgeeks.org/find-frequency-even-odd-numbers-matrix/)

给定一个阶数为`m * n`的矩阵，则任务是在矩阵中查找偶数和奇数的频率。示例：

```
Input : m = 3, n = 3
        { 1, 2, 3 }, 
        { 4, 5, 6 }, 
        { 7, 8, 9 }
Output : Frequency of odd number =  5 
         Frequency of even number = 4

Input :   m = 3, n = 3
         { 10, 11, 12 },
         { 13, 14, 15 },
         { 16, 17, 18 }
Output : Frequency of odd number  =  4 
         Frequency of even number  = 5

```



## CPP

```

// C++ Program to Find the frequency 
// of even and odd numbers in a matrix 
#include<bits/stdc++.h> 
using namespace std; 

#define MAX 100 

// function for calculating frequency 
void freq(int ar[][MAX], int m, int n) 
{ 
    int even = 0, odd = 0; 

    for (int i = 0; i < m; ++i) 
    { 
        for (int j = 0; j < n; ++j) 
        { 
            // modulo by 2 to check 
            // even and odd 
            if ((ar[i][j] % 2) == 0) 
                ++even; 
            else
                ++odd; 
        } 
    } 

    // print Frequency of numbers 
    printf(" Frequency of odd number = %d \n", odd); 
    printf(" Frequency of even number = %d \n", even); 
} 

// Driver code 
int main() 
{ 
    int m = 3, n = 3;     

    int array[][MAX] = { { 1, 2, 3 }, 
                        { 4, 5, 6 }, 
                        { 7, 8, 9 } }; 

    freq(array, m, n); 
    return 0; 
}         

```

## Java

```java

// Java Program to Find the frequency 
// of even and odd numbers in a matrix 

class GFG { 
static final int MAX = 100; 

// function for calculating frequency 
static void freq(int ar[][], int m, int n) { 
    int even = 0, odd = 0; 

    for (int i = 0; i < m; ++i)  
    { 
        for (int j = 0; j < n; ++j) 
        { 
            // modulo by 2 to check 
            // even and odd 
            if ((ar[i][j] % 2) == 0) 
                ++even; 
            else
                ++odd; 
    } 
    } 

    // print Frequency of numbers 
    System.out.print(" Frequency of odd number =" + 
                       odd + " \n"); 
    System.out.print(" Frequency of even number = " + 
                       even + " \n"); 
} 

// Driver code 
public static void main(String[] args) { 
    int m = 3, n = 3; 

    int array[][] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}; 

    freq(array, m, n); 
} 
} 
// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python Program to Find the frequency 
# of even and odd numbers in a matrix 

MAX=100

# Function for calculating frequency 
def freq(ar, m, n): 
    even = 0
    odd = 0

    for i in range(m): 
        for j in range(n): 

            # modulo by 2 to check 
            # even and odd 
            if ((ar[i][j] % 2) == 0): 
                even += 1
            else: 
                odd += 1

    # print Frequency of numbers 
    print(" Frequency of odd number =", odd) 
    print(" Frequency of even number =", even) 

# Driver code 
m = 3
n = 3    

array = [ [ 1, 2, 3 ], 
        [ 4, 5, 6 ], 
        [ 7, 8, 9 ] ] 

freq(array, m, n) 

# This code is contributed 
# by Anant Agarwal. 

```

## C# 

```cs

// C# Program to Find the frequency 
// of even and odd numbers in a matrix 
using System; 

class GFG  
{ 
    //static int MAX = 100; 

    // function for calculating frequency 
    static void freq(int [,]ar, int m, int n)  
    { 
        int even = 0, odd = 0; 

        for (int i = 0; i < m; ++i)  
        { 
            for (int j = 0; j < n; ++j) 
            { 
                // modulo by 2 to check 
                // even and odd 
                if ((ar[i, j] % 2) == 0) 
                    ++even; 
                else
                    ++odd; 
        } 
        } 

        // print Frequency of numbers 
        Console.WriteLine(" Frequency of odd number =" + 
                        odd ); 
        Console.WriteLine(" Frequency of even number = " + 
                        even ); 
    } 

    // Driver code 
    public static void Main()  
    { 
        int m = 3, n = 3; 

        int [,]array = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}; 

        freq(array, m, n); 
    } 
} 
// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP Program to Find the frequency 
// of even and odd numbers in a matrix 
$MAX = 100; 

// function for calculating frequency 
function freq($ar, $m, $n) 
{ 
    $even = 0; $odd = 0; 

    for($i = 0; $i < $m; ++$i) 
    { 
        for ( $j = 0; $j < $n; ++$j) 
        { 
            // modulo by 2 to check 
            // even and odd 
            if (($ar[$i][$j] % 2) == 0) 
                ++$even; 
            else
                ++$odd; 
        } 
    } 

    // print Frequency of numbers 
    echo " Frequency of odd number = "
                           , $odd,"\n"; 
    echo " Frequency of even number = "
                               , $even; 
} 

    // Driver code 
    $m = 3; $n = 3;  
    $array = array(array(1, 2, 3), 
                   array(4, 5, 6), 
                   array(7, 8, 9)); 
    freq($array, $m, $n); 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
 Frequency of odd number = 5  
 Frequency of even number = 4

```



* * *

* * *



