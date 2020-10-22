# 查找矩阵中每一行的最大元素

> 原文： [https://www.geeksforgeeks.org/find-maximum-element-row-matrix/](https://www.geeksforgeeks.org/find-maximum-element-row-matrix/)

给定一个矩阵，任务是找到每一行的最大元素。

**示例**：

```
Input :  [1, 2, 3]
         [1, 4, 9]
         [76, 34, 21]

Output :
3
9
76

Input : [1, 2, 3, 21]
        [12, 1, 65, 9]
        [1, 56, 34, 2]
Output :
21
65
56

```



**方法**：方法非常简单。 这个想法是为`no_of_rows`运行循环。 检查行内的每个元素，并找到最大元素。 最后，打印元素。

下面是实现：

## C++ 

```cpp

// C++ program to find maximum  
// element of each row in a matrix 
#include<bits/stdc++.h> 
using namespace std; 
const int N = 4;  

    // Print array element 
    void printArray(int result[], int no_of_rows) { 
        for (int i = 0; i < no_of_rows; i++) { 
            cout<< result[i]<<"\n"; 
        } 

    } 

    // Function to get max element 
    void maxelement(int no_of_rows, int arr[][N]) { 
        int i = 0; 

        // Initialize max to 0 at beginning 
        // of finding max element of each row 
        int max = 0; 
        int result[no_of_rows]; 
        while (i < no_of_rows) { 
            for (int j = 0; j < N; j++) { 
                if (arr[i][j] > max) { 
                    max = arr[i][j]; 
                } 
            } 
            result[i] = max; 
            max = 0; 
            i++; 

        } 
        printArray(result,no_of_rows); 

    } 

    // Driver code 
    int main() 
    { 
        int arr[][N] = { {3, 4, 1, 8}, 
                        {1, 4, 9, 11}, 
                        {76, 34, 21, 1}, 
                        {2, 1, 4, 5} }; 
    // Calling the function  
        maxelement(4, arr); 
    } 

// This code is contributed by Rajput-Ji 

```

## Java

```java
// Java program to find maximum  
// element of each row in a matrix 
public class GFG{ 
  
    // Function to get max element 
    public static void maxelement(int no_of_rows, int[][] arr) { 
        int i = 0; 
          
        // Initialize max to 0 at beginning 
        // of finding max element of each row 
        int max = 0; 
        int[] result = new int[no_of_rows]; 
        while (i < no_of_rows) { 
            for (int j = 0; j < arr[i].length; j++) { 
                if (arr[i][j] > max) { 
                    max = arr[i][j]; 
                } 
            } 
            result[i] = max; 
            max =0; 
            i++; 
  
        } 
        printArray(result); 
  
    } 
  
    // Print array element 
    private static void printArray(int[] result) { 
        for (int i =0; i<result.length;i++) { 
            System.out.println(result[i]); 
        } 
  
    } 
  
    // Driver code 
    public static void main(String[] args) { 
        int[][] arr = new int[][] { {3, 4, 1, 8}, 
                                    {1, 4, 9, 11}, 
                                    {76, 34, 21, 1}, 
                                   {2, 1, 4, 5} }; 
       // Calling the function   
        maxelement(4, arr); 
    } 
}
```

## Python

```py
# Python program to find maximum  
# element of each row in a matrix 
  
# importing numpy 
import numpy 
  
# Function to get max element 
def maxelement(arr): 
      
    # get number of rows and columns 
    no_of_rows = len(arr) 
    no_of_column = len(arr[0]) 
      
    for i in range(no_of_rows): 
          
        # Initialize max1 to 0 at beginning 
        # of finding max element of each row 
        max1 = 0
        for j in range(no_of_column): 
            if arr[i][j] > max1 : 
                max1 = arr[i][j] 
                  
        # print maximum element of each row 
        print(max1) 
  
# Driver Code 
arr = [[3, 4, 1, 8], 
       [1, 4, 9, 11], 
       [76, 34, 21, 1], 
       [2, 1, 4, 5]] 
  
# Calling the function         
maxelement(arr)
```

## C#

```cs
// C# program to find maximum  
// element of each row in a matrix  
using System; 
  
class GFG 
{ 
  
// Function to get max element  
public static void maxelement(int no_of_rows,  
                              int[][] arr) 
{ 
    int i = 0; 
  
    // Initialize max to 0 at beginning  
    // of finding max element of each row  
    int max = 0; 
    int[] result = new int[no_of_rows]; 
    while (i < no_of_rows) 
    { 
        for (int j = 0;  
                 j < arr[i].Length; j++) 
        { 
            if (arr[i][j] > max) 
            { 
                max = arr[i][j]; 
            } 
        } 
        result[i] = max; 
        max = 0; 
        i++; 
  
    } 
    printArray(result); 
  
} 
  
// Print array element  
private static void printArray(int[] result) 
{ 
    for (int i = 0; i < result.Length;i++) 
    { 
        Console.WriteLine(result[i]); 
    } 
  
} 
  
// Driver code  
public static void Main(string[] args) 
{ 
    int[][] arr = new int[][] 
    { 
        new int[] {3, 4, 1, 8}, 
        new int[] {1, 4, 9, 11}, 
        new int[] {76, 34, 21, 1}, 
        new int[] {2, 1, 4, 5} 
    }; 
      
    // Calling the function  
    maxelement(4, arr); 
} 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```php
<?php 
// PHP program to find maximum  
// element of each row in a matrix 
$N = 4;  
  
  
// Print array element 
function printArray($result, $no_of_rows)  
{ 
    for ($i = 0; $i < $no_of_rows; $i++) 
    { 
        echo $result[$i]."\n"; 
    } 
  
} 
  
// Function to get max element 
function maxelement($no_of_rows, $arr)  
{ 
    global $N; 
    $i = 0; 
      
    // Initialize max to 0 at beginning 
    // of finding max element of each row 
    $max = 0; 
    $result=array_fill(0,$no_of_rows,0); 
    while ($i < $no_of_rows)  
    { 
        for ($j = 0; $j < $N; $j++)  
        { 
            if ($arr[$i][$j] > $max)  
            { 
                $max = $arr[$i][$j]; 
            } 
        } 
        $result[$i] = $max; 
        $max = 0; 
        $i++; 
  
    } 
    printArray($result,$no_of_rows); 
  
} 
  
// Driver code 
$arr = array(array(3, 4, 1, 8), 
                array(1, 4, 9, 11), 
                array(76, 34, 21, 1), 
                array(2, 1, 4, 5)); 
// Calling the function  
maxelement(4, $arr); 
  
// This code is contributed by mits 
?>
```

输出：

```
8
11
76
5
```

