# 在范围

内找到一个缺失的数字

> 原文:[https://www . geesforgeks . org/find-one-missing-number-range/](https://www.geeksforgeeks.org/find-one-missing-number-range/)

给定一个大小为 n 的数组，也给定了一个从最小数到最小数+ n 的数字范围，其中**最小数**是数组中的最小数。数组包含此范围内的数字，但缺少一个数字，因此任务是找到这个缺少的数字。
**例:**

```
Input  :  arr[] = {13, 12, 11, 15}
Output :  14

Input  :  arr[] = {33, 36, 35, 34};
Output : 37
```

问题很接近[找漏号](https://www.geeksforgeeks.org/find-the-missing-number/)。
解决这个问题有很多方法。
一个**简单的做法**就是先找到最小值，然后一个一个的搜索所有元素。这种方法的时间复杂度是 O(n*n)
A **更好的解决方案**是对数组进行排序。然后遍历数组，找到第一个不存在的元素。这种方法的时间复杂度为 O(n Log n)
**的最佳解决方案**是首先对所有数字进行异或运算。然后将这个结果与从最小到 n+最小的所有数字进行异或运算。异或是我们的结果。
示例:-

```
arr[n] = {13, 12, 11, 15}
smallestNumber = 11

first find the xor of this array
13^12^11^15 = 5

Then find the XOR first number to first number + n
11^12^13^14^15 = 11;

Then xor these two number's
5^11 = 14 // this is the missing number
```

## C++

```
// CPP program to find missing
// number in a range.
#include <bits/stdc++.h>
using namespace std;

// Find the missing number
// in a range
int missingNum(int arr[], int n)
{
    int minvalue = *min_element(arr, arr+n);

    // here we xor of all the number
    int xornum = 0;
    for (int i = 0; i < n; i++) {
        xornum ^= (minvalue) ^ arr[i];
        minvalue++;
    }

    // xor last number
    return xornum ^ minvalue;
}

// Driver code
int main()
{
    int arr[] = { 13, 12, 11, 15 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << missingNum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// missing number in a range.
import java.io.*;
import java.util.*;

class GFG {

// Find the missing number in a range
static int missingNum(int arr[], int n)
{
    List<Integer> list = new ArrayList<>(arr.length);
    for (int i :arr)
    {
        list.add(Integer.valueOf(i));
    }
    int minvalue = Collections.min(list);;

    // here we xor of all the number
    int xornum = 0;
    for (int i = 0; i < n; i++) {
        xornum ^= (minvalue) ^ arr[i];
        minvalue++;
    }

    // xor last number
    return xornum ^ minvalue;
}

public static void main (String[] args) {
     int arr[] = { 13, 12, 11, 15 };
    int n = arr.length;
    System.out.println(missingNum(arr, n));  

    }
}

//This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python3 program to check
# missingnumber in a range

# Find the missing number
# in a range
def missingNum( arr,  n):

    minvalue = min(arr)

    # here we xor of all the number
    xornum = 0
    for  i in range (0,n):
        xornum ^= (minvalue) ^ arr[i]
        minvalue = minvalue+1

    # xor last number
    return xornum ^ minvalue

# Driver method
arr = [ 13, 12, 11, 15 ]
n = len(arr)
print (missingNum(arr, n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to find
// missing number in a range.
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

// Find the missing number in a range
static int missingNum(int []arr, int n)
{
    List<int> list = new List<int>(arr.Length);
    foreach (int i in arr)
    {
        list.Add(i);
    }
    int minvalue = list.Min();

    // here we xor of all the number
    int xornum = 0;
    for (int i = 0; i < n; i++)
    {
        xornum ^= (minvalue) ^ arr[i];
        minvalue++;
    }

    // xor last number
    return xornum ^ minvalue;
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = { 13, 12, 11, 15 };
    int n = arr.Length;
    Console.WriteLine(missingNum(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find missing
// number in a range.

// Find the missing number
// in a range
function missingNum($arr, $n)
{
    $minvalue = min($arr);

    // here we xor of all the number
    $xornum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $xornum ^= ($minvalue) ^ $arr[$i];
        $minvalue++;
    }

    // xor last number
    return $xornum ^ $minvalue;
}

// Driver code
$arr = array( 13, 12, 11, 15 );
$n = sizeof($arr);
echo missingNum($arr, $n);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>
// Javascript program to find missing
// number in a range.

// Find the missing number
// in a range
function missingNum(arr, n)
{
    let minvalue = Math.min(...arr);

    // here we xor of all the number
    let xornum = 0;
    for (let i = 0; i < n; i++) {
        xornum ^= (minvalue) ^ arr[i];
        minvalue++;
    }

    // xor last number
    return xornum ^ minvalue;
}

// Driver code
    let arr = [ 13, 12, 11, 15 ];
    let n = arr.length;
    document.write(missingNum(arr, n));

</script>
```

**输出:**

```
14
```