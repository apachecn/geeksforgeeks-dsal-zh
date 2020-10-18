# 最大循环子数组总和

> 原文： [https://www.geeksforgeeks.org/maximum-contiguous-circular-sum/](https://www.geeksforgeeks.org/maximum-contiguous-circular-sum/)

给定`n`个数字（`+ve`和`-ve`），它们排列成一个圆圈，找出连续数字的最大和。

例子：

```
Input: a[] = {8, -8, 9, -9, 10, -11, 12}
Output: 22 (12 + 8 - 8 + 9 - 9 + 10)

Input: a[] = {10, -3, -4, 7, 6, 5, -4, -1} 
Output:  23 (7 + 6 + 5 - 4 -1 + 10) 

Input: a[] = {-1, 40, -14, 7, 6, 5, -4, -1}
Output: 52 (7 + 6 + 5 - 4 - 1 - 1 + 40)
```



最大和可以有两种情况：

**情况 1**：排列有助于最大和的元素，使其中不存在换行。 示例：`{-10, 2, -1, 5}`，`{-2, 4, -1, 4, -1}`。 在这种情况下， [Kadane 的算法](https://www.geeksforgeeks.org/archives/576)将产生结果。

**情况 2**：排列有助于最大和的元素，使其位于其中。 示例：`{10, -12, 11}`，`{12, -5, 4, -8, 11}`。 在这种情况下，我们将换行更改为不换行。 让我们看看如何。 包装有贡献的元素意味着不包装无贡献的元素，因此请找出无贡献的元素的总和，然后从总和中减去该总和。 要找出无贡献的总和，请反转每个元素的符号，然后运行 Kadane 的算法。

我们的数组就像一个圆环，我们必须消除最大连续负值，这意味着倒置数组中的最大连续正值。

最后，我们比较两种情况下获得的总和，并返回两个总和的最大值。

感谢 ashishdey0 建议这种解决方案。 以下是上述方法的 C/C++ ，Java 和 Python 实现。

## C++ 

```cpp

// C++ program for maximum contiguous circular sum problem  
#include <bits/stdc++.h> 
using namespace std; 

// Standard Kadane's algorithm to  
// find maximum subarray sum  
int kadane(int a[], int n);  

// The function returns maximum  
// circular contiguous sum in a[]  
int maxCircularSum(int a[], int n)  
{  
    // Case 1: get the maximum sum using standard kadane'  
    // s algorithm  
    int max_kadane = kadane(a, n);  

    // Case 2: Now find the maximum sum that includes  
    // corner elements.  
    int max_wrap = 0, i;  
    for (i = 0; i < n; i++)  
    {  
            max_wrap += a[i]; // Calculate array-sum  
            a[i] = -a[i]; // invert the array (change sign)  
    }  

    // max sum with corner elements will be:  
    // array-sum - (-max subarray sum of inverted array)  
    max_wrap = max_wrap + kadane(a, n);  

    // The maximum circular sum will be maximum of two sums  
    return (max_wrap > max_kadane)? max_wrap: max_kadane;  
}  

// Standard Kadane's algorithm to find maximum subarray sum  
// See https://www.geeksforgeeks.org/archives/576 for details  
int kadane(int a[], int n)  
{  
    int max_so_far = 0, max_ending_here = 0;  
    int i;  
    for (i = 0; i < n; i++)  
    {  
        max_ending_here = max_ending_here + a[i];  
        if (max_ending_here < 0)  
            max_ending_here = 0;  
        if (max_so_far < max_ending_here)  
            max_so_far = max_ending_here;  
    }  
    return max_so_far;  
}  

/* Driver program to test maxCircularSum() */
int main()  
{  
    int a[] = {11, 10, -20, 5, -3, -5, 8, -13, 10};  
    int n = sizeof(a)/sizeof(a[0]);  
    cout << "Maximum circular sum is " << maxCircularSum(a, n) << endl;  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c
// C program for maximum contiguous circular sum problem 
#include <stdio.h> 
  
// Standard Kadane's algorithm to find maximum subarray 
// sum 
int kadane(int a[], int n); 
  
// The function returns maximum circular contiguous sum 
// in a[] 
int maxCircularSum(int a[], int n) 
{ 
    // Case 1: get the maximum sum using standard kadane' 
    // s algorithm 
    int max_kadane = kadane(a, n); 
  
    // Case 2: Now find the maximum sum that includes 
    // corner elements. 
    int max_wrap = 0, i; 
    for (i = 0; i < n; i++) { 
        max_wrap += a[i]; // Calculate array-sum 
        a[i] = -a[i]; // invert the array (change sign) 
    } 
  
    // max sum with corner elements will be: 
    // array-sum - (-max subarray sum of inverted array) 
    max_wrap = max_wrap + kadane(a, n); 
  
    // The maximum circular sum will be maximum of two sums 
    return (max_wrap > max_kadane) ? max_wrap : max_kadane; 
} 
  
// Standard Kadane's algorithm to find maximum subarray sum 
// See https:// www.geeksforgeeks.org/archives/576 for details 
int kadane(int a[], int n) 
{ 
    int max_so_far = 0, max_ending_here = 0; 
    int i; 
    for (i = 0; i < n; i++) { 
        max_ending_here = max_ending_here + a[i]; 
        if (max_ending_here < 0) 
            max_ending_here = 0; 
        if (max_so_far < max_ending_here) 
            max_so_far = max_ending_here; 
    } 
    return max_so_far; 
} 
  
/* Driver program to test maxCircularSum() */
int main() 
{ 
    int a[] = { 11, 10, -20, 5, -3, -5, 8, -13, 10 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    printf("Maximum circular sum is %dn", 
           maxCircularSum(a, n)); 
    return 0; 
} 
```

## Java

```java
// Java program for maximum contiguous circular sum problem 
import java.io.*; 
import java.util.*; 
  
class MaxCircularSum { 
    // The function returns maximum circular contiguous sum 
    // in a[] 
    static int maxCircularSum(int a[]) 
    { 
        int n = a.length; 
  
        // Case 1: get the maximum sum using standard kadane' 
        // s algorithm 
        int max_kadane = kadane(a); 
  
        // Case 2: Now find the maximum sum that includes 
        // corner elements. 
        int max_wrap = 0; 
        for (int i = 0; i < n; i++) { 
            max_wrap += a[i]; // Calculate array-sum 
            a[i] = -a[i]; // invert the array (change sign) 
        } 
  
        // max sum with corner elements will be: 
        // array-sum - (-max subarray sum of inverted array) 
        max_wrap = max_wrap + kadane(a); 
  
        // The maximum circular sum will be maximum of two sums 
        return (max_wrap > max_kadane) ? max_wrap : max_kadane; 
    } 
  
    // Standard Kadane's algorithm to find maximum subarray sum 
    // See https:// www.geeksforgeeks.org/archives/576 for details 
    static int kadane(int a[]) 
    { 
        int n = a.length; 
        int max_so_far = 0, max_ending_here = 0; 
        for (int i = 0; i < n; i++) { 
            max_ending_here = max_ending_here + a[i]; 
            if (max_ending_here < 0) 
                max_ending_here = 0; 
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 
        } 
        return max_so_far; 
    } 
  
    public static void main(String[] args) 
    { 
        int a[] = { 11, 10, -20, 5, -3, -5, 8, -13, 10 }; 
        System.out.println("Maximum circular sum is " + maxCircularSum(a)); 
    } 
} /* This code is contributed by Devesh Agrawal*/
```

## Python

```py
# Python program for maximum contiguous circular sum problem 
  
# Standard Kadane's algorithm to find maximum subarray sum 
def kadane(a): 
    n = len(a) 
    max_so_far = 0
    max_ending_here = 0
    for i in range(0, n): 
        max_ending_here = max_ending_here + a[i] 
        if (max_ending_here < 0): 
            max_ending_here = 0
        if (max_so_far < max_ending_here): 
            max_so_far = max_ending_here 
    return max_so_far 
  
# The function returns maximum circular contiguous sum in 
# a[] 
def maxCircularSum(a): 
  
    n = len(a) 
  
    # Case 1: get the maximum sum using standard kadane's 
    # algorithm 
    max_kadane = kadane(a) 
  
    # Case 2: Now find the maximum sum that includes corner 
    # elements. 
    max_wrap = 0
    for i in range(0, n): 
        max_wrap += a[i] 
        a[i] = -a[i] 
  
    # Max sum with corner elements will be: 
    # array-sum - (-max subarray sum of inverted array) 
    max_wrap = max_wrap + kadane(a) 
  
    # The maximum circular sum will be maximum of two sums 
    if max_wrap > max_kadane: 
        return max_wrap 
    else: 
        return max_kadane 
  
# Driver function to test above function 
a = [11, 10, -20, 5, -3, -5, 8, -13, 10] 
print "Maximum circular sum is", maxCircularSum(a) 
  
# This code is contributed by Devesh Agrawal 
```

## C#

```cs
// C# program for maximum contiguous 
// circular sum problem 
using System; 
  
class MaxCircularSum { 
  
    // The function returns maximum circular 
    // contiguous sum in a[] 
    static int maxCircularSum(int[] a) 
    { 
        int n = a.Length; 
  
        // Case 1: get the maximum sum using standard kadane' 
        // s algorithm 
        int max_kadane = kadane(a); 
  
        // Case 2: Now find the maximum sum that includes 
        // corner elements. 
        int max_wrap = 0; 
        for (int i = 0; i < n; i++) { 
            max_wrap += a[i]; // Calculate array-sum 
            a[i] = -a[i]; // invert the array (change sign) 
        } 
  
        // max sum with corner elements will be: 
        // array-sum - (-max subarray sum of inverted array) 
        max_wrap = max_wrap + kadane(a); 
  
        // The maximum circular sum will be maximum of two sums 
        return (max_wrap > max_kadane) ? max_wrap : max_kadane; 
    } 
  
    // Standard Kadane's algorithm to find maximum subarray sum 
    // See https:// www.geeksforgeeks.org/archives/576 for details 
    static int kadane(int[] a) 
    { 
        int n = a.Length; 
        int max_so_far = 0, max_ending_here = 0; 
        for (int i = 0; i < n; i++) { 
            max_ending_here = max_ending_here + a[i]; 
            if (max_ending_here < 0) 
                max_ending_here = 0; 
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 
        } 
        return max_so_far; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] a = { 11, 10, -20, 5, -3, -5, 8, -13, 10 }; 
  
        Console.Write("Maximum circular sum is " + maxCircularSum(a)); 
    } 
} 
  
/* This code is contributed by vt_m*/
```

## PHP

```php
<?php 
  
// PHP program for maximum  
// contiguous circular sum problem  
  
// The function returns maximum  
// circular contiguous sum $a[]  
function maxCircularSum($a, $n)  
{  
    // Case 1: get the maximum sum  
    // using standard kadane' s algorithm  
    $max_kadane = kadane($a, $n);  
      
    // Case 2: Now find the maximum   
    // sum that includes corner elements.  
    $max_wrap = 0; 
    for ($i = 0; $i < $n; $i++)  
    {  
            $max_wrap += $a[$i]; // Calculate array-sum  
            $a[$i] = -$a[$i]; // invert the array (change sign)  
    }  
      
    // max sum with corner elements will be:  
    // array-sum - (-max subarray sum of inverted array)  
    $max_wrap = $max_wrap + kadane($a, $n);  
      
    // The maximum circular sum will be maximum of two sums  
    return ($max_wrap > $max_kadane)? $max_wrap: $max_kadane;  
}  
  
// Standard Kadane's algorithm to  
// find maximum subarray sum  
// See https://www.geeksforgeeks.org/archives/576 for details  
function kadane($a, $n)  
{  
    $max_so_far = 0; 
    $max_ending_here = 0;  
    for ($i = 0; $i < $n; $i++)  
    {  
        $max_ending_here = $max_ending_here +$a[$i];  
        if ($max_ending_here < 0)  
            $max_ending_here = 0;  
        if ($max_so_far < $max_ending_here)  
            $max_so_far = $max_ending_here;  
    }  
    return $max_so_far;  
}  
  
    /* Driver code */
    $a = array(11, 10, -20, 5, -3, -5, 8, -13, 10);  
    $n = count($a); 
    echo "Maximum circular sum is ". maxCircularSum($a, $n);  
  
// This code is contributed by rathbhupendra 
?> 
```

输出：

```
Maximum circular sum is 31
```

复杂度分析：

时间复杂度：`O(n)`，其中·是输入数组中元素的数量。

由于仅需要数组的线性遍历。

辅助空间：`O(1)`。

由于不需要额外的空间。

请注意，如果所有数字均为负数，例如`{-1, -2, -3}`，则上述算法无效。 在这种情况下，它返回 0。 在运行上述算法之前，可以通过添加预检查以查看所有数字是否均为负来处理这种情况。

方法二：

方法：在这种方法中，修改 Kadane 的算法，以找到最小连续子数组和和最大连续子数组和，然后检查`max_value`和从总和中减去`min_value`之后剩下的值中的最大值。

算法：

我们将计算给定数组的总和。

+   我们将变量`curr_max`，`max_so_far`，`curr_min`，`min_so_far`声明为数组的第一个值。

+   现在，我们将使用 Kadane 的算法来找到最大子数组和和最小子数组和。

+   检查数组中的所有值：

    +   如果`min_so_far`等于和，即所有值均为负，则返回max_so_far。

    +   否则，我们将计算`max_so_far`和`sum – min_so_far`的最大值并将其返回。

下面给出上述方法的 C++ 实现。

## C++

```cpp
// C++ program for maximum contiguous circular sum problem 
#include <bits/stdc++.h> 
using namespace std; 
  
// The function returns maximum 
// circular contiguous sum in a[] 
int maxCircularSum(int a[], int n) 
{ 
    // Corner Case 
    if (n == 1) 
        return a[0]; 
  
    // Initialize sum variable which store total sum of the array. 
    int sum = 0; 
    for (int i = 0; i < n; i++) { 
        sum += a[i]; 
    } 
  
    // Initialize every variable with first value of array. 
    int curr_max = a[0], max_so_far = a[0], curr_min = a[0], min_so_far = a[0]; 
  
    // Concept of Kadane's Algorithm 
    for (int i = 1; i < n; i++) { 
        // Kadane's Algorithm to find Maximum subarray sum. 
        curr_max = max(curr_max + a[i], a[i]); 
        max_so_far = max(max_so_far, curr_max); 
  
        // Kadane's Algorithm to find Minimum subarray sum. 
        curr_min = min(curr_min + a[i], a[i]); 
        min_so_far = min(min_so_far, curr_min); 
    } 
  
    if (min_so_far == sum) 
        return max_so_far; 
  
    // returning the maximum value 
    return max(max_so_far, sum - min_so_far); 
} 
  
/* Driver program to test maxCircularSum() */
int main() 
{ 
    int a[] = { 11, 10, -20, 5, -3, -5, 8, -13, 10 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << "Maximum circular sum is " << maxCircularSum(a, n) << endl; 
    return 0; 
} 
```

输出：

```
Maximum circular sum is 31
```

复杂度分析：

时间复杂度：`O(n)`，其中·是输入数组中元素的数量。

由于仅需要数组的线性遍历。

辅助空间：`O(1)`。

由于不需要额外的空间。