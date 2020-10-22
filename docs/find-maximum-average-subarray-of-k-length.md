# 查找`k`个长度的最大平均子数组

> 原文： [https://www.geeksforgeeks.org/find-maximum-average-subarray-of-k-length/](https://www.geeksforgeeks.org/find-maximum-average-subarray-of-k-length/)

给定具有正数和负数的数组，请找到给定长度的最大平均子数组。

例：

```
Input:  arr[] = {1, 12, -5, -6, 50, 3}, k = 4
Output: Maximum average subarray of length 4 begins
        at index 1.
Maximum average is (12 - 5 - 6 + 50)/4 = 51/4

```



一个**简单解决方案**是运行两个循环。 外循环选择起始点，内循环从起始点开始直到长度`k`，然后计算元素的平均值。 该解决方案的时间复杂度为`O(n * k)`。

**更好的解决方案**是创建大小为`n`的辅助数组。 将元素的累积和存储在此数组中。 令数组为`csum[]`。 `csum[i]`存储从`arr[0]`到`arr[i]`的元素之和。 一旦有了`csum[]`数组，就可以在`O(1)`时间中计算两个索引之间的和。

以下是此想法的实现。 一个观察是，给定长度的子数组如果具有最大和，则具有最大平均值。 因此我们可以通过比较和来避免浮点运算。

## CPP

```

// C++ program to find maximum average subarray 
// of given length. 
#include<bits/stdc++.h> 
using namespace std; 

// Returns beginning index of maximum average 
// subarray of length 'k' 
int findMaxAverage(int arr[], int n, int k) 
{ 
    // Check if 'k' is valid 
    if (k > n) 
        return -1; 

    // Create and fill array to store cumulative 
    // sum. csum[i] stores sum of arr[0] to arr[i] 
    int *csum = new int[n]; 
    csum[0] = arr[0]; 
    for (int i=1; i<n; i++) 
       csum[i] = csum[i-1] + arr[i]; 

    // Initialize max_sm as sum of first subarray 
    int max_sum = csum[k-1], max_end = k-1; 

    // Find sum of other subarrays and update 
    // max_sum if required. 
    for (int i=k; i<n; i++) 
    { 
        int curr_sum = csum[i] - csum[i-k]; 
        if (curr_sum > max_sum) 
        { 
            max_sum = curr_sum; 
            max_end = i; 
        } 
    } 

    delete [] csum; // To avoid memory leak 

    // Return starting index 
    return max_end - k + 1; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {1, 12, -5, -6, 50, 3}; 
    int k = 4; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "The maximum average subarray of "
         "length "<< k << " begins at index "
         << findMaxAverage(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find maximum average 
// subarray of given length. 
import java .io.*; 

class GFG { 

    // Returns beginning index  
    // of maximum average 
    // subarray of length 'k' 
    static int findMaxAverage(int []arr,  
                           int n, int k) 
    { 

        // Check if 'k' is valid 
        if (k > n) 
            return -1; 

        // Create and fill array  
        // to store cumulative 
        // sum. csum[i] stores  
        // sum of arr[0] to arr[i] 
        int []csum = new int[n]; 

        csum[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
        csum[i] = csum[i - 1] + arr[i]; 

        // Initialize max_sm as  
        // sum of first subarray 
        int max_sum = csum[k - 1],  
                    max_end = k - 1; 

        // Find sum of other  
        // subarrays and update 
        // max_sum if required. 
        for (int i = k; i < n; i++) 
        { 
            int curr_sum = csum[i] -  
                    csum[i - k]; 
            if (curr_sum > max_sum) 
            { 
                max_sum = curr_sum; 
                max_end = i; 
            } 
        } 

        // To avoid memory leak 
        //delete [] csum;  

        // Return starting index 
        return max_end - k + 1; 
    } 

    // Driver Code 
    static public void main (String[] args) 
    { 
        int []arr = {1, 12, -5, -6, 50, 3}; 
        int k = 4; 
        int n = arr.length; 

        System.out.println("The maximum "
          + "average subarray of length "
                + k + " begins at index "
            + findMaxAverage(arr, n, k)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## C# 

```cs

// C# program to find maximum average 
// subarray of given length. 
using System; 
class GFG{ 

// Returns beginning index  
// of maximum average 
// subarray of length 'k' 
static int findMaxAverage(int []arr,  
                       int n, int k) 
{ 

    // Check if 'k' is valid 
    if (k > n) 
        return -1; 

    // Create and fill array  
    // to store cumulative 
    // sum. csum[i] stores  
    // sum of arr[0] to arr[i] 
    int []csum = new int[n]; 

    csum[0] = arr[0]; 
    for (int i = 1; i < n; i++) 
    csum[i] = csum[i - 1] + arr[i]; 

    // Initialize max_sm as  
    // sum of first subarray 
    int max_sum = csum[k - 1],  
              max_end = k - 1; 

    // Find sum of other  
    // subarrays and update 
    // max_sum if required. 
    for (int i = k; i < n; i++) 
    { 
        int curr_sum = csum[i] -  
                   csum[i - k]; 
        if (curr_sum > max_sum) 
        { 
            max_sum = curr_sum; 
            max_end = i; 
        } 
    } 

    // To avoid memory leak 
    //delete [] csum;  

    // Return starting index 
    return max_end - k + 1; 
} 

    // Driver Code 
    static public void Main () 
    { 
        int []arr = {1, 12, -5, -6, 50, 3}; 
        int k = 4; 
        int n = arr.Length; 
        Console.WriteLine("The maximum average subarray of "+ 
                            "length "+ k + " begins at index "
                                    + findMaxAverage(arr, n, k)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## Python3

```py

# Python program to find maximum average subarray 
# of given length. 

# Returns beginning index of maximum average 
# subarray of length 'k' 
def findMaxAverage(arr, n, k): 
    # Check if 'k' is valid 
    if k > n: 
        return -1

    # Create and fill array to store cumulative 
    # sum. csum[i] stores sum of arr[0] to arr[i] 
    csum = [0]*n 
    csum[0] = arr[0] 
    for i in range(1, n): 
        csum[i] = csum[i-1] + arr[i]; 

    # Initialize max_sm as sum of first subarray 
    max_sum = csum[k-1] 
    max_end = k-1

    # Find sum of other subarrays and update 
    # max_sum if required. 
    for i in range(k, n): 

        curr_sum = csum[i] - csum[i-k] 
        if curr_sum > max_sum: 

            max_sum = curr_sum 
            max_end = i 

    # Return starting index 
    return max_end - k + 1

# Driver program 
arr = [1, 12, -5, -6, 50, 3] 
k = 4
n = len(arr) 
print("The maximum average subarray of length",k, 
"begins at index",findMaxAverage(arr, n, k)) 

#This code is contributed by 
#Smitha Dinesh Semwal 

```

## PHP

```php

<?php 
// PHP program to find maximum 
// average subarray of given length. 

// Returns beginning index of 
// maximum average subarray of  
// length 'k' 
function findMaxAverage($arr, $n, $k) 
{ 

    // Check if 'k' is valid 
    if ($k > $n) 
        return -1; 

    // Create and fill array to 
    // store cumulative sum.  
    // csum[i] stores sum of  
    // arr[0] to arr[i] 
    $csum = array(); 
    $csum[0] = $arr[0]; 
    for($i = 1; $i < $n; $i++) 
    $csum[$i] = $csum[$i - 1] +  
                $arr[$i]; 

    // Initialize max_sm as sum 
    // of first subarray 
    $max_sum = $csum[$k - 1];  
    $max_end = $k - 1; 

    // Find sum of other subarrays  
    // and update max_sum if required. 
    for($i = $k; $i < $n; $i++) 
    { 
        $curr_sum = $csum[$i] -  
                    $csum[$i - $k]; 
        if ($curr_sum > $max_sum) 
        { 
            $max_sum = $curr_sum; 
            $max_end = $i; 
        } 
    } 

    // Return starting index 
    return $max_end - $k + 1; 
} 

    // Driver Code 
    $arr = array(1, 12, -5, -6, 50, 3); 
    $k = 4; 
    $n = count($arr); 
    echo "The maximum average subarray of "
        ,"length ", $k , " begins at index "
        , findMaxAverage($arr, $n, $k); 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
The maximum average subarray of length 4 begins at index 1
```

上述解决方案的时间复杂度为`O(n)`，但需要`O(n)`辅助空间。

通过使用以下**有效方法**，我们可以避免多余的空间。

1.  计算第一个`k`个元素的总和，即元素`arr[0..k-1]`。 将此总和设为`sum`。 将`max_sum`初始化为`sum`。

2.  对`i`从`k`到`n-1`的每个元素`arr[i]`执行以下操作：

    1.  从`sum`中删除`arr[ik]`并添加`arr[i]`，即`sum += arr[i] – arr[ik]`。

    2.  如果到目前为止新的总和大于`max_sum`，则更新`max_sum`。

3.  返回`max_sum`。

## CPP

```

// C++ program to find maximum average subarray 
// of given length. 
#include<bits/stdc++.h> 
using namespace std; 

// Returns beginning index of maximum average 
// subarray of length 'k' 
int findMaxAverage(int arr[], int n, int k) 
{ 
    // Check if 'k' is valid 
    if (k > n) 
        return -1; 

    // Compute sum of first 'k' elements 
    int sum = arr[0]; 
    for (int i=1; i<k; i++) 
        sum += arr[i]; 

    int max_sum = sum, max_end = k-1; 

    // Compute sum of remaining subarrays 
    for (int i=k; i<n; i++) 
    { 
        int sum = sum + arr[i] - arr[i-k]; 
        if (sum > max_sum) 
        { 
            max_sum = sum; 
            max_end = i; 
        } 
    } 

    // Return starting index 
    return max_end - k + 1; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {1, 12, -5, -6, 50, 3}; 
    int k = 4; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "The maximum average subarray of "
         "length "<< k << " begins at index "
         << findMaxAverage(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find maximum average subarray 
// of given length. 

import java.io.*; 

class GFG { 

    // Returns beginning index of maximum average 
    // subarray of length 'k' 
    static int findMaxAverage(int arr[], int n, int k) 
    { 

        // Check if 'k' is valid 
        if (k > n) 
            return -1; 

        // Compute sum of first 'k' elements 
        int sum = arr[0]; 
        for (int i = 1; i < k; i++) 
            sum += arr[i]; 

        int max_sum = sum, max_end = k-1; 

        // Compute sum of remaining subarrays 
        for (int i = k; i < n; i++) 
        { 
            sum = sum + arr[i] - arr[i-k]; 
            if (sum > max_sum) 
            { 
                max_sum = sum; 
                max_end = i; 
            } 
        } 

        // Return starting index 
        return max_end - k + 1; 
    } 

    // Driver program 
    public static void main (String[] args) 
    { 
        int arr[] = {1, 12, -5, -6, 50, 3}; 
        int k = 4; 
        int n = arr.length; 
        System.out.println( "The maximum average"
                     + " subarray of length " + k  
                     + " begins at index "
                    + findMaxAverage(arr, n, k)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## Python3

```py

# Python 3 program to find maximum 
# average subarray of given length. 

# Returns beginning index of maximum 
# average subarray of length 'k' 
def findMaxAverage(arr, n, k): 

    # Check if 'k' is valid 
    if (k > n): 
        return -1

    # Compute sum of first 'k' elements 
    sum = arr[0]  

    for i in range(1, k): 
        sum += arr[i]  

    max_sum = sum
    max_end = k - 1

    # Compute sum of remaining subarrays 
    for i in range(k, n): 

        sum = sum + arr[i] - arr[i - k]  

        if (sum > max_sum): 

            max_sum = sum
            max_end = i  

    # Return starting index 
    return max_end - k + 1

# Driver program 
arr = [1, 12, -5, -6, 50, 3]  
k = 4
n = len(arr)  

print("The maximum average subarray of length", k, 
                                "begins at index",  
                        findMaxAverage(arr, n, k)) 

# This code is contributed by 
# Smitha Dinesh Semwal 

```

## C#

```cs

// C# program to find maximum average  
// subarray of given length. 
using System; 

class GFG { 

    // Returns beginning index of  
    // maximum average subarray of 
    // length 'k' 
    static int findMaxAverage(int []arr, 
                           int n, int k) 
    { 

        // Check if 'k' is valid 
        if (k > n) 
            return -1; 

        // Compute sum of first 'k'  
        // elements 
        int sum = arr[0]; 
        for (int i = 1; i < k; i++) 
            sum += arr[i]; 

        int max_sum = sum; 
        int max_end = k-1; 

        // Compute sum of remaining  
        // subarrays 
        for (int i = k; i < n; i++) 
        { 
            sum = sum + arr[i] - arr[i-k]; 
            if (sum > max_sum) 
            { 
                max_sum = sum; 
                max_end = i; 
            } 
        } 

        // Return starting index 
        return max_end - k + 1; 
    } 

    // Driver program 
    public static void Main () 
    { 
        int []arr = {1, 12, -5, -6, 50, 3}; 
        int k = 4; 
        int n = arr.Length; 
        Console.WriteLine( "The maximum "
          + "average subarray of length "
                + k + " begins at index "
            + findMaxAverage(arr, n, k)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## PHP

```php

<?php 
// PHP program to find maximum 
// average subarray of given length. 

// Returns beginning index 
// of maximum average 
// subarray of length 'k' 
function findMaxAverage($arr, $n, $k) 
{ 

    // Check if 'k' is valid 
    if ($k > $n) 
        return -1; 

    // Compute sum of first 
    // 'k' elements 
    $sum = $arr[0]; 
    for($i = 1; $i < $k; $i++) 
        $sum += $arr[$i]; 

    $max_sum = $sum; 
    $max_end = $k-1; 

    // Compute sum of 
    // remaining subarrays 
    for($i = $k; $i < $n; $i++) 
    { 
        $sum = $sum + $arr[$i] -  
                 $arr[$i - $k]; 
        if ($sum > $max_sum) 
        { 
            $max_sum = $sum; 
            $max_end = $i; 
        } 
    } 

    // Return starting index 
    return $max_end - $k + 1; 
} 

    // Driver Code 
    $arr = array(1, 12, -5, -6, 50, 3); 
    $k = 4; 
    $n = count($arr); 
    echo "The maximum average subarray of ", 
         "length ", $k , " begins at index "
        , findMaxAverage($arr, $n, $k); 

// This code is contributed by anuj_67\. 
?> 

```

输出：

```
The maximum average subarray of length 4 begins at index 1
```

该方法的时间复杂度也是`O(n)`，但是它需要恒定的额外空间。

