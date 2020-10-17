# 程序以查找数组中的最大元素

> 原文： [https://www.geeksforgeeks.org/c-program-find-largest-element-array/](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

给定一个数组，在其中找到最大的元素。

**示例**：

```
Input : arr[] = {10, 20, 4}
Output : 20

Input : arr[] = {20, 10, 20, 4, 100}
Output : 100

```



解决方案是将`max`初始化为第一个元素，然后从第二个元素遍历给定的数组直至结束。 对于每个遍历的元素，将其与`max`进行比较，如果它大于`max`，则更新`max`。

## C++ 

```cpp

// C++ program to find maximum 
// in arr[] of size n  
#include <bits/stdc++.h> 
using namespace std; 

int largest(int arr[], int n) 
{ 
    int i; 

    // Initialize maximum element 
    int max = arr[0]; 

    // Traverse array elements  
    // from second and compare 
    // every element with current max  
    for (i = 1; i < n; i++) 
        if (arr[i] > max) 
            max = arr[i]; 

    return max; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {10, 324, 45, 90, 9808}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Largest in given array is " 
         << largest(arr, n); 
    return 0; 
} 

// This Code is contributed  
// by Shivi_Aggarwal 

```

## C

```c
// C program to find maximum in arr[] of size n  
#include <stdio.h> 
  
// C function to find maximum in arr[] of size n 
int largest(int arr[], int n) 
{ 
    int i; 
     
    // Initialize maximum element 
    int max = arr[0]; 
  
    // Traverse array elements from second and 
    // compare every element with current max   
    for (i = 1; i < n; i++) 
        if (arr[i] > max) 
            max = arr[i]; 
  
    return max; 
} 
  
int main() 
{ 
    int arr[] = {10, 324, 45, 90, 9808}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printf("Largest in given array is %d", largest(arr, n)); 
    return 0; 
} 
```

## Java

```java
// Java Program to find maximum in arr[]  
class Test 
{ 
     static int arr[] = {10, 324, 45, 90, 9808}; 
       
     // Method to find maximum in arr[] 
     static int largest() 
     { 
         int i; 
           
         // Initialize maximum element 
         int max = arr[0]; 
        
         // Traverse array elements from second and 
         // compare every element with current max   
         for (i = 1; i < arr.length; i++) 
             if (arr[i] > max) 
                 max = arr[i]; 
        
         return max; 
     } 
       
     // Driver method 
     public static void main(String[] args)  
     { 
         System.out.println("Largest in given array is " + largest()); 
        } 
 } 
```

## Python3

```py
# Python3 program to find maximum 
# in arr[] of size n  
  
# python function to find maximum 
# in arr[] of size n 
def largest(arr,n): 
  
    # return max using max   
    # inbuilt max() function 
    return (max(arr)) 
  
# Driver Code 
arr = [10, 324, 45, 90, 9808] 
n = len(arr) 
  
#calculating length of an array 
  
Ans = largest(arr,n) 
  
#display max 
print ("Largest in given array is",Ans) 
  
# This code is contributed by Jai Parkash Bhardwaj 
C#
filter_none
edit
play_arrow

brightness_4
// C# Program to find maximum in arr[]  
using System; 
  
class GFG { 
      
    static int []arr = {10, 324, 45, 90, 9808}; 
      
    // Method to find maximum in arr[] 
    static int largest() 
    { 
        int i; 
          
        // Initialize maximum element 
        int max = arr[0]; 
      
        // Traverse array elements from second and 
        // compare every element with current max  
        for (i = 1; i < arr.Length; i++) 
            if (arr[i] > max) 
                max = arr[i]; 
      
        return max; 
    } 
      
    // Driver method 
    public static void Main()  
    { 
        Console.WriteLine("Largest in given "
                  + "array is " + largest()); 
    } 
} 
  
// This code is contributed by anuj_67. 
```

## PHP

```php
<?php 
// PHP program to find maximum 
// in arr[] of size n  
  
// PHP function to find maximum  
// in arr[] of size n 
function largest($arr, $n) 
{ 
    $i; 
      
    // Initialize maximum element 
    $max = $arr[0]; 
  
    // Traverse array elements 
    // from second and 
    // compare every element  
    // with current max  
    for ($i = 1; $i < $n; $i++) 
        if ($arr[$i] > $max) 
            $max = $arr[$i]; 
  
    return $max; 
}    
      
    // Driver Code 
    $arr= array(10, 324, 45, 90, 9808); 
    $n = sizeof($arr); 
    echo "Largest in given array is "
                 , largest($arr, $n); 
      
// This code is contributed by aj_36 
?> 
```

输出：

```
Largest in given array is 9808
```

使用库函数：

我们使用 C++ 中的[`std::max_element`](https://www.geeksforgeeks.org/stdmax_element-in-cpp/)。

## C++

```cpp
// C++ program to find maximum in arr[] of size n  
#include <bits/stdc++.h> 
using namespace std; 
  
// returns maximum in arr[] of size n 
int largest(int arr[], int n) 
{ 
    return *max_element(arr, arr+n); 
} 
  
int main() 
{ 
    int arr[] = {10, 324, 45, 90, 9808}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << largest(arr, n); 
    return 0; 
} 
```

## Java

```java
// Java program to  
// find maximum in 
// arr[] of size n 
import java .io.*; 
import java.util.*; 
  
class GFG 
{ 
      
    // returns maximum in 
    // arr[] of size n 
    static int largest(int []arr,    
                       int n) 
    { 
        Arrays.sort(arr); 
        return arr[n - 1]; 
    } 
  
    // Driver code 
    static public void main (String[] args) 
    { 
        int []arr = {10, 324, 45,  
                     90, 9808}; 
        int n = arr.length; 
        System.out.println(largest(arr, n)); 
    } 
} 
  
// This code is contributed  
// by anuj_67. 
```

## Python3

```py
# Python 3 program to find 
# maximum in arr[] of size n  
  
# returns maximum 
# in arr[] of size n 
def largest(arr, n): 
  
    return max(arr) 
  
# driver code 
arr = [10, 324, 45, 90, 9808] 
n = len(arr) 
  
print(largest(arr, n)) 
  
# This code is contributed by 
# Smitha Dinesh Semwal 
```

## C#

```cs
// C# program to find maximum in 
// arr[] of size n 
using System; 
using System.Linq; 
  
public class GFG { 
      
    // returns maximum in arr[] of size n 
    static int largest(int []arr, int n) 
    { 
        return arr.Max(); 
    } 
  
    // Driver code 
    static public void Main () 
    { 
        int []arr = {10, 324, 45, 90, 9808}; 
        int n = arr.Length; 
        Console.WriteLine( largest(arr, n)); 
    } 
} 
  
// This code is contributed by anuj_67. 
```

## PHP

```php
<?php 
// PHP program to find maximum 
// in arr[] of size n  
  
// returns maximum in  
// arr[] of size n 
function largest( $arr, $n) 
{ 
    return max($arr); 
} 
  
    // Driver COde 
    $arr = array(10, 324, 45, 90, 9808); 
    $n = count($arr); 
    echo largest($arr, $n); 
  
// This code is contributed by anuj_67. 
?> 
```

输出：

```
9808
```

上述解决方案的时间复杂度为`Theta(n)`。