# 最大乘积子数组

> 原文： [https://www.geeksforgeeks.org/maximum-product-subarray/](https://www.geeksforgeeks.org/maximum-product-subarray/)

给定一个同时包含正整数和负整数的数组，请找到最大乘积子数组的乘积。 预期的时间复杂度为`O(n)`，并且只能使用`O(1)`的额外空间。

**示例**：

```
Input: arr[] = {6, -3, -10, 0, 2}
Output:   180  // The subarray is {6, -3, -10}

Input: arr[] = {-1, -3, -10, 0, 60}
Output:   60  // The subarray is {60}

Input: arr[] = {-2, -3, 0, -2, -40}
Output:   80  // The subarray is {-2, -40}

```



以下解决方案假定给定的输入数组始终具有正输出。 该解决方案适用于上述所有情况。 它不适用于`{0, 0, -20, 0}`，`{0, 0, 0}`等数组。等等。可以轻松修改解决方案以处理这种情况。

与[最大和连续子数组](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)问题相似。 这里唯一需要注意的是，最大乘积也可以通过以前一个元素乘以该元素结尾的最小（负）乘积来获得。 例如，在数组`{12, 2, -3, -5, -6, -2}`中，当我们在元素 -2 处时，最大乘积是的乘积，最小乘积以 -6 和 -2 结尾。

## C++ 

```cpp

// C++ program to find Maximum Product Subarray 
#include <bits/stdc++.h> 
using namespace std; 

/* Returns the product of max product subarray.  
Assumes that the given array always has a subarray  
with product more than 1 */
int maxSubarrayProduct(int arr[], int n) 
{ 
    // max positive product ending at the current position 
    int max_ending_here = 1; 

    // min negative product ending at the current position 
    int min_ending_here = 1; 

    // Initialize overall max product 
    int max_so_far = 1; 
    int flag = 0; 
    /* Traverse through the array. Following values are  
    maintained after the i'th iteration:  
    max_ending_here is always 1 or some positive product  
                    ending with arr[i]  
    min_ending_here is always 1 or some negative product  
                    ending with arr[i] */
    for (int i = 0; i < n; i++) { 
        /* If this element is positive, update max_ending_here.  
        Update min_ending_here only if min_ending_here is  
        negative */
        if (arr[i] > 0) { 
            max_ending_here = max_ending_here * arr[i]; 
            min_ending_here = min(min_ending_here * arr[i], 1); 
            flag = 1; 
        } 

        /* If this element is 0, then the maximum product  
        cannot end here, make both max_ending_here and  
        min_ending_here 0  
        Assumption: Output is alway greater than or equal  
                    to 1\. */
        else if (arr[i] == 0) { 
            max_ending_here = 1; 
            min_ending_here = 1; 
        } 

       /* If element is negative. This is tricky   
        max_ending_here can either be 1 or positive.   
        min_ending_here can either be 1 or negative.   
        next max_ending_here will always be prev.   
        min_ending_here * arr[i] ,next min_ending_here   
        will be 1 if prev max_ending_here is 1, otherwise   
        next min_ending_here will be prev max_ending_here *   
        arr[i] */

        else { 
            int temp = max_ending_here; 
            max_ending_here = max(min_ending_here * arr[i], 1); 
            min_ending_here = temp * arr[i]; 
        } 

        // update max_so_far, if needed 
        if (max_so_far < max_ending_here) 
            max_so_far = max_ending_here; 
    } 
    if (flag == 0 && max_so_far == 1) 
        return 0; 
    return max_so_far; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, -2, -3, 0, 7, -8, -2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Maximum Sub array product is "
         << maxSubarrayProduct(arr, n); 
    return 0; 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c
// C program to find Maximum Product Subarray 
#include <stdio.h> 
  
// Utility functions to get minimum of two integers 
int min(int x, int y) { return x < y ? x : y; } 
  
// Utility functions to get maximum of two integers 
int max(int x, int y) { return x > y ? x : y; } 
  
/* Returns the product of max product subarray.  
Assumes that the given array always has a subarray  
with product more than 1 */
int maxSubarrayProduct(int arr[], int n) 
{ 
    // max positive product ending at the current position 
    int max_ending_here = 1; 
  
    // min negative product ending at the current position 
    int min_ending_here = 1; 
  
    // Initialize overall max product 
    int max_so_far = 1; 
    int flag = 0; 
  
    /* Traverse through the array. Following values are  
    maintained after the i'th iteration:  
    max_ending_here is always 1 or some positive product  
                    ending with arr[i]  
    min_ending_here is always 1 or some negative product  
                    ending with arr[i] */
    for (int i = 0; i < n; i++) { 
        /* If this element is positive, update max_ending_here.  
        Update min_ending_here only if min_ending_here is  
        negative */
        if (arr[i] > 0) { 
            max_ending_here = max_ending_here * arr[i]; 
            min_ending_here = min(min_ending_here * arr[i], 1); 
            flag = 1; 
        } 
  
        /* If this element is 0, then the maximum product  
        cannot end here, make both max_ending_here and  
        min_ending_here 0  
        Assumption: Output is alway greater than or equal  
                    to 1. */
        else if (arr[i] == 0) { 
            max_ending_here = 1; 
            min_ending_here = 1; 
        } 
  
        /* If element is negative. This is tricky  
        max_ending_here can either be 1 or positive.  
        min_ending_here can either be 1 or negative.  
        next min_ending_here will always be prev.  
        max_ending_here * arr[i] next max_ending_here  
        will be 1 if prev min_ending_here is 1, otherwise  
        next max_ending_here will be prev min_ending_here *  
        arr[i] */
        else { 
            int temp = max_ending_here; 
            max_ending_here = max(min_ending_here * arr[i], 1); 
            min_ending_here = temp * arr[i]; 
        } 
  
        // update max_so_far, if needed 
        if (max_so_far < max_ending_here) 
            max_so_far = max_ending_here; 
    } 
    if (flag == 0 && max_so_far == 1) 
        return 0; 
    return max_so_far; 
  
    return max_so_far; 
} 
  
// Driver Program to test above function 
int main() 
{ 
    int arr[] = { 1, -2, -3, 0, 7, -8, -2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printf("Maximum Sub array product is %d", 
           maxSubarrayProduct(arr, n)); 
    return 0; 
} 
```

## Java

```java
// Java program to find maximum product subarray 
import java.io.*; 
  
class ProductSubarray { 
  
    // Utility functions to get minimum of two integers 
    static int min(int x, int y) { return x < y ? x : y; } 
  
    // Utility functions to get maximum of two integers 
    static int max(int x, int y) { return x > y ? x : y; } 
  
    /* Returns the product of max product subarray. 
    Assumes that the given array always has a subarray 
    with product more than 1 */
    static int maxSubarrayProduct(int arr[]) 
    { 
        int n = arr.length; 
        // max positive product ending at the current position 
        int max_ending_here = 1; 
  
        // min negative product ending at the current position 
        int min_ending_here = 1; 
  
        // Initialize overall max product 
        int max_so_far = 1; 
        int flag = 0; 
  
        /* Traverse through the array. Following 
        values are maintained after the ith iteration: 
        max_ending_here is always 1 or some positive product 
                        ending with arr[i] 
        min_ending_here is always 1 or some negative product 
                        ending with arr[i] */
        for (int i = 0; i < n; i++) { 
            /* If this element is positive, update max_ending_here. 
                Update min_ending_here only if min_ending_here is 
                negative */
            if (arr[i] > 0) { 
                max_ending_here = max_ending_here * arr[i]; 
                min_ending_here = min(min_ending_here * arr[i], 1); 
                flag = 1; 
            } 
  
            /* If this element is 0, then the maximum product cannot 
            end here, make both max_ending_here and min_ending 
            _here 0 
            Assumption: Output is alway greater than or equal to 1. */
            else if (arr[i] == 0) { 
                max_ending_here = 1; 
                min_ending_here = 1; 
            } 
  
            /* If element is negative. This is tricky 
            max_ending_here can either be 1 or positive. 
            min_ending_here can either be 1 or negative. 
            next min_ending_here will always be prev. 
            max_ending_here * arr[i] 
            next max_ending_here will be 1 if prev 
            min_ending_here is 1, otherwise 
            next max_ending_here will be  
                        prev min_ending_here * arr[i] */
            else { 
                int temp = max_ending_here; 
                max_ending_here = max(min_ending_here * arr[i], 1); 
                min_ending_here = temp * arr[i]; 
            } 
  
            // update max_so_far, if needed 
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 
        } 
  
        if (flag == 0 && max_so_far == 1) 
            return 0; 
        return max_so_far; 
    } 
  
    public static void main(String[] args) 
    { 
  
        int arr[] = { 1, -2, -3, 0, 7, -8, -2 }; 
        System.out.println("Maximum Sub array product is "
                           + maxSubarrayProduct(arr)); 
    } 
} /*This code is contributed by Devesh Agrawal*/
```

## Python

```py
# Python program to find maximum product subarray 
  
# Returns the product of max product subarray. 
# Assumes that the given array always has a subarray 
# with product more than 1 
def maxsubarrayproduct(arr): 
  
    n = len(arr) 
  
    # max positive product ending at the current position 
    max_ending_here = 1
  
    # min positive product ending at the current position 
    min_ending_here = 1
  
    # Initialize maximum so far 
    max_so_far = 1
    flag = 0
  
    # Traverse throughout the array. Following values 
    # are maintained after the ith iteration: 
    # max_ending_here is always 1 or some positive product 
    # ending with arr[i] 
    # min_ending_here is always 1 or some negative product 
    # ending with arr[i] 
    for i in range(0, n): 
  
        # If this element is positive, update max_ending_here. 
        # Update min_ending_here only if min_ending_here is 
        # negative 
        if arr[i] > 0: 
            max_ending_here = max_ending_here * arr[i] 
            min_ending_here = min (min_ending_here * arr[i], 1) 
            flag = 1
  
        # If this element is 0, then the maximum product cannot 
        # end here, make both max_ending_here and min_ending_here 0 
        # Assumption: Output is alway greater than or equal to 1. 
        elif arr[i] == 0: 
            max_ending_here = 1
            min_ending_here = 1
  
        # If element is negative. This is tricky 
        # max_ending_here can either be 1 or positive. 
        # min_ending_here can either be 1 or negative. 
        # next min_ending_here will always be prev. 
        # max_ending_here * arr[i] 
        # next max_ending_here will be 1 if prev 
        # min_ending_here is 1, otherwise 
        # next max_ending_here will be prev min_ending_here * arr[i] 
        else: 
            temp = max_ending_here 
            max_ending_here = max (min_ending_here * arr[i], 1) 
            min_ending_here = temp * arr[i] 
        if (max_so_far < max_ending_here): 
            max_so_far = max_ending_here 
              
    if flag == 0 and max_so_far == 1: 
        return 0
    return max_so_far 
  
# Driver function to test above function 
arr = [1, -2, -3, 0, 7, -8, -2] 
print "Maximum product subarray is", maxsubarrayproduct(arr) 
  
# This code is contributed by Devesh Agrawal 
```

## C#

```cs
// C# program to find maximum product subarray 
using System; 
  
class GFG { 
  
    // Utility functions to get minimum of two integers 
    static int min(int x, int y) { return x < y ? x : y; } 
  
    // Utility functions to get maximum of two integers 
    static int max(int x, int y) { return x > y ? x : y; } 
  
    /* Returns the product of max product subarray. 
    Assumes that the given array always has a subarray 
    with product more than 1 */
    static int maxSubarrayProduct(int[] arr) 
    { 
        int n = arr.Length; 
        // max positive product ending at the current 
        // position 
        int max_ending_here = 1; 
  
        // min negative product ending at the current 
        // position 
        int min_ending_here = 1; 
  
        // Initialize overall max product 
        int max_so_far = 1; 
        int flag = 0; 
  
        /* Traverse through the array. Following 
        values are maintained after the ith iteration: 
        max_ending_here is always 1 or some positive 
        product ending with arr[i] min_ending_here is 
        always 1 or some negative product ending  
        with arr[i] */
        for (int i = 0; i < n; i++) { 
            /* If this element is positive, update  
            max_ending_here. Update min_ending_here  
            only if min_ending_here is negative */
            if (arr[i] > 0) { 
                max_ending_here = max_ending_here * arr[i]; 
                min_ending_here = min(min_ending_here 
                                          * arr[i], 
                                      1); 
                flag = 1; 
            } 
  
            /* If this element is 0, then the maximum  
            product cannot end here, make both  
            max_ending_here and min_ending_here 0 
            Assumption: Output is alway greater than or 
            equal to 1. */
            else if (arr[i] == 0) { 
                max_ending_here = 1; 
                min_ending_here = 1; 
            } 
  
            /* If element is negative. This is tricky 
            max_ending_here can either be 1 or positive. 
            min_ending_here can either be 1 or negative. 
            next min_ending_here will always be prev. 
            max_ending_here * arr[i] 
            next max_ending_here will be 1 if prev 
            min_ending_here is 1, otherwise 
            next max_ending_here will be  
            prev min_ending_here * arr[i] */
            else { 
                int temp = max_ending_here; 
                max_ending_here = max(min_ending_here 
                                          * arr[i], 
                                      1); 
                min_ending_here = temp * arr[i]; 
            } 
  
            // update max_so_far, if needed 
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 
        } 
  
        if (flag == 0 && max_so_far == 1) 
            return 0; 
  
        return max_so_far; 
    } 
  
    public static void Main() 
    { 
  
        int[] arr = { 1, -2, -3, 0, 7, -8, -2 }; 
  
        Console.WriteLine("Maximum Sub array product is "
                          + maxSubarrayProduct(arr)); 
    } 
} 
  
/*This code is contributed by vt_m*/
```

## PHP

```php
<?php 
// php program to find Maximum Product 
// Subarray 
  
// Utility functions to get minimum of 
// two integers 
function minn ($x, $y)  
{ 
    return $x < $y? $x : $y; 
} 
  
// Utility functions to get maximum of 
// two integers 
function maxx ($x, $y)  
{ 
    return $x > $y? $x : $y;  
} 
  
/* Returns the product of max product 
subarray. Assumes that the given array 
always has a subarray with product 
more than 1 */
function maxSubarrayProduct($arr, $n) 
{ 
      
    // max positive product ending at  
    // the current position 
    $max_ending_here = 1; 
  
    // min negative product ending at 
    // the current position 
    $min_ending_here = 1; 
  
    // Initialize overall max product 
    $max_so_far = 1; 
    $flag = 0; 
  
    /* Traverse through the array. 
    Following values are maintained  
    after the i'th iteration:  
    max_ending_here is always 1 or 
    some positive product ending with 
    arr[i] min_ending_here is always 
    1 or some negative product ending 
    with arr[i] */
    for ($i = 0; $i < $n; $i++) 
    { 
          
        /* If this element is positive, 
        update max_ending_here. Update 
        min_ending_here only if  
        min_ending_here is negative */
        if ($arr[$i] > 0) 
        { 
            $max_ending_here =  
            $max_ending_here * $arr[$i]; 
              
            $min_ending_here =  
                min ($min_ending_here
                        * $arr[$i], 1); 
            $flag = 1; 
        } 
  
        /* If this element is 0, then the 
        maximum product cannot end here, 
        make both max_ending_here and  
        min_ending_here 0 
        Assumption: Output is alway  
        greater than or equal to 1. */
        else if ($arr[$i] == 0) 
        { 
            $max_ending_here = 1; 
            $min_ending_here = 1; 
        } 
  
        /* If element is negative. This 
        is tricky max_ending_here can 
        either be 1 or positive.  
        min_ending_here can either be 1 or 
        negative. next min_ending_here will 
        always be prev. max_ending_here *  
        arr[i] next max_ending_here will be 
        1 if prev min_ending_here is 1, 
        otherwise next max_ending_here will 
        be prev min_ending_here * arr[i] */
        else
        { 
            $temp = $max_ending_here; 
            $max_ending_here = 
                max ($min_ending_here
                        * $arr[$i], 1); 
                              
            $min_ending_here = 
                        $temp * $arr[$i]; 
        } 
  
        // update max_so_far, if needed 
        if ($max_so_far < $max_ending_here) 
            $max_so_far = $max_ending_here; 
    } 
  
    if($flag==0 && $max_so_far==1) return 0;  
    return $max_so_far; 
} 
  
// Driver Program to test above function 
    $arr = array(1, -2, -3, 0, 7, -8, -2); 
    $n = sizeof($arr) / sizeof($arr[0]); 
    echo("Maximum Sub array product is "); 
    echo (maxSubarrayProduct($arr, $n)); 
  
// This code is contributed by nitin mittal  
?> 
```

输出：

```
Maximum Sub array product is 112
```
时间复杂度：`O(n)`。

辅助空间：`O(1)`。