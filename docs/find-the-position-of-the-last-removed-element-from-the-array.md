# 找到数组中最后一个被移除元素的位置

> 原文:[https://www . geeksforgeeks . org/find-最后一个从数组中移除的元素的位置/](https://www.geeksforgeeks.org/find-the-position-of-the-last-removed-element-from-the-array/)

给定一个大小为![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")的数组和一个整数![M  ](img/20aead0a95215a9a83fdd34d16c40b4d.png "Rendered by QuickLaTeX.com")。对给定阵列执行以下操作:

1.  如果**a【I】>M**然后将**a【I】–M**推到数组末尾，否则将其从数组中移除。
2.  当数组非空时执行第一个操作。

任务是找到最后被移除的元素的原始位置。

**示例:**

> **输入:** arr[] = {4，3}，M = 2
> **输出:** 2
> 从数组中移除 4，数组变为{3，2}具有原始位置{2，1}
> 从数组中移除 3，数组变为{2，1}具有原始位置{1，2}
> 从数组中移除 2，数组变为{1}具有原始位置{2}
> 因此，第 2 个定位的元素是最后一个从数组中移除的元素。
> 
> **输入:** arr[] = {2，5，4}，M = 2
> T3】输出: 2

这个想法是观察将从数组中移除的最后一个元素。可以很容易地说，最后被移除的元素将是在数组的所有元素中可以被![M  ](img/20aead0a95215a9a83fdd34d16c40b4d.png "Rendered by QuickLaTeX.com")减去最大次数的元素。也就是 **ceil(a[i] / M)** 最大值的元素。

因此，任务现在简化为寻找数组中最大值为 **ceil(a[i] / M)** 的元素的索引。

下面是上述方法的实现:

## C++

```
// C++ program to find the position of the
// last removed element from the array
#include <bits/stdc++.h>
using namespace std;

// Function to find the original position
// of the element which will be
// removed last
int getPosition(int a[], int n, int m)
{
    // take ceil of every number
    for (int i = 0; i < n; i++) {
        a[i] = (a[i] / m + (a[i] % m != 0));
    }

    int ans = -1, max = -1;
    for (int i = n - 1; i >= 0; i--) {
        if (max < a[i]) {
            max = a[i];
            ans = i;
        }
    }

    // Since position is index+1
    return ans + 1;
}

// Driver code
int main()
{
    int a[] = { 2, 5, 4 };

    int n = sizeof(a) / sizeof(a[0]);

    int m = 2;

    cout << getPosition(a, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the position of the
// last removed element from the array
import java.util.*;

class solution
{

// Function to find the original position
// of the element which will be
// removed last

static int getPosition(int a[], int n, int m)
{
    // take ceil of every number
    for (int i = 0; i < n; i++) {
        a[i] = (a[i] / m + (a[i] % m));
    }

    int ans = -1, max = -1;
    for (int i = n - 1; i >= 0; i--) {
        if (max < a[i]) {
            max = a[i];
            ans = i;
        }
    }

    // Since position is index+1
    return ans + 1;
}

// Driver code
public static void main(String args[])
{
    int a[] = { 2, 5, 4 };

    int n = a.length;

    int m = 2;

System.out.println(getPosition(a, n, m));

}

}
//This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find the position of
# the last removed element from the array
import math as mt

# Function to find the original
# position of the element which
# will be removed last
def getPosition(a, n, m):

    # take ceil of every number
    for i in range(n):
        a[i] = (a[i] // m +
               (a[i] % m != 0))

    ans, maxx = -1,-1
    for i in range(n - 1, -1, -1):
        if (maxx < a[i]):
            maxx = a[i]
            ans = i

    # Since position is index+1
    return ans + 1

# Driver code
a = [2, 5, 4]

n = len(a)

m = 2

print(getPosition(a, n, m))

# This is contributed by Mohit kumar 29
```

## C#

```
// C# program to find the position of the
// last removed element from the array
using System;

class GFG
{

// Function to find the original
// position of the element which
// will be removed last
static int getPosition(int []a,
                       int n, int m)
{
    // take ceil of every number
    for (int i = 0; i < n; i++)
    {
        a[i] = (a[i] / m + (a[i] % m));
    }

    int ans = -1, max = -1;
    for (int i = n - 1; i >= 0; i--)
    {
        if (max < a[i])
        {
            max = a[i];
            ans = i;
        }
    }

    // Since position is index+1
    return ans + 1;
}

// Driver code
static public void Main ()
{
    int []a = { 2, 5, 4 };
    int n = a.Length;
    int m = 2;
    Console.WriteLine(getPosition(a, n, m));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the position of the
// last removed element from the array

// Function to find the original
// position of the element which
// will be removed last
function getPosition($a, $n, $m)
{
    // take ceil of every number
    for ( $i = 0; $i < $n; $i++)
    {
        $a[$i] = ($a[$i] / $m +
                 ($a[$i] % $m != 0));
    }

    $ans = -1;
    $max = -1;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        if ($max < $a[$i])
        {
            $max = $a[$i];
            $ans = $i;
        }
    }

    // Since position is index+1
    return $ans + 1;
}

// Driver code
$a = array( 2, 5, 4 );
$n = sizeof($a);
$m = 2;

echo getPosition($a, $n, $m);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to find the position
// of the last removed element from the array

// Function to find the original
// position of the element which
// will be removed last
function getPosition(a, n, m)
{

    // Take ceil of every number
    for(let i = 0; i < n; i++)
    {
        a[i] = (a[i] / m + (a[i] % m));
    }

    let ans = -1, max = -1;
    for(let i = n - 1; i >= 0; i--)
    {
        if (max < a[i])
        {
            max = a[i];
            ans = i;
        }
    }

    // Since position is index+1
    return ans + 1;
}

// Driver code
let a = [ 2, 5, 4 ];
let n = a.length;
let m = 2;

document.write(getPosition(a, n, m));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
2
```