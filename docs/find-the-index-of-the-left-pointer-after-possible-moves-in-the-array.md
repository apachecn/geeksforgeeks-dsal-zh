# 在数组中找到可能移动后左指针的索引

> 原文:[https://www . geesforgeks . org/find-数组中可能移动后的左指针索引/](https://www.geeksforgeeks.org/find-the-index-of-the-left-pointer-after-possible-moves-in-the-array/)

给定一组大小![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。移动两个指针，一个从数组的左侧移动，一个从数组的右侧移动，一个指针只有在它已经通过的所有数字的总和小于另一个指针已经通过的数字的总和时才会向前移动。当左指针小于右指针或不能移动时，继续该过程。打印最后左边指针的位置。

**注**:数组考虑基于 0 的索引。

**示例:**

> **输入:** arr[] = {2，7，9，8，7}
> **输出:** 2
> 初始位置:ptrL = 0，ptrR = 4 加和 2 和 7
> 移动 1 : ptrL = 1，ptrR = 4 加和 9 和 7
> 移动 2 : ptrL = 1，ptrR = 3 加和 9 和 15
> 移动 3 : ptrL = 2，ptrR = 3 加和 18 和 7
> 
> **输入:** arr[] = {1，2，3，1，2}
> **输出:** 1

**方法:**一种有效的方法是同时从左向右移动，并保持两个指针的运行总和。

下面是上述方法的实现:

## C++

```
// C++ program to find the index of the left pointer

#include <bits/stdc++.h>
using namespace std;

// Function that returns the index of the left pointer
int getIndex(int a[], int n)
{
    // there's only one element in the array
    if(n == 1)
        return 0;

    // initially both are at end
    int ptrL = 0, ptrR = n-1, sumL = a[0], sumR = a[n-1];

    while (ptrR - ptrL > 1) {
        if (sumL < sumR) {
            ptrL++;
            sumL += a[ptrL];
        }
        else if (sumL > sumR) {
            ptrR--;
            sumR += a[ptrR];
        }
        else {
            break;
        }
    }
    return ptrL;
}

// Driver code
int main()
{
    int a[] = { 2, 7, 9, 8, 7 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << getIndex(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the index of the left pointer

import java.io.*;

class GFG {

// Function that returns the index of the left pointer
static int getIndex(int a[], int n)
{
    // there's only one element in the array
    if(n == 1)
        return 0;

    // initially both are at end
    int ptrL = 0, ptrR = n-1, sumL = a[0], sumR = a[n-1];

    while (ptrR - ptrL > 1) {
        if (sumL < sumR) {
            ptrL++;
            sumL += a[ptrL];
        }
        else if (sumL > sumR) {
            ptrR--;
            sumR += a[ptrR];
        }
        else {
            break;
        }
    }
    return ptrL;
}

// Driver code

    public static void main (String[] args) {
        int a[] = { 2, 7, 9, 8, 7 };

    int n =a.length;

    System.out.println ( getIndex(a, n));
    }
}
// This code is contributed by  anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find the
# index of the left pointer

# Function that returns the
# index of the left pointer
def getIndex(a, n):

    # there's only one element
    # in the array
    if(n == 1):
        return 0

    # initially both are at end
    ptrL = 0
    ptrR = n-1
    sumL = a[0]
    sumR = a[n-1]

    while (ptrR - ptrL > 1) :
        if (sumL < sumR) :
            ptrL += 1
            sumL += a[ptrL]

        elif (sumL > sumR) :
            ptrR -= 1
            sumR += a[ptrR]

        else :
            break
    return ptrL

# Driver code
if __name__ == "__main__":

    a = [ 2, 7, 9, 8, 7 ]

    n = len(a)

    print(getIndex(a, n))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to find the index of the left pointer

using System;

class GFG {

// Function that returns the index of the left pointer
static int getIndex(int []a, int n)
{
    // there's only one element in the array
    if(n == 1)
        return 0;

    // initially both are at end
    int ptrL = 0, ptrR = n-1, sumL = a[0], sumR = a[n-1];

    while (ptrR - ptrL > 1) {
        if (sumL < sumR) {
            ptrL++;
            sumL += a[ptrL];
        }
        else if (sumL > sumR) {
            ptrR--;
            sumR += a[ptrR];
        }
        else {
            break;
        }
    }
    return ptrL;
}

// Driver code

    public static void Main () {
        int []a = { 2, 7, 9, 8, 7 };

    int n =a.Length;

    Console.WriteLine( getIndex(a, n));
    }
}
// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the index
// of the left pointer

// Function that returns the index
// of the left pointer
function getIndex($a, $n)
{
    // there's only one element
    // in the array
    if($n == 1)
        return 0;

    // initially both are at end
    $ptrL = 0; $ptrR = $n - 1;
    $sumL = $a[0]; $sumR = $a[$n - 1];

    while ($ptrR - $ptrL > 1)
    {
        if ($sumL < $sumR)
        {
            $ptrL++;
            $sumL += $a[$ptrL];
        }
        else if ($sumL > $sumR)
        {
            $ptrR--;
            $sumR += $a[$ptrR];
        }
        else
        {
            break;
        }
    }
    return $ptrL;
}

// Driver code
$a = array( 2, 7, 9, 8, 7 );

$n = count($a);

echo getIndex($a, $n);

// This code is contributed by anuj_67..
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the index of the left pointer

// Function that returns the
// index of the left pointer
function getIndex(a, n)
{

    // There's only one element
    // in the array
    if(n == 1)
        return 0;

    // Initially both are at end
    let ptrL = 0, ptrR = n - 1,
        sumL = a[0], sumR = a[n - 1];

    while (ptrR - ptrL > 1)
    {
        if (sumL < sumR)
        {
            ptrL++;
            sumL += a[ptrL];
        }
        else if (sumL > sumR)
        {
            ptrR--;
            sumR += a[ptrR];
        }
        else
        {
            break;
        }
    }
    return ptrL;
}

// Driver code
let a = [ 2, 7, 9, 8, 7 ];
let n = a.length;

document.write(getIndex(a, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
2
```