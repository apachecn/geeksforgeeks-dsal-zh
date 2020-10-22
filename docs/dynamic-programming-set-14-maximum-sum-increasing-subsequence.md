# 最大总和增加子序列| DP-14

> 原文： [https://www.geeksforgeeks.org/dynamic-programming-set-14-maximum-sum-increasing-subsequence/](https://www.geeksforgeeks.org/dynamic-programming-set-14-maximum-sum-increasing-subsequence/)

给定`n`个正整数数组。 编写程序以查找给定数组的最大和子序列的总和，以使子序列中的整数按升序排序。 例如，如果输入为`{1, 101, 2, 3, 100, 4, 5}`，则输出应为`106 (1 + 2 + 3 + 100)`；如果输入数组为`{3, 4, 5, 10}`，则输出应为`22 (3 + 4 + 5 + 10)`，如果输入数组为`{10, 5, 4, 3}`，则输出应为 10。



**解决方案**：

此问题是标准[最长子序列（LIS）问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的变体。 我们需要对 [LIS 问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的动态规划解决方案进行一些更改。 我们需要更改的只是使用总和作为标准，而不是增加子序列的长度。

以下是该问题的动态规划解决方案：

## C++ 

```cpp

/* Dynamic Programming implementation  
of Maximum Sum Increasing Subsequence  
(MSIS) problem */
#include <bits/stdc++.h> 
using namespace std; 

/* maxSumIS() returns the maximum  
sum of increasing subsequence  
in arr[] of size n */
int maxSumIS(int arr[], int n)  
{  
    int i, j, max = 0;  
    int msis[n];  

    /* Initialize msis values  
    for all indexes */
    for ( i = 0; i < n; i++ )  
        msis[i] = arr[i];  

    /* Compute maximum sum values  
    in bottom up manner */
    for ( i = 1; i < n; i++ )  
        for ( j = 0; j < i; j++ )  
            if (arr[i] > arr[j] &&  
                msis[i] < msis[j] + arr[i])  
                msis[i] = msis[j] + arr[i];  

    /* Pick maximum of  
    all msis values */
    for ( i = 0; i < n; i++ )  
        if ( max < msis[i] )  
            max = msis[i];  

    return max;  
}  

// Driver Code  
int main()  
{  
    int arr[] = {1, 101, 2, 3, 100, 4, 5};  
    int n = sizeof(arr)/sizeof(arr[0]);  
    cout << "Sum of maximum sum increasing "
            "subsequence is " << maxSumIS( arr, n ) << endl;  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## Java

```java
/* Dynamic Programming Java  
   implementation of Maximum Sum 
   Increasing Subsequence (MSIS) 
   problem */
class GFG 
{ 
    /* maxSumIS() returns the  
    maximum sum of increasing 
    subsequence in arr[] of size n */
    static int maxSumIS(int arr[], int n) 
    { 
        int i, j, max = 0; 
        int msis[] = new int[n]; 
  
        /* Initialize msis values  
           for all indexes */
        for (i = 0; i < n; i++) 
            msis[i] = arr[i]; 
  
        /* Compute maximum sum values 
           in bottom up manner */
        for (i = 1; i < n; i++) 
            for (j = 0; j < i; j++) 
                if (arr[i] > arr[j] && 
                    msis[i] < msis[j] + arr[i]) 
                    msis[i] = msis[j] + arr[i]; 
  
        /* Pick maximum of all 
           msis values */
        for (i = 0; i < n; i++) 
            if (max < msis[i]) 
                max = msis[i]; 
  
        return max; 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = new int[]{1, 101, 2, 3, 100, 4, 5}; 
        int n = arr.length; 
        System.out.println("Sum of maximum sum "+ 
                            "increasing subsequence is "+ 
                              maxSumIS(arr, n)); 
    } 
} 
  
// This code is contributed  
// by Rajat Mishra
```

## Python

```py
# Dynamic Programming bsed Python  
# implementation of Maximum Sum  
# Increasing Subsequence (MSIS) 
# problem 
  
# maxSumIS() returns the maximum  
# sum of increasing subsequence  
# in arr[] of size n 
def maxSumIS(arr, n): 
    max = 0
    msis = [0 for x in range(n)] 
  
    # Initialize msis values 
    # for all indexes 
    for i in range(n): 
        msis[i] = arr[i] 
  
    # Compute maximum sum  
    # values in bottom up manner 
    for i in range(1, n): 
        for j in range(i): 
            if (arr[i] > arr[j] and
                msis[i] < msis[j] + arr[i]): 
                msis[i] = msis[j] + arr[i] 
  
    # Pick maximum of 
    # all msis values 
    for i in range(n): 
        if max < msis[i]: 
            max = msis[i] 
  
    return max
  
# Driver Code 
arr = [1, 101, 2, 3, 100, 4, 5] 
n = len(arr) 
print("Sum of maximum sum increasing " + 
                     "subsequence is " +
                  str(maxSumIS(arr, n))) 
  
# This code is contributed  
# by Bhavya Jain
```

## C#

```cs
// Dynamic Programming C# implementation 
// of Maximum Sum Increasing Subsequence 
// (MSIS) problem  
using System; 
class GFG { 
      
    // maxSumIS() returns the  
    // maximum sum of increasing 
    // subsequence in arr[] of size n  
    static int maxSumIS( int []arr, int n ) 
    { 
        int i, j, max = 0; 
        int []msis = new int[n]; 
  
        /* Initialize msis values 
           for all indexes */
        for ( i = 0; i < n; i++ ) 
            msis[i] = arr[i]; 
  
        /* Compute maximum sum values 
           in bottom up manner */
        for ( i = 1; i < n; i++ ) 
            for ( j = 0; j < i; j++ ) 
                if ( arr[i] > arr[j] && 
                    msis[i] < msis[j] + arr[i]) 
                    msis[i] = msis[j] + arr[i]; 
  
        /* Pick maximum of all  
           msis values */
        for ( i = 0; i < n; i++ ) 
            if ( max < msis[i] ) 
                max = msis[i]; 
  
        return max; 
    } 
      
    // Driver Code 
    public static void Main() 
    { 
        int []arr = new int[]{1, 101, 2, 3, 100, 4, 5}; 
        int n = arr.Length; 
        Console.WriteLine("Sum of maximum sum increasing "+ 
                                        " subsequence is "+ 
        maxSumIS(arr, n)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// Dynamic Programming implementation 
// of Maximum Sum Increasing 
// Subsequence (MSIS) problem  
  
// maxSumIS() returns the maximum  
// sum of increasing subsequence 
// in arr[] of size n  
function maxSumIS($arr, $n) 
{ 
    $max = 0; 
    $msis= array($n); 
  
    // Initialize msis values 
    // for all indexes  
    for($i = 0; $i < $n; $i++ ) 
        $msis[$i] = $arr[$i]; 
  
    // Compute maximum sum values 
    // in bottom up manner  
    for($i = 1; $i < $n; $i++) 
        for($j = 0; $j < $i; $j++) 
            if ($arr[$i] > $arr[$j] &&  
                $msis[$i] < $msis[$j] + $arr[$i]) 
                $msis[$i] = $msis[$j] + $arr[$i]; 
  
    // Pick maximum of all msis values 
    for($i = 0;$i < $n; $i++ ) 
        if ($max < $msis[$i] ) 
            $max = $msis[$i]; 
  
    return $max; 
} 
  
    // Driver Code 
    $arr = array(1, 101, 2, 3, 100, 4, 5); 
    $n = count($arr); 
    echo "Sum of maximum sum increasing subsequence is " 
                                   .maxSumIS( $arr, $n ); 
          
// This code is contributed by Sam007 
?>
```

输出：

```
Sum of maximum sum increasing subsequence is 106
```

时间复杂度：`O(n^2)`。

