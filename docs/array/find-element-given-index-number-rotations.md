# 旋转几次后，在给定索引处查找元素

> 原文： [https://www.geeksforgeeks.org/find-element-given-index-number-rotations/](https://www.geeksforgeeks.org/find-element-given-index-number-rotations/)

给出了一个由`n`个整数组成的数组。 我们执行范围为`[L..R]`的[右旋转](https://www.geeksforgeeks.org/array-rotation/)。 完成这些旋转之后，我们需要在给定索引处找到元素。

**示例**：

```
Input : arr[] : {1, 2, 3, 4, 5}
        ranges[] = { {0, 2}, {0, 3} }
        index : 1
Output : 3
Explanation : After first given rotation {0, 2}
                arr[] = {3, 1, 2, 4, 5}
              After second rotation {0, 3} 
                arr[] = {4, 3, 1, 2, 5}
After all rotations we have element 3 at given
index 1\. 

```



**方法（暴力）**：暴力方法是针对所有给定范围实际[旋转数组](https://www.geeksforgeeks.org/array-rotation/)，最后返回修改后数组中给定索引处的元素。

**方法（高效）**：保存所有范围后，我们可以进行离线处理。

假设我们的旋转范围是：`[0..2]`和`[0..3]`。

我们从反向开始遍历这些范围。

在范围`[0..3]`之后，索引 0 将具有位于索引 3 上的元素。

在范围`[0..2]`之后，索引 3 将保持不变。

因此，我们可以得出 3 种情况：如果`index = left`，索引将变为`right`。如果索引不受范围限制，则没有旋转效果。如果`index`处于范围内，则`index`的元素将位于`index-1`处。

下面是实现：

## C++ 

```cpp

// CPP code to rotate an array 
// and answer the index query 
#include <bits/stdc++.h> 
using namespace std; 

// Function to compute the element at 
// given index 
int findElement(int arr[], int ranges[][2], 
               int rotations, int index) 
{ 
    for (int i = rotations - 1; i >= 0; i--) { 

        // Range[left...right] 
        int left = ranges[i][0]; 
        int right = ranges[i][1]; 

        // Rotation will not have any effect 
        if (left <= index && right >= index) { 
            if (index == left) 
                index = right; 
            else
                index--; 
        } 
    } 

    // Returning new element 
    return arr[index]; 
} 

// Driver 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 

    // No. of rotations 
    int rotations = 2; 

    // Ranges according to 0-based indexing 
    int ranges[rotations][2] = { { 0, 2 }, { 0, 3 } }; 

    int index = 1; 

    cout << findElement(arr, ranges, rotations, index); 

    return 0; 

} 

```

## Java

```java
// Java code to rotate an array 
// and answer the index query 
import java.util.*; 
  
class GFG 
{ 
    // Function to compute the element at 
    // given index 
    static int findElement(int[] arr, int[][] ranges, 
                            int rotations, int index) 
    { 
        for (int i = rotations - 1; i >= 0; i--) { 
  
            // Range[left...right] 
            int left = ranges[i][0]; 
            int right = ranges[i][1]; 
  
            // Rotation will not have any effect 
            if (left <= index && right >= index) { 
                if (index == left) 
                    index = right; 
                else
                    index--; 
            } 
        } 
  
        // Returning new element 
        return arr[index]; 
    } 
  
    // Driver 
    public static void main (String[] args) { 
        int[] arr = { 1, 2, 3, 4, 5 }; 
  
        // No. of rotations 
        int rotations = 2; 
      
        // Ranges according to 0-based indexing 
        int[][] ranges = { { 0, 2 }, { 0, 3 } }; 
  
        int index = 1; 
        System.out.println(findElement(arr, ranges, 
                                 rotations, index)); 
    } 
} 
  
/* This code is contributed by Mr. Somesh Awasthi */
```

## Python3

```py
# Python 3 code to rotate an array 
# and answer the index query 
  
# Function to compute the element  
# at given index 
def findElement(arr, ranges, rotations, index) : 
      
    for i in range(rotations - 1, -1, -1 ) : 
      
        # Range[left...right] 
        left = ranges[i][0] 
        right = ranges[i][1] 
  
        # Rotation will not have  
        # any effect 
        if (left <= index and right >= index) : 
            if (index == left) : 
                index = right 
            else : 
                index = index - 1
          
    # Returning new element 
    return arr[index] 
  
# Driver Code 
arr = [ 1, 2, 3, 4, 5 ] 
  
# No. of rotations 
rotations = 2
  
# Ranges according to  
# 0-based indexing 
ranges = [ [ 0, 2 ], [ 0, 3 ] ] 
  
index = 1
  
print(findElement(arr, ranges, rotations, index)) 
      
# This code is contributed by Nikita Tiwari. 
```

## C#

```cs
// C# code to rotate an array 
// and answer the index query 
using System; 
  
class GFG 
{ 
    // Function to compute the  
    // element at given index 
    static int findElement(int []arr, int [,]ranges, 
                           int rotations, int index) 
    { 
        for (int i = rotations - 1; i >= 0; i--)  
        { 
  
            // Range[left...right] 
            int left = ranges[i, 0]; 
            int right = ranges[i, 1]; 
  
            // Rotation will not  
            // have any effect 
            if (left <= index &&  
                right >= index) 
            { 
                if (index == left) 
                    index = right; 
                else
                    index--; 
            } 
        } 
  
        // Returning new element 
        return arr[index]; 
    } 
  
    // Driver Code 
    public static void Main ()  
    { 
        int []arr = { 1, 2, 3, 4, 5 }; 
  
        // No. of rotations 
        int rotations = 2; 
      
        // Ranges according  
        // to 0-based indexing 
        int [,]ranges = { { 0, 2 },  
                          { 0, 3 } }; 
  
        int index = 1; 
        Console.Write(findElement(arr, ranges, 
                                    rotations,  
                                      index)); 
    } 
} 
  
// This code is contributed 
// by nitin mittal. 
```

## PHP

```php
<?php 
// PHP code to rotate an array 
// and answer the index query 
  
// Function to compute the  
// element at given index 
function findElement($arr, $ranges, 
                     $rotations, $index) 
{ 
    for ($i = $rotations - 1;  
         $i >= 0; $i--)  
    { 
  
        // Range[left...right] 
        $left = $ranges[$i][0]; 
        $right = $ranges[$i][1]; 
  
        // Rotation will not 
        // have any effect 
        if ($left <= $index &&  
            $right >= $index) 
        { 
            if ($index == $left) 
                $index = $right; 
            else
                $index--; 
        } 
    } 
  
    // Returning new element 
    return $arr[$index]; 
} 
  
// Driver Code 
$arr = array(1, 2, 3, 4, 5); 
  
// No. of rotations 
$rotations = 2; 
  
// Ranges according  
// to 0-based indexing 
$ranges = array(array(0, 2), 
                array(0, 3)); 
  
$index = 1; 
  
echo findElement($arr, $ranges, 
                 $rotations, $index); 
  
// This code is contributed by ajit 
?> 
```

输出：

```
3
```

