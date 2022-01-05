# 当一个物品总成本的其他物品免费时获得最大物品

> 原文:[https://www . geeksforgeeks . org/get-最大项目数-当一个项目的总成本中的其他项目是免费的/](https://www.geeksforgeeks.org/get-maximum-items-when-other-items-of-total-cost-of-an-item-are-free/)

给定“N”项的价格列表。一个人只能购买任何价格的一件物品，他可以免费获得其他物品，这样其余物品的总价就不会超过购买物品的价格。任务是找到这个人能拥有的最大物品数量。
**例:**

> **输入:** n = 5，arr = {5，3，1，5，6}
> **输出:** 3
> 该人可以购买价格为 5 或 6 的任何物品，并免费下载价格为 1 和 3 的物品。所以，他最多只能得到 3 件物品。
> **输入:** n = 2，arr = {7，7}
> **输出:** 2

**进场:**

> 这个人应该购买最贵的物品，然后从最便宜的价格开始购买物品(直到总价小于或等于购买的物品)，以使物品的总数最大化。
> 因此，我们对价格列表进行排序并选择最后一个元素，然后我们将从第一个索引迭代到第 n-2 个索引，并检查总和是否小于或等于最后一个元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the
// total number of items
int  items(int n, int a[]){

    // Sort the prices
    sort(a,a+n);

    // Choose the last element
    int z = a[n-1];

    // Initial count of item
    int x = 1;

    // Sum to keep track of
    // the total price
    // of free items
    int s = 0;
    for (int i=0;i<n-1;i++)
    {
        s += a[i];

        // If total is less than
        // or equal to z then
        // we will add 1 to the answer
        if (s <= z)
            x+= 1;
        else
            break;
    }
    return x;
}
int main()
{
int n = 5;

int a[]= {5, 3, 1, 5, 6};

cout<<items(n, a);
}

//contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.Arrays;
import java.io.*;

class GFG {

// Function to count the
// total number of items
static int items(int n, int a[]){

    // Sort the prices
    Arrays.sort(a);

    // Choose the last element
    int z = a[n-1];

    // Initial count of item
    int x = 1;

    // Sum to keep track of
    // the total price
    // of free items
    int s = 0;
    for (int i=0;i<n-1;i++)
    {
        s += a[i];

        // If total is less than
        // or equal to z then
        // we will add 1 to the answer
        if (s <= z)
            x+= 1;
        else
            break;
    }
    return x;
}
        // Driver code
    public static void main (String[] args) {

        int n = 5;
        int a[]= {5, 3, 1, 5, 6};
        System.out.println(items(n, a));
    }
//This code is contributed by ajit   
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to count the
# total number of items
def items(n, a):

    # Sort the prices
    a.sort()

    # Choose the last element
    z = a[n-1]

    # Initial count of item
    x = 1

    # Sum to keep track of
    # the total price
    # of free items
    s = 0
    for i in range(0, n-1):

        s += a[i]

        # If total is less than
        # or equal to z then
        # we will add 1 to the answer
        if (s <= z):
            x+= 1
        else:
            break
    return x

n = 5
a = [5, 3, 1, 5, 6]
print(items(n, a))
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{
// Function to count the
// total number of items
static int items(int n, int []a)
{

    // Sort the prices
    Array.Sort(a);

    // Choose the last element
    int z = a[n - 1];

    // Initial count of item
    int x = 1;

    // Sum to keep track of
    // the total price
    // of free items
    int s = 0;
    for (int i = 0; i < n - 1; i++)
    {
        s += a[i];

        // If total is less than or equal to z
        // then we will add 1 to the answer
        if (s <= z)
            x += 1;
        else
            break;
    }
    return x;
}

// Driver code
static public void Main ()
{
    int n = 5;
    int []a = {5, 3, 1, 5, 6};
    Console.WriteLine(items(n, a));
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of
// the above approach
// Function to count the
// total number of items

function items($n, $a){

    // Sort the prices
    sort($a);

    // Choose the last element
    $z = $a[$n-1];

    // Initial count of item
    $x = 1;

    // Sum to keep track of
    // the total price
    // of free items
    $s = 0;
    for ($i=0;$i<$n-1;$i++)
    {
        $s += $a[$i];

        // If total is less than
        // or equal to z then
        // we will add 1 to the answer
        if ($s <= $z)
            $x+= 1;
        else
            break;
    }
    return $x;
}
//Code driven
$n = 5;
$a= array(5, 3, 1, 5, 6);

echo items($n, $a);

//This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to count the
    // total number of items
    function items(n, a)
    {

        // Sort the prices
        a.sort(function(a, b){return a - b});

        // Choose the last element
        let z = a[n - 1];

        // Initial count of item
        let x = 1;

        // Sum to keep track of
        // the total price
        // of free items
        let s = 0;
        for (let i = 0; i < n - 1; i++)
        {
            s += a[i];

            // If total is less than or equal to z
            // then we will add 1 to the answer
            if (s <= z)
                x += 1;
            else
                break;
        }
        return x;
    }

    let n = 5;
    let a = [5, 3, 1, 5, 6];
    document.write(items(n, a));

</script>
```

**Output:** 

```
3
```