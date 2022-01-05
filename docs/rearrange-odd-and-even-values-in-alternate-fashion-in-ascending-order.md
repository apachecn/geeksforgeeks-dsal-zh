# 按照升序以交替方式重新排列奇数和偶数值

> 原文:[https://www . geesforgeks . org/重排-奇数和偶数值-交替-按升序排列/](https://www.geeksforgeeks.org/rearrange-odd-and-even-values-in-alternate-fashion-in-ascending-order/)

给定一个整数数组(奇数和偶数)，任务是将它们排列成奇数和偶数值分别以非递减顺序(升序)交替出现。

*   如果最小值是**偶数**，那么我们必须打印**奇偶**图案。
*   如果最小值是**奇数**，那么我们必须打印**奇数-偶数**图案。

**注意:** **输入数组中奇数元素的个数必须等于偶数元素的个数。**
**例:**

> **输入:** arr[] = {1，3，2，5，4，7，10}
> **输出:** 1，2，3，4，5，10，7
> 最小值为 **1** (奇数)，因此输出将为奇偶模式。
> **输入:** arr[] = {9，8，13，2，19，14}
> **输出:** 2，9，8，13，14，19
> 最小值为 **2** (偶数)，因此输出将为奇偶模式。

**问于:**微软技术-设定-开始-2018

**算法:**

1.  给定数组排序。
2.  在列表-1 中插入**偶数**值，在列表-2 中插入**奇数**值。
3.  现在如果最小值是偶数，那么从列表 1 插入一个偶数，从列表 2 插入一个奇数到原始数组，以此类推。
4.  但是如果最小值是奇数，那么从列表 2 插入一个奇数，从列表 1 插入一个偶数到原始数组，以此类推。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

void AlternateRearrange(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n);

    vector<int> v1; // to insert even values
    vector<int> v2; // to insert odd values

    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 0)
            v1.push_back(arr[i]);
        else
            v2.push_back(arr[i]);

    int index = 0, i = 0, j = 0;

    bool flag = false;

    // Set flag to true if first element is even
    if (arr[0] % 2 == 0)
        flag = true;

    // Start rearranging array
    while (index < n) {

        // If first element is even
        if (flag == true) {
            arr[index++] = v1[i++];
            flag = !flag;
        }

        // Else, first element is Odd
        else {
            arr[index++] = v2[j++];
            flag = !flag;
        }
    }

    // Print the rearranged array
    for (i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 9, 8, 13, 2, 19, 14 };
    int n = sizeof(arr) / sizeof(int);
    AlternateRearrange(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.* ;

class GFG
{

    static void AlternateRearrange(int arr[], int n)
    {
        // Sort the array

        // Collection.sort() sorts the
        // collection in ascending order
        Arrays.sort(arr) ;

        Vector v1 = new Vector(); // to insert even values
        Vector v2 = new Vector(); // to insert odd values

        for (int i = 0; i < n; i++)
            if (arr[i] % 2 == 0)
                v1.add(arr[i]);
            else
                v2.add(arr[i]);

        int index = 0, i = 0, j = 0;

        boolean flag = false;

        // Set flag to true if first element is even
        if (arr[0] % 2 == 0)
            flag = true;

        // Start rearranging array
        while (index < n)
        {

            // If first element is even
            if (flag == true)
            {
                arr[index] = (int)v1.get(i);
                i += 1 ;
                index += 1 ;
                flag = !flag;
            }

            // Else, first element is Odd
            else
            {
                arr[index] = (int)v2.get(j) ;
                j += 1 ;
                index += 1 ;
                flag = !flag;
            }
        }

        // Print the rearranged array
        for (i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String []args)
    {
        int arr[] = { 9, 8, 13, 2, 19, 14 };
        int n = arr.length ;

        AlternateRearrange(arr, n);
    }
}

// This code is contributed by aishwarya.27
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
def AlternateRearrange(arr, n):

    # Sort the array
    arr.sort()

    v1 = list()  # to insert even values
    v2 = list()  # to insert odd values

    for i in range(n):
        if (arr[i] % 2 == 0):
            v1.append(arr[i])
        else:
            v2.append(arr[i])

    index = 0
    i = 0
    j = 0

    flag = False

    # Set flag to true if first element is even
    if (arr[0] % 2 == 0):
        flag = True

    # Start rearranging array
    while (index < n):

        # If first element is even
        if (flag == True and i < len(v1)):
            arr[index] = v1[i]
            index += 1
            i += 1
            flag = ~flag

        # Else, first element is Odd
        elif j < len(v2):
            arr[index] = v2[j]
            index += 1
            j += 1

            flag = ~flag

    # Print the rearranged array
    for i in range(n):
        print(arr[i], end=" ")

# Driver code
arr = [9, 8, 13, 2, 19, 14, 21, 23, 25]
n = len(arr)

AlternateRearrange(arr, n)

# This code is contributed
# by Mohit Kumar 29.
```

## C#

```
// C# implementation of the above approach

using System;
using System.Collections;
class GFG
{

    static void AlternateRearrange(int []arr, int n)
    {
        // Sort the array

        // Collection.sort() sorts the
        // collection in ascending order
        Array.Sort(arr) ;

        ArrayList v1 = new ArrayList(); // to insert even values
        ArrayList v2 = new ArrayList(); // to insert odd values

        for (int j = 0; j < n; j++)
            if (arr[j] % 2 == 0)
                v1.Add(arr[j]);
            else
                v2.Add(arr[j]);

        int index = 0, i = 0, k = 0;

        bool flag = false;

        // Set flag to true if first element is even
        if (arr[0] % 2 == 0)
            flag = true;

        // Start rearranging array
        while (index < n)
        {

            // If first element is even
            if (flag == true)
            {
                arr[index] = (int)v1[i];
                i += 1 ;
                index += 1 ;
                flag = !flag;
            }

            // Else, first element is Odd
            else
            {
                arr[index] = (int)v2[k] ;
                k += 1 ;
                index += 1 ;
                flag = !flag;
            }
        }

        // Print the rearranged array
        for (i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    static void Main()
    {
        int []arr = { 9, 8, 13, 2, 19, 14 };
        int n = arr.Length ;

        AlternateRearrange(arr, n);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
function AlternateRearrange($arr, $n)
{

    // Sort the array
    sort($arr);

    $v1 = array(); // to insert even values
    $v2 = array(); // to insert odd values

    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] % 2 == 0)
            array_push($v1, $arr[$i]);
        else
            array_push($v2, $arr[$i]);

    $index = 0;
    $i = 0;
    $j = 0;

    $flag = false;

    // Set flag to true if first element is even
    if ($arr[0] % 2 == 0)
        $flag = true;

    // Start rearranging array
    while ($index < $n)
    {

        // If first element is even
        if ($flag == true)
        {
            $arr[$index++] = $v1[$i++];
            $flag = !$flag;
        }

        // Else, first element is Odd
        else
        {
            $arr[$index++] = $v2[$j++];
            $flag = !$flag;
        }
    }

    // Print the rearranged array
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i], " " ;
}

// Driver code
$arr = array( 9, 8, 13, 2, 19, 14 );
$n = sizeof($arr);

AlternateRearrange($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

function AlternateRearrange(arr, n)
{
    // Sort the array
    arr.sort((a,b)=>a-b);

    var v1 = []; // to insert even values
    var v2 = []; // to insert odd values

    for (var i = 0; i < n; i++)
        if (arr[i] % 2 == 0)
            v1.push(arr[i]);
        else
            v2.push(arr[i]);

    var index = 0, i = 0, j = 0;

    var flag = false;

    // Set flag to true if first element is even
    if (arr[0] % 2 == 0)
        flag = true;

    // Start rearranging array
    while (index < n) {

        // If first element is even
        if (flag == true) {
            arr[index++] = v1[i++];
            flag = !flag;
        }

        // Else, first element is Odd
        else {
            arr[index++] = v2[j++];
            flag = !flag;
        }
    }

    // Print the rearranged array
    for (i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Driver code
var arr = [9, 8, 13, 2, 19, 14];
var n = arr.length;
AlternateRearrange(arr, n);

</script>
```

**Output:** 

```
2 9 8 13 14 19
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(N)