# 创建具有`O`和`X`的交替矩形的矩阵

> 原文： [https://www.geeksforgeeks.org/create-a-matrix-with-alternating-rectangles-of-0-and-x/](https://www.geeksforgeeks.org/create-a-matrix-with-alternating-rectangles-of-0-and-x/)

编写代码，输入两个数字`m`和`n`，并创建一个大小为`mxn`（`m`行和`n`列）的矩阵，其中每个元素均为`X`或`O`。 `x`和`O`必须交替填充，矩阵应具有`x`的最外面的矩形，然后是`O`的矩形，然后是`X`的矩形，依此类推。

**示例**：

```
Input: m = 3, n = 3
Output: Following matrix 
X X X
X 0 X
X X X

Input: m = 4, n = 5
Output: Following matrix
X X X X X
X 0 0 0 X
X 0 0 0 X
X X X X X

Input:  m = 5, n = 5
Output: Following matrix
X X X X X
X 0 0 0 X
X 0 X 0 X
X 0 0 0 X
X X X X X

Input:  m = 6, n = 7
Output: Following matrix
X X X X X X X
X 0 0 0 0 0 X
X 0 X X X 0 X
X 0 X X X 0 X
X 0 0 0 0 0 X
X X X X X X X 
```

**我们强烈建议最小化浏览器，然后自己尝试。**

在 Shreepartners Gurgaon 的校园招聘中提出了这个问题。 我遵循以下方法。

1.  使用代码[以螺旋形式](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)打印矩阵。

2.  而不是打印数组，而是在数组中插入元素`X`或`O`。

以下是上述方法的实现。

## C++

```
#include <stdio.h> 
  
// Function to print alternating rectangles of 0 and X 
void fill0X(int m, int n) 
{ 
    /*  k - starting row index 
        m - ending row index 
        l - starting column index 
        n - ending column index 
        i - iterator    */
    int i, k = 0, l = 0; 
  
    // Store given number of rows and columns for later use 
    int r = m, c = n; 
  
    // A 2D array to store the output to be printed 
    char a[m][n]; 
    char x = 'X'; // Iniitialize the character to be stoed in a[][] 
  
    // Fill characters in a[][] in spiral form. Every iteration fills 
    // one rectangle of either Xs or Os 
    while (k < m && l < n) 
    { 
        /* Fill the first row from the remaining rows */
        for (i = l; i < n; ++i) 
            a[k][i] = x; 
        k++; 
  
        /* Fill the last column from the remaining columns */
        for (i = k; i < m; ++i) 
            a[i][n-1] = x; 
        n--; 
  
        /* Fill the last row from the remaining rows */
        if (k < m) 
        { 
            for (i = n-1; i >= l; --i) 
                a[m-1][i] = x; 
            m--; 
        } 
  
        /* Print the first column from the remaining columns */
        if (l < n) 
        { 
            for (i = m-1; i >= k; --i) 
                a[i][l] = x; 
            l++; 
        } 
  
        // Flip character for next iteration 
        x = (x == '0')? 'X': '0'; 
    } 
  
    // Print the filled matrix 
    for (i = 0; i < r; i++) 
    { 
        for (int j = 0; j < c; j++) 
            printf("%c ", a[i][j]); 
        printf("\n"); 
    } 
} 
  
/* Driver program to test above functions */
int main() 
{ 
    puts("Output for m = 5, n = 6"); 
    fill0X(5, 6); 
  
    puts("\nOutput for m = 4, n = 4"); 
    fill0X(4, 4); 
  
    puts("\nOutput for m = 3, n = 4"); 
    fill0X(3, 4); 
  
    return 0; 
}
```

## Java

```
// Java code to demonstrate the working. 
  
import java.io.*; 
  
class GFG { 
  
// Function to print alternating 
// rectangles of 0 and X 
 static void fill0X(int m, int n) 
{ 
    /* k - starting row index 
        m - ending row index 
        l - starting column index 
        n - ending column index 
        i - iterator */
    int i, k = 0, l = 0; 
  
    // Store given number of rows 
        // and columns for later use 
    int r = m, c = n; 
  
    // A 2D array to store 
        // the output to be printed 
    char a[][] = new char[m][n]; 
  
        // Iniitialize the character 
        // to be stoed in a[][] 
    char x = 'X';  
  
    // Fill characters in a[][] in spiral 
        // form. Every iteration fills 
    // one rectangle of either Xs or Os 
    while (k < m && l < n) 
    { 
        /* Fill the first row from the remaining rows */
        for (i = l; i < n; ++i) 
            a[k][i] = x; 
        k++; 
  
        /* Fill the last column from the remaining columns */
        for (i = k; i < m; ++i) 
            a[i][n-1] = x; 
        n--; 
  
        /* Fill the last row from the remaining rows */
        if (k < m) 
        { 
            for (i = n-1; i >= l; --i) 
                a[m-1][i] = x; 
            m--; 
        } 
  
        /* Print the first column 
                // from the remaining columns */
        if (l < n) 
        { 
            for (i = m-1; i >= k; --i) 
                a[i][l] = x; 
            l++; 
        } 
  
        // Flip character for next iteration 
        x = (x == '0')? 'X': '0'; 
    } 
  
    // Print the filled matrix 
    for (i = 0; i < r; i++) 
    { 
        for (int j = 0; j < c; j++) 
            System.out.print(a[i][j] + " "); 
        System.out.println(); 
    } 
} 
  
/* Driver program to test above functions */
public static void main (String[] args) { 
  
    System.out.println("Output for m = 5, n = 6"); 
    fill0X(5, 6); 
  
    System.out.println("Output for m = 4, n = 4"); 
    fill0X(4, 4); 
  
    System.out.println("Output for m = 3, n = 4"); 
    fill0X(3, 4); 
          
    } 
} 
  
// This code  is contributed by vt_m
```

## Python3

```
# Python3 program to Create a matrix with 
# alternating rectangles of O and X 
  
# Function to pralternating rectangles  
# of 0 and X  
def fill0X(m, n): 
      
    # k - starting row index  
    # m - ending row index  
    # l - starting column index  
    # n - ending column index  
    # i - iterator  
    i, k, l = 0, 0, 0
  
    # Store given number of rows and  
    # columns for later use  
    r = m 
    c = n  
  
    # A 2D array to store the output  
    # to be printed  
    a = [[None] * n for i in range(m)]  
    x = 'X' # Iniitialize the character to 
            # be stoed in a[][]  
  
    # Fill characters in a[][] in spiral form.  
    # Every iteration fills one rectangle of  
    # either Xs or Os  
    while k < m and l < n: 
          
        # Fill the first row from the  
        # remaining rows 
        for i in range(l, n): 
            a[k][i] = x  
        k += 1
  
        # Fill the last column from  
        # the remaining columns 
        for i in range(k, m): 
            a[i][n - 1] = x  
        n -= 1
  
        # Fill the last row from the  
        # remaining rows  
        if k < m: 
            for i in range(n - 1, l - 1, -1): 
                a[m - 1][i] = x  
            m -= 1
  
        # Print the first column from  
        # the remaining columns  
        if l < n: 
            for i in range(m - 1, k - 1, -1): 
                a[i][l] = x  
            l += 1
  
        # Flip character for next iteration 
        x = 'X' if x == '0' else '0'
  
    # Print the filled matrix  
    for i in range(r): 
        for j in range(c): 
            print(a[i][j], end = " ") 
        print() 
  
# Driver Code 
if __name__ == '__main__': 
      
    print("Output for m = 5, n = 6")  
    fill0X(5, 6)  
  
    print("Output for m = 4, n = 4")  
    fill0X(4, 4)  
  
    print("Output for m = 3, n = 4")  
    fill0X(3, 4) 
      
# This code is contributed by pranchalK
```

## C#

```
// C# code to demonstrate the working. 
using System; 
  
class GFG { 
  
    // Function to print alternating 
    // rectangles of 0 and X 
    static void fill0X(int m, int n) 
    { 
          
        /* k - starting row index 
        m - ending row index 
        l - starting column index 
        n - ending column index 
        i - iterator */
        int i, k = 0, l = 0; 
      
        // Store given number of rows 
        // and columns for later use 
        int r = m, c = n; 
      
        // A 2D array to store 
        // the output to be printed 
        char [,]a = new char[m,n]; 
      
        // Iniitialize the character 
        // to be stoed in a[][] 
        char x = 'X';  
      
        // Fill characters in a[][] in spiral 
        // form. Every iteration fills 
        // one rectangle of either Xs or Os 
        while (k < m && l < n) 
        { 
              
            /* Fill the first row from the 
            remaining rows */
            for (i = l; i < n; ++i) 
                a[k,i] = x; 
            k++; 
      
            /* Fill the last column from the 
            remaining columns */
            for (i = k; i < m; ++i) 
                a[i,n-1] = x; 
            n--; 
      
            /* Fill the last row from the 
            remaining rows */
            if (k < m) 
            { 
                for (i = n-1; i >= l; --i) 
                    a[m-1,i] = x; 
                m--; 
            } 
      
            /* Print the first column 
            from the remaining columns */
            if (l < n) 
            { 
                for (i = m-1; i >= k; --i) 
                    a[i,l] = x; 
                l++; 
            } 
      
            // Flip character for next 
            // iteration 
            x = (x == '0')? 'X': '0'; 
        } 
      
        // Print the filled matrix 
        for (i = 0; i < r; i++) 
        { 
            for (int j = 0; j < c; j++) 
                Console.Write(a[i,j] + " "); 
            Console.WriteLine(); 
        } 
    } 
      
    /* Driver program to test  
    above functions */
    public static void Main () 
    { 
        Console.WriteLine("Output for"
                    + " m = 5, n = 6"); 
        fill0X(5, 6); 
      
        Console.WriteLine("Output for"
                    + " m = 4, n = 4"); 
        fill0X(4, 4); 
      
        Console.WriteLine("Output for"
                    + " m = 3, n = 4"); 
        fill0X(3, 4); 
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```
<?php 
// PHP program to Create a matrix with 
// alternating rectangles of O and X 
  
// Function to print alternating 
// rectangles of 0 and X 
function fill0X($m, $n) 
{ 
      
    /* k - starting row index 
        m - ending row index 
        l - starting column index 
        n - ending column index 
        i - iterator */
    $k = 0; 
    $l = 0; 
  
    // Store given number of rows  
    // and columns for later use 
    $r = $m;  
    $c = $n; 
  
    // A 2D array to store the  
    // output to be printed 
    // Iniitialize the character 
    // to be stoed in a[][] 
    $x = 'X';  
  
    // Fill characters in a[][] in  
    // spiral form. Every iteration fills 
    // one rectangle of either Xs or Os 
    while ($k < $m && $l < $n) 
    { 
          
        /* Fill the first row from  
           the remaining rows */
        for ($i = $l; $i < $n; ++$i) 
            $a[$k][$i] = $x; 
        $k++; 
  
        /* Fill the last column from 
           the remaining columns */
        for ($i = $k; $i < $m; ++$i) 
            $a[$i][$n - 1] = $x; 
        $n--; 
  
        /* Fill the last row from  
           the remaining rows */
        if ($k < $m) 
        { 
            for ($i = $n - 1; $i >= $l; --$i) 
                $a[$m - 1][$i] = $x; 
            $m--; 
        } 
  
        /* Print the first column from 
           the remaining columns */
        if ($l < $n) 
        { 
            for ($i = $m - 1; $i >= $k; --$i) 
                $a[$i][$l] = $x; 
            $l++; 
        } 
  
        // Flip character for 
        // next iteration 
        $x = ($x == '0')? 'X': '0'; 
    } 
  
    // Print the filled matrix 
    for ($i = 0; $i < $r; $i++) 
    { 
        for ($j = 0; $j < $c; $j++) 
            echo($a[$i][$j]." "); 
        echo "\n"; 
    } 
} 
  
// Driver Code 
echo "Output for m = 5, n = 6\n"; 
fill0X(5, 6); 
  
echo "\nOutput for m = 4, n = 4\n"; 
fill0X(4, 4); 
  
echo "\nOutput for m = 3, n = 4\n"; 
fill0X(3, 4); 
  
// This code is contributed by ChitraNayal. 
?>
```

输出：

```
Output for m = 5, n = 6
X X X X X X
X 0 0 0 0 X
X 0 X X 0 X
X 0 0 0 0 X
X X X X X X

Output for m = 4, n = 4
X X X X
X 0 0 X
X 0 0 X
X X X X

Output for m = 3, n = 4
X X X X
X 0 0 X
X X X X 
```

时间复杂度：`O(mn)`。

辅助空间：`O(mn)`。

请建议是否有人在空间和时间方面有更好的解决方案，并且效率更高。