# 求所有 I 和 j 对上 a[i] % a[j]的最大可能值

> 原文:[https://www . geesforgeks . org/find-最大可能值-ai-aj-over-all-pair-I-and-j/](https://www.geeksforgeeks.org/find-the-maximum-possible-value-of-ai-aj-over-all-pairs-of-i-and-j/)

给定一个正整数数组**arr[]****N**。任务是在所有对 **i** 和 **j** 上找到 **a[i] % a[j]** 的最大可能值。
**举例:**

> **输入:** arr[] = {4，5，1，8}
> **输出:** 5
> 如果我们选择对(5，8)，那么 5 % 8 给我们 5
> 这是最大可能。
> **输入:** arr[] = {7，7，8，8，1}
> **输出:** 7

**方法:**既然我们可以选择任何一对，因此 **arr[i]** 应该是数组的第二个最大值， **arr[j]** 应该是最大元素，以便最大化所需值。因此，数组的第二个最大值将是我们的答案。如果不存在任何第二大数字，那么 **0** 将是答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the second largest
// element in the array if exists, else 0
int getMaxValue(int arr[], int arr_size)
{
    int i, first, second;

    // There must be at least two elements
    if (arr_size < 2) {
        return 0;
    }

    // To store the maximum and the second
    // maximum element from the array
    first = second = INT_MIN;
    for (i = 0; i < arr_size; i++) {

        // If current element is greater than first
        // then update both first and second
        if (arr[i] > first) {
            second = first;
            first = arr[i];
        }

        // If arr[i] is in between first and
        // second then update second
        else if (arr[i] > second && arr[i] != first)
            second = arr[i];
    }

    // No second maximum found
    if (second == INT_MIN)
        return 0;
    else
        return second;
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 1, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << getMaxValue(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns the second largest
    // element in the array if exists, else 0
    static int getMaxValue(int arr[], int arr_size)
    {
        int i, first, second;

        // There must be at least two elements
        if (arr_size < 2)
        {
            return 0;
        }

        // To store the maximum and the second
        // maximum element from the array
        first = second = Integer.MIN_VALUE;
        for (i = 0; i < arr_size; i++)
        {

            // If current element is greater than first
            // then update both first and second
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }

            // If arr[i] is in between first and
            // second then update second
            else if (arr[i] > second && arr[i] != first)
            {
                second = arr[i];
            }
        }

        // No second maximum found
        if (second == Integer.MIN_VALUE)
        {
            return 0;
        }
        else
        {
            return second;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 5, 1, 8};
        int n = arr.length;
        System.out.println(getMaxValue(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
import sys
# Python 3 implementation of the approach

# Function that returns the second largest
# element in the array if exists, else 0
def getMaxValue(arr,arr_size):

    # There must be at least two elements
    if (arr_size < 2):
        return 0

    # To store the maximum and the second
    # maximum element from the array
    first = -sys.maxsize-1
    second = -sys.maxsize-1
    for i in range(arr_size):

        # If current element is greater than first
        # then update both first and second
        if (arr[i] > first):
            second = first
            first = arr[i]

        # If arr[i] is in between first and
        # second then update second
        elif (arr[i] > second and arr[i] != first):
            second = arr[i]

    # No second maximum found
    if (second == -sys.maxsize-1):
        return 0
    else:
        return second

# Driver code
if __name__ == '__main__':
    arr = [4, 5, 1, 8]
    n = len(arr)
    print(getMaxValue(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns the second largest
    // element in the array if exists, else 0
    static int getMaxValue(int []arr,
                           int arr_size)
    {
        int i, first, second;

        // There must be at least two elements
        if (arr_size < 2)
        {
            return 0;
        }

        // To store the maximum and the second
        // maximum element from the array
        first = second = int.MinValue;
        for (i = 0; i < arr_size; i++)
        {

            // If current element is greater than first
            // then update both first and second
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }

            // If arr[i] is in between first and
            // second then update second
            else if (arr[i] > second &&
                     arr[i] != first)
            {
                second = arr[i];
            }
        }

        // No second maximum found
        if (second == int.MinValue)
        {
            return 0;
        }
        else
        {
            return second;
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = {4, 5, 1, 8};
        int n = arr.Length;
        Console.Write(getMaxValue(arr, n));
    }
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns the second largest
// element in the array if exists, else 0
function getMaxValue($arr, $arr_size)
{
    // There must be at least two elements
    if ($arr_size < 2)
    {
        return 0;
    }

    // To store the maximum and the second
    // maximum element from the array
    $first = $second = -(PHP_INT_MAX - 1);
    for ($i = 0; $i < $arr_size; $i++)
    {

        // If current element is greater than first
        // then update both first and second
        if ($arr[$i] > $first)
        {
            $second = $first;
            $first = $arr[$i];
        }

        // If arr[i] is in between first and
        // second then update second
        else if ($arr[$i] > $second &&
                 $arr[$i] != $first)
            $second = $arr[$i];
    }

    // No second maximum found
    if ($second == -(PHP_INT_MAX-1))
        return 0;
    else
        return $second;
}

// Driver code
$arr = array(4, 5, 1, 8);
$n = count($arr);

echo getMaxValue($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

 // Function that returns the second largest
// element in the array if exists, else 0
    function getMaxValue(arr, arr_size)
    {
        let i, first, second;

        // There must be at least two elements
        if (arr_size < 2)
        {
            return 0;
        }

        // To store the maximum and the second
        // maximum element from the array
        first = second = Number.MIN_VALUE;
        for (i = 0; i < arr_size; i++)
        {

            // If current element is greater than first
            // then update both first and second
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }

            // If arr[i] is in between first and
            // second then update second
            else if (arr[i] > second && arr[i] != first)
            {
                second = arr[i];
            }
        }

        // No second maximum found
        if (second == Number.MIN_VALUE)
        {
            return 0;
        }
        else
        {
            return second;
        }
    }

// Driver Code

        let arr = [4, 5, 1, 8];
        let n = arr.length;
        document.write(getMaxValue(arr, n));

</script>
```

**Output:** 

```
5
```