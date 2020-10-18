# 重新排列数组，如果`i`为偶数则`arr[i] >= arr[j]`，如果`i`为奇数且`j < i`则`arr[i] <= arr[j]`

> 原文： [https://www.geeksforgeeks.org/rearrange-array-arri-arrj-even-arri/](https://www.geeksforgeeks.org/rearrange-array-arri-arrj-even-arri/)

给定`n`个元素的数组。 我们的任务是编写一个程序来重新排列数组，以使偶数位置的元素大于其之前的所有元素，奇数位置的元素小于其之前的所有元素。

**示例**：

```
Input : arr[] = {1, 2, 3, 4, 5, 6, 7}
Output : 4 5 3 6 2 7 1

Input : arr[] = {1, 2, 1, 4, 5, 6, 8, 8} 
Output : 4 5 2 6 1 8 1 8

```



解决此问题的想法是，首先创建原始数组的辅助副本，然后对复制的数组进行排序。 现在，具有`n`个元素的数组中偶数位置的总数将为`floor(n / 2)`，其余为奇数位置的数量。 现在，以以下方式使用排序后的数组填充原始数组中的奇数和偶数位置：

*   总奇数位将为`n – floor(n / 2)`。 从已排序数组的第（`n - floor(n / 2)`）个位置开始，然后将元素复制到已排序数组的第一个位置。 从此位置开始向左遍历已排序的数组，并继续向右填充原始数组中的奇数位置。

*   从第（`n - floor(n / 2) + 1`）个位置开始向右遍历已排序的数组，并从第 2 个位置开始继续填充原始数组。

以下是上述想法的实现：

## C++ 

```cpp

// C++ program to rearrange the array 
// as per the given condition 

#include <bits/stdc++.h> 
using namespace std; 

// function to rearrange the array 
void rearrangeArr(int arr[], int n) 
{ 
    // total even positions 
    int evenPos = n / 2; 

    // total odd positions 
    int oddPos = n - evenPos; 

    int tempArr[n]; 

    // copy original array in an 
    // auxiliary array 
    for (int i = 0; i < n; i++) 
        tempArr[i] = arr[i]; 

    // sort the auxiliary array 
    sort(tempArr, tempArr + n); 

    int j = oddPos - 1; 

    // fill up odd position in original 
    // array 
    for (int i = 0; i < n; i += 2) { 
        arr[i] = tempArr[j]; 
        j--; 
    } 

    j = oddPos; 

    // fill up even positions in original 
    // array 
    for (int i = 1; i < n; i += 2) { 
        arr[i] = tempArr[j]; 
        j++; 
    } 

    // display array 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 }; 
    int size = sizeof(arr) / sizeof(arr[0]); 
    rearrangeArr(arr, size); 
    return 0; 
} 

```

## Java

```java
// Java program to rearrange the array 
// as per the given condition 
import java.util.*; 
import java.lang.*; 
  
public class GfG{ 
    // function to rearrange the array 
    public static void rearrangeArr(int arr[], 
                                        int n) 
    { 
        // total even positions 
        int evenPos = n / 2; 
  
        // total odd positions 
        int oddPos = n - evenPos; 
  
        int[] tempArr = new int [n]; 
  
        // copy original array in an 
        // auxiliary array 
        for (int i = 0; i < n; i++) 
            tempArr[i] = arr[i]; 
  
        // sort the auxiliary array 
        Arrays.sort(tempArr); 
  
        int j = oddPos - 1; 
  
        // fill up odd position in  
        // original array 
        for (int i = 0; i < n; i += 2) { 
            arr[i] = tempArr[j]; 
            j--; 
        } 
  
        j = oddPos; 
  
        // fill up even positions in  
        // original array 
        for (int i = 1; i < n; i += 2) { 
            arr[i] = tempArr[j]; 
            j++; 
        } 
  
        // display array 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 
      
    // Driver function  
    public static void main(String argc[]){ 
        int[] arr = new int []{ 1, 2, 3, 4, 5, 
                                        6, 7 }; 
        int size = 7; 
        rearrangeArr(arr, size); 
          
    } 
} 
  
/* This code is contributed by Sagar Shukla */
```

## Python3

```py
# Python3 code to rearrange the array 
# as per the given condition 
import array as a 
import numpy as np 
  
# function to rearrange the array 
def rearrangeArr(arr, n): 
      
    # total even positions 
    evenPos = int(n / 2) 
  
    # total odd positions 
    oddPos = n - evenPos 
  
    # intialising empty array in python 
    tempArr = np.empty(n, dtype = object) 
  
    # copy original array in an 
    # auxiliary array 
    for i in range(0, n): 
          
        tempArr[i] = arr[i] 
  
    # sort the auxiliary array 
    tempArr.sort() 
  
    j = oddPos - 1
  
    # fill up odd position in original 
    # array 
    for i in range(0, n, 2): 
  
        arr[i] = tempArr[j] 
        j = j - 1
      
    j = oddPos 
  
    # fill up even positions in original 
    # array 
    for i in range(1, n, 2): 
        arr[i] = tempArr[j] 
        j = j + 1
      
    # display array 
    for i in range(0, n): 
        print (arr[i], end = ' ') 
  
# Driver code 
arr = a.array('i', [ 1, 2, 3, 4, 5, 6, 7 ]) 
rearrangeArr(arr, 7) 
  
# This code is contributed by saloni1297 
```

## C#

```cs
// C# program to rearrange the array 
// as per the given condition 
using System; 
  
public class GfG { 
      
    // Function to rearrange the array 
    public static void rearrangeArr(int []arr, int n) 
    { 
        // total even positions 
        int evenPos = n / 2; 
  
        // total odd positions 
        int oddPos = n - evenPos; 
  
        int[] tempArr = new int [n]; 
  
        // copy original array in an 
        // auxiliary array 
        for (int i = 0; i < n; i++) 
            tempArr[i] = arr[i]; 
  
        // sort the auxiliary array 
        Array.Sort(tempArr); 
  
        int j = oddPos - 1; 
  
        // Fill up odd position in  
        // original array 
        for (int i = 0; i < n; i += 2) { 
            arr[i] = tempArr[j]; 
            j--; 
        } 
  
        j = oddPos; 
  
        // Fill up even positions in  
        // original array 
        for (int i = 1; i < n; i += 2) { 
            arr[i] = tempArr[j]; 
            j++; 
        } 
  
        // display array 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 
      
    // Driver Code  
    public static void Main() 
    { 
        int[] arr = new int []{ 1, 2, 3, 4, 5, 6, 7 }; 
        int size = 7; 
        rearrangeArr(arr, size); 
    } 
} 
  
/* This code is contributed by vt_m */
```

## PHP

```php
<?php  
// PHP program to rearrange the array 
// as per the given condition 
  
// function to rearrange the array 
function rearrangeArr(&$arr, $n) 
{ 
    // total even positions 
    $evenPos = intval($n / 2); 
  
    // total odd positions 
    $oddPos = $n - $evenPos; 
  
    $tempArr = array_fill(0, $n, NULL); 
  
    // copy original array in an 
    // auxiliary array 
    for ($i = 0; $i < $n; $i++) 
        $tempArr[$i] = $arr[$i]; 
  
    // sort the auxiliary array 
    sort($tempArr); 
  
    $j = $oddPos - 1; 
  
    // fill up odd position in  
    // original array 
    for ($i = 0; $i < $n; $i += 2)  
    { 
        $arr[$i] = $tempArr[$j]; 
        $j--; 
    } 
  
    $j = $oddPos; 
  
    // fill up even positions in  
    // original array 
    for ($i = 1; $i < $n; $i += 2) 
    { 
        $arr[$i] = $tempArr[$j]; 
        $j++; 
    } 
  
    // display array 
    for ($i = 0; $i < $n; $i++) 
        echo $arr[$i] ." "; 
} 
  
// Driver code 
$arr = array(1, 2, 3, 4, 5, 6, 7 ); 
$size = sizeof($arr); 
rearrangeArr($arr, $size); 
  
// This code is contributed  
// by ChitraNayal 
?> 
```

输出：

```
4 5 3 6 2 7 1
```

时间复杂度：`O(n logn)`。

辅助空间：`O(n)`。