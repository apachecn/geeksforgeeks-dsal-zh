# 查找最大数量为 1 的行

> 原文： [https://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/](https://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/)

给定一个布尔 2D 数组，其中对每一行进行排序。 查找 1s 最多的行。

**示例**：

```
Input matrix
0 1 1 1
0 0 1 1
1 1 1 1  // this row has maximum 1s
0 0 0 0

Output: 2

```



**一种简单的方法**是对矩阵进行逐行遍历，计算每行中 1 的数量，然后将其与最大值进行比较。 最后，返回最大为 1s 的行的索引。 此方法的时间复杂度为`O(m * n)`，其中`m`是矩阵中的行数，`n`是矩阵中的列数。

我们可以做得更好。 由于每一行都已排序，因此我们可以**使用二分搜索**在每一行中计数 1。 我们在每一行中找到 1 的第一个实例的索引。 1 的计数等于列总数减去前 1 的索引。

请参见以下代码，以实现上述方法。

## C++

```cpp
// CPP program to find the row  
// with maximum number of 1s  
#include <bits/stdc++.h> 
using namespace std; 
#define R 4  
#define C 4  
  
// Function to find the index of first index  
// of 1 in a boolean array arr[]  
int first(bool arr[], int low, int high)  
{  
    if(high >= low)  
    {  
        // Get the middle index  
        int mid = low + (high - low)/2;  
      
        // Check if the element at middle index is first 1  
        if ( ( mid == 0 || arr[mid-1] == 0) && arr[mid] == 1)  
            return mid;  
      
        // If the element is 0, recur for right side  
        else if (arr[mid] == 0)  
            return first(arr, (mid + 1), high);  
          
        // If element is not first 1, recur for left side  
        else
            return first(arr, low, (mid -1));  
    }  
    return -1;  
}  
  
// Function that returns index of row  
// with maximum number of 1s.  
int rowWithMax1s(bool mat[R][C])  
{  
    // Initialize max values  
    int max_row_index = 0, max = -1;  
  
    // Traverse for each row and count number of 1s  
    // by finding the index of first 1  
    int i, index;  
    for (i = 0; i < R; i++)  
    {  
        index = first (mat[i], 0, C-1);  
        if (index != -1 && C-index > max)  
        {  
            max = C - index;  
            max_row_index = i;  
        }  
    }  
  
    return max_row_index;  
}  
  
// Driver Code  
int main()  
{  
    bool mat[R][C] = { {0, 0, 0, 1},  
                    {0, 1, 1, 1},  
                    {1, 1, 1, 1},  
                    {0, 0, 0, 0}};  
  
    cout << "Index of row with maximum 1s is " << rowWithMax1s(mat);  
  
    return 0;  
}  
  
// This is code is contributed by rathbhupendra
```

## C

```c
// C program to find the row 
// with maximum number of 1s 
#include <stdio.h> 
#define R 4 
#define C 4 
  
// Function to find the index of first index 
// of 1 in a boolean array arr[]  
int first(bool arr[], int low, int high) 
{ 
if(high >= low) 
{ 
    // Get the middle index  
    int mid = low + (high - low)/2;  
  
    // Check if the element at middle index is first 1 
    if ( ( mid == 0 || arr[mid-1] == 0) && arr[mid] == 1) 
    return mid; 
  
    // If the element is 0, recur for right side 
    else if (arr[mid] == 0) 
    return first(arr, (mid + 1), high); 
      
    // If element is not first 1, recur for left side 
    else 
    return first(arr, low, (mid -1)); 
} 
return -1; 
} 
  
// Function that returns index of row 
// with maximum number of 1s.  
int rowWithMax1s(bool mat[R][C]) 
{ 
    // Initialize max values 
    int max_row_index = 0, max = -1;  
  
    // Traverse for each row and count number of 1s  
    // by finding the index of first 1 
    int i, index; 
    for (i = 0; i < R; i++) 
    { 
    index = first (mat[i], 0, C-1); 
    if (index != -1 && C-index > max) 
    { 
        max = C - index; 
        max_row_index = i; 
    } 
    } 
  
    return max_row_index; 
} 
  
// Driver Code 
int main() 
{ 
    bool mat[R][C] = { {0, 0, 0, 1}, 
                       {0, 1, 1, 1}, 
                       {1, 1, 1, 1}, 
                       {0, 0, 0, 0}}; 
  
    printf("Index of row with maximum 1s is %d "
                                , rowWithMax1s(mat)); 
  
    return 0; 
}
```

## Java

```java
// Java program to find the row 
// with maximum number of 1s 
import java.io.*; 
  
class GFG { 
    static int R = 4, C = 4; 
    // Function to find the index of first index 
    // of 1 in a boolean array arr[]  
    static int first(int arr[], int low, int high) 
    { 
        if (high >= low) { 
            // Get the middle index 
            int mid = low + (high - low) / 2; 
  
            // Check if the element at middle index is first 1 
            if ((mid == 0 || (arr[mid - 1] == 0)) && arr[mid] == 1) 
                return mid; 
  
            // If the element is 0, recur for right side 
            else if (arr[mid] == 0) 
                return first(arr, (mid + 1), high); 
                  
            // If element is not first 1, recur for left side 
            else 
                return first(arr, low, (mid - 1)); 
        } 
        return -1; 
    } 
  
    // Function that returns index of row 
    // with maximum number of 1s. 
    static int rowWithMax1s(int mat[][]) 
    { 
        // Initialize max values 
        int max_row_index = 0, max = -1;  
  
        // Traverse for each row and count number of  
        // 1s by finding the index of first 1 
        int i, index; 
        for (i = 0; i < R; i++) { 
            index = first(mat[i], 0, C - 1); 
            if (index != -1 && C - index > max) { 
                max = C - index; 
                max_row_index = i; 
            } 
        } 
  
        return max_row_index; 
    } 
    // Driver Code 
    public static void main(String[] args) 
    { 
        int mat[][] = { { 0, 0, 0, 1 }, 
                        { 0, 1, 1, 1 }, 
                        { 1, 1, 1, 1 }, 
                        { 0, 0, 0, 0 } }; 
        System.out.println("Index of row with maximum 1s is "
                                            + rowWithMax1s(mat)); 
    } 
} 
  
// This code is contributed by 'Gitanjali'.
```

## Python 3

```
# Python3 program to find the row 
# with maximum number of 1s 
  
# Function to find the index 
# of first index of 1 in a  
# boolean array arr[]  
def first( arr, low, high): 
    if high >= low: 
          
        # Get the middle index  
        mid = low + (high - low)//2
  
        # Check if the element at  
        # middle index is first 1 
        if (mid == 0 or arr[mid - 1] == 0) and arr[mid] == 1: 
            return mid 
  
        # If the element is 0,  
        # recur for right side 
        elif arr[mid] == 0: 
            return first(arr, (mid + 1), high) 
      
        # If element is not first 1,  
        # recur for left side 
        else: 
            return first(arr, low, (mid - 1)) 
    return -1
  
# Function that returns  
# index of row with maximum  
# number of 1s.  
def rowWithMax1s( mat): 
      
    # Initialize max values 
    R = len(mat) 
    C = len(mat[0]) 
    max_row_index = 0
    max = -1
      
    # Traverse for each row and  
    # count number of 1s by finding 
    #  the index of first 1 
    for i in range(0, R): 
        index = first (mat[i], 0, C - 1) 
        if index != -1 and C - index > max: 
            max = C - index 
            max_row_index = i 
  
    return max_row_index 
  
# Driver Code 
mat = [[0, 0, 0, 1], 
       [0, 1, 1, 1], 
       [1, 1, 1, 1], 
       [0, 0, 0, 0]] 
print ("Index of row with maximum 1s is",  
      rowWithMax1s(mat)) 
  
# This code is contributed  
# by shreyanshi_arun
```

## C#

```cs
// C# program to find the row with maximum 
// number of 1s  
using System; 
  
class GFG 
{ 
public static int R = 4, C = 4; 
  
// Function to find the index of first index  
// of 1 in a boolean array arr[]  
public static int first(int[] arr,  
                        int low, int high) 
{ 
    if (high >= low) 
    { 
        // Get the middle index  
        int mid = low + (high - low) / 2; 
  
        // Check if the element at middle  
        // index is first 1  
        if ((mid == 0 || (arr[mid - 1] == 0)) && 
                          arr[mid] == 1) 
        { 
            return mid; 
        } 
  
        // If the element is 0, recur  
        // for right side  
        else if (arr[mid] == 0) 
        { 
            return first(arr, (mid + 1), high); 
        } 
  
        // If element is not first 1, recur 
        // for left side  
        else
        { 
            return first(arr, low, (mid - 1)); 
        } 
    } 
    return -1; 
} 
  
// Function that returns index of row  
// with maximum number of 1s.  
public static int rowWithMax1s(int[][] mat) 
{ 
    // Initialize max values  
    int max_row_index = 0, max = -1; 
  
    // Traverse for each row and count number   
    // of 1s by finding the index of first 1  
    int i, index; 
    for (i = 0; i < R; i++) 
    { 
        index = first(mat[i], 0, C - 1); 
        if (index != -1 && C - index > max) 
        { 
            max = C - index; 
            max_row_index = i; 
        } 
    } 
  
    return max_row_index; 
} 
  
// Driver Code  
public static void Main(string[] args) 
{ 
    int[][] mat = new int[][] 
    { 
        new int[] {0, 0, 0, 1}, 
        new int[] {0, 1, 1, 1}, 
        new int[] {1, 1, 1, 1}, 
        new int[] {0, 0, 0, 0} 
    }; 
    Console.WriteLine("Index of row with maximum 1s is " +  
                                       rowWithMax1s(mat)); 
} 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```php
<?php 
// PHP program to find the row  
// with maximum number of 1s  
define("R", 4); 
define("C", 4);  
  
// Function to find the index of first  
// index of 1 in a boolean array arr[]  
function first($arr, $low, $high)  
{  
    if($high >= $low)  
    {  
        // Get the middle index  
        $mid = $low + intval(($high - $low) / 2);  
      
        // Check if the element at middle  
        // index is first 1  
        if (($mid == 0 || $arr[$mid - 1] == 0) &&  
                          $arr[$mid] == 1)  
        return $mid;  
      
        // If the element is 0, recur for 
        // right side  
        else if ($arr[$mid] == 0)  
        return first($arr, ($mid + 1), $high);  
          
        // If element is not first 1, recur  
        // for left side  
        else
        return first($arr, $low, ($mid - 1));  
    }  
    return -1;  
}  
  
// Function that returns index of row  
// with maximum number of 1s.  
function rowWithMax1s($mat)  
{  
      
    // Initialize max values  
    $max_row_index = 0; 
    $max = -1;  
  
    // Traverse for each row and count number  
    // of 1s by finding the index of first 1  
      
    for ($i = 0; $i < R; $i++)  
    {  
    $index = first ($mat[$i], 0, (C - 1));  
    if ($index != -1 && (C - $index) > $max)  
    {  
        $max = C - $index;  
        $max_row_index = $i;  
    }  
    }  
  
    return $max_row_index;  
}  
  
// Driver Code  
$mat = array(array(0, 0, 0, 1),  
             array(0, 1, 1, 1),  
             array(1, 1, 1, 1),  
             array(0, 0, 0, 0));  
  
echo "Index of row with maximum 1s is " .                
                      rowWithMax1s($mat);  
  
// This code is contributed by rathbhupendra 
?>
```

输出：

```
Index of row with maximum 1s is 2
```

时间复杂度：`O(mLogn)`其中`m`是矩阵中的行数，`n`是矩阵中的列数。

上述解决方案可以进一步优化。 我们首先检查该行是否比最大行数多1，而不是对每一行进行二进制搜索。 如果该行具有更多的 1，则仅在该行中计数 1。 另外，要连续计算 1s，我们不会在整行中进行二进制搜索，而是在最后一个最大值的索引之前进行搜索。

以下是上述解决方案的优化版本。

## C++

```cpp
#include <bits/stdc++.h> 
using namespace std; 
  
// The main function that returns index 
// of row with maximum number of 1s.  
int rowWithMax1s(bool mat[R][C])  
{  
    int i, index;  
  
    // Initialize max using values from first row.  
    int max_row_index = 0;  
    int max = first(mat[0], 0, C - 1);  
  
    // Traverse for each row and count number of 1s  
    // by finding the index of first 1  
    for (i = 1; i < R; i++)  
    {  
        // Count 1s in this row only if this row  
        // has more 1s than max so far  
  
        // Count 1s in this row only if this row  
        // has more 1s than max so far  
        if (max != -1 && mat[i][C - max - 1] == 1)  
        {  
            // Note the optimization here also  
            index = first (mat[i], 0, C - max);  
  
            if (index != -1 && C - index > max)  
            {  
                max = C - index;  
                max_row_index = i;  
            }  
        }  
        else 
        {  
            max = first(mat[i], 0, C - 1);  
        }  
    }  
    return max_row_index;  
}  
  
// This code is contributed by rathbhupendra
```

## C

```c
// The main function that returns index of row with maximum number of 1s. 
int rowWithMax1s(bool mat[R][C]) 
{ 
    int i, index; 
   
    // Initialize max using values from first row.   
    int max_row_index = 0; 
    int max = first(mat[0], 0, C-1); 
   
    // Traverse for each row and count number of 1s by finding the index 
    // of first 1 
    for (i = 1; i < R; i++) 
    { 
        // Count 1s in this row only if this row has more 1s than 
        // max so far 
  
        // Count 1s in this row only if this row has more 1s than 
        // max so far 
        if (max != -1 && mat[i][C-max-1] == 1) 
        { 
            // Note the optimization here also 
            index = first (mat[i], 0, C-max); 
   
            if (index != -1 && C-index > max) 
            { 
                max = C - index; 
                max_row_index = i; 
            }    
        } 
        else { 
            max = first(mat[i], 0, C - 1);  
        }    
    }    
    return max_row_index; 
}
```

上述优化版本的最坏情况下的时间复杂度也是`O(mLogn)`，意志解决方案的平均效果更好。 感谢 Naveen Kumar Singh 建议上述解决方案。

上述解决方案的最坏情况发生在如下矩阵中。

```
0 0 0 … 0 1
0 0 0 ..0 1 1
0 … 0 1 1 1
….0 1 1 1 1
```

在最坏的情况下，以下方法适用于`O(m + n)`时间复杂度。

步骤 1：获取第一行中第一个（或最左边的）1 的索引。

步骤 2：对第一行之后的每一行进行跟踪

…如果前最左 1 左边的元素为 0，则忽略此行。

…否则向左移动，直到找到 0。 将最左边的索引更新为此索引，并将`max_row_index`更新为当前行。

时间复杂度为`O(m + n)`，因为我们可以尽可能快地走到第一步。

以下是此方法的 C++ 实现。

```
// The main function that returns index of row with maximum number of 1s. 
int rowWithMax1s(bool mat[R][C]) 
{ 
    // Initialize first row as row with max 1s 
    int max_row_index = 0; 
  
    // The function first() returns index of first 1 in row 0. 
    // Use this index to initialize the index of leftmost 1 seen so far 
    int j = first(mat[0], 0, C-1); 
    if (j == -1) // if 1 is not present in first row 
      j = C - 1; 
  
    for (int i = 1; i < R; i++) 
    { 
        // Move left until a 0 is found 
        while (j >= 0 && mat[i][j] == 1) 
        { 
           j = j-1;  // Update the index of leftmost 1 seen so far 
           max_row_index = i;  // Update max_row_index 
        } 
    } 
    return max_row_index; 
```

感谢 Tylor，Ankan 和 Palash 的投入。