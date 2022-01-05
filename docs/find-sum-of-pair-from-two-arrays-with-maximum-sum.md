# 从两个最大和的数组中求对的和

> 原文:[https://www . geeksforgeeks . org/从两个最大和数组中查找对和/](https://www.geeksforgeeks.org/find-sum-of-pair-from-two-arrays-with-maximum-sum/)

给定两个正整数和不同整数的数组。任务是从两个具有最大和的数组中找到一对。
**注意**:这一对应该包含两个数组中的一个元素。
T4【示例】T5:

```
Input : arr1[] = {1, 2, 3},  arr2[] = {4, 5, 6}
Output : Max Sum = 9
Pair (3, 6) has the maximum sum.

Input : arr1[] = {10, 2, 3},  arr2[] = {3, 4, 7}
Output : Max Sum = 17
```

**天真法**:简单的方法是两次运行两个嵌套循环，生成所有可能的对，找到和最大的对。
时间复杂度:O(N*M)，其中 N 为第一个数组的长度，M 为第二个数组的长度。
**有效方法**:有效方法是观察各个数组中最大的元素对最大和对的贡献。因此，任务简化为从两个数组中找到最大元素并打印它们的总和。
以下是上述方法的实现:

## C++

```
// C++ program to find maximum sum
// pair from two arrays

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum
// pair from two arrays
int maxSumPair(int arr1[], int n1, int arr2[], int n2)
{
    int max1 = INT_MIN; // max from 1st array
    int max2 = INT_MIN; // max from 2nd array

    // Find max from 1st array
    for (int i = 0; i < n1; i++) {
        if (arr1[i] > max1)
            max1 = arr1[i];
    }

    // Find max from 2nd array
    for (int i = 0; i < n2; i++) {
        if (arr2[i] > max2)
            max2 = arr2[i];
    }

    // Return sum of max from both arrays
    return max1 + max2;
}

// Driver Code
int main()
{

    int arr1[] = { 10, 2, 3 };

    int arr2[] = { 3, 4, 7 };

    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    cout << maxSumPair(arr1, n1, arr2, n2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find maximum sum
//pair from two arrays
public class AAB {

    //Function to find maximum sum
    //pair from two arrays
    static int maxSumPair(int arr1[], int n1, int arr2[], int n2)
    {
     int max1 = Integer.MIN_VALUE; // max from 1st array
     int max2 = Integer.MIN_VALUE; // max from 2nd array

     // Find max from 1st array
     for (int i = 0; i < n1; i++) {
         if (arr1[i] > max1)
             max1 = arr1[i];
     }

     // Find max from 2nd array
     for (int i = 0; i < n2; i++) {
         if (arr2[i] > max2)
             max2 = arr2[i];
     }

     // Return sum of max from both arrays
     return max1 + max2;
    }

    //Driver Code
    public static void main(String[] args) {

        int arr1[] = { 10, 2, 3 };

         int arr2[] = { 3, 4, 7 };

         int n1 = arr1.length;

         int n2 = arr2.length;

         System.out.println(maxSumPair(arr1, n1, arr2, n2));

    }

}
```

## 蟒蛇 3

```
# Python3 program to find maximum
# sum pair from two arrays
import sys

# Function to find maximum sum
# pair from two arrays
def maxSumPair(arr1, n1, arr2, n2):

    max1 = -sys.maxsize -1 # max from 1st array
    max2 = -sys.maxsize -1 # max from 2nd array

    # Find max from 1st array
    for i in range(0, n1):
        if (arr1[i] > max1):
            max1 = arr1[i]

    # Find max from 2nd array
    for i in range(0, n2):
        if (arr2[i] > max2):
            max2 = arr2[i]

    # Return sum of max from
    # both arrays
    return max1 + max2

# Driver Code
arr1 = [ 10, 2, 3 ]

arr2 = [ 3, 4, 7 ]

n1 = len(arr1)

n2 = len(arr2)

print(maxSumPair(arr1, n1, arr2, n2))

# This code is contributed
# by Yatin Gupta
```

## C#

```
// C# program to find maximum sum
//pair from two arrays
using System;

public class AAB {

    //Function to find maximum sum
    //pair from two arrays
    static int maxSumPair(int []arr1, int n1, int []arr2, int n2)
    {
     int max1 = int.MinValue; // max from 1st array
     int max2 = int.MinValue; // max from 2nd array

     // Find max from 1st array
     for (int i = 0; i < n1; i++) {
         if (arr1[i] > max1)
             max1 = arr1[i];
     }

     // Find max from 2nd array
     for (int i = 0; i < n2; i++) {
         if (arr2[i] > max2)
             max2 = arr2[i];
     }

     // Return sum of max from both arrays
     return max1 + max2;
    }

    //Driver Code
    public static void Main() {

        int []arr1 = { 10, 2, 3 };

         int []arr2 = { 3, 4, 7 };

         int n1 = arr1.Length;

         int n2 = arr2.Length;

         Console.Write(maxSumPair(arr1, n1, arr2, n2));

    }

}

/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum sum
// pair from two arrays

// Function to find maximum sum
// pair from two arrays
function maxSumPair($arr1, $n1, $arr2, $n2)
{
    $max1 = -1; // max from 1st array
    $max2 = -1; // max from 2nd array

    // Find max from 1st array
    for ($i = 0; $i < $n1; $i++)
    {
        if ($arr1[$i] > $max1)
            $max1 = $arr1[$i];
    }

    // Find max from 2nd array
    for ($i = 0; $i < $n2; $i++)
    {
        if ($arr2[$i] > $max2)
            $max2 = $arr2[$i];
    }

    // Return sum of max from both arrays
    return $max1 + $max2;
}

// Driver Code
$arr1 = array( 10, 2, 3 );

$arr2 = array( 3, 4, 7 );

$n1 = count($arr1);

$n2 = count($arr2);

echo maxSumPair($arr1, $n1, $arr2, $n2);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum sum
// pair from two arrays

    // Function to find maximum sum
    // pair from two arrays
    function maxSumPair(arr1,n1,arr2,n2)
    {
        // max from 1st array
        let max1 = Number.MIN_VALUE;
        // max from 2nd array
        let max2 = Number.MIN_VALUE;

     // Find max from 1st array
     for (let i = 0; i < n1; i++) {
         if (arr1[i] > max1)
             max1 = arr1[i];
     }

     // Find max from 2nd array
     for (let i = 0; i < n2; i++) {
         if (arr2[i] > max2)
             max2 = arr2[i];
     }

     // Return sum of max from both arrays
     return max1 + max2;
    }

    // Driver Code

    let arr1=[10, 2, 3 ];
    let arr2=[3, 4, 7 ];
    let n1 = arr1.length;
    let n2 = arr2.length;
    document.write(maxSumPair(arr1, n1, arr2, n2));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
17
```

**时间复杂度** : O(N + M)，其中 N 为第一个数组的长度，M 为第二个数组的长度。