# 总和大于所有其他元素的最小子集

> 原文:[https://www . geesforgeks . org/最小-子集-总和-较大-元素/](https://www.geeksforgeeks.org/smallest-subset-sum-greater-elements/)

给定一个非负整数数组。我们的任务是找到最小数量的元素，这样它们的总和应该大于数组中其余元素的总和。
**例:**

```
Input : arr[] = {3, 1, 7, 1}
Output : 1
Smallest subset is {7}. Sum of
this subset is greater than all
other elements {3, 1, 1}

Input : arr[] = {2, 1, 2}
Output : 2
In this example one element is not 
enough. We can pick elements with 
values 1, 2 or 2, 2\. In any case, 
the minimum count is 2.
```

**蛮力**方法是找到所有可能子集的和，然后将和与剩余元素的和进行比较。
**高效的方法**是采取最大的元素。我们按降序对值进行排序，然后从最大的值开始取元素，直到我们得到给定数组总和的一半以上。

## C++

```
// CPP program to find minimum number of
// elements such that their sum is greater
// than sum of remaining elements of the array.
#include <bits/stdc++.h>
#include <string.h>
using namespace std;

// function to find minimum elements needed.
int minElements(int arr[], int n)
{
    // calculating HALF of array sum
    int halfSum = 0;
    for (int i = 0; i < n; i++)
        halfSum = halfSum + arr[i];   
    halfSum = halfSum / 2;

    // sort the array in descending order.
    sort(arr, arr + n, greater<int>());

    int res = 0, curr_sum = 0;
    for (int i = 0; i < n; i++) {

        curr_sum += arr[i];
        res++;

        // current sum greater than sum
        if (curr_sum > halfSum)        
            return res;
    }
    return res;
}

// Driver function
int main()
{
    int arr[] = {3, 1, 7, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minElements(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find minimum number of elements
// such that their sum is greater than sum of
// remaining elements of the array.
import java.io.*;
import java.util.*;

class GFG {

    // Function to find minimum elements needed
    static int minElements(int arr[], int n)
    {
        // Calculating HALF of array sum
        int halfSum = 0;
        for (int i = 0; i < n; i++)
            halfSum = halfSum + arr[i];
        halfSum = halfSum / 2;

        // Sort the array in ascending order and
        // start traversing array from the ascending
        // sort in descending order.
        Arrays.sort(arr);

        int res = 0, curr_sum = 0;
        for (int i = n-1; i >= 0; i--) {

            curr_sum += arr[i];
            res++;

            // Current sum greater than sum
            if (curr_sum > halfSum)        
                return res;
        }
        return res;
    }

    // Driver Code
    public static void main (String[] args) {
        int arr[] = {3, 1, 7, 1};
        int n = arr.length;
        System.out.println(minElements(arr, n));
    }
    }

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Python3 code to find minimum number of
# elements such that their sum is greater
# than sum of remaining elements of the array.

# function to find minimum elements needed.
def minElements(arr , n):

    # calculating HALF of array sum
    halfSum = 0
    for i in range(n):
        halfSum = halfSum + arr[i]

    halfSum = int(halfSum / 2)

    # sort the array in descending order.
    arr.sort(reverse = True)

    res = 0
    curr_sum = 0
    for i in range(n):

        curr_sum += arr[i]
        res += 1

        # current sum greater than sum
        if curr_sum > halfSum:
            return res

    return res

# driver code
arr = [3, 1, 7, 1]
n = len(arr)
print(minElements(arr, n) )

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# code to find minimum number of elements
// such that their sum is greater than sum of
// remaining elements of the array.
using System;

class GFG {

    // Function to find minimum elements needed
    static int minElements(int []arr, int n)
    {

        // Calculating HALF of array sum
        int halfSum = 0;

        for (int i = 0; i < n; i++)
            halfSum = halfSum + arr[i];

        halfSum = halfSum / 2;

        // Sort the array in ascending order and
        // start traversing array from the ascending
        // sort in descending order.
        Array.Sort(arr);

        int res = 0, curr_sum = 0;
        for (int i = n-1; i >= 0; i--) {

            curr_sum += arr[i];
            res++;

            // Current sum greater than sum
            if (curr_sum > halfSum)    
                return res;
        }

        return res;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {3, 1, 7, 1};
        int n = arr.Length;

        Console.WriteLine(minElements(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number
// of elements such that their sum is
// greater than sum of remaining
// elements of the array.

// function to find minimum elements needed.
function minElements($arr, $n)
{

    // calculating HALF of array sum
    $halfSum = 0;
    for ($i = 0; $i < $n; $i++)
        $halfSum = $halfSum + $arr[$i];
    $halfSum = $halfSum / 2;

    // sort the array in descending order.
    rsort($arr);

    $res = 0;
    $curr_sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $curr_sum += $arr[$i];
        $res++;

        // current sum greater than sum
        if ($curr_sum > $halfSum)        
            return $res;
    }
    return $res;
}

// Driver Code
$arr = array(3, 1, 7, 1);
$n = sizeof($arr);
echo minElements($arr, $n);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum number of
    // elements such that their sum is greater
    // than sum of remaining elements of the array.

    // function to find minimum elements needed.
    function minElements(arr, n)
    {
        // calculating HALF of array sum
        let halfSum = 0;
        for (let i = 0; i < n; i++)
            halfSum = halfSum + arr[i];   
        halfSum = parseInt(halfSum / 2, 10);

        // sort the array in descending order.
        arr.sort(function(a, b){return a - b});
        arr.reverse();

        let res = 0, curr_sum = 0;
        for (let i = 0; i < n; i++) {

            curr_sum += arr[i];
            res++;

            // current sum greater than sum
            if (curr_sum > halfSum)        
                return res;
        }
        return res;
    }

    let arr = [3, 1, 7, 1];
    let n = arr.length;
    document.write(minElements(arr, n));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
1
```

**时间复杂度:** O(n Log n)