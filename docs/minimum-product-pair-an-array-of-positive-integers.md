# 最小乘积对为正整数数组

> 原文： [https://www.geeksforgeeks.org/minimum-product-pair-an-array-of-positive-integers/](https://www.geeksforgeeks.org/minimum-product-pair-an-array-of-positive-integers/)

给定一个正整数数组。 我们需要编写一个程序来打印给定数组的任何两个数字的最小乘积。

例子：

```
Input : 11 8 5 7 5 100
Output : 25 
Explanation : The minimum product of any 
two numbers will be 5 * 5 = 25.

Input : 198 76 544 123 154 675 
Output : 7448
Explanation : The minimum product of any 
two numbers will be 76 * 123 = 7448.

```



**简单方法**：一种简单方法是运行两个嵌套循环以生成所有可能的一对元素并跟踪最小乘积。

时间复杂度：`O(n * n)`。

辅助空间：`O(1)`。

**更好的方法**：一种有效的方法是首先对给定的数组排序并打印前两个数字的乘积，排序将花费`O(N log N)`。 答案将是`a[0] * a[1]`。

时间复杂度：`O(n * log(n))`。

辅助空间：`O(1)`。

**最佳方法**：该想法是线性遍历给定数组并跟踪最少两个元素。 最后返回两个最小元素的乘积。

下面是上述方法的实现。

## C++ 

```cpp

// C++ program to calculate minimum 
// product of a pair 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate minimum product 
// of pair 
int printMinimumProduct(int arr[], int n) 
{ 
    // Initialize first and second 
    // minimums. It is assumed that the 
    // array has at least two elements. 
    int first_min = min(arr[0], arr[1]); 
    int second_min = max(arr[0], arr[1]); 

    // Traverse remaining array and keep 
    // track of two minimum elements (Note 
    // that the two minimum elements may 
    // be same if minimum element appears 
    // more than once) 
    // more than once) 
    for (int i=2; i<n; i++) 
    { 
       if (arr[i] < first_min) 
       { 
          second_min = first_min; 
          first_min = arr[i]; 
       } 
       else if (arr[i] < second_min) 
          second_min = arr[i]; 
    } 

    return first_min * second_min; 
} 

// Driver program to test above function 
int main() 
{ 
    int a[] = { 11, 8 , 5 , 7 , 5 , 100 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << printMinimumProduct(a,n); 
    return 0; 
} 

```

## Java

```java
// Java program to calculate minimum 
// product of a pair 
import java.util.*; 
  
class GFG { 
      
    // Function to calculate minimum product 
    // of pair 
    static int printMinimumProduct(int arr[], int n) 
    { 
        // Initialize first and second 
        // minimums. It is assumed that the 
        // array has at least two elements. 
        int first_min = Math.min(arr[0], arr[1]); 
        int second_min = Math.max(arr[0], arr[1]); 
       
        // Traverse remaining array and keep 
        // track of two minimum elements (Note 
        // that the two minimum elements may 
        // be same if minimum element appears 
        // more than once) 
        // more than once) 
        for (int i = 2; i < n; i++) 
        { 
           if (arr[i] < first_min) 
           { 
              second_min = first_min; 
              first_min = arr[i]; 
           } 
           else if (arr[i] < second_min) 
              second_min = arr[i]; 
        } 
       
        return first_min * second_min; 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int a[] = { 11, 8 , 5 , 7 , 5 , 100 }; 
        int n = a.length; 
        System.out.print(printMinimumProduct(a,n)); 
       
    } 
} 
  
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python program to 
# calculate minimum 
# product of a pair 
  
# Function to calculate 
# minimum product 
# of pair 
def printMinimumProduct(arr,n): 
  
    # Initialize first and second 
    # minimums. It is assumed that the 
    # array has at least two elements. 
    first_min = min(arr[0], arr[1]) 
    second_min = max(arr[0], arr[1]) 
   
    # Traverse remaining array and keep 
    # track of two minimum elements (Note 
    # that the two minimum elements may 
    # be same if minimum element appears 
    # more than once) 
    # more than once) 
    for i in range(2,n): 
      
         if (arr[i] < first_min): 
         
            second_min = first_min 
            first_min = arr[i] 
         
         elif (arr[i] < second_min): 
            second_min = arr[i] 
      
    return first_min * second_min 
  
# Driver code 
  
a= [ 11, 8 , 5 , 7 , 5 , 100 ] 
n = len(a) 
  
print(printMinimumProduct(a,n)) 
  
# This code is contributed 
# by Anant Agarwal.
```

## C#

```cs
// C# program to calculate minimum 
// product of a pair 
using System; 
  
class GFG { 
      
    // Function to calculate minimum 
    // product of pair 
    static int printMinimumProduct(int []arr, 
                                       int n) 
    { 
          
        // Initialize first and second 
        // minimums. It is assumed that 
        // the array has at least two 
        // elements. 
        int first_min = Math.Min(arr[0], 
                                    arr[1]); 
                                      
        int second_min = Math.Max(arr[0], 
                                    arr[1]); 
      
        // Traverse remaining array and 
        // keep track of two minimum 
        // elements (Note that the two 
        // minimum elements may be same 
        // if minimum element appears 
        // more than once) 
        for (int i = 2; i < n; i++) 
        { 
            if (arr[i] < first_min) 
            { 
                second_min = first_min; 
                first_min = arr[i]; 
            } 
            else if (arr[i] < second_min) 
                second_min = arr[i]; 
        } 
      
        return first_min * second_min; 
    } 
      
    /* Driver program to test above 
    function */
    public static void Main()  
    { 
        int []a = { 11, 8 , 5 , 7 , 
                            5 , 100 }; 
        int n = a.Length; 
          
        Console.WriteLine( 
            printMinimumProduct(a, n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program to calculate minimum 
// product of a pair 
  
// Function to calculate minimum  
// product of pair 
function printMinimumProduct($arr, $n) 
{ 
      
    // Initialize first and second 
    // minimums. It is assumed that the 
    // array has at least two elements. 
    $first_min = min($arr[0], $arr[1]); 
    $second_min = max($arr[0], $arr[1]); 
  
    // Traverse remaining array and keep 
    // track of two minimum elements (Note 
    // that the two minimum elements may 
    // be same if minimum element appears 
    // more than once) 
    // more than once) 
    for ($i = 2; $i < $n; $i++) 
    { 
        if ($arr[$i] < $first_min) 
        { 
            $second_min = $first_min; 
            $first_min = $arr[$i]; 
        } 
        else if ($arr[$i] < $second_min) 
            $second_min = $arr[$i]; 
    } 
  
    return $first_min * $second_min; 
} 
  
// Driver Code 
$a = array(11, 8 , 5 , 7 , 5 , 100); 
$n = sizeof($a); 
echo(printMinimumProduct($a, $n)); 
  
// This code is contributed by Ajit. 
?>
```

输出：

```
25
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。