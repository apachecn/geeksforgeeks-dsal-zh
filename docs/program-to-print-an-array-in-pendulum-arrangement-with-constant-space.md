# 程序打印一个等间距摆式排列的数组

> 原文:[https://www . geeksforgeeks . org/program-to-print-a-a-array-in-the-array-in-switch-array-in-constant-space/](https://www.geeksforgeeks.org/program-to-print-an-array-in-pendulum-arrangement-with-constant-space/)

给定整数数组**arr【】**，任务是以类似于钟摆来回运动的方式排列它们，而不使用任何额外的空间。
T3】摆式排列:T5

*   整数列表中的最小元素必须位于数组的中心位置。
*   最小数旁边的升序数字向右移动，下一个更高的数字向左移动，它继续移动。
*   当达到更高的数字时，一个人以类似钟摆的往复方式走到一边。

**例:**

> **输入:** arr[] = {2，3，5，1，4}
> **输出:** 5 3 1 2 4
> 最小元素为 1，所以移到中间。
> 下一个较高的元素 2 被移动到
> 中间元素的右侧，而下一个较高的元素 3 被
> 移动到中间元素的左侧，并且
> 该过程继续。
> **输入:** arr[] = {11，2，4，55，6，8}
> **输出:** 11 6 2 4 8 55

**方法:**在[这篇](https://www.geeksforgeeks.org/program-print-array-pendulum-arrangement/)文章中已经讨论了一种使用辅助数组的方法。这里有一个不使用额外空间的方法:

1.  给定数组排序。
2.  移动数组右侧的所有奇数位置元素。
3.  将元素从 0 反转到数组的(n-1)/2 位置。

> 例如，让 arr[] = {2，3，5，1，4}
> 排序后的数组将是 arr[] = {1，2，3，4，5}。
> 将所有奇数索引位置元素向右移动后，
> arr[] = {1，3，5，2，4} (1 和 3 为奇数索引位置)
> 将元素从 0 反转为(n–1)/2 后，
> arr[] = {5，3，1，2，4}为所需数组。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the Pendulum
// arrangement of the given array
void pendulumArrangement(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n);

    int odd, temp, in, pos;

    // pos stores the index of
    // the last element of the array
    pos = n - 1;

    // odd stores the last odd index in the array
    if (n % 2 == 0)
        odd = n - 1;
    else
        odd = n - 2;

    // Move all odd index positioned
    // elements to the right
    while (odd > 0) {
        temp = arr[odd];
        in = odd;

        // Shift the elements by one position
        // from odd to pos
        while (in != pos) {
            arr[in] = arr[in + 1];
            in++;
        }
        arr[in] = temp;
        odd = odd - 2;
        pos = pos - 1;
    }

    // Reverse the element from 0 to (n - 1) / 2
    int start = 0, end = (n - 1) / 2;

    for (; start < end; start++, end--) {
        temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
    }

    // Printing the pendulum arrangement
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 11, 2, 4, 55, 6, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pendulumArrangement(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
import java.io.*;

class GFG {

    // Function to print the Pendulum
    // arrangement of the given array
    static void pendulumArrangement(int arr[], int n)
    {
        // Sort the array
        // sort(arr, arr + n);

        Arrays.sort(arr);

        int odd, temp, in, pos;

        // pos stores the index of
        // the last element of the array
        pos = n - 1;

        // odd stores the last odd index in the array
        if (n % 2 == 0)
            odd = n - 1;
        else
            odd = n - 2;

        // Move all odd index positioned
        // elements to the right
        while (odd > 0) {
            temp = arr[odd];
            in = odd;

            // Shift the elements by one position
            // from odd to pos
            while (in != pos) {
                arr[in] = arr[in + 1];
                in++;
            }
            arr[in] = temp;
            odd = odd - 2;
            pos = pos - 1;
        }

        // Reverse the element from 0 to (n - 1) / 2
        int start = 0, end = (n - 1) / 2;

        for (; start < end; start++, end--) {
            temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
        }

        // Printing the pendulum arrangement
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 11, 2, 4, 55, 6, 8 };
        int n = arr.length;

        pendulumArrangement(arr, n);
    }
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print the Pendulum
# arrangement of the given array
def pendulumArrangement(arr, n):

    # Sort the array
    arr.sort(reverse = False)

    # pos stores the index of
    # the last element of the array
    pos = n - 1

    # odd stores the last odd index in the array
    if (n % 2 == 0):
        odd = n - 1
    else:
        odd = n - 2

    # Move all odd index positioned
    # elements to the right
    while (odd > 0):
        temp = arr[odd]
        in1 = odd

        # Shift the elements by one position
        # from odd to pos
        while (in1 != pos):
            arr[in1] = arr[in1 + 1]
            in1 += 1

        arr[in1] = temp
        odd = odd - 2
        pos = pos - 1

    # Reverse the element from 0 to (n - 1) / 2
    start = 0
    end = int((n - 1) / 2)

    while(start < end):
        temp = arr[start]
        arr[start] = arr[end]
        arr[end] = temp
        start += 1
        end -= 1

    # Printing the pendulum arrangement
    for i in range(n):
        print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [11, 2, 4, 55, 6, 8]
    n = len(arr)

    pendulumArrangement(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the Pendulum
    // arrangement of the given array
    static void pendulumArrangement(int[] arr, int n)
    {
        // Sort the array
        // sort(arr, arr + n);

        Array.Sort(arr);

        int odd, temp, p, pos;

        // pos stores the index of
        // the last element of the array
        pos = n - 1;

        // odd stores the last odd index in the array
        if (n % 2 == 0)
            odd = n - 1;
        else
            odd = n - 2;

        // Move all odd index positioned
        // elements to the right
        while (odd > 0)
        {
            temp = arr[odd];
            p = odd;

            // Shift the elements by one position
            // from odd to pos
            while (p != pos)
            {
                arr[p] = arr[p + 1];
                p++;
            }
            arr[p] = temp;
            odd = odd - 2;
            pos = pos - 1;
        }

        // Reverse the element from 0 to (n - 1) / 2
        int start = 0, end = (n - 1) / 2;

        for (; start < end; start++, end--)
        {
            temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
        }

        // Printing the pendulum arrangement
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main()
    {

        int[] arr = { 11, 2, 4, 55, 6, 8 };
        int n = arr.Length;

        pendulumArrangement(arr, n);
    }
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the Pendulum
// arrangement of the given array
function pendulumArrangement($arr, $n)
{
    // Sort the array
    sort($arr) ;

    // pos stores the index of
    // the last element of the array
    $pos = $n - 1;

    // odd stores the last odd index in the array
    if ($n % 2 == 0)
        $odd = $n - 1;
    else
        $odd = $n - 2;

    // Move all odd index positioned
    // elements to the right
    while ($odd > 0)
    {
        $temp = $arr[$odd];
        $in = $odd;

        // Shift the elements by one position
        // from odd to pos
        while ($in != $pos)
        {
            $arr[$in] = $arr[$in + 1];
            $in++;
        }
        $arr[$in] = $temp;
        $odd = $odd - 2;
        $pos = $pos - 1;
    }

    // Reverse the element from 0 to (n - 1) / 2
    $start = 0;
    $end = floor(($n - 1) / 2);

    for (; $start < $end; $start++, $end--)
    {
        $temp = $arr[$start];
        $arr[$start] = $arr[$end];
        $arr[$end] = $temp;
    }

    // Printing the pendulum arrangement
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i], " ";
}

// Driver code
$arr = array( 11, 2, 4, 55, 6, 8 );
$n = count($arr);

pendulumArrangement($arr, $n);

// This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to print the Pendulum
    // arrangement of the given array
    function pendulumArrangement(arr, n)
    {
        // Sort the array
        // sort(arr, arr + n);

        arr.sort(function(a, b){return a - b});

        let odd, temp, p, pos;

        // pos stores the index of
        // the last element of the array
        pos = n - 1;

        // odd stores the last odd index in the array
        if (n % 2 == 0)
            odd = n - 1;
        else
            odd = n - 2;

        // Move all odd index positioned
        // elements to the right
        while (odd > 0)
        {
            temp = arr[odd];
            p = odd;

            // Shift the elements by one position
            // from odd to pos
            while (p != pos)
            {
                arr[p] = arr[p + 1];
                p++;
            }
            arr[p] = temp;
            odd = odd - 2;
            pos = pos - 1;
        }

        // Reverse the element from 0 to (n - 1) / 2
        let start = 0, end = parseInt((n - 1) / 2, 10);

        for (; start < end; start++, end--)
        {
            temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
        }

        // Printing the pendulum arrangement
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    let arr = [ 11, 2, 4, 55, 6, 8 ];
    let n = arr.length;

    pendulumArrangement(arr, n);

</script>
```

**Output:** 

```
11 6 2 4 8 55
```