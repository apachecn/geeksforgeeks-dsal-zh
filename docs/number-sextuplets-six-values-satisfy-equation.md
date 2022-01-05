# 满足等式

的六个组(或六个值)的数量

> 原文:[https://www . geeksforgeeks . org/number-sex tuples-six-values-submit-equation/](https://www.geeksforgeeks.org/number-sextuplets-six-values-satisfy-equation/)

给定一组 **n 个**元素。任务是找到满足下面等式的六个图的数量，使得 a、b、c、d、e 和 f 属于给定的数组:

```
a * b + c - e = f
    d
```

**示例:**

```
Input :  arr[] = { 1 }.
Output : 1
a = b = c = d = e = f = 1 satisfy
the equation.

Input :  arr[] = { 2, 3 }
Output : 4

Input :  arr[] = { 1, -1 }
Output : 24
```

首先，对方程重新排序，a * b + c = (f + e) * d.
现在，制作两个数组，一个用于方程的 LHS(左手边)，一个用于方程的 RHS(右手边)。在 LHS 数组中搜索 RHS 数组的每个元素。无论何时你在 LHS 找到一个 RHS 值，检查它在 LHS 重复了多少次，并把这个计数加到总数中。通过对 LHS 数组进行排序，可以使用二分搜索法进行搜索。

下面是该方法的实现:

## C++

```
// C++ program to count of 6 values from an array
// that satisfy an equation with 6 variables
#include<bits/stdc++.h>
using namespace std;

// Returns count of 6 values from arr[]
// that satisfy an equation with 6 variables
int findSextuplets(int arr[], int n)
{
    // Generating possible values of RHS of the equation
    int index = 0;
    int RHS[n*n*n + 1];
    for (int i = 0; i < n; i++)
      if (arr[i])  // Checking d should be non-zero.
        for (int j = 0; j < n; j++)
          for (int k = 0; k < n; k++)
            RHS[index++] = arr[i] * (arr[j] + arr[k]);

    // Sort RHS[] so that we can do binary search in it.
    sort(RHS, RHS + n);

    // Generating all possible values of LHS of the equation
    // and finding the number of occurrences of the value in RHS.
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            for(int k = 0; k < n; k++)
            {
                int val = arr[i] * arr[j] + arr[k];
                result += (upper_bound(RHS, RHS + index, val) -
                          lower_bound(RHS, RHS + index, val));
            }
        }
    }

    return result;
}

// Driven Program
int main()
{
    int arr[] = {2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << findSextuplets(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of 6 values from an array
// that satisfy an equation with 6 variables
import java.util.Arrays;
class GFG{
static int upper_bound(int[] array, int length, int value) {
        int low = 0;
        int high = length;
        while (low < high) {
            final int mid = (low + high) / 2;
            if (value >= array[mid]) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }
  static int lower_bound(int[] array, int length, int value) {
        int low = 0;
        int high = length;
        while (low < high) {
            final int mid = (low + high) / 2;
            if (value <= array[mid]) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low;
    } 
static int findSextuplets(int[] arr, int n)
{
    // Generating possible values of RHS of the equation
    int index = 0;
    int[] RHS = new int[n * n * n + 1];
    for (int i = 0; i < n; i++)
    {
      if (arr[i] != 0) // Checking d should be non-zero.
      {
        for (int j = 0; j < n; j++)
        {
          for (int k = 0; k < n; k++)
          {
            RHS[index++] = arr[i] * (arr[j] + arr[k]);
          }
        }
      }
    }

    // Sort RHS[] so that we can do binary search in it.
    Arrays.sort(RHS);

    // Generating all possible values of LHS of the equation
    // and finding the number of occurrences of the value in RHS.
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            for (int k = 0; k < n; k++)
            {
                int val = arr[i] * arr[j] + arr[k];
                result += (upper_bound(RHS, index, val)-lower_bound(RHS, index, val));
            }
        }
    }

    return result;
}

// Driven Program
public static void main(String[] args)
{
    int[] arr = {2, 3};
    int n = arr.length;

    System.out.println(findSextuplets(arr, n));

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to count of 6 values
# from an array that satisfy an equation
# with 6 variables

def upper_bound(array, length, value):
    low = 0;
    high = length;
    while (low < high):
        mid = int((low + high) / 2);
        if (value >= array[mid]):
                low = mid + 1;
        else:
            high = mid;

    return low;

def lower_bound(array, length, value):
    low = 0;
    high = length;
    while (low < high):
        mid = int((low + high) / 2);
        if (value <= array[mid]):
            high = mid;
        else:
            low = mid + 1;
    return low;

def findSextuplets(arr, n):

    # Generating possible values of
    # RHS of the equation
    index = 0;
    RHS = [0] * (n * n * n + 1);

    for i in range(n):
        if (arr[i] != 0):

            # Checking d should be non-zero.
            for j in range(n):
                for k in range(n):
                    RHS[index] = arr[i] * (arr[j] +
                                           arr[k]);
                    index += 1;

    # Sort RHS[] so that we can do
    # binary search in it.
    RHS.sort();

    # Generating all possible values of
    # LHS of the equation and finding the
    # number of occurrences of the value in RHS.
    result = 0;
    for i in range(n):
        for j in range(n):
            for k in range(n):
                val = arr[i] * arr[j] + arr[k];
                result += (upper_bound(RHS, index, val) -
                           lower_bound(RHS, index, val));

    return result;

# Driver Code
arr = [2, 3];
n = len(arr);

print(findSextuplets(arr, n));

# This code is contributed by mits
```

## C#

```
// C# program to count of 6 values from an array
// that satisfy an equation with 6 variables
using System;
using System.Collections;

class GFG{
static int upper_bound(int[] array, int length, int value) {
        int low = 0;
        int high = length;
        while (low < high) {
            int mid = (low + high) / 2;
            if (value >= array[mid]) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }
static int lower_bound(int[] array, int length, int value) {
        int low = 0;
        int high = length;
        while (low < high) {
            int mid = (low + high) / 2;
            if (value <= array[mid]) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low;
    }
static int findSextuplets(int[] arr, int n)
{
    // Generating possible values of RHS of the equation
    int index = 0;
    int[] RHS = new int[n * n * n + 1];
    for (int i = 0; i < n; i++)
    {
    if (arr[i] != 0) // Checking d should be non-zero.
    {
        for (int j = 0; j < n; j++)
        {
        for (int k = 0; k < n; k++)
        {
            RHS[index++] = arr[i] * (arr[j] + arr[k]);
        }
        }
    }
    }

    // Sort RHS[] so that we can do binary search in it.
    Array.Sort(RHS);

    // Generating all possible values of LHS of the equation
    // and finding the number of occurrences of the value in RHS.
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            for (int k = 0; k < n; k++)
            {
                int val = arr[i] * arr[j] + arr[k];
                result += (upper_bound(RHS, index, val)-lower_bound(RHS, index, val));
            }
        }
    }

    return result;
}

// Driven Program
static void Main()
{
    int[] arr = {2, 3};
    int n = arr.Length;

    Console.WriteLine(findSextuplets(arr, n));

}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count of 6 values from
// an array that satisfy an equation
// with 6 variables

function upper_bound($array, $length, $value)
{
    $low = 0;
    $high = $length;
    while ($low < $high)
    {
        $mid = (int)(($low + $high) / 2);
        if ($value >= $array[$mid])
                $low = $mid + 1;
        else
            $high = $mid;
    }
    return $low;
}

function lower_bound($array, $length, $value)
{
    $low = 0;
    $high = $length;
    while ($low < $high)
    {
        $mid = (int)(($low + $high) / 2);
        if ($value <= $array[$mid])
            $high = $mid;
        else
            $low = $mid + 1;
    }
    return $low;
}

// Returns count of 6 values from arr[]
// that satisfy an equation with 6 variables
function findSextuplets($arr, $n)
{
    // Generating possible values of
    // RHS of the equation
    $index = 0;
    $RHS = array_fill(0, $n * $n * $n + 1, 0);
    for ($i = 0; $i < $n; $i++)
    if ($arr[$i] != 0) // Checking d should be non-zero.
        for ($j = 0; $j < $n; $j++)
        for ($k = 0; $k < $n; $k++)
            $RHS[$index++] = $arr[$i] *
                            ($arr[$j] + $arr[$k]);

    // Sort RHS[] so that we can do
    // binary search in it.
    sort($RHS);

    // Generating all possible values of LHS
    // of the equation and finding the number
    // of occurrences of the value in RHS.
    $result = 0;
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)
            for ($k = 0; $k < $n; $k++)
            {
                $val = $arr[$i] * $arr[$j] + $arr[$k];
                $result += (upper_bound($RHS, $index, $val) -
                            lower_bound($RHS, $index, $val));
            }

    return $result;
}

// Driver Code
$arr = array(2, 3);
$n = count($arr);

print(findSextuplets($arr, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count of
// 6 values from an array
// that satisfy an equation with
// 6 variables

function upper_bound(array , length , value)
{
        var low = 0;
        var high = length;
        while (low < high) {
            var mid = parseInt((low + high) / 2);
            if (value >= array[mid]) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }
  function lower_bound(array , length , value)
  {
        var low = 0;
        var high = length;
        while (low < high) {
            var mid = parseInt((low + high) / 2);
            if (value <= array[mid]) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low;
    } 
function findSextuplets(arr , n)
{
    // Generating possible values of
    // RHS of the equation
    var index = 0;
    var RHS = Array.from({length: n * n * n + 1},
    (_, i) => 0);
    for (i = 0; i < n; i++)
    {
    // Checking d should be non-zero.
      if (arr[i] != 0)
      {
        for (j = 0; j < n; j++)
        {
          for (k = 0; k < n; k++)
          {
            RHS[index++] = arr[i] *
            (arr[j] + arr[k]);
          }
        }
      }
    }

    // Sort RHS so that we can do
    // binary search in it.
    RHS.sort((a,b)=>a-b);

    // Generating all possible values
    // of LHS of the equation
    // and finding the number of occurrences
    // of the value in RHS.
    var result = 0;
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            for (k = 0; k < n; k++)
            {
                var val = arr[i] * arr[j] + arr[k];
                result += (upper_bound(RHS, index, val)-
                lower_bound(RHS, index, val));
            }
        }
    }

    return result;
}

// Driven Program
var arr = [2, 3];
var n = arr.length;

document.write(findSextuplets(arr, n));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(N <sup>3</sup> log N)

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。