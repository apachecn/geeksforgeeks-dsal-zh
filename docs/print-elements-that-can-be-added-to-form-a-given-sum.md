# 打印可以相加形成给定总和的元素

> 原文:[https://www . geesforgeks . org/print-elements-可添加到给定金额中的元素/](https://www.geeksforgeeks.org/print-elements-that-can-be-added-to-form-a-given-sum/)

给定一个正整数数组 *arr[]* 和一个*和*，任务是打印将要包含的元素以获得给定的和。
**注:**

1.  考虑队列形式的元素，即从开始到元素总和小于或等于给定总和的元素。
2.  此外，数组元素的和不一定等于给定的和。

因为任务是检查柠檬是否可以包含在内。

**示例:**

> **输入:** arr[] = {3，5，3，2，1}，Sum = 10
> **输出:** 3 5 2
> 通过加 3，5 和 3，Sum 变成 11，所以去掉最后的 3。
> 然后加 2，和变成 10。所以不需要添加其他元素
> 。
> 
> **输入:** arr[] = {7，10，6，4}，总和= 12
> **输出:** 7 4
> As，7+10 和 7+6 的总和大于 12
> ，但 7+4 = 11 小于 12。
> 所以，7 和 4 可以包含在内

**进场:**

1.  检查添加当前元素时，总和是否小于给定的总和。
2.  如果是，则添加它。
3.  否则转到下一个元素，重复相同的操作，直到它们的总和小于或等于给定的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds whether an element
// will be included or not
void includeElement(int a[], int n, int sum)
{
    for (int i = 0; i < n; i++) {

        // Check if the current element
        // will be incuded or not
        if ((sum - a[i]) >= 0) {
            sum = sum - a[i];
            cout << a[i]<< " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 3, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 10;

    includeElement(arr, n, sum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
class GFG
{

// Function that finds whether
// an element will be included
// or not
static void includeElement(int a[],
                           int n, int sum)
{
    for (int i = 0; i < n; i++)
    {

        // Check if the current element
        // will be included or not
        if ((sum - a[i]) >= 0)
        {
            sum = sum - a[i];
            System.out.print(a[i] + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 5, 3, 2, 1 };
    int n = arr.length;
    int sum = 10;

    includeElement(arr, n, sum);
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function that finds whether an element
# will be included or not
def includeElement(a, n, sum) :

    for i in range(n) :

        # Check if the current element
        # will be incuded or not
        if sum - a[i] >= 0 :

            sum = sum - a[i]

            print(a[i],end = " ")

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 5, 3, 2, 1]
    n = len(arr)
    sum = 10

    includeElement(arr, n, sum)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation
// of above approach
using System;

class GFG
{
// Function that finds whether
// an element will be included
// or not
static void includeElement(int[] a,
                           int n, int sum)
{
    for (int i = 0; i < n; i++)
    {

        // Check if the current element
        // will be included or not
        if ((sum - a[i]) >= 0)
        {
            sum = sum - a[i];
            Console.Write(a[i] + " ");
        }
    }
}

// Driver code
static void Main()
{
    int[] arr = new int[]{ 3, 5, 3, 2, 1 };
    int n = arr.Length;
    int sum = 10;

    includeElement(arr, n, sum);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that finds whether an
// element will be included or not
function includeElement(&$a, $n, $sum)
{
    for ($i = 0; $i < $n; $i++)
    {
        // Check if the current element
        // will be incuded or not
        if (($sum - $a[$i]) >= 0)
        {
            $sum = $sum - $a[$i];
            echo $a[$i] . " ";
        }
    }
}

// Driver Code
$arr = array( 3, 5, 3, 2, 1 );
$n = sizeof($arr);
$sum = 10;

includeElement($arr, $n, $sum);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that finds whether an element
// will be included or not
function includeElement(a, n, sum)
{
    for(var i = 0; i < n; i++)
    {

        // Check if the current element
        // will be incuded or not
        if ((sum - a[i]) >= 0)
        {
            sum = sum - a[i];
            document.write( a[i] + " ");
        }
    }
}

// Driver Code
var arr = [ 3, 5, 3, 2, 1 ];
var n = arr.length;
var sum = 10;

includeElement(arr, n, sum);

// This code is contributed by itsok

</script>
```

**Output:** 

```
3 5 2
```