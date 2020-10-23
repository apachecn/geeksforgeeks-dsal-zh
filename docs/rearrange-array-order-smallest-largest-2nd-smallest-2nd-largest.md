# 按顺序重新排列数组：最小，最大，第二小，第二大..

> 原文： [https://www.geeksforgeeks.org/rearrange-array-order-smallest-largest-2nd-smallest-2nd-largest/](https://www.geeksforgeeks.org/rearrange-array-order-smallest-largest-2nd-smallest-2nd-largest/)

给定一个整数数组，任务是按以下顺序打印该数组：最小数，最大数，第二小数，第二大数，第三最小数，第三最大数，依此类推。

**示例**：

```
Input : arr[] = [5, 8, 1, 4, 2, 9, 3, 7, 6]
Output :arr[] = {1, 9, 2, 8, 3, 7, 4, 6, 5}

Input : arr[] = [1, 2, 3, 4]
Output :arr[] = {1, 4, 2, 3}

```



**简单解决方案**是先找到最小的元素，然后将其与第一个元素交换。 然后找到最大的元素，将其与第二个元素交换，依此类推。 该解决方案的时间复杂度为`O(n^2)`。

**有效解决方案**是使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。

1.  对数组的元素进行排序。

2.  取两个变量`i`和`j`分别指向数组的第一个索引和最后一个索引。

3.  现在运行循环，并通过递增`i`和递减`j`来将元素逐一存储在数组中。

让我们以输入为`5 8 1 4 2 9 3 7 6`的数组为例，对它们进行排序，使该数组变为`1 2 3 4 5 6 7 8 9`。 两个变量分别说`i`和`j`并将它们分别指向数组的第一个索引和最后一个索引，运行循环并通过递增`i`和递减`j`将值存储到新数组中。 我们得到的最终结果为`1 9 2 8 3 7 4 65`。

## C++ 

```cpp

// C++ program to print the array in given order 
#include <bits/stdc++.h> 
using namespace std; 

// Function which arrange the array. 
void rearrangeArray(int arr[], int n) 
{    
    // Sorting the array elements 
    sort(arr, arr + n); 

    int tempArr[n];  // To store modified array 

    // Adding numbers from sorted array to  
    // new array accordingly 
    int ArrIndex = 0; 

    // Traverse from begin and end simultaneously  
    for (int i = 0, j = n-1; i <= n / 2 ||  
                    j > n / 2; i++, j--) { 
        tempArr[ArrIndex] = arr[i]; 
        ArrIndex++; 
        tempArr[ArrIndex] = arr[j]; 
        ArrIndex++; 
    } 

    // Modifying original array 
    for (int i = 0; i < n; i++) 
        arr[i] = tempArr[i]; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 5, 8, 1, 4, 2, 9, 3, 7, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    rearrangeArray(arr, n); 

    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 

    return 0; 
} 

```

## Java

```java
// Java program to print the array in given order 
import java.util.Arrays; 
  
public class GFG {  
  
    // Function which arrange the array. 
    static void rearrangeArray(int arr[], int n) 
    {    
        // Sorting the array elements 
        Arrays.sort(arr); 
       
        int[] tempArr = new int[n]; // To store modified array 
          
        // Adding numbers from sorted array to  
        // new array accordingly 
        int ArrIndex = 0; 
       
        // Traverse from begin and end simultaneously  
        for (int i = 0, j = n-1; i <= n / 2 || j > n / 2; 
                                           i++, j--) { 
            if(ArrIndex < n) 
            { 
                tempArr[ArrIndex] = arr[i]; 
                ArrIndex++; 
            } 
              
            if(ArrIndex < n) 
            { 
                tempArr[ArrIndex] = arr[j]; 
                ArrIndex++; 
            } 
        } 
       
        // Modifying original array 
        for (int i = 0; i < n; i++) 
            arr[i] = tempArr[i]; 
    } 
       
    // Driver Code 
    public static void main(String args[]) 
    { 
        int arr[] = { 5, 8, 1, 4, 2, 9, 3, 7, 6 }; 
        int n = arr.length; 
        rearrangeArray(arr, n); 
       
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i]+" "); 
    } 
} 
// This code is contributed by Sumit Ghosh 
```

## Python3

```py
# Python 3 program to print 
# the array in given order 
  
# Function which arrange the 
# array. 
def rearrangeArray(arr, n) : 
  
    # Sorting the array elements 
    arr.sort() 
  
    # To store modified array 
    tempArr = [0] * (n + 1) 
  
    # Adding numbers from sorted  
    # array to new array accordingly 
    ArrIndex = 0
  
    # Traverse from begin and end 
    # simultaneously  
    i = 0
    j = n-1
      
    while(i <= n // 2 or j > n // 2 ) : 
      
        tempArr[ArrIndex] = arr[i] 
        ArrIndex = ArrIndex + 1
        tempArr[ArrIndex] = arr[j] 
        ArrIndex = ArrIndex + 1
        i = i + 1
        j = j - 1
      
    # Modifying original array 
    for i in range(0, n) : 
        arr[i] = tempArr[i] 
          
  
# Driver Code 
arr = [ 5, 8, 1, 4, 2, 9, 3, 7, 6 ] 
n = len(arr) 
rearrangeArray(arr, n) 
  
for i in range(0, n) : 
    print( arr[i], end = " ") 
      
# This code is contributed by Nikita Tiwari. 
```

## C#

```cs
// C# program to print the  
// array in given order 
using System; 
  
public class GFG {  
  
    // Function which arrange the array. 
    static void rearrangeArray(int []arr, int n) 
    {  
        // Sorting the array elements 
        Array.Sort(arr); 
      
        // To store modified array 
        int []tempArr = new int[n];  
          
        // Adding numbers from sorted array   
        // to new array accordingly 
        int ArrIndex = 0; 
      
        // Traverse from begin and end simultaneously  
        for (int i = 0, j = n-1; i <= n / 2  
             || j > n / 2; i++, j--) { 
                                          
            if(ArrIndex < n) 
            { 
                tempArr[ArrIndex] = arr[i]; 
                ArrIndex++; 
            } 
              
            if(ArrIndex < n) 
            { 
                tempArr[ArrIndex] = arr[j]; 
                ArrIndex++; 
            } 
        } 
      
        // Modifying original array 
        for (int i = 0; i < n; i++) 
            arr[i] = tempArr[i]; 
    } 
      
    // Driver Code 
    public static void Main(String []args) 
    { 
        int []arr = {5, 8, 1, 4, 2, 9, 3, 7, 6}; 
        int n = arr.Length; 
        rearrangeArray(arr, n); 
      
        for (int i = 0; i < n; i++) 
        Console.Write(arr[i] + " "); 
    } 
} 
  
// This code is contributed by Nitin Mittal. 
```

## PHP

```php
<?php 
// PHP program to print  
// the array in given order 
  
// Function which 
// arrange the array. 
function rearrangeArray($arr, $n) 
{  
    // Sorting the  
    // array elements 
    sort($arr); 
  
    // To store modified array 
    $tempArr = array($n);  
      
    // Adding numbers from  
    // sorted array to new 
    // array accordingly 
    $ArrIndex = 0; 
  
    // Traverse from begin  
    // and end simultaneously  
    for ($i = 0, $j = $n - 1; 
         $i <= $n / 2 || $j > $n / 2; 
         $i++, $j--)  
    { 
        $tempArr[$ArrIndex] = $arr[$i]; 
        $ArrIndex++; 
        $tempArr[$ArrIndex] = $arr[$j]; 
        $ArrIndex++; 
    } 
  
    // Modifying original array 
    for ($i = 0; $i < $n; $i++) 
        $arr[$i] = $tempArr[$i]; 
      
    for ($i = 0; $i < $n; $i++) 
        echo $arr[$i] . " "; 
} 
  
// Driver Code 
$arr = array(5, 8, 1, 4, 2,  
             9, 3, 7, 6 ); 
$n = count($arr) ; 
rearrangeArray($arr, $n); 
  
// This code is contributed  
// by Sam007 
?> 
```

输出：

```
1 9 2 8 3 7 4 6 5
```

时间复杂度：`O(n Log n)`。

辅助空间：`O(n)`。