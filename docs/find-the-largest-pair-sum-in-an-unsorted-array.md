# 在未排序的数组中找到最大的对和

> 原文： [https://www.geeksforgeeks.org/find-the-largest-pair-sum-in-an-unsorted-array/](https://www.geeksforgeeks.org/find-the-largest-pair-sum-in-an-unsorted-array/)

给定一个未排序的不同整数，在其中找到最大的对和。 例如，`{12, 34, 10, 6, 40}`中最大的对和为 74。

+   难度等级：菜鸟

+   预期时间复杂度：`O(n)`【仅允许遍历数组一次】



这个问题主要归结为找到数组中最大和第二大元素。 通过遍历数组一次，我们可以找到`O(n)`时间中最大和第二大的值。

```
1) Initialize both first and second largest
   first = max(arr[0], arr[1])
   second = min(arr[0], arr[1])
2) Loop through remaining elements (from 3rd to end)
   a) If the current element is greater than first, then update first 
       and second. 
   b) Else if the current element is greater than second then update 
    second
3) Return (first + second)

```

下面是上述算法的实现：

## C++ 

```cpp

// C++ program to find largest pair sum in a given array 
#include<iostream> 
using namespace std; 

/* Function to return largest pair sum. Assumes that  
   there are at-least  two elements in arr[] */
int findLargestSumPair(int arr[], int n) 
{ 
    // Initialize first and second largest element 
    int first, second; 
    if (arr[0] > arr[1]) 
    { 
        first = arr[0]; 
        second = arr[1]; 
    } 
    else
    { 
        first = arr[1]; 
        second = arr[0]; 
    } 

    // Traverse remaining array and find first and second largest 
    // elements in overall array 
    for (int i = 2; i<n; i ++) 
    { 
        /* If current element is greater than first then update both 
          first and second */
        if (arr[i] > first) 
        { 
            second = first; 
            first = arr[i]; 
        } 

        /* If arr[i] is in between first and second then update second  */
        else if (arr[i] > second && arr[i] != first) 
            second = arr[i]; 
    } 
    return (first + second); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {12, 34, 10, 6, 40}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "Max Pair Sum is " << findLargestSumPair(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find largest pair sum in a given array 
  
class Test 
{ 
    static int arr[] = new int[]{12, 34, 10, 6, 40}; 
      
    /* Method to return largest pair sum. Assumes that  
       there are at-least  two elements in arr[] */
    static int findLargestSumPair() 
    { 
        // Initialize first and second largest element 
        int first, second; 
        if (arr[0] > arr[1]) 
        { 
            first = arr[0]; 
            second = arr[1]; 
        } 
        else
        { 
            first = arr[1]; 
            second = arr[0]; 
        } 
       
        // Traverse remaining array and find first and second largest 
        // elements in overall array 
        for (int i = 2; i<arr.length; i ++) 
        { 
            /* If current element is greater than first then update both 
              first and second */
            if (arr[i] > first) 
            { 
                second = first; 
                first = arr[i]; 
            } 
       
            /* If arr[i] is in between first and second then update second  */
            else if (arr[i] > second && arr[i] != first) 
                second = arr[i]; 
        } 
        return (first + second); 
    } 
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
          
        System.out.println("Max Pair Sum is " + findLargestSumPair()); 
          
    } 
}
```

## Python3

```py
# Python3 program to find largest  
# pair sum in a given array 
  
# Function to return largest pair  
# sum. Assumes that there are  
# at-least two elements in arr[]  
def findLargestSumPair(arr, n): 
  
    # Initialize first and second 
    # largest element 
    if arr[0] > arr[1]: 
        first = arr[0] 
        second = arr[1] 
      
    else: 
        first = arr[1] 
        second = arr[0] 
      
  
    # Traverse remaining array and  
    # find first and second largest 
    # elements in overall array 
    for i in range(2, n): 
      
        # If current element is greater 
        # than first then update both 
        # first and second  
        if arr[i] > first: 
            second = first 
            first = arr[i] 
          
  
        # If arr[i] is in between first  
        # and second then update second  
        elif arr[i] > second and arr[i] != first: 
            second = arr[i] 
      
    return (first + second) 
  
# Driver program to test above function */ 
arr = [12, 34, 10, 6, 40] 
n = len(arr) 
print("Max Pair Sum is",  
      findLargestSumPair(arr, n)) 
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find largest 
// pair sum in a given array 
using System; 
  
class GFG 
{ 
    /* Method to return largest pair 
    sum. Assumes that there are 
    at-least two elements in arr[] */
    static int findLargestSumPair(int []arr) 
    { 
        // Initialize first and  
        // second largest element 
        int first, second; 
        if (arr[0] > arr[1]) 
        { 
            first = arr[0]; 
            second = arr[1]; 
        } 
        else
        { 
            first = arr[1]; 
            second = arr[0]; 
        } 
      
        // Traverse remaining array and 
        // find first and second largest 
        // elements in overall array 
        for (int i = 2; i < arr.Length; i ++) 
        { 
            /* If current element is greater  
               than first then update both 
               first and second */
            if (arr[i] > first) 
            { 
                second = first; 
                first = arr[i]; 
            } 
      
            /* If arr[i] is in between first 
               and second then update second */
            else if (arr[i] > second &&  
                     arr[i] != first) 
                second = arr[i]; 
        } 
        return (first + second); 
    } 
    // Driver Code 
    public static void Main()  
    { 
        int []arr1 = new int[]{12, 34, 10, 6, 40}; 
        Console.Write("Max Pair Sum is " +  
                       findLargestSumPair(arr1)); 
          
    } 
}
```

## PHP

```php
<?php 
// PHP program to find largest  
// pair sum in a given array 
  
// Function to return largest  
// pair sum. Assumes that  
// there are at-least two  
// elements in arr[] */ 
function findLargestSumPair($arr, $n) 
{ 
      
    // Initialize first and  
    // second largest element 
    $first;  
    $second; 
      
    if ($arr[0] > $arr[1]) 
    { 
        $first = $arr[0]; 
        $second = $arr[1]; 
    } 
    else
    { 
        $first = $arr[1]; 
        $second = $arr[0]; 
    } 
  
    // Traverse remaining array  
    // and find first and second  
    // largest elements in overall 
    // array 
    for ( $i = 2; $i<$n; $i ++) 
    { 
          
        // If current element is greater 
        // than first then update both 
        // first and second  
        if ($arr[$i] > $first) 
        { 
            $second = $first; 
            $first = $arr[$i]; 
        } 
  
        // If arr[i] is in between first  
        // and second then update second 
        else if ($arr[$i] > $second and
                 $arr[$i] != $first) 
            $second = $arr[$i]; 
    } 
    return ($first + $second); 
} 
  
    // Driver Code  
    $arr = array(12, 34, 10, 6, 40); 
    $n = count($arr); 
    echo "Max Pair Sum is " 
          , findLargestSumPair($arr, $n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
Max Pair Sum is 74
```

上述解决方案的时间复杂度为`O(n)`。