# 第一个数组中元素的总和，使得第二个数组中小于或等于它们的元素数量最大

> 原文:[https://www . geeksforgeeks . org/第一个数组中的元素之和使得第二个数组中的元素数量小于或等于最大值/](https://www.geeksforgeeks.org/sum-of-elements-in-1st-array-such-that-number-of-elements-less-than-or-equal-to-them-in-2nd-array-is-maximum/)

给定两个未排序的数组 **arr1[]** 和 **arr2[]** ，任务是找到 **arr1[]** 的元素之和，使得 **arr2[]** 中小于或等于它们的元素数量最大。

**示例:**

> **输入:** arr1[] = {1，2，3，4，7，9}，arr2[] = {0，1，2，1，1，4}
> **输出:** 20
> 下表显示了 arr2[]中≤arr 1[]
> 
> <figure class="table">元素的元素数量
> 
> | arr1[i] | 数数 |
> | --- | --- |
> | one | four |
> | Two | five |
> | three | five |
> | four | six |
> | seven | six |
> | nine | six |
> 
> 4、7 和 9 的计数是最大值。
> 因此，结果和为 4 + 7 + 9 = 20。
> **输入:** arr1[] = {5，10，2，6，1，8，6，12}，arr2[] = {6，5，11，4，2，3，7}
> **输出:** 12
> 
> </figure>

**方法:**高效解决上述问题背后的思想是使用第二个数组的散列，然后找到散列数组的累积和。此后，可以容易地计算出小于或等于第一阵列的元素的第二阵列的元素数。这将给出一个频率数组，它表示第二个数组中的元素数小于或等于第一个数组中的元素数，由此可以计算出第一个数组中对应于频率数组中最大频率的元素之和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;
#define MAX 100000

// Function to return the required sum
int findSumofEle(int arr1[], int m,
                 int arr2[], int n)
{
    // Creating hash array initially
    // filled with zero
    int hash[MAX] = { 0 };

    // Calculate the frequency
    // of elements of arr2[]
    for (int i = 0; i < n; i++)
        hash[arr2[i]]++;

    // Running sum of hash array
    // such that hash[i] will give count of
    // elements less than or equal to i in arr2[]
    for (int i = 1; i < MAX; i++)
        hash[i] = hash[i] + hash[i - 1];

    // To store the maximum value of
    // the number of elements in arr2[] which are
    // smaller than or equal to some element of arr1[]
    int maximumFreq = 0;
    for (int i = 0; i < m; i++)
        maximumFreq = max(maximumFreq, hash[arr1[i]]);

    // Calculate the sum of elements from arr1[]
    // corresponding to maximum frequency
    int sumOfElements = 0;
    for (int i = 0; i < m; i++)
        sumOfElements += (maximumFreq == hash[arr1[i]]) ? arr1[i] : 0;

    // Return the required sum
    return sumOfElements;
}

// Driver code
int main()
{
    int arr1[] = { 2, 5, 6, 8 };
    int arr2[] = { 4, 10 };
    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);

    cout << findSumofEle(arr1, m, arr2, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    static int MAX = 100000;

    // Function to return the required sum
    static int findSumofEle(int arr1[], int m,
                            int arr2[], int n)
    {
        // Creating hash array initially
        // filled with zero
        int hash[] = new int[MAX];

        // Calculate the frequency
        // of elements of arr2[]
        for (int i = 0; i < n; i++)
        {
            hash[arr2[i]]++;
        }

        // Running sum of hash array
        // such that hash[i] will give count of
        // elements less than or equal to i in arr2[]
        for (int i = 1; i < MAX; i++)
        {
            hash[i] = hash[i] + hash[i - 1];
        }

        // To store the maximum value of
        // the number of elements in arr2[] which are
        // smaller than or equal to some element of arr1[]
        int maximumFreq = 0;
        for (int i = 0; i < m; i++)
        {
            maximumFreq = Math.max(maximumFreq, hash[arr1[i]]);
        }

        // Calculate the sum of elements from arr1[]
        // corresponding to maximum frequency
        int sumOfElements = 0;
        for (int i = 0; i < m; i++)
        {
            sumOfElements += (maximumFreq == hash[arr1[i]]) ? arr1[i] : 0;
        }

        // Return the required sum
        return sumOfElements;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = {2, 5, 6, 8};
        int arr2[] = {4, 10};
        int m = arr1.length;
        int n = arr2.length;

        System.out.println(findSumofEle(arr1, m, arr2, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 100000

# Function to return the required sum
def findSumofEle(arr1, m, arr2, n):

    # Creating hash array initially
    # filled with zero
    hash = [0 for i in range(MAX)]

    # Calculate the frequency
    # of elements of arr2[]
    for i in range(n):
        hash[arr2[i]] += 1

    # Running sum of hash array
    # such that hash[i] will give count of
    # elements less than or equal to i in arr2[]
    for i in range(1, MAX, 1):
        hash[i] = hash[i] + hash[i - 1]

    # To store the maximum value of
    # the number of elements in arr2[]
    # which are smaller than or equal
    # to some element of arr1[]
    maximumFreq = 0
    for i in range(m):
        maximumFreq = max(maximumFreq,
                          hash[arr1[i]])

    # Calculate the sum of elements from arr1[]
    # corresponding to maximum frequency
    sumOfElements = 0
    for i in range(m):
        if (maximumFreq == hash[arr1[i]]):
            sumOfElements += arr1[i]

    # Return the required sum
    return sumOfElements

# Driver code
if __name__ == '__main__':
    arr1 = [2, 5, 6, 8]
    arr2 = [4, 10]
    m = len(arr1)
    n = len(arr2)
    print(findSumofEle(arr1, m, arr2, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAX = 100000;

    // Function to return the required sum
    static int findSumofEle(int[] arr1, int m,
                            int[] arr2, int n)
    {
        // Creating hash array initially
        // filled with zero
        int[] hash = new int[MAX];

        // Calculate the frequency
        // of elements of arr2[]
        for (int i = 0; i < n; i++)
        {
            hash[arr2[i]]++;
        }

        // Running sum of hash array
        // such that hash[i] will give count of
        // elements less than or equal to i in arr2[]
        for (int i = 1; i < MAX; i++)
        {
            hash[i] = hash[i] + hash[i - 1];
        }

        // To store the maximum value of
        // the number of elements in arr2[] which are
        // smaller than or equal to some element of arr1[]
        int maximumFreq = 0;
        for (int i = 0; i < m; i++)
        {
            maximumFreq = Math.Max(maximumFreq, hash[arr1[i]]);
        }

        // Calculate the sum of elements from arr1[]
        // corresponding to maximum frequency
        int sumOfElements = 0;
        for (int i = 0; i < m; i++)
        {
            sumOfElements += (maximumFreq == hash[arr1[i]]) ? arr1[i] : 0;
        }

        // Return the required sum
        return sumOfElements;
    }

    // Driver code
    public static void Main()
    {
        int[] arr1 = {2, 5, 6, 8};
        int[] arr2 = {4, 10};
        int m = arr1.Length;
        int n = arr2.Length;

        Console.WriteLine(findSumofEle(arr1, m, arr2, n));
    }
}

// This code has been contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 10000;

// Function to return the required sum
function findSumofEle($arr1, $m, $arr2, $n)
{
    // Creating hash array initially
    // filled with zero
    $hash = array_fill(0, $GLOBALS['MAX'], 0);

    // Calculate the frequency
    // of elements of arr2[]
    for ($i = 0; $i < $n; $i++)
        $hash[$arr2[$i]]++;

    // Running sum of hash array
    // such that hash[i] will give count of
    // elements less than or equal to i in arr2[]
    for ($i = 1; $i < $GLOBALS['MAX']; $i++)
        $hash[$i] = $hash[$i] + $hash[$i - 1];

    // To store the maximum value of
    // the number of elements in arr2[] which are
    // smaller than or equal to some element of arr1[]
    $maximumFreq = 0;
    for ($i = 0; $i < $m; $i++)
        $maximumFreq = max($maximumFreq,
                           $hash[$arr1[$i]]);

    // Calculate the sum of elements from arr1[]
    // corresponding to maximum frequency
    $sumOfElements = 0;
    for ($i = 0; $i < $m; $i++)
        $sumOfElements += ($maximumFreq == $hash[$arr1[$i]]) ?
                                                   $arr1[$i] : 0;

    // Return the required sum
    return $sumOfElements;
}

// Driver code
$arr1 = array( 2, 5, 6, 8 );
$arr2 = array( 4, 10 );
$m = count($arr1);
$n = count($arr2);

echo findSumofEle($arr1, $m, $arr2, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required sum
function findSumofEle(arr1, m, arr2, n)
{
    let MAX = 100000;

    // Creating hash array initially
    // filled with zero
    let hash = new Array(MAX);

    for(let i = 0; i < MAX; i++)
        hash[i] = 0;

    // Calculate the frequency
    // of elements of arr2[]
    for(let i = 0; i < n; i++)
        hash[arr2[i]]++;

    // Running sum of hash array such
    // that hash[i] will give count of
    // elements less than or equal
    // to i in arr2[]
    for(let i = 1; i < MAX; i++)
        hash[i] = hash[i] + hash[i - 1];

    // To store the maximum value of
    // the number of elements in
    // arr2[] which are smaller
    // than or equal to some
    // element of arr1[]
    let maximumFreq = 0;
    for(let i = 0; i < m; i++)
    {
        maximumFreq = Math.max(maximumFreq,
                               hash[arr1[i]]);
    }

    // Calculate the sum of elements from arr1[]
    // corresponding to maximum frequency
    let sumOfElements = 0;
    for(let i = 0; i < m; i++)
    {
        if (maximumFreq == hash[arr1[i]])
           sumOfElements += arr1[i];
    }

    // Return the required sum
    return sumOfElements;
}

// Driver code
let arr1 = [ 2, 5, 6, 8 ];
let arr2 = [ 4, 10 ];
let m = arr1.length;
let n = arr2.length;

document.write(findSumofEle(arr1, m, arr2, n));

// This code is contributed by mohit kumar 29

</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(MAX)*

***辅助空间:** O(MAX)*