# 每个数组元素的最小绝对差之和

> 原文： [https://www.geeksforgeeks.org/sum-minimum-absolute-difference-array-element/](https://www.geeksforgeeks.org/sum-minimum-absolute-difference-array-element/)

给定`n`个不同整数的数组。 问题是找到每个数组元素的最小绝对差之和。 对于数组中索引为`i`的元素`x`，其最小绝对差的计算公式如下：

**最小绝对差**`minAbsDiff(x) = min(abs(x – arr[j]))`，其中`1 <= j <= n`且`j != i`，`abs`是绝对值。

**输入约束**： `2 <= n`。

例子：

```
Input : arr = {4, 1, 5}
Output : 5
Sum of absolute differences is |4-5| + |1-4| + |5-4|

Input : arr = {5, 10, 1, 4, 8, 7}
Output : 9

Input : {12, 10, 15, 22, 21, 20, 1, 8, 9}
Output : 18

```



**朴素的方法**：使用两个循环。 使用外循环选择一个数组元素，并使用内循环计算与其余数组元素的绝对差。 找到最小绝对值并将其添加到总和中。 时间复杂度 `O(n^2)`。

**有效方法**：以下步骤是：

1.  对大小为`n`的数组进行排序。

2.  对于数组的**第一个**元素，其最小绝对差是使用第二数组元素计算的。

3.  对于**最后一个**数组元素，其最小绝对差是使用倒数第二个数组元素计算的。

4.  对于其余数组元素`1 <= i <= n-2`，索引为`i`的元素的最小绝对差计算为：`minAbsDiff = min(abs(arr[i] – arr[i-1]), abs(ar[i] – arr[i + 1]))`。

## C++ 

```cpp

// C++ implementation to find the sum of minimum  
// absolute difference of each array element 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the sum of  
// minimum absolute difference 
int sumOfMinAbsDifferences(int arr[], int n) 
{ 
    // sort the given array 
    sort(arr, arr+n); 

    // initialize sum 
    int sum = 0; 

    // min absolute difference for 
    // the 1st array element 
    sum += abs(arr[0] - arr[1]); 

    // min absolute difference for 
    // the last array element 
    sum += abs(arr[n-1] - arr[n-2]); 

    // find min absolute difference for rest of the 
    // array elements and add them to sum 
    for (int i=1; i<n-1; i++) 
        sum += min(abs(arr[i] - arr[i-1]), abs(arr[i] - arr[i+1])); 

    // required sum     
    return sum;     
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = {5, 10, 1, 4, 8, 7}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Sum = "
         << sumOfMinAbsDifferences(arr, n); 
}  

```

## Java

```java

// java implementation to find the sum 
// of minimum absolute difference of 
// each array element 
import java.*; 
import java.util.Arrays; 

public class GFG { 

    // function to find the sum of  
    // minimum absolute difference 
    static int sumOfMinAbsDifferences( 
                         int arr[] ,int n) 
    { 

        // sort the given array 
        Arrays.sort(arr); 

        // initialize sum 
        int sum = 0; 

        // min absolute difference for 
        // the 1st array element 
        sum += Math.abs(arr[0] - arr[1]); 

        // min absolute difference for 
        // the last array element 
        sum += Math.abs(arr[n-1] - arr[n-2]); 

        // find min absolute difference for 
        // rest of the array elements and  
        // add them to sum 
        for (int i = 1; i < n - 1; i++) 
            sum +=  
            Math.min(Math.abs(arr[i] - arr[i-1]), 
                    Math.abs(arr[i] - arr[i+1])); 

        // required sum  
        return sum;  
    }      

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = {5, 10, 1, 4, 8, 7}; 
        int n = arr.length; 

        System.out.println( "Sum = "
        + sumOfMinAbsDifferences(arr, n)); 
    } 
} 

// This code is contributed by Sam007\. 

```

## Python3

```py

# Python implementation to find the  
# sum of minimum absolute difference  
# of each array element 

# function to find the sum of  
# minimum absolute difference 

def sumOfMinAbsDifferences(arr,n): 
    # sort the given array 
    arr.sort() 
    # initialize sum 
    sum = 0

    # min absolute difference for 
    # the 1st array element 
    sum += abs(arr[0] - arr[1]); 

    # min absolute difference for 
    # the last array element 
    sum += abs(arr[n - 1] - arr[n - 2]); 

    # find min absolute difference for 
    # rest of the array elements and 
    # add them to sum 
    for i in range(1, n - 1): 
        sum += min(abs(arr[i] - arr[i - 1]),  
                  abs(arr[i] - arr[i + 1])) 

    # required sum  
    return sum;  

# Driver code 
arr = [5, 10, 1, 4, 8, 7] 
n = len(arr) 
print( "Sum = ", sumOfMinAbsDifferences(arr, n)) 

#This code is contributed by Sam007 

```

## C# 

```cs

// C# implementation to find the sum 
// of minimum absolute difference of 
// each array element 
using System; 

public class GFG { 

    // function to find the sum of  
    // minimum absolute difference 
    static int sumOfMinAbsDifferences( 
                         int []arr ,int n) 
    { 

        // sort the given array 
        Array.Sort(arr); 

        // initialize sum 
        int sum = 0; 

        // min absolute difference for 
        // the 1st array element 
        sum += Math.Abs(arr[0] - arr[1]); 

        // min absolute difference for 
        // the last array element 
        sum += Math.Abs(arr[n-1] - arr[n-2]); 

        // find min absolute difference for 
        // rest of the array elements and 
        // add them to sum 
        for (int i = 1; i < n - 1; i++) 
            sum +=  
            Math.Min(Math.Abs(arr[i] - arr[i-1]), 
                    Math.Abs(arr[i] - arr[i+1])); 

        // required sum  
        return sum;  
    }      

    // Driver code 
    public static void Main () 
    { 
        int []arr = {5, 10, 1, 4, 8, 7}; 
        int n = arr.Length; 

        Console.Write( "Sum = "
        + sumOfMinAbsDifferences(arr, n)); 
    } 
} 

// This code is contributed by Sam007\. 

```

## PHP

```php

<?php 
// PHP implementation to find 
// the sum of minimum absolute 
// difference of each array element 

// function to find the sum of  
// minimum absolute difference 
function sumOfMinAbsDifferences($arr, $n) 
{ 

    // sort the given array 
    sort($arr); 
    sort( $arr,$n); 

    // initialize sum 
    $sum = 0; 

    // min absolute difference for 
    // the 1st array element 
    $sum += abs($arr[0] - $arr[1]); 

    // min absolute difference for 
    // the last array element 
    $sum += abs($arr[$n - 1] - $arr[$n - 2]); 

    // find min absolute difference 
    // for rest of the array elements 
    // and add them to sum 
    for ($i = 1; $i < $n - 1; $i++) 
        $sum += min(abs($arr[$i] - $arr[$i - 1]),  
                   abs($arr[$i] - $arr[$i + 1])); 

    // required sum  
    return $sum;  
} 

    // Driver Code 
    $arr = array(5, 10, 1, 4, 8, 7); 
    $n = sizeof($arr); 
    echo "Sum = ", sumOfMinAbsDifferences($arr, $n); 

// This code is contributed by nitin mittal. 
?> 

```

输出：

```
Sum = 9

```

时间复杂度：`O(nLogn)`。

