# 数组中某个元素的最小差值总和

> 原文:[https://www . geeksforgeeks . org/数组中元素的最小差值总和/](https://www.geeksforgeeks.org/minimum-sum-of-differences-with-an-element-in-an-array/)

给定一个数组，我们需要在改变元素后找到数组元素的和，因为 arr[i]将变成 abs(arr[i]-x)，其中 x 是数组元素。

**示例:**

```
Input  : {2, 5, 1, 7, 4}
Output : 9
We get minimum sum when we choose
x = 4\. The minimum sum is 
abs(2-4) + abs(5-4) + abs(1-4) + (7-4)
abs(4-4) = 9

Input  : {5, 11, 14, 10, 17, 15}
Output : 20
We can either choose x = 14 or x = 11
```

这个想法是基于这样一个事实，即中间元素会导致最小的差异。当有偶数个元素时，我们可以取中间两个元素中的任何一个。我们可以举几个例子来验证这个事实。

以下是上述想法的实现:

## C++

```
// C++ program to find minimum sum of absolute
// differences with an array element.
#include<bits/stdc++.h>
using namespace std;
    // function to find min sum after operation
    int absSumDidd(int a[],int n)
    {
        // Sort the array
        sort(a,a+n);

        // Pick middle value
        int midValue = a[(int)(n / 2)];

        // Sum of absolute differences.
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum = sum + abs(a[i] - midValue);
        }

        return sum;    
    }

    // Driver Code
    int main()
    {
        int arr[] = { 5, 11, 14, 10, 17, 15 };
        int n=sizeof(arr)/sizeof(arr[0]);
        cout<< absSumDidd(arr,n);    
    }
    // Contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum sum of absolute
// differences with an array element.
import java.lang.*;
import java.util.*;

public class GFG {

    // function to find min sum after operation
    static int absSumDidd(int a[])
    {
        // Sort the array
        Arrays.sort(a);

        // Pick middle value
        int midValue = a[a.length / 2];

        // Sum of absolute differences.
        int sum = 0;
        for (int i = 0; i < a.length; i++) {
            sum = sum + Math.abs(a[i] - midValue);
        }

        return sum;      
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 5, 11, 14, 10, 17, 15 };
        System.out.print(absSumDidd(arr));       
    }
    // Contributed by Saurav Jain
}
```

## 蟒蛇 3

```
# Python3 program to find minimum sum of
# absolute differences with an array element.

# function to find min sum after operation
def absSumDidd(a, n):

    # Sort the array
    a.sort()

    # Pick middle value
    midValue = a[(int)(n // 2)]

    # Sum of absolute differences.
    sum = 0
    for i in range(n):
        sum = sum + abs(a[i] - midValue)
    return sum

# Driver Code
arr = [5, 11, 14, 10, 17, 15]
n = len(arr)
print(absSumDidd(arr, n))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# program to find minimum sum of absolute
// differences with an array element.
using System;

 class GFG {

    // function to find min sum after operation
    static int absSumDidd(int []a)
    {
        // Sort the array
        Array.Sort(a);

        // Pick middle value
        int midValue = a[a.Length / 2];

        // Sum of absolute differences.
        int sum = 0;
        for (int i = 0; i < a.Length; i++) {
            sum = sum + Math.Abs(a[i] - midValue);
        }

        return sum;       
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 5, 11, 14, 10, 17, 15 };
        Console.Write(absSumDidd(arr));        
    }
    // Contributed by Subhadeep
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// sum of absolute differences
// with an array element.

// function to find min sum
// after operation
function absSumDidd($a, $n)
{
    // Sort the array
    sort($a);

    // Pick middle value
    $midValue = $a[($n / 2)];

    // Sum of absolute differences.
    $sum = 0;
    for ( $i = 0; $i < $n; $i++)
    {
        $sum = $sum + abs($a[$i] -
               $midValue);
    }

    return $sum;    
}

// Driver Code
$arr = array(5, 11, 14, 10, 17, 15 );
$n = count($arr);
echo absSumDidd($arr, $n);

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum sum of absolute
// differences with an array element.

// Function to find min sum after operation
function absSumDidd(a)
{

    // Sort the array
    a.sort((a, b) => a - b);

    // Pick middle value
    var midValue = a[a.length / 2];

    // Sum of absolute differences.
    var sum = 0;
    for(var i = 0; i < a.length; i++)
    {
        sum = sum + Math.abs(a[i] - midValue);
    }
    return sum;      
}

// Driver Code
var arr = [ 5, 11, 14, 10, 17, 15 ];
document.write(absSumDidd(arr)); 

// This code is contributed by shikhasingrajput

</script>
```

**Output:** 

```
20
```

**时间复杂度:** O(n Log n)
利用[线性时间算法求中值，可以进一步将上述解优化为 O(n)。](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)