# 找出任何两个元素之间的最小差异

> 原文： [https://www.geeksforgeeks.org/find-minimum-difference-pair/](https://www.geeksforgeeks.org/find-minimum-difference-pair/)

给定一个未排序的数组，找到给定数组中任何一对之间的最小差。

**示例**：

```
Input  : {1, 5, 3, 19, 18, 25};
Output : 1
Minimum difference is between 18 and 19

Input  : {30, 5, 20, 9};
Output : 4
Minimum difference is between 5 and 9

Input  : {1, 19, -4, 31, 38, 25, 100};
Output : 5
Minimum difference is between 1 and -4

```



**方法 1（简单：`O(n^2)`）**：

一个简单的解决方案是使用两个循环。

## C/C++ 

```

// C++ implementation of simple method to find 
// minimum difference between any pair 
#include <bits/stdc++.h> 
using namespace std; 

// Returns minimum difference between any pair 
int findMinDiff(int arr[], int n) 
{ 
   // Initialize difference as infinite 
   int diff = INT_MAX; 

   // Find the min diff by comparing difference 
   // of all possible pairs in given array 
   for (int i=0; i<n-1; i++) 
      for (int j=i+1; j<n; j++) 
          if (abs(arr[i] - arr[j]) < diff) 
                diff = abs(arr[i] - arr[j]); 

   // Return min diff 
   return diff; 
} 

// Driver code 
int main() 
{ 
   int arr[] = {1, 5, 3, 19, 18, 25}; 
   int n = sizeof(arr)/sizeof(arr[0]); 
   cout << "Minimum difference is " << findMinDiff(arr, n); 
   return 0; 
} 

```

## Java

```java
// Java implementation of simple method to find 
// minimum difference between any pair 
  
class GFG 
{ 
    // Returns minimum difference between any pair 
    static int findMinDiff(int[] arr, int n) 
    { 
        // Initialize difference as infinite 
        int diff = Integer.MAX_VALUE; 
      
        // Find the min diff by comparing difference 
        // of all possible pairs in given array 
        for (int i=0; i<n-1; i++) 
            for (int j=i+1; j<n; j++) 
                if (Math.abs((arr[i] - arr[j]) )< diff) 
                    diff = Math.abs((arr[i] - arr[j])); 
      
        // Return min diff     
        return diff; 
    } 
  
    // Driver method to test the above function 
    public static void main(String[] args) 
    { 
        int arr[] = new int[]{1, 5, 3, 19, 18, 25}; 
        System.out.println("Minimum difference is "+ 
                              findMinDiff(arr, arr.length)); 
      
    } 
}
```

## Python

```py
# Python implementation of simple method to find 
# minimum difference between any pair 
  
# Returns minimum difference between any pair 
def findMinDiff(arr, n): 
    # Initialize difference as infinite 
    diff = 10**20
      
    # Find the min diff by comparing difference 
    # of all possible pairs in given array 
    for i in range(n-1): 
        for j in range(i+1,n): 
            if abs(arr[i]-arr[j]) < diff: 
                diff = abs(arr[i] - arr[j]) 
  
    # Return min diff 
    return diff 
  
# Driver code 
arr = [1, 5, 3, 19, 18, 25] 
n = len(arr) 
print("Minimum difference is " + str(findMinDiff(arr, n))) 
  
# This code is contributed by Pratik Chhajer
```

## C#

```cs
// C# implementation of simple method to find 
// minimum difference between any pair 
using System; 
  
class GFG { 
      
    // Returns minimum difference between any pair 
    static int findMinDiff(int []arr, int n) 
    { 
          
        // Initialize difference as infinite 
        int diff = int.MaxValue; 
      
        // Find the min diff by comparing difference 
        // of all possible pairs in given array 
        for (int i = 0; i < n-1; i++) 
            for (int j = i+1; j < n; j++) 
                if (Math.Abs((arr[i] - arr[j]) ) < diff) 
                    diff = Math.Abs((arr[i] - arr[j])); 
      
        // Return min diff  
        return diff; 
    } 
  
    // Driver method to test the above function 
    public static void Main() 
    { 
        int []arr = new int[]{1, 5, 3, 19, 18, 25}; 
        Console.Write("Minimum difference is " + 
                        findMinDiff(arr, arr.Length)); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// PHP implementation of simple  
// method to find minimum  
// difference between any pair 
  
// Returns minimum difference 
// between any pair 
function findMinDiff($arr, $n) 
{ 
// Initialize difference 
// as infinite 
$diff = PHP_INT_MAX; 
  
// Find the min diff by comparing 
// difference of all possible  
// pairs in given array 
for ($i = 0; $i < $n - 1; $i++) 
    for ($j = $i + 1; $j < $n; $j++) 
        if (abs($arr[$i] - $arr[$j]) < $diff) 
                $diff = abs($arr[$i] - $arr[$j]); 
  
// Return min diff 
return $diff; 
} 
  
// Driver code 
$arr = array(1, 5, 3, 19, 18, 25); 
$n = sizeof($arr); 
echo "Minimum difference is " , 
         findMinDiff($arr, $n); 
  
// This code is contributed by ajit 
?>
```

输出：

```
Minimum difference is 1
```

方法 2（有效：`O(n Log n)`）：

这个想法是使用排序。 以下是步骤。

1.  按升序对数组进行排序。 此步骤需要`O(n Log n)`时间。
2.  将差初始化为无穷大。 此步骤需要`O(1)`时间。
3.  比较排序数组中的所有相邻对，并跟踪最小差异。 此步骤需要`O(n)`时间。

以下是上述想法的实现。

## C++

```cpp
// C++ program to find minimum difference between 
// any pair in an unsorted array 
#include <bits/stdc++.h> 
using namespace std; 
  
// Returns minimum difference between any pair 
int findMinDiff(int arr[], int n) 
{ 
   // Sort array in non-decreasing order 
   sort(arr, arr+n); 
  
   // Initialize difference as infinite 
   int diff = INT_MAX; 
  
   // Find the min diff by comparing adjacent 
   // pairs in sorted array 
   for (int i=0; i<n-1; i++) 
      if (arr[i+1] - arr[i] < diff) 
          diff = arr[i+1] - arr[i]; 
  
   // Return min diff 
   return diff; 
} 
  
// Driver code 
int main() 
{ 
   int arr[] = {1, 5, 3, 19, 18, 25}; 
   int n = sizeof(arr)/sizeof(arr[0]); 
   cout << "Minimum difference is " << findMinDiff(arr, n); 
   return 0; 
}
```

## Java

```java
// Java program to find minimum difference between 
// any pair in an unsorted array 
  
import java.util.Arrays; 
  
class GFG 
{ 
    // Returns minimum difference between any pair 
    static int findMinDiff(int[] arr, int n) 
    { 
           // Sort array in non-decreasing order 
           Arrays.sort(arr); 
           
           // Initialize difference as infinite 
           int diff = Integer.MAX_VALUE; 
           
           // Find the min diff by comparing adjacent 
           // pairs in sorted array 
           for (int i=0; i<n-1; i++) 
              if (arr[i+1] - arr[i] < diff) 
                  diff = arr[i+1] - arr[i]; 
           
           // Return min diff 
           return diff; 
    } 
  
    // Driver method to test the above function 
    public static void main(String[] args) 
    { 
        int arr[] = new int[]{1, 5, 3, 19, 18, 25}; 
        System.out.println("Minimum difference is "+ 
                              findMinDiff(arr, arr.length)); 
      
    } 
}
```

## Python

```py
# Python program to find minimum difference between 
# any pair in an unsorted array 
  
# Returns minimum difference between any pair 
def findMinDiff(arr, n): 
  
    # Sort array in non-decreasing order 
    arr = sorted(arr) 
  
    # Initialize difference as infinite 
    diff = 10**20
  
    # Find the min diff by comparing adjacent 
    # pairs in sorted array 
    for i in range(n-1): 
        if arr[i+1] - arr[i] < diff: 
            diff = arr[i+1] - arr[i] 
  
    # Return min diff 
    return diff 
  
# Driver code 
arr = [1, 5, 3, 19, 18, 25] 
n = len(arr) 
print("Minimum difference is " + str(findMinDiff(arr, n))) 
  
# This code is contributed by Pratik Chhajer
```

## C#

```cs
// C# program to find minimum  
// difference between any pair 
// in an unsorted array 
using System; 
  
class GFG 
{ 
    // Returns minimum difference  
    // between any pair 
    static int findMinDiff(int[] arr,  
                           int n) 
    { 
        // Sort array in  
        // non-decreasing order 
        Array.Sort(arr); 
          
        // Initialize difference 
        // as infinite 
        int diff = int.MaxValue; 
          
        // Find the min diff by  
        // comparing adjacent pairs 
        // in sorted array 
        for (int i = 0; i < n - 1; i++) 
            if (arr[i + 1] - arr[i] < diff) 
                diff = arr[i + 1] - arr[i]; 
          
        // Return min diff 
        return diff; 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        int []arr = new int[]{1, 5, 3, 19, 18, 25}; 
        Console.WriteLine("Minimum difference is " + 
                           findMinDiff(arr, arr.Length)); 
      
    } 
} 
  
//This code is contributed by anuj_67.
```

## PHP

```php
<?php 
// PHP program to find minimum  
// difference between any pair  
// in an unsorted array 
  
// Returns minimum difference 
// between any pair 
function findMinDiff($arr, $n) 
{ 
      
// Sort array in  
// non-decreasing order 
sort($arr); 
  
// Initialize difference 
// as infinite 
$diff = PHP_INT_MAX; 
  
// Find the min diff by  
// comparing adjacent  
// pairs in sorted array 
for ($i = 0; $i < $n - 1; $i++) 
    if ($arr[$i + 1] - $arr[$i] < $diff) 
        $diff = $arr[$i + 1] - $arr[$i]; 
  
// Return min diff 
return $diff; 
} 
  
// Driver code 
$arr = array(1, 5, 3, 19, 18, 25); 
$n = sizeof($arr); 
echo "Minimum difference is " ,  
         findMinDiff($arr, $n); 
  
// This code is contributed ajit 
?>
```

输出：

```
Minimum difference is 1
```

