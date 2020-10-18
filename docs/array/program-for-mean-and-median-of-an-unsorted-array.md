# 未排序数组的均值和中位数的程序

> 原文： [https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)

给定`n`大小的未排序数组，找到其均值和中位数。

```
数组的平均值 =（所有元素的总和）/（元素数量）
```

**大小为`n`的排序数组的中位数**，当`n`为奇数时定义为中间元素，而当`n`为偶数时定义为中间两个元素的平均值。

由于这里未对数组进行排序，因此我们首先对数组进行排序，然后应用上述公式。

**示例**：

```
Input  : a[] = {1, 3, 4, 2, 6, 5, 8, 7}
Output : Mean = 4.5
         Median = 4.5
Sum of the elements is 1 + 3 + 4 + 2 + 6 + 
5 + 8 + 7 = 36
Mean = 36/8 = 4.5
Since number of elements are even, median
is average of 4th and 5th largest elements.
which means (4 + 5)/2 = 4.5

Input  : a[] = {4, 4, 4, 4, 4}
Output : Mean = 4
         Median = 4 

```



下面是代码实现：

## C++ 

```cpp

// CPP program to find mean and median of  
// an array 
#include <bits/stdc++.h> 
using namespace std; 

// Function for calculating mean 
double findMean(int a[], int n) 
{ 
    int sum = 0; 
    for (int i = 0; i < n; i++)  
        sum += a[i]; 

    return (double)sum/(double)n; 
} 

// Function for calculating median 
double findMedian(int a[], int n) 
{ 
    // First we sort the array 
    sort(a, a+n); 

    // check for even case 
    if (n % 2 != 0) 
       return (double)a[n/2]; 

    return (double)(a[(n-1)/2] + a[n/2])/2.0; 
} 

// Driver program 
int main() 
{ 
    int a[] = { 1, 3, 4, 2, 7, 5, 8, 6 }; 
    int n = sizeof(a)/sizeof(a[0]); 
    cout << "Mean = " << findMean(a, n) << endl;  
    cout << "Median = " << findMedian(a, n) << endl;  
    return 0; 
} 

```

## Java

```java
// Java program to find mean
// and median of an array
import java.util.*;
 
class GFG 
{
    // Function for calculating mean
    public static double findMean(int a[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += a[i];
 
        return (double)sum / (double)n;
    }
 
    // Function for calculating median
    public static double findMedian(int a[], int n)
    {
        // First we sort the array
        Arrays.sort(a);
 
        // check for even case
        if (n % 2 != 0)
            return (double)a[n / 2];
 
        return (double)(a[(n - 1) / 2] + a[n / 2]) / 2.0;
    }
 
    // Driver code
    public static void main(String args[])
    {
        int a[] = { 1, 3, 4, 2, 7, 5, 8, 6 };
        int n = a.length;
       
        // Function call
        System.out.println("Mean = " + findMean(a, n));
        System.out.println("Median = " + findMedian(a, n));
    }
}
 
// This article is contributed by Anshika Goyal.
```

## Python3

```py
# Python3 program to find mean
# and median of an array
 
# Function for calculating mean
 
 
def findMean(a, n):
 
    sum = 0
    for i in range(0, n):
        sum += a[i]
 
    return float(sum/n)
 
# Function for calculating median
 
 
def findMedian(a, n):
 
    # First we sort the array
    sorted(a)
 
    # check for even case
    if n % 2 != 0:
        return float(a[int(n/2)])
 
    return float((a[int((n-1)/2)] +
                  a[int(n/2)])/2.0)
 
 
# Driver code
a = [1, 3, 4, 2, 7, 5, 8, 6]
n = len(a)
 
# Function call
print("Mean =", findMean(a, n))
print("Median =", findMedian(a, n))
 
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find mean
// and median of an array
using System;
 
class GFG 
{
    // Function for
    // calculating mean
    public static double findMean(int[] a, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += a[i];
 
        return (double)sum / (double)n;
    }
 
    // Function for
    // calculating median
    public static double findMedian(int[] a, int n)
    {
        // First we sort
        // the array
        Array.Sort(a);
 
        // check for
        // even case
        if (n % 2 != 0)
            return (double)a[n / 2];
 
        return (double)(a[(n - 1) / 2] + a[n / 2]) / 2.0;
    }
 
    // Driver Code
    public static void Main()
    {
        int[] a = { 1, 3, 4, 2, 7, 5, 8, 6 };
        int n = a.Length;
       
        // Function call
        Console.Write("Mean = " + findMean(a, n) + "\n");
        Console.Write("Median = " + findMedian(a, n)
                      + "\n");
    }
}
 
// This code is contributed by Smitha .
```

## PHP

```php
<?php 
// PHP program to find mean 
// and median of an array
 
// Function for calculating mean
function findMean(&$a, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++) 
        $sum += $a[$i];
     
    return (double)$sum / 
           (double)$n;
}
 
// Function for 
// calculating median
function findMedian(&$a, $n)
{
    // First we sort the array
    sort($a);
 
    // check for even case
    if ($n % 2 != 0)
    return (double)$a[$n / 2];
     
    return (double)($a[($n - 1) / 2] +
                    $a[$n / 2]) / 2.0;
}
 
// Driver Code
$a = array(1, 3, 4, 2, 
           7, 5, 8, 6);
$n = sizeof($a);
 
// Function call
echo "Mean = " . 
      findMean($a, $n)."\n"; 
echo "Median = " . 
      findMedian($a, $n); 
 
// This code is contributed
// by ChitraNayal
?>
```

输出：

```
Mean = 4.5
Median = 4.5
```

找到均值的时间复杂度：`O(n)`。

找到中位数的时间复杂度：`O(n Log n)`，因为我们需要首先对数组进行排序。 

请注意，我们可以使用[此处](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)和[此处](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)讨论的方法，在`O(n)`时间中找到中值。