# 从数组中精确删除一个元素，使最大–最小为最小

> 原文:[https://www . geeksforgeeks . org/从数组中移除恰好一个元素-这样-max-min-is-minimum/](https://www.geeksforgeeks.org/remove-exactly-one-element-from-the-array-such-that-max-min-is-minimum/)

给定一个由 N 个正整数组成的数组。任务是从该数组中删除恰好一个元素，以最小化**最大值(a)–最小值(a)** 并打印最小可能的**(最大值(a)–最小值(a)】**。
**注:**最大(a)表示数组![a   ](img/1d69a70cf3f4a43dd0f94fdd77b8b38d.png "Rendered by QuickLaTeX.com")中最大的数，最小(a)表示数组![a   ](img/1d69a70cf3f4a43dd0f94fdd77b8b38d.png "Rendered by QuickLaTeX.com")中最小的数。
数组中至少有 2 个元素。
**举例:**

```
Input: arr[] = {1, 3, 3, 7}
Output: 2
Remove 7, then max(a) will be 3 and min(a) will be 1.
So our answer will be 3-1 = 2.

Input: arr[] = {1, 1000}
Output: 0
Remove either 1 or 1000, then our answer will 1-1 =0 or
1000-1000=0
```

**简单方法:**这里可以看到，我们总是要去掉数组的最小值或者最大值。我们首先对数组进行排序。排序后，如果我们去掉最小元素，则差将是 a[n-1]–a[1]。如果我们去掉最大元素，差就是 a[n-2]–a[0]。我们返回这两个差异的最小值。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// function to calculate max-min
int max_min(int a[], int n)
{
    sort(a, a + n);

    return min(a[n - 2] - a[0], a[n - 1] - a[1]);
}

// Driver code
int main()
{
    int a[] = { 1, 3, 3, 7 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << max_min(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;
class GFG
{
    // function to calculate max-min
    static int max_min(int a[], int n)
    {
        Arrays.sort(a);

        return Math.min(a[n - 2] - a[0], a[n - 1] - a[1]);
    }

    // Driver code
    public static void main(String []args)
    {
        int a[] = { 1, 3, 3, 7 };
        int n = a.length;

        System.out.println(max_min(a, n));

    }
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# function to calculate max-min
def max_min(a, n):
    a.sort()
    return min(a[n - 2] - a[0],
               a[n - 1] - a[1])

# Driver code
a = [1, 3, 3, 7]
n = len(a)
print(max_min(a, n))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{
    // function to calculate max-min
    static int max_min(int []a, int n)
    {
        Array.Sort(a);

        return Math.Min(a[n - 2] - a[0], a[n - 1] - a[1]);
    }

    // Driver code
    public static void Main()
    {
        int []a = { 1, 3, 3, 7 };
        int n = a.Length;

        Console.WriteLine(max_min(a, n));

    }
}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// function to calculate max-min
function max_min(&$a, $n)
{
    sort($a);

    return min($a[$n - 2] - $a[0],
               $a[$n - 1] - $a[1]);
}

// Driver code
$a = array(1, 3, 3, 7);
$n = sizeof($a);

echo(max_min($a, $n));

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program of the above approach

 // function to calculate max-min
    function max_min(a, n)
    {
        a.sort();

        return Math.min(a[n - 2] - a[0], a[n - 1] - a[1]);
    }

// Driver code

        let a = [ 1, 3, 3, 7 ];
        let n = a.length;

        document.write(max_min(a, n));

</script>
```

**Output:** 

```
2
```