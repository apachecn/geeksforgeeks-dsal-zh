# 给定`1, 2, 3, ..., k`以 Z 字形打印它们。

> 原文： [https://www.geeksforgeeks.org/given-1s-2s-3s-ks-print-zig-zag-way/](https://www.geeksforgeeks.org/given-1s-2s-3s-ks-print-zig-zag-way/)

给定的行数和列数。 并给定需要打印的数字`1, 2, 3, ..., k`。 以之字形打印它们。

确保`n * m = 1 的个数 + 2 的个数 + 3 + … + k 的个数`。

例子：

```
Input :  2 3
         2 1 2 1
Output : 1 1 2
         4 3 3
Explanation :
Here number of rows are 2 and number of columns are 3
and number of 1's are 2
    number of 2's are 1
    number of 3's are 2
    number of 4's are 1
    -----------
   | 1 | 1 | 2 |
   | 3 | 3 | 4 |
    -----------

Input :  4 3
         2 4 3 1 2
Output : 1 1 2
         2 2 2
         3 3 3
         5 5 4
Explanation :
Here number of rows are 4 and number of columns are 3
and number of 1's are 2
    number of 2's are 4 [Note that 2s are printed in]
    number of 3's are 3 [zig zag manner]
    number of 4's are 1
    number of 5's are 2

```



**方法**：我们制作了一个二维数组，以之字形方式存储所有元素。 我们将遍历数字数组的所有元素，并将第`i`个索引的数组的所有数字插入二维数组，直到其变为零。

## C++

```cpp
// CPP program to print  given number of 1's,  
// 2's, 3's ....k's in  zig-zag way. 
#include <bits/stdc++.h> 
using namespace std; 
  
// function that prints  given number of 1's,  
// 2's, 3's ....k's in zig-zag way. 
void ZigZag(int rows, int columns, int numbers[]) 
{ 
    int k = 0; 
      
    // two-dimensional array to store numbers.  
    int arr[rows][columns]; 
      
    for (int i=0; i<rows; i++) 
    { 
        // for even row. 
        if (i%2==0) 
        { 
            // for each column. 
            for (int j=0; j<columns and  
                    numbers[k]>0; j++) 
            { 
                // storing element. 
                arr[i][j] = k+1; 
  
                // decrement element at  
                // kth index.  
                numbers[k]--; 
                  
                // if array contains zero 
                // then increment index to  
                // make this next index 
                if (numbers[k] == 0) 
                    k++; 
            } 
        } 
          
        // for odd row. 
        else
        { 
            // for each column. 
            for (int j=columns-1; j>=0 and  
                numbers[k]>0; j--) 
            { 
                // storing element. 
                arr[i][j] = k+1; 
                  
                // decrement element  
                // at kth index. 
                numbers[k]--; 
                  
                // if array contains zero then  
                // increment index to make this  
                // next index. 
                if (numbers[k]==0) 
                    k++; 
            } 
        } 
    } 
      
    // printing the stored elements. 
    for (int i=0;i<rows;i++) 
    { 
        for (int j=0;j<columns;j++) 
            cout << arr[i][j] << " "; 
              
        cout << endl; 
    } 
} 
  
// Driver code for above function. 
int main() 
{ 
    int rows = 4; 
    int columns = 5; 
    int Numbers[] = {3, 4, 2, 2, 3, 1, 5}; 
    ZigZag(rows, columns, Numbers);     
    return 0; 
}
```

## Java

```java
// Java program to print given 
// number of 1's, 2's, 3's ....k's  
// in zig-zag way. 
import java.util.*; 
import java.lang.*; 
  
public class GfG{ 
      
    // function that prints given number of 1's,  
    // 2's, 3's ....k's in zig-zag way. 
    public static void ZigZag(int rows,  
                              int columns,  
                              int numbers[]) 
    { 
        int k = 0; 
      
        // two-dimensional array to store numbers.  
        int[][] arr = new int[rows][columns]; 
      
        for (int i=0; i<rows; i++) 
        { 
            // for even row. 
            if (i%2==0) 
            { 
                // for each column. 
                for (int j=0; j<columns && 
                        numbers[k]>0; j++) 
                { 
                    // storing element. 
                    arr[i][j] = k+1; 
  
                    // decrement element at  
                    // kth index.  
                    numbers[k]--; 
                  
                    // if array contains zero 
                    // then increment index to  
                    // make this next index 
                    if (numbers[k] == 0) 
                        k++; 
                } 
            } 
          
            // for odd row. 
            else
            { 
                // for each column. 
                for (int j=columns-1; j>=0 && 
                    numbers[k]>0; j--) 
                { 
                    // storing element. 
                    arr[i][j] = k+1; 
                  
                    // decrement element  
                    // at kth index. 
                    numbers[k]--; 
                  
                    // if array contains zero then  
                    // increment index to make this  
                    // next index. 
                    if (numbers[k]==0) 
                        k++; 
                } 
            } 
        } 
      
        // printing the stored elements. 
        for (int i=0;i<rows;i++) 
        { 
            for (int j=0;j<columns;j++) 
                System.out.print(arr[i][j] + " "); 
              
            System.out.println(); 
        } 
    } 
      
    // Driver function  
    public static void main(String argc[]) 
    { 
        int rows = 4; 
        int columns = 5; 
        int[] Numbers = new int[]{3, 4, 2, 
                                  2, 3, 1, 5}; 
        ZigZag(rows, columns, Numbers);  
    } 
} 
  
/* This code is contributed by Sagar Shukla */
```

## Python 3

```
# Python3 program to print given number of 1's,  
# 2's, 3's ....k's in zig-zag way.  
  
# function that prints given number of 1's,  
# 2's, 3's ....k's in zig-zag way.  
def ZigZag(rows, columns, numbers): 
    k = 0
      
    # two-dimensional array to store numbers. 
    arr = [[0 for i in range(columns)] for j in range(rows)]  
    for i in range(rows): 
          
        # for even row. 
        if (i % 2 == 0): 
              
            # for each column. 
            j = 0
            while j < columns and numbers[k] > 0: 
                  
                # storing element. 
                arr[i][j] = k + 1
                  
                # decrement element at 
                # kth index. 
                numbers[k] -= 1    
                  
                # if array contains zero 
                # then increment index to 
                # make this next index 
                if numbers[k] == 0: 
                    k += 1
                j += 1
        # for odd row. 
        else: 
              
            # for each column. 
            j = columns-1
            while j>=0 and numbers[k]>0: 
                  
                # storing element. 
                arr[i][j] = k+1
                  
                # decrement element 
                # at kth index. 
                numbers[k] -= 1
                  
                # if array contains zero then 
                # increment index to make this 
                # next index. 
                if numbers[k] == 0: 
                    k += 1
                j -= 1
      
    # printing the stored elements.  
    for i in arr: 
        for j in i: 
            print(j, end =" ") 
        print() 
  
# Driver code 
rows = 4;  
columns = 5;  
Numbers = [3, 4, 2, 2, 3, 1, 5]  
ZigZag(rows, columns, Numbers) 
  
# This code is contributed by 
# Rajnis09
```

## C#

```cs
// C# program to print given 
// number of 1's, 2's, 3's ....k's  
// in zig-zag way. 
using System; 
  
public class GfG{ 
      
    // function that prints given number of 1's,  
    // 2's, 3's ....k's in zig-zag way. 
    public static void ZigZag(int rows,  
                            int columns,  
                            int []numbers) 
    { 
        int k = 0; 
      
        // two-dimensional array to store numbers.  
        int[,] arr = new int[rows,columns]; 
      
        for (int i = 0; i < rows; i++) 
        { 
            // for even row. 
            if (i % 2 == 0) 
            { 
                // for each column. 
                for (int j = 0; j < columns && 
                        numbers[k] > 0; j++) 
                { 
                    // storing element. 
                    arr[i,j] = k + 1; 
  
                    // decrement element at  
                // kth index.  
                    numbers[k]--; 
                  
                    // if array contains zero 
                    // then increment index to  
                    // make this next index 
                    if (numbers[k] == 0) 
                        k++; 
                } 
            } 
          
            // for odd row. 
            else
            { 
                // for each column. 
                for (int j = columns - 1; j >= 0 && 
                    numbers[k] > 0; j--) 
                { 
                    // storing element. 
                    arr[i,j] = k + 1; 
                  
                    // decrement element  
                    // at kth index. 
                    numbers[k]--; 
                  
                    // if array contains zero then  
                    // increment index to make this  
                    // next index. 
                    if (numbers[k] == 0) 
                        k++; 
                } 
            } 
        } 
      
        // printing the stored elements. 
        for (int i = 0;i < rows; i++) 
        { 
            for (int j = 0; j < columns; j++) 
            Console.Write(arr[i, j] + " "); 
              
            Console.WriteLine(); 
        } 
    } 
      
    // Driver function  
    public static void Main() 
    { 
        int rows = 4; 
        int columns = 5; 
        int []Numbers = new int[]{3, 4, 2, 
                                2, 3, 1, 5}; 
        ZigZag(rows, columns, Numbers);  
    } 
} 
  
/* This code is contributed by vt_m*/
```

## PHP

```php
<?php 
// PHP program to print given number of 1's,  
// 2's, 3's ....k's in zig-zag way. 
  
// function that prints given number of 1's,  
// 2's, 3's ....k's in zig-zag way. 
function ZigZag($rows, $columns, $numbers) 
{ 
    $k = 0; 
      
    // two-dimensional array  
    // to store numbers.  
    $arr = array(array()); 
      
    for($i = 0; $i < $rows; $i++) 
    { 
          
        // for even row. 
        if ($i % 2==0) 
        { 
              
            // for each column. 
            for($j = 0; $j < $columns and
                  $numbers[$k] > 0; $j++) 
            { 
                  
                // storing element. 
                $arr[$i][$j] = $k + 1; 
  
                // decrement element at  
                // kth index.  
                $numbers[$k]--; 
                  
                // if array contains zero 
                // then increment index to  
                // make this next index 
                if ($numbers[$k] == 0) 
                    $k++; 
            } 
        } 
          
        // for odd row. 
        else
        { 
              
            // for each column. 
            for($j = $columns - 1; $j >= 0 and
                       $numbers[$k] > 0; $j--) 
            { 
                  
                // storing element. 
                $arr[$i][$j] = $k + 1; 
                  
                // decrement element  
                // at kth index. 
                $numbers[$k]--; 
                  
                // if array contains zero then  
                // increment index to make this  
                // next index. 
                if ($numbers[$k]==0) 
                    $k++; 
            } 
        } 
    } 
      
    // printing the stored elements. 
    for($i = 0; $i < $rows;$i++) 
    { 
        for($j = 0; $j < $columns; $j++) 
            echo $arr[$i][$j] , " "; 
              
        echo "\n"; 
    } 
} 
  
    // Driver Code 
    $rows = 4; 
    $columns = 5; 
    $Numbers = array(3, 4, 2, 2, 3, 1, 5); 
    ZigZag($rows, $columns,$Numbers);  
      
// This code is contributed by anuj_67. 
?>
```

输出：

```
1 1 1 2 2 
4 3 3 2 2 
4 5 5 5 6 
7 7 7 7 7
```

