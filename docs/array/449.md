# 形成矩阵线圈

> 原文： [https://www.geeksforgeeks.org/form-coils-matrix/](https://www.geeksforgeeks.org/form-coils-matrix/)

给定一个正整数`n`，该整数表示`4n x 4n`矩阵的维，值从 1 到`n`从左到右，从上到下填充。 从矩阵形成两个线圈，然后打印线圈。

例子：

```
Input  : n = 1;
Output : Coil 1 : 10 6 2 3 4 8 12 16 
         Coil 2 : 7 11 15 14 13 9 5 1
Explanation : Matrix is 
1  2  3  4 
5  6  7  8 
9  10 11 12 
13 14 15 16

Input  : n = 2;
Output : Coil 1 : 36 28 20 21 22 30 38 46 54 
                  53 52 51 50 42 34 26 18 10 
                  2 3 4 5 6 7 8 16 24 32 40 
                  48 56 64 
        Coil 2 : 29 37 45 44 43 35 27 19 11 12 
                 13 14 15 23 31 39 47 55 63 62 
                 61 60 59 58 57 49 41 33 25 17
                 9 1 

```



矩阵中的元素总数为`16n ^ 2`。 所有元件均分为两个线圈。 每个线圈具有`8n ^ 2`个元素。 我们制作两个这样大小的数组。 我们首先以给定的顺序遍历来填充线圈 1 中的元素。 一旦我们在线圈 1 中填充了元素，就可以使用公式`coil2[i] = 16 * n * n + 1 - coil1[i]`获得其他线圈 2 的元素。

## C++ 

```cpp

// C++ program to print 2 coils of a 
// 4n x 4n matrix. 
#include<iostream> 
using namespace std; 

// Print coils in a matrix of size 4n x 4n  
void printCoils(int n) 
{ 
    // Number of elements in each coil 
    int m = 8*n*n; 

    // Let us fill elements in coil 1\. 
    int coil1[m]; 

    // First element of coil1 
    // 4*n*2*n + 2*n; 
    coil1[0] = 8*n*n + 2*n; 
    int curr = coil1[0]; 

    int nflg = 1, step = 2; 

    // Fill remaining m-1 elements in coil1[] 
    int index = 1; 
    while (index < m) 
    { 
        // Fill elements of current step from 
        // down to up 
        for (int i=0; i<step; i++) 
        { 
            // Next element from current element 
            curr = coil1[index++] = (curr - 4*n*nflg); 
            if (index >= m) 
                break; 
        } 
        if (index >= m) 
            break; 

        // Fill elements of current step from 
        // up to down. 
        for (int i=0; i<step; i++) 
        { 
            curr = coil1[index++] = curr + nflg; 
            if (index >= m) 
                break; 
        } 
        nflg = nflg*(-1); 
        step += 2; 
    } 

    /* get coil2 from coil1 */
    int coil2[m]; 
    for (int i=0; i<8*n*n; i++) 
        coil2[i] = 16*n*n + 1 -coil1[i]; 

    // Print both coils 
    cout << "Coil 1 : "; 
    for(int i=0; i<8*n*n; i++) 
        cout << coil1[i] << " "; 
    cout << "\nCoil 2 : "; 
    for (int i=0; i<8*n*n; i++) 
        cout << coil2[i] << " "; 
} 

// Driver code 
int main() 
{ 
    int n = 1; 
    printCoils(n); 
    return 0; 
} 

```

## Java

```java

// Java program to print 2 coils  
// of a 4n x 4n matrix. 

class GFG { 

    // Print coils in a matrix of size 4n x 4n 
    static void printCoils(int n)  
    { 
        // Number of elements in each coil 
        int m = 8 * n * n; 

        // Let us fill elements in coil 1\. 
        int coil1[] = new int[m]; 

        // First element of coil1 
        // 4*n*2*n + 2*n; 
        coil1[0] = 8 * n * n + 2 * n; 
        int curr = coil1[0]; 

        int nflg = 1, step = 2; 

        // Fill remaining m-1 elements in coil1[] 
        int index = 1; 
        while (index < m) 
        { 
            // Fill elements of current step from 
            // down to up 
            for (int i = 0; i < step; i++)  
                { 
                    // Next element from current element 
                    curr = coil1[index++] = (curr - 4 * n * nflg); 
                    if (index >= m) 
                    break; 
                } 
            if (index >= m) 
                break; 

            // Fill elements of current step from 
            // up to down. 
            for (int i = 0; i < step; i++)  
            { 
                curr = coil1[index++] = curr + nflg; 
                if (index >= m) 
                break; 
            } 

            nflg = nflg * (-1); 
            step += 2; 
        } 

        /* get coil2 from coil1 */
        int coil2[] = new int[m]; 
        for (int i = 0; i < 8 * n * n; i++) 
            coil2[i] = 16 * n * n + 1 - coil1[i]; 

        // Print both coils 
        System.out.print("Coil 1 : "); 

        for (int i = 0; i < 8 * n * n; i++) 
            System.out.print(coil1[i] + " "); 

        System.out.print("\nCoil 2 : "); 

        for (int i = 0; i < 8 * n * n; i++) 
            System.out.print(coil2[i] + " "); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int n = 1; 
        printCoils(n); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to pr2 coils of a 
# 4n x 4n matrix. 

# Prcoils in a matrix of size 4n x 4n  
def printCoils(n): 

    # Number of elements in each coil 
    m = 8*n*n 

    # Let us fill elements in coil 1\. 
    coil1 = [0]*m 

    # First element of coil1 
    # 4*n*2*n + 2*n 
    coil1[0] = 8*n*n + 2*n 

    curr = coil1[0] 

    nflg = 1
    step = 2

    # Fill remaining m-1 elements in coil1[] 
    index = 1
    while (index < m): 

        # Fill elements of current step from 
        # down to up 
        for i in range(step): 

            # Next element from current element 
            curr = coil1[index] = (curr - 4*n*nflg) 
            index += 1
            if (index >= m): 
                break
        if (index >= m): 
            break

        # Fill elements of current step from 
        # up to down. 
        for i in range(step): 

            curr = coil1[index] = curr + nflg 
            index += 1
            if (index >= m): 
                break
        nflg = nflg*(-1) 
        step += 2

    #get coil2 from coil1 */ 

    coil2 = [0]*m 
    i = 0
    while(i < 8*n*n): 
        coil2[i] = 16*n*n + 1 -coil1[i] 
        i += 1
    # Prboth coils 
    print("Coil 1 :", end = " ") 
    i = 0
    while(i < 8*n*n): 
        print(coil1[i], end = " ") 
        i += 1
    print("\nCoil 2 :", end = " ") 
    i = 0
    while(i < 8*n*n): 
        print(coil2[i], end = " ") 
        i += 1

# Driver code 

n = 1
printCoils(n) 

# This code is contributed by shubhamsingh10 

```

## C# 

```cs

// C# program to print 2 coils  
// of a 4n x 4n matrix. 
using System; 

class GFG { 

    // Print coils in a matrix of 
    // size 4n x 4n 
    static void printCoils(int n)  
    { 

        // Number of elements in 
        // each coil 
        int m = 8 * n * n; 

        // Let us fill elements in 
        // coil 1\. 
        int [] coil1 = new int[m]; 

        // First element of coil1 
        // 4*n*2*n + 2*n; 
        coil1[0] = 8 * n * n + 2 * n; 
        int curr = coil1[0]; 

        int nflg = 1, step = 2; 

        // Fill remaining m-1 elements 
        // in coil1[] 
        int index = 1; 
        while (index < m) 
        { 

            // Fill elements of current 
            // step from down to up 
            for (int i = 0; i < step; i++)  
                { 
                    // Next element from  
                    // current element 
                    curr = coil1[index++]  
                    = (curr - 4 * n * nflg); 

                    if (index >= m) 
                        break; 
                } 

            if (index >= m) 
                break; 

            // Fill elements of current step 
            // from up to down. 
            for (int i = 0; i < step; i++)  
            { 
                curr = coil1[index++] = curr  
                                     + nflg; 
                if (index >= m) 
                    break; 
            } 

            nflg = nflg * (-1); 
            step += 2; 
        } 

        /* get coil2 from coil1 */
        int [] coil2 = new int[m]; 

        for (int i = 0; i < 8 * n * n; i++) 
            coil2[i] = 16 * n * n + 1 - coil1[i]; 

        // Print both coils 
        Console.Write("Coil 1 : "); 

        for (int i = 0; i < 8 * n * n; i++) 
            Console.Write(coil1[i] + " "); 

        Console.Write("\nCoil 2 : "); 

        for (int i = 0; i < 8 * n * n; i++) 
            Console.Write(coil2[i] + " "); 
    } 

    // Driver code 
    public static void Main() 
    { 
        int n = 1; 

        printCoils(n); 
    } 
} 

// This code is contributed by KRV. 

```

## PHP

```php

<?php 
// PHP program to print 2 coils of a 
// 4n x 4n matrix. 

// Print coils in a matrix of size 4n x 4n  
function printCoils( $n) 
{ 

    // Number of elements in each coil 
    $m = 8 * $n * $n; 

    // Let us fill elements in coil 1\. 
    $coil1 = array(); 

    // First element of coil1 
    // 4*n*2*n + 2*n; 
    $coil1[0] = 8 * $n * $n + 2 * $n; 
    $curr = $coil1[0]; 

    $nflg = 1; $step = 2; 

    // Fill remaining m-1 elements in coil1[] 
    $index = 1; 
    while ($index < $m) 
    { 
        // Fill elements of current step from 
        // down to up 
        for ( $i = 0; $i < $step; $i++) 
        { 
            // Next element from current element 
            $curr = $coil1[$index++] =  
                     ($curr - 4*$n*$nflg); 
            if ($index >= $m) 
                break; 
        } 
        if ($index >= $m) 
            break; 

        // Fill elements of current step from 
        // up to down. 
        for ( $i=0; $i<$step; $i++) 
        { 
            $curr = $coil1[$index++] =  
                            $curr + $nflg; 
            if ($index >= $m) 
                break; 
        } 
        $nflg = $nflg * (-1); 
        $step += 2; 
    } 

    /* get coil2 from coil1 */
    $coil2 = array(); 

    for ( $i = 0; $i < 8 * $n * $n; $i++) 
        $coil2[$i] = 16 * $n * $n + 1 -$coil1[$i]; 

    // Print both coils 
    echo "Coil 1 : "; 
    for( $i = 0; $i < 8 * $n * $n; $i++) 
    echo $coil1[$i] , " "; 

    echo "\nCoil 2 : "; 
    for ( $i = 0; $i < 8 * $n * $n; $i++) 
        echo $coil2[$i] , " "; 
} 

// Driver code 
$n = 1; 
printCoils($n); 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
Coil 1 : 10 6 2 3 4 8 12 16 
Coil 2 : 7 11 15 14 13 9 5 1 

```

在 **Yahoo** 中询问。

