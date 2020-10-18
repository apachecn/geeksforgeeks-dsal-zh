# 查找数组中最接近的数字

> 原文： [https://www.geeksforgeeks.org/find-closest-number-array/](https://www.geeksforgeeks.org/find-closest-number-array/)

给定一个排序的整数数组。 我们需要找到最接近给定数字的值。 数组可能包含重复值和负数。

**示例**：

```
Input : arr[] = {1, 2, 4, 5, 6, 6, 8, 9}
             Target number = 11
Output : 9
9 is closest to 11 in given array

Input :arr[] = {2, 5, 6, 7, 8, 8, 9}; 
       Target number = 4
Output : 5
```



**简单解决方案**是遍历给定数组，并跟踪每个元素与当前元素的绝对差。 最后返回具有最小绝对值差的元素。

一种有效的**解决方案**是使用[二分搜索](https://www.geeksforgeeks.org/binary-search/)。

## C++

```
// CPP program to find element 
// closet to given target. 
#include <bits/stdc++.h> 
using namespace std; 
  
int getClosest(int, int, int); 
  
// Returns element closest to target in arr[] 
int findClosest(int arr[], int n, int target) 
{ 
    // Corner cases 
    if (target <= arr[0]) 
        return arr[0]; 
    if (target >= arr[n - 1]) 
        return arr[n - 1]; 
  
    // Doing binary search 
    int i = 0, j = n, mid = 0; 
    while (i < j) { 
        mid = (i + j) / 2; 
  
        if (arr[mid] == target) 
            return arr[mid]; 
  
        /* If target is less than array element, 
            then search in left */
        if (target < arr[mid]) { 
  
            // If target is greater than previous 
            // to mid, return closest of two 
            if (mid > 0 && target > arr[mid - 1]) 
                return getClosest(arr[mid - 1], 
                                  arr[mid], target); 
  
            /* Repeat for left half */
            j = mid; 
        } 
  
        // If target is greater than mid 
        else { 
            if (mid < n - 1 && target < arr[mid + 1]) 
                return getClosest(arr[mid], 
                                  arr[mid + 1], target); 
            // update i 
            i = mid + 1;  
        } 
    } 
  
    // Only single element left after search 
    return arr[mid]; 
} 
  
// Method to compare which one is the more close. 
// We find the closest by taking the difference 
// between the target and both values. It assumes 
// that val2 is greater than val1 and target lies 
// between these two. 
int getClosest(int val1, int val2, 
               int target) 
{ 
    if (target - val1 >= val2 - target) 
        return val2; 
    else
        return val1; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 4, 5, 6, 6, 8, 9 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int target = 11; 
    cout << (findClosest(arr, n, target)); 
} 
  
// This code is contributed bu Smitha Dinesh Semwal
```

## Java

```
// Java program to find element closet to given target. 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class FindClosestNumber { 
      
    // Returns element closest to target in arr[] 
    public static int findClosest(int arr[], int target) 
    { 
        int n = arr.length; 
  
        // Corner cases 
        if (target <= arr[0]) 
            return arr[0]; 
        if (target >= arr[n - 1]) 
            return arr[n - 1]; 
  
        // Doing binary search  
        int i = 0, j = n, mid = 0; 
        while (i < j) { 
            mid = (i + j) / 2; 
  
            if (arr[mid] == target) 
                return arr[mid]; 
  
            /* If target is less than array element, 
               then search in left */
            if (target < arr[mid]) { 
         
                // If target is greater than previous 
                // to mid, return closest of two 
                if (mid > 0 && target > arr[mid - 1])  
                    return getClosest(arr[mid - 1],  
                                  arr[mid], target); 
                  
                /* Repeat for left half */
                j = mid;               
            } 
  
            // If target is greater than mid 
            else { 
                if (mid < n-1 && target < arr[mid + 1])  
                    return getClosest(arr[mid],  
                          arr[mid + 1], target);                 
                i = mid + 1; // update i 
            } 
        } 
  
        // Only single element left after search 
        return arr[mid]; 
    } 
  
    // Method to compare which one is the more close 
    // We find the closest by taking the difference 
    //  between the target and both values. It assumes 
    // that val2 is greater than val1 and target lies 
    // between these two. 
    public static int getClosest(int val1, int val2,  
                                         int target) 
    { 
        if (target - val1 >= val2 - target)  
            return val2;         
        else 
            return val1;         
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 2, 4, 5, 6, 6, 8, 9 }; 
        int target = 11; 
        System.out.println(findClosest(arr, target)); 
    } 
}
```

## Python 3

```
# Python3 program to find element 
# closet to given target. 
  
# Returns element closest to target in arr[] 
def findClosest(arr, n, target): 
  
    # Corner cases 
    if (target <= arr[0]): 
        return arr[0] 
    if (target >= arr[n - 1]): 
        return arr[n - 1] 
  
    # Doing binary search 
    i = 0; j = n; mid = 0
    while (i < j):  
        mid = (i + j) / 2
  
        if (arr[mid] == target): 
            return arr[mid] 
  
        # If target is less than array  
        # element, then search in left 
        if (target < arr[mid]) : 
  
            # If target is greater than previous 
            # to mid, return closest of two 
            if (mid > 0 and target > arr[mid - 1]): 
                return getClosest(arr[mid - 1], arr[mid], target) 
  
            # Repeat for left half  
            j = mid 
          
        # If target is greater than mid 
        else : 
            if (mid < n - 1 and target < arr[mid + 1]): 
                return getClosest(arr[mid], arr[mid + 1], target) 
                  
            # update i 
            i = mid + 1
          
    # Only single element left after search 
    return arr[mid] 
  
  
# Method to compare which one is the more close. 
# We find the closest by taking the difference 
# between the target and both values. It assumes 
# that val2 is greater than val1 and target lies 
# between these two. 
def getClosest(val1, val2, target): 
  
    if (target - val1 >= val2 - target): 
        return val2 
    else: 
        return val1 
  
# Driver code 
arr = [1, 2, 4, 5, 6, 6, 8, 9]  
n = len(arr) 
target = 11
print(findClosest(arr, n, target)) 
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find element  
// closet to given target. 
using System; 
  
class GFG 
{ 
      
    // Returns element closest 
    // to target in arr[] 
    public static int findClosest(int []arr,  
                                  int target) 
    { 
        int n = arr.Length; 
  
        // Corner cases 
        if (target <= arr[0]) 
            return arr[0]; 
        if (target >= arr[n - 1]) 
            return arr[n - 1]; 
  
        // Doing binary search  
        int i = 0, j = n, mid = 0; 
        while (i < j) 
        { 
            mid = (i + j) / 2; 
  
            if (arr[mid] == target) 
                return arr[mid]; 
  
            /* If target is less  
            than array element, 
            then search in left */
            if (target < arr[mid])  
            { 
          
                // If target is greater  
                // than previous to mid,  
                // return closest of two 
                if (mid > 0 && target > arr[mid - 1])  
                    return getClosest(arr[mid - 1],  
                                 arr[mid], target); 
                  
                /* Repeat for left half */
                j = mid;              
            } 
  
            // If target is  
            // greater than mid 
            else 
            { 
                if (mid < n-1 && target < arr[mid + 1])  
                    return getClosest(arr[mid],  
                         arr[mid + 1], target);          
                i = mid + 1; // update i 
            } 
        } 
  
        // Only single element 
        // left after search 
        return arr[mid]; 
    } 
  
    // Method to compare which one  
    // is the more close We find the  
    // closest by taking the difference 
    // between the target and both  
    // values. It assumes that val2 is 
    // greater than val1 and target 
    // lies between these two. 
    public static int getClosest(int val1, int val2,  
                                 int target) 
    { 
        if (target - val1 >= val2 - target)  
            return val2;      
        else
            return val1;      
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int []arr = {1, 2, 4, 5,  
                     6, 6, 8, 9}; 
        int target = 11; 
        Console.WriteLine(findClosest(arr, target)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```
<?php 
// PHP program to find element closest  
// to given target.  
  
// Returns element closest to target in arr[]  
function findClosest($arr, $n, $target)  
{  
    // Corner cases  
    if ($target <= $arr[0])  
        return $arr[0];  
    if ($target >= $arr[$n - 1])  
        return $arr[$n - 1];  
  
    // Doing binary search  
    $i = 0; 
    $j = $n; 
    $mid = 0;  
    while ($i < $j)  
    {  
        $mid = ($i + $j) / 2;  
  
        if ($arr[$mid] == $target)  
            return $arr[$mid];  
  
        /* If target is less than array element,  
            then search in left */
        if ($target < $arr[$mid])  
        {  
  
            // If target is greater than previous  
            // to mid, return closest of two  
            if ($mid > 0 && $target > $arr[$mid - 1])  
                return getClosest($arr[$mid - 1],  
                                  $arr[$mid], $target);  
  
            /* Repeat for left half */
            $j = $mid;  
        }  
  
        // If target is greater than mid  
        else
        {  
            if ($mid < $n - 1 &&  
                $target < $arr[$mid + 1])  
                return getClosest($arr[$mid],  
                                  $arr[$mid + 1], $target);  
            // update i  
            $i = $mid + 1;  
        }  
    }  
  
    // Only single element left after search  
    return $arr[$mid];  
}  
  
// Method to compare which one is the more close.  
// We find the closest by taking the difference  
// between the target and both values. It assumes  
// that val2 is greater than val1 and target lies  
// between these two.  
function getClosest($val1, $val2, $target)  
{  
    if ($target - $val1 >= $val2 - $target)  
        return $val2;  
    else
        return $val1;  
}  
  
// Driver code  
$arr = array( 1, 2, 4, 5, 6, 6, 8, 9 );  
$n = sizeof($arr);  
$target = 11;  
echo (findClosest($arr, $n, $target));  
  
// This code is contributed bu Sachin. 
?>
```

输出：

```
9
```
